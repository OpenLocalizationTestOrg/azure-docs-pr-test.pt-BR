---
title: logs de aaaVisualize fluxo NSG de Inspetor de rede do Azure usando as ferramentas de software livre | Microsoft Docs
description: "Esta página descreve como toouse Abrir fonte ferramentas toovisualize NSG fluxo logs."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="1bab3-103">Visualizar logs de fluxo NSG do Observador de Rede do Azure usando ferramentas de código aberto</span><span class="sxs-lookup"><span data-stu-id="1bab3-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="1bab3-104">Os logs de fluxo do Grupo de Segurança de Rede fornecem informações que podem ser usadas para entender a entrada e a saída de tráfego IP em Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="1bab3-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="1bab3-105">Esses logs de fluxo Mostrar saídas e fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, informações de tupla 5 sobre o fluxo de saudação (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego de saudação é permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="1bab3-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="1bab3-106">Esses logs de fluxo podem ser difícil toomanually análise e obter ideias de.</span><span class="sxs-lookup"><span data-stu-id="1bab3-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="1bab3-107">No entanto, há várias ferramentas de código livre que podem ajudar a visualizar esses dados.</span><span class="sxs-lookup"><span data-stu-id="1bab3-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="1bab3-108">Este artigo fornecem uma solução toovisualize esses logs usando Olá pilha Elástico, que permitem que você tooquickly índice e visualizar seus logs de fluxo em um painel Kibana.</span><span class="sxs-lookup"><span data-stu-id="1bab3-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="1bab3-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="1bab3-109">Scenario</span></span>

<span data-ttu-id="1bab3-110">Neste artigo, podemos configurar uma solução que permitirá que você toovisualize logs de fluxo de grupo de segurança de rede usando Olá pilha Elástico.</span><span class="sxs-lookup"><span data-stu-id="1bab3-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="1bab3-111">Um plug-in de entrada de Logstash obterá logs de fluxo Olá diretamente saudação do blob de armazenamento configurada para que contém os logs de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bab3-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="1bab3-112">Em seguida, os logs de fluxo hello usando Olá pilha Elástico, serão indexados e usado toocreate um Kibana painel toovisualize Olá de informações.</span><span class="sxs-lookup"><span data-stu-id="1bab3-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![cenário][scenario]

## <a name="steps"></a><span data-ttu-id="1bab3-114">Etapas</span><span class="sxs-lookup"><span data-stu-id="1bab3-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="1bab3-115">Habilitar os registros em logs do fluxo do Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="1bab3-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="1bab3-116">Nessa situação, você deve habilitar o Registro em Log do Fluxo do Grupo de Segurança de Rede em um ou mais Grupos de Segurança de Rede em sua conta.</span><span class="sxs-lookup"><span data-stu-id="1bab3-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="1bab3-117">Para obter instruções sobre como ativar Logs de fluxo de segurança de rede, consulte toohello artigo a seguir [registro em log tooflow de Introdução para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1bab3-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="1bab3-118">Configurar Olá pilha Elástico</span><span class="sxs-lookup"><span data-stu-id="1bab3-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="1bab3-119">Conectando-se NSG fluxo de logs com hello pilha Elástico, podemos criar um painel Kibana o que permite toosearch, gráfico, analisar e derivar informações de nossos logs.</span><span class="sxs-lookup"><span data-stu-id="1bab3-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="1bab3-120">Instalar Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="1bab3-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="1bab3-121">Olá Elástico pilha de versão 5.0 e superior requer Java 8.</span><span class="sxs-lookup"><span data-stu-id="1bab3-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="1bab3-122">Execute o comando Olá `java -version` toocheck sua versão.</span><span class="sxs-lookup"><span data-stu-id="1bab3-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="1bab3-123">Se você não tiver java de instalação, consulte toodocumentation em [site da Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="1bab3-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="1bab3-124">Baixe pacote de binário correto Olá para o seu sistema:</span><span class="sxs-lookup"><span data-stu-id="1bab3-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="1bab3-125">Outros métodos de instalação podem ser encontrados em [Instalação do Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="1bab3-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="1bab3-126">Verifique se Elasticsearch está em execução com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="1bab3-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="1bab3-127">Você verá um toothis semelhante de resposta:</span><span class="sxs-lookup"><span data-stu-id="1bab3-127">You should see a response similar toothis:</span></span>

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

<span data-ttu-id="1bab3-128">Para obter mais instruções sobre pesquisa elástica instalar, consulte a página de toohello [instalação](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="1bab3-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="1bab3-129">Instalar Logstash</span><span class="sxs-lookup"><span data-stu-id="1bab3-129">Install Logstash</span></span>

1. <span data-ttu-id="1bab3-130">tooinstall Logstash execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bab3-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="1bab3-131">Em seguida precisamos tooconfigure Logstash tooaccess e analise logs de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bab3-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="1bab3-132">Crie um arquivo logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="1bab3-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="1bab3-133">Adicione Olá toohello conteúdo de arquivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bab3-133">Add hello following content toohello file:</span></span>

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

<span data-ttu-id="1bab3-134">Para obter mais informações sobre como instalar Logstash, consulte toohello [documentação oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="1bab3-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="1bab3-135">Instalar Olá Logstash entrada plug-in para o armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="1bab3-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="1bab3-136">Este plug-in Logstash permitirá que você os logs de fluxo de saudação do acesso toodirectly da sua conta de armazenamento designadas.</span><span class="sxs-lookup"><span data-stu-id="1bab3-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="1bab3-137">tooinstall este plug-in do diretório de instalação de Logstash saudação padrão (em /usr/share/logstash/bin neste caso) execute Olá comando:</span><span class="sxs-lookup"><span data-stu-id="1bab3-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="1bab3-138">toostart Logstash executar comando hello:</span><span class="sxs-lookup"><span data-stu-id="1bab3-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="1bab3-139">Para obter mais informações sobre este plug-in, consulte toodocumentation [aqui](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="1bab3-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="1bab3-140">Instalar Kibana</span><span class="sxs-lookup"><span data-stu-id="1bab3-140">Install Kibana</span></span>

1. <span data-ttu-id="1bab3-141">Execute Olá comandos tooinstall Kibana a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bab3-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="1bab3-142">toorun Kibana usar comandos de saudação:</span><span class="sxs-lookup"><span data-stu-id="1bab3-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="1bab3-143">tooview Kibana web interface, navegue até muito`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="1bab3-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="1bab3-144">Para este cenário, o padrão de índice de saudação usado para logs de fluxo de saudação é "logs de fluxo nsg".</span><span class="sxs-lookup"><span data-stu-id="1bab3-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="1bab3-145">Você pode alterar o padrão de índice Olá Olá "saída" seção do arquivo logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="1bab3-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="1bab3-146">Se você quiser o painel de Kibana Olá tooview remotamente, criar uma regra NSG entrada permitindo acesso muito**porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="1bab3-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="1bab3-147">Criar um painel Kibana</span><span class="sxs-lookup"><span data-stu-id="1bab3-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="1bab3-148">Neste artigo, nós fornecemos um painel de exemplo para você tooview tendências e os detalhes de alertas.</span><span class="sxs-lookup"><span data-stu-id="1bab3-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![figura 1][1]

1. <span data-ttu-id="1bab3-150">Baixar o arquivo do painel Olá [aqui](https://aka.ms/networkwatchernsgflowlogdashboard), arquivo de visualização de saudação [aqui](https://aka.ms/networkwatchernsgflowlogvisualizations)e o arquivo de pesquisa Olá salvada [aqui](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="1bab3-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="1bab3-151">Em Olá **gerenciamento** guia de Kibana, navegue muito**objetos salvos** e importar todos os três arquivos.</span><span class="sxs-lookup"><span data-stu-id="1bab3-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="1bab3-152">Depois de saudação **painel** guia você pode abrir e carga Olá painel de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1bab3-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="1bab3-153">Você também pode criar suas próprias visualizações e painéis personalizados para métricas de seu próprio interesse.</span><span class="sxs-lookup"><span data-stu-id="1bab3-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="1bab3-154">Leia mais sobre como criar visualizações do Kibana a partir da [documentação oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) do Kibana.</span><span class="sxs-lookup"><span data-stu-id="1bab3-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="1bab3-155">Visualizar logs de fluxo NSG</span><span class="sxs-lookup"><span data-stu-id="1bab3-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="1bab3-156">Painel de exemplo Hello fornece várias visualizações de saudação fluxo logs:</span><span class="sxs-lookup"><span data-stu-id="1bab3-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="1bab3-157">Fluxos por decisão/direção ao longo do tempo - gráficos de série de tempo mostrando o número de saudação de fluxos em Olá período de tempo.</span><span class="sxs-lookup"><span data-stu-id="1bab3-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="1bab3-158">Você pode editar unidade Olá de tempo e o intervalo de ambas as essas visualizações.</span><span class="sxs-lookup"><span data-stu-id="1bab3-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="1bab3-159">Fluxos de decisão mostra Olá proporção de permitem ou negar as decisões tomadas durante fluxos por direção mostra Olá proporção do tráfego de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="1bab3-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="1bab3-160">Com esses elementos visuais, você pode examinar as tendências de tráfego ao longo do tempo e procure por picos ou padrões incomuns.</span><span class="sxs-lookup"><span data-stu-id="1bab3-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![figura2][2]

1. <span data-ttu-id="1bab3-162">Fluxos por porta de origem/destino – gráficos de pizza mostrando a divisão de saudação de fluxos tootheir respectivas portas.</span><span class="sxs-lookup"><span data-stu-id="1bab3-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="1bab3-163">Nesta exibição, você pode ver as portas usadas com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="1bab3-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="1bab3-164">Se você clicar em uma porta específica no gráfico de pizza hello, restante de saudação do painel Olá filtrará para baixo tooflows da porta.</span><span class="sxs-lookup"><span data-stu-id="1bab3-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![figura3][3]

1. <span data-ttu-id="1bab3-166">Número de fluxos e a hora de Log mais antigo – métricas mostrando Olá o número de fluxos registradas e data de saudação do log mais antigo Olá capturada.</span><span class="sxs-lookup"><span data-stu-id="1bab3-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![figura4][4]

1. <span data-ttu-id="1bab3-168">Fluxos de NSG e regra – um gráfico de barras mostrando a distribuição de saudação de fluxos em cada NSG, bem como distribuição Olá regras dentro de cada NSG.</span><span class="sxs-lookup"><span data-stu-id="1bab3-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="1bab3-169">Aqui você pode ver quais NSG e as regras geradas Olá a maior parte do tráfego.</span><span class="sxs-lookup"><span data-stu-id="1bab3-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![figura5][5]

1. <span data-ttu-id="1bab3-171">10 principais origem/destino IPs – gráficos de barras, mostrando a fonte de 10 principais hello e IPs de destino.</span><span class="sxs-lookup"><span data-stu-id="1bab3-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="1bab3-172">Você pode ajustar essas tooshow gráficos IPs superior mais ou menos.</span><span class="sxs-lookup"><span data-stu-id="1bab3-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="1bab3-173">Aqui você pode consulte hello mais comumente ocorrendo IPs bem como Olá decisão de tráfego (permitir ou negar) que estão sendo feitas para cada IP.</span><span class="sxs-lookup"><span data-stu-id="1bab3-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figura6][6]

1. <span data-ttu-id="1bab3-175">Tuplas de fluxo – esta tabela mostra Olá informações contidas em cada tupla de fluxo, bem como seu NGS correspondente e a regra.</span><span class="sxs-lookup"><span data-stu-id="1bab3-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figura7][7]

<span data-ttu-id="1bab3-177">Usando a barra de consulta de saudação na parte superior de saudação do painel de saudação, você pode filtrar para baixo do painel de saudação com base em qualquer parâmetro de fluxos de saudação, como ID de assinatura, grupos de recursos, regra ou qualquer outra variável de interesse.</span><span class="sxs-lookup"><span data-stu-id="1bab3-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="1bab3-178">Para obter mais informações sobre filtros e consultas do Kibana, consulte toohello [documentação oficial](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="1bab3-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="1bab3-179">Conclusão</span><span class="sxs-lookup"><span data-stu-id="1bab3-179">Conclusion</span></span>

<span data-ttu-id="1bab3-180">Combinando registros de fluxo de grupo de segurança de rede Olá com hello pilha Elástico, ter obtemos toovisualize de maneira eficiente e personalizável o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="1bab3-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="1bab3-181">Esses painéis permitem que você obtenha tooquickly e compartilhem informações sobre o tráfego de rede, bem como filtro para baixo e investigar em qualquer anomalias em potencial.</span><span class="sxs-lookup"><span data-stu-id="1bab3-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="1bab3-182">Usando Kibana, você pode personalizar esses painéis e criar visualizações específicas toomeet necessidades de segurança, auditoria e conformidade.</span><span class="sxs-lookup"><span data-stu-id="1bab3-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bab3-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1bab3-183">Next steps</span></span>

<span data-ttu-id="1bab3-184">Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="1bab3-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
