---
title: "Visualizar logs de fluxo NSG de Observador de Rede do Azure usando ferramentas de código aberto | Microsoft Docs"
description: "Esta página descreve como usar ferramentas de código aberto para visualizar logs de fluxo NSG."
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
ms.openlocfilehash: 20f60ccd9108a7473705c2368f28d3152d0dd614
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="161fa-103">Visualizar logs de fluxo NSG do Observador de Rede do Azure usando ferramentas de código aberto</span><span class="sxs-lookup"><span data-stu-id="161fa-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="161fa-104">Os logs de fluxo do Grupo de Segurança de Rede fornecem informações que podem ser usadas para entender a entrada e a saída de tráfego IP em Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="161fa-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="161fa-105">Esses logs de fluxo exibem os fluxos de entrada e saída baseados em regras. A NIC de fluxo se aplica às informações de 5 tuplas sobre o fluxo (IP de Origem/Destino, Porta de Origem/Destino e Protocolo) e se o tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="161fa-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="161fa-106">Esses logs de fluxo podem ser difíceis de serem analisados e de obter ideias de forma manual.</span><span class="sxs-lookup"><span data-stu-id="161fa-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="161fa-107">No entanto, há várias ferramentas de código livre que podem ajudar a visualizar esses dados.</span><span class="sxs-lookup"><span data-stu-id="161fa-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="161fa-108">Esse artigo fornece uma solução para visualizar esses logs usando o Elastic Stack que permite indexar e visualizar seus logs de fluxo em um painel Kibana.</span><span class="sxs-lookup"><span data-stu-id="161fa-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="161fa-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="161fa-109">Scenario</span></span>

<span data-ttu-id="161fa-110">Neste artigo, vamos configurar uma solução que permitirá a visualização dos logs de fluxo do Grupo de Segurança de Rede usando o Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="161fa-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="161fa-111">Um plug-in de entrada Logstash obterá os logs de fluxo diretamente do blob de armazenamento configurado para conter os logs do fluxo.</span><span class="sxs-lookup"><span data-stu-id="161fa-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="161fa-112">Em seguida, usando o Elastic Stack, os logs do fluxo serão indexados e usados para criar um painel Kibana para visualizar as informações.</span><span class="sxs-lookup"><span data-stu-id="161fa-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![cenário][scenario]

## <a name="steps"></a><span data-ttu-id="161fa-114">Etapas</span><span class="sxs-lookup"><span data-stu-id="161fa-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="161fa-115">Habilitar os registros em logs do fluxo do Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="161fa-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="161fa-116">Nessa situação, você deve habilitar o Registro em Log do Fluxo do Grupo de Segurança de Rede em um ou mais Grupos de Segurança de Rede em sua conta.</span><span class="sxs-lookup"><span data-stu-id="161fa-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="161fa-117">Confira o artigo [Introdução ao registro em log do fluxo para Grupos de Segurança de Rede](network-watcher-nsg-flow-logging-overview.md) para obter instruções sobre como habilitar os Logs do Fluxo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="161fa-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="161fa-118">Configurar o Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="161fa-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="161fa-119">Ao conectar os logs de fluxo NSG ao Elastic Stack, podemos criar um painel Kibana que nos permitirá pesquisar, criar gráficos, analisar e derivar informações de nossos logs.</span><span class="sxs-lookup"><span data-stu-id="161fa-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="161fa-120">Instalar Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="161fa-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="161fa-121">O Elastic Stack da versão 5.0 e superior exige o Java 8.</span><span class="sxs-lookup"><span data-stu-id="161fa-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="161fa-122">Execute o comando `java -version` para verificar sua versão.</span><span class="sxs-lookup"><span data-stu-id="161fa-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="161fa-123">Se você não tiver o java instalado, consulte a documentação no [site da Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="161fa-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="161fa-124">Baixe o pacote de binários correto para seu sistema:</span><span class="sxs-lookup"><span data-stu-id="161fa-124">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="161fa-125">Outros métodos de instalação podem ser encontrados em [Instalação do Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="161fa-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="161fa-126">Verifique se o Elasticsearch está sendo executado com o comando:</span><span class="sxs-lookup"><span data-stu-id="161fa-126">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="161fa-127">Você deve ver uma resposta semelhante a essa:</span><span class="sxs-lookup"><span data-stu-id="161fa-127">You should see a response similar to this:</span></span>

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

<span data-ttu-id="161fa-128">Para obter instruções adicionais sobre a instalação da pesquisa elástica, consulte a página [Instalação](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="161fa-128">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="161fa-129">Instalar Logstash</span><span class="sxs-lookup"><span data-stu-id="161fa-129">Install Logstash</span></span>

1. <span data-ttu-id="161fa-130">Para instalar o Logstash, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="161fa-130">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="161fa-131">Em seguida, precisamos configurar o Logstash para acessar e analisar os logs de fluxo.</span><span class="sxs-lookup"><span data-stu-id="161fa-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="161fa-132">Crie um arquivo logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="161fa-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="161fa-133">Adicione o seguinte conteúdo ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="161fa-133">Add the following content to the file:</span></span>

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

<span data-ttu-id="161fa-134">Para obter mais informações sobre como instalar o Logstash, consulte a [documentação oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="161fa-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="161fa-135">Instalar o plugin de entrada do Logstash para o armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="161fa-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="161fa-136">Esse plug-in do Logstash permitirá o acesso direto aos logs do fluxo por meio da conta de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="161fa-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="161fa-137">Para instalar esse plug-in, no diretório de instalação padrão do Logstash (nesse caso, /usr/share/logstash/bin), execute o comando:</span><span class="sxs-lookup"><span data-stu-id="161fa-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="161fa-138">Para iniciar o Logstash, execute o comando:</span><span class="sxs-lookup"><span data-stu-id="161fa-138">To start Logstash run the command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="161fa-139">Para obter mais informações sobre esse plug-in, consulte a documentação [aqui](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="161fa-139">For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="161fa-140">Instalar Kibana</span><span class="sxs-lookup"><span data-stu-id="161fa-140">Install Kibana</span></span>

1. <span data-ttu-id="161fa-141">Execute os seguintes comandos para instalar o Kibana:</span><span class="sxs-lookup"><span data-stu-id="161fa-141">Run the following commands to install Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="161fa-142">Para executar o Kibana, use os comandos:</span><span class="sxs-lookup"><span data-stu-id="161fa-142">To run Kibana use the commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="161fa-143">Para exibir a interface da Web do Kibana, navegue até `http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="161fa-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="161fa-144">Para esse cenário, o padrão de índice usado para os logs do fluxo é "nsg-flow-logs".</span><span class="sxs-lookup"><span data-stu-id="161fa-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="161fa-145">Você pode alterar o padrão de índice na seção "saída" do arquivo logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="161fa-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="161fa-146">Se você quiser exibir o painel Kibana remotamente, crie uma regra NSG de entrada permitindo o acesso à **porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="161fa-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="161fa-147">Criar um painel Kibana</span><span class="sxs-lookup"><span data-stu-id="161fa-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="161fa-148">Nesse artigo, fornecemos um painel de exemplo para exibir detalhes e tendências em seus alertas.</span><span class="sxs-lookup"><span data-stu-id="161fa-148">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

![figura 1][1]

1. <span data-ttu-id="161fa-150">Baixe o arquivo do painel [aqui](https://aka.ms/networkwatchernsgflowlogdashboard), o arquivo de visualização [aqui](https://aka.ms/networkwatchernsgflowlogvisualizations) e o arquivo de pesquisa salva [aqui](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="161fa-150">Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="161fa-151">Na guia **Management** (Gerenciamento) do Kibana, navegue até **Saved Objects** (Objetos Salvos) e importe todos os três arquivos.</span><span class="sxs-lookup"><span data-stu-id="161fa-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="161fa-152">Em seguida, na guia **Painel**, você pode abrir e carregar o painel de exemplo.</span><span class="sxs-lookup"><span data-stu-id="161fa-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="161fa-153">Você também pode criar suas próprias visualizações e painéis personalizados para métricas de seu próprio interesse.</span><span class="sxs-lookup"><span data-stu-id="161fa-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="161fa-154">Leia mais sobre como criar visualizações do Kibana a partir da [documentação oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) do Kibana.</span><span class="sxs-lookup"><span data-stu-id="161fa-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="161fa-155">Visualizar logs de fluxo NSG</span><span class="sxs-lookup"><span data-stu-id="161fa-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="161fa-156">O painel de exemplo fornece várias visualizações dos logs de fluxo:</span><span class="sxs-lookup"><span data-stu-id="161fa-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="161fa-157">Fluxos por Decisão/Direção ao Longo do Tempo - gráficos da série de tempo mostrando o número de fluxos durante o período de tempo.</span><span class="sxs-lookup"><span data-stu-id="161fa-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="161fa-158">Você pode editar a unidade de tempo e o alcance das duas visualizações.</span><span class="sxs-lookup"><span data-stu-id="161fa-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="161fa-159">Os Fluxos por Decisão mostram a proporção de permitir ou negar decisões tomadas, enquanto os Fluxos por Direção mostram a proporção do tráfego de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="161fa-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="161fa-160">Com esses elementos visuais, você pode examinar as tendências de tráfego ao longo do tempo e procure por picos ou padrões incomuns.</span><span class="sxs-lookup"><span data-stu-id="161fa-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![figura2][2]

1. <span data-ttu-id="161fa-162">Fluxos por Porta de Origem/Destino - gráficos de pizza mostrando a divisão dos fluxos pelas respectivas portas.</span><span class="sxs-lookup"><span data-stu-id="161fa-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="161fa-163">Nesta exibição, você pode ver as portas usadas com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="161fa-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="161fa-164">Se você clicar em uma porta específica dentro do gráfico de pizza, o restante do painel filtrará em busca de fluxos dessa porta.</span><span class="sxs-lookup"><span data-stu-id="161fa-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

  ![figura3][3]

1. <span data-ttu-id="161fa-166">Número de Fluxos e Hora do Primeiro Log - métricas mostrando o número de fluxos registrados e a data do primeiro log capturado.</span><span class="sxs-lookup"><span data-stu-id="161fa-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

  ![figura4][4]

1. <span data-ttu-id="161fa-168">Fluxos de NSG e Regra - um gráfico de barras mostrando a distribuição dos fluxos em cada NSG, além da distribuição de regras em cada NSG.</span><span class="sxs-lookup"><span data-stu-id="161fa-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="161fa-169">A partir daqui, você pode ver quais regras e NSG geraram mais tráfego.</span><span class="sxs-lookup"><span data-stu-id="161fa-169">From here you can see which NSG and rules generated the most traffic.</span></span>

  ![figura5][5]

1. <span data-ttu-id="161fa-171">Os 10 Principais IPs de Origem/Destino - gráficos de barras mostrando os 10 principais IPs de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="161fa-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="161fa-172">Você pode ajustar esses gráficos para mostrar mais ou menos IPs principais.</span><span class="sxs-lookup"><span data-stu-id="161fa-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="161fa-173">A partir daqui, você pode ver os IPs que ocorrem mais frequentemente, além da decisão de tráfego (permitir ou negar) tomada para cada IP.</span><span class="sxs-lookup"><span data-stu-id="161fa-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figura6][6]

1. <span data-ttu-id="161fa-175">Tuplas de Fluxo - essa tabela mostra as informações contidas em cada tupla de fluxo, além da regra e NGS correspondentes.</span><span class="sxs-lookup"><span data-stu-id="161fa-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figura7][7]

<span data-ttu-id="161fa-177">Usando a barra de consulta na parte superior do painel, você pode filtrar o conteúdo do painel com base nos parâmetros dos fluxos, como a ID da assinatura, grupos de recursos, regra ou qualquer outra variável de interesse.</span><span class="sxs-lookup"><span data-stu-id="161fa-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="161fa-178">Para obter mais informações sobre consultas e filtros do Kibana, consulte a [documentação oficial](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="161fa-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="161fa-179">Conclusão</span><span class="sxs-lookup"><span data-stu-id="161fa-179">Conclusion</span></span>

<span data-ttu-id="161fa-180">Combinando os logs de fluxo do Grupo de Segurança de Rede com o Elastic Stack, podemos encontrar uma maneira poderosa e personalizável para visualizar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="161fa-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="161fa-181">Esses painéis permitem obter e compartilhar informações sobre o tráfego de rede com rapidez, além de filtrar e investigar quaisquer possíveis anomalias.</span><span class="sxs-lookup"><span data-stu-id="161fa-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="161fa-182">Com o Kibana, você pode personalizar esses painéis e criar visualizações específicas para atender às necessidades de segurança, auditoria e conformidade.</span><span class="sxs-lookup"><span data-stu-id="161fa-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="161fa-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="161fa-183">Next steps</span></span>

<span data-ttu-id="161fa-184">Para saber como visualizar os logs de fluxo NSG com o Power BI, veja [Como visualizar logs de fluxos NSG com Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="161fa-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
