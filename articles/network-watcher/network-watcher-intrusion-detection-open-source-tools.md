---
title: "detecção de intrusão de rede aaaPerform com ferramentas de software livre e o observador de rede do Azure | Microsoft Docs"
description: "Este artigo descreve como toouse observador de rede do Azure tooperform de ferramentas de software livre de rede e detecção de intrusões"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="af09e-103">Executar a detecção de invasão de rede com o Observador de Rede e ferramentas de software livre</span><span class="sxs-lookup"><span data-stu-id="af09e-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="af09e-104">Captura de pacote é um componente-chave para implementar sistemas de detecção de invasão de rede (IDS) e executar o Monitoramento de Segurança de Rede (NSM).</span><span class="sxs-lookup"><span data-stu-id="af09e-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="af09e-105">Há várias ferramentas de IDS de software livre que processam capturas de pacote e procuram assinaturas de possíveis invasões de rede e atividades mal-intencionadas.</span><span class="sxs-lookup"><span data-stu-id="af09e-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="af09e-106">Usando capturas de pacote hello fornecidas pelo observador de rede, você pode analisar para qualquer invasões prejudiciais ou vulnerabilidades em sua rede.</span><span class="sxs-lookup"><span data-stu-id="af09e-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="af09e-107">Uma dessas ferramentas de software livre é Suricata, um mecanismo de IDS que usa o tráfego de rede de toomonitor conjuntos de regras e dispara alertas sempre que ocorrerem eventos suspeitos.</span><span class="sxs-lookup"><span data-stu-id="af09e-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="af09e-108">O Suricata oferece um mecanismo de vários segmentos, o que significa que ele pode realizar análise de tráfego de rede com mais velocidade e eficiência.</span><span class="sxs-lookup"><span data-stu-id="af09e-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="af09e-109">Para obter mais detalhes sobre o Suricata e seus recursos, visite o site em https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="af09e-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="af09e-110">Cenário</span><span class="sxs-lookup"><span data-stu-id="af09e-110">Scenario</span></span>

<span data-ttu-id="af09e-111">Este artigo explica como tooset backup tooperform seu ambiente de rede usando o observador de rede, Suricata, a detecção de intrusão e Olá pilha Elástico.</span><span class="sxs-lookup"><span data-stu-id="af09e-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="af09e-112">Observador de rede oferece a que você com o pacote de saudação capturas usado tooperform detecção de intrusão de rede.</span><span class="sxs-lookup"><span data-stu-id="af09e-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="af09e-113">Captura de pacote de saudação do Suricata processos e gatilho alertas com base nos pacotes que correspondem a seu conjunto de regras específico de ameaças.</span><span class="sxs-lookup"><span data-stu-id="af09e-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="af09e-114">Esses alertas são armazenados em um arquivo de log no computador local.</span><span class="sxs-lookup"><span data-stu-id="af09e-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="af09e-115">Usando Olá pilha Elástico, logs de saudação gerados pela Suricata podem ser indexados e usado toocreate um painel Kibana, fornecendo uma representação visual dos logs de saudação e uma vulnerabilidade de rede significa tooquickly ganho insights toopotential.</span><span class="sxs-lookup"><span data-stu-id="af09e-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![cenário de aplicativo Web simples][1]

<span data-ttu-id="af09e-117">Ambas as ferramentas do código-fonte aberto podem ser configuradas em uma VM do Azure, permitindo que você tooperform essa análise dentro de seu próprio ambiente de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="af09e-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="af09e-118">Etapas</span><span class="sxs-lookup"><span data-stu-id="af09e-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="af09e-119">Instalar o Suricata</span><span class="sxs-lookup"><span data-stu-id="af09e-119">Install Suricata</span></span>

<span data-ttu-id="af09e-120">Para todos os outros métodos de instalação, visite http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="af09e-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="af09e-121">No terminal de linha de comando de saudação da VM execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="af09e-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="af09e-122">tooverify a instalação, execute o comando Olá `suricata -h` lista completa de saudação de toosee de comandos.</span><span class="sxs-lookup"><span data-stu-id="af09e-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="af09e-123">Baixar o conjunto de regras de ameaças emergentes Olá</span><span class="sxs-lookup"><span data-stu-id="af09e-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="af09e-124">Neste estágio, não temos todas as regras para Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="af09e-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="af09e-125">Se houver rede tooyour de ameaças específicas que deseja toodetect, ou você também pode usar desenvolvido conjuntos de regras de um número de provedores, como ameaças emergentes ou regras VRT Snort, você pode criar suas próprias regras.</span><span class="sxs-lookup"><span data-stu-id="af09e-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="af09e-126">Usamos Olá livremente acessível ameaças emergentes ruleset aqui:</span><span class="sxs-lookup"><span data-stu-id="af09e-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="af09e-127">Baixar o conjunto de regras de saudação e copie-os no diretório hello:</span><span class="sxs-lookup"><span data-stu-id="af09e-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="af09e-128">Capturas de pacotes de processo com o Suricata</span><span class="sxs-lookup"><span data-stu-id="af09e-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="af09e-129">pacote de tooprocess captura usando Suricata, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="af09e-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="af09e-130">toocheck Olá resultante alertas, ler Olá fast.log arquivo:</span><span class="sxs-lookup"><span data-stu-id="af09e-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="af09e-131">Configurar Olá pilha Elástico</span><span class="sxs-lookup"><span data-stu-id="af09e-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="af09e-132">Enquanto os logs de saudação que produz Suricata contêm informações valiosas sobre o que está acontecendo na rede, esses arquivos de log não são tooread mais fácil hello e entenderem.</span><span class="sxs-lookup"><span data-stu-id="af09e-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="af09e-133">Conectando Suricata com hello pilha Elástico, podemos criar um painel Kibana o que permite toosearch, gráfico, analisar e derivar informações de nossos logs.</span><span class="sxs-lookup"><span data-stu-id="af09e-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="af09e-134">Instalar Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="af09e-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="af09e-135">Olá Elástico pilha de versão 5.0 e superior requer Java 8.</span><span class="sxs-lookup"><span data-stu-id="af09e-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="af09e-136">Execute o comando Olá `java -version` toocheck sua versão.</span><span class="sxs-lookup"><span data-stu-id="af09e-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="af09e-137">Se você não tiver java de instalação, consulte toodocumentation em [site da Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="af09e-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="af09e-138">Baixe pacote de binário correto Olá para o seu sistema:</span><span class="sxs-lookup"><span data-stu-id="af09e-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="af09e-139">Outros métodos de instalação podem ser encontrados em [Instalação do Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="af09e-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="af09e-140">Verifique se Elasticsearch está em execução com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="af09e-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="af09e-141">Você verá um toothis semelhante de resposta:</span><span class="sxs-lookup"><span data-stu-id="af09e-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="af09e-142">Para obter mais instruções sobre pesquisa elástica instalar, consulte a página de toohello [instalação](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="af09e-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="af09e-143">Instalar Logstash</span><span class="sxs-lookup"><span data-stu-id="af09e-143">Install Logstash</span></span>

1. <span data-ttu-id="af09e-144">tooinstall Logstash execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="af09e-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="af09e-145">Em seguida, nós precisamos tooconfigure Logstash tooread da saída de saudação do arquivo eve.json.</span><span class="sxs-lookup"><span data-stu-id="af09e-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="af09e-146">Crie um arquivo logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="af09e-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="af09e-147">Adicionar Olá toohello conteúdo de arquivo a seguir (Verifique se o arquivo hello caminho toohello eve.json está correto):</span><span class="sxs-lookup"><span data-stu-id="af09e-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. <span data-ttu-id="af09e-148">Fazer com certeza toogive Olá permissões corretas toohello eve.json arquivo para que Logstash pode incluir o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="af09e-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="af09e-149">toostart Logstash executar comando hello:</span><span class="sxs-lookup"><span data-stu-id="af09e-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="af09e-150">Para obter mais informações sobre como instalar Logstash, consulte toohello [documentação oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="af09e-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="af09e-151">Instalar Kibana</span><span class="sxs-lookup"><span data-stu-id="af09e-151">Install Kibana</span></span>

1. <span data-ttu-id="af09e-152">Execute Olá comandos tooinstall Kibana a seguir:</span><span class="sxs-lookup"><span data-stu-id="af09e-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="af09e-153">toorun Kibana usar comandos de saudação:</span><span class="sxs-lookup"><span data-stu-id="af09e-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="af09e-154">tooview Kibana web interface, navegue até muito`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="af09e-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="af09e-155">Para este cenário, padrão de índice de Olá usado para Olá Suricata registra em log é "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="af09e-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="af09e-156">Se você quiser o painel de Kibana Olá tooview remotamente, criar uma regra NSG entrada permitindo acesso muito**porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="af09e-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="af09e-157">Criar um painel Kibana</span><span class="sxs-lookup"><span data-stu-id="af09e-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="af09e-158">Neste artigo, nós fornecemos um painel de exemplo para você tooview tendências e os detalhes de alertas.</span><span class="sxs-lookup"><span data-stu-id="af09e-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="af09e-159">Baixar o arquivo do painel Olá [aqui](https://aka.ms/networkwatchersuricatadashboard), arquivo de visualização de saudação [aqui](https://aka.ms/networkwatchersuricatavisualization)e o arquivo de pesquisa Olá salvada [aqui](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="af09e-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="af09e-160">Em Olá **gerenciamento** guia de Kibana, navegue muito**objetos salvos** e importar todos os três arquivos.</span><span class="sxs-lookup"><span data-stu-id="af09e-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="af09e-161">Depois de saudação **painel** guia você pode abrir e carga Olá painel de exemplo.</span><span class="sxs-lookup"><span data-stu-id="af09e-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="af09e-162">Você também pode criar suas próprias visualizações e painéis personalizados para métricas de seu próprio interesse.</span><span class="sxs-lookup"><span data-stu-id="af09e-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="af09e-163">Leia mais sobre como criar visualizações do Kibana na [documentação oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) do Kibana.</span><span class="sxs-lookup"><span data-stu-id="af09e-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![painel kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="af09e-165">Visualizar logs de alerta de IDS</span><span class="sxs-lookup"><span data-stu-id="af09e-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="af09e-166">Painel de exemplo Hello fornece várias visualizações dos logs de alertas de Suricata hello:</span><span class="sxs-lookup"><span data-stu-id="af09e-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="af09e-167">Alertas por GeoIP – um mapa mostrando a distribuição de saudação de alertas de seu país de origem com base na localização geográfica (determinada por IP)</span><span class="sxs-lookup"><span data-stu-id="af09e-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![ip geográfico][3]

1. <span data-ttu-id="af09e-169">Principais 10 alertas – um resumo de alertas de saudação 10 mais frequentes disparada e sua descrição.</span><span class="sxs-lookup"><span data-stu-id="af09e-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="af09e-170">Clicar em um alerta individual filtra informações de toohello painel Olá pertencentes alerta específico toothat.</span><span class="sxs-lookup"><span data-stu-id="af09e-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![image 4][4]

1. <span data-ttu-id="af09e-172">Número de alertas – Olá a contagem total de alertas disparados pela Olá ruleset</span><span class="sxs-lookup"><span data-stu-id="af09e-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![imagem 5][5]

1. <span data-ttu-id="af09e-174">IPs de origem/destino 20 principais/portas - gráficos de pizza mostrando Olá IPs 20 principais e portas que o alerta foram disparadas em.</span><span class="sxs-lookup"><span data-stu-id="af09e-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="af09e-175">Você pode filtrar para baixo em toosee específico de IPs/portas quantos e qual tipos de alertas de seja iniciada.</span><span class="sxs-lookup"><span data-stu-id="af09e-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![imagem 6][6]

1. <span data-ttu-id="af09e-177">Resumo de alertas – uma tabela de resumo de detalhes específicos de cada alerta individual.</span><span class="sxs-lookup"><span data-stu-id="af09e-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="af09e-178">Você pode personalizar essa tabela tooshow outros parâmetros de interesse para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="af09e-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![imagem 7][7]

<span data-ttu-id="af09e-180">Para obter mais documentação sobre a criação de painéis e visualizações personalizadas, consulte [documentação oficial do Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="af09e-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="af09e-181">Conclusão</span><span class="sxs-lookup"><span data-stu-id="af09e-181">Conclusion</span></span>

<span data-ttu-id="af09e-182">Combinando pacote captura fornecida pelo Observador de Rede e ferramentas de IDS de código-fonte aberto como Suricata, você pode executar detecção de invasão de rede para uma ampla variedade de ameaças.</span><span class="sxs-lookup"><span data-stu-id="af09e-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="af09e-183">Esses painéis permitem que você tooquickly identificar tendências e anomalias dentro de sua rede, também examinar Olá causas raiz de toodiscover de dados de alertas, como agentes de usuário mal-intencionado ou portas vulneráveis.</span><span class="sxs-lookup"><span data-stu-id="af09e-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="af09e-184">Com esses dados extraídos, você pode tomar decisões informadas sobre como tooreact tooand proteger sua rede de qualquer tentativa de invasão prejudiciais e criar regras tooprevent invasões futuras tooyour rede.</span><span class="sxs-lookup"><span data-stu-id="af09e-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af09e-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af09e-185">Next steps</span></span>

<span data-ttu-id="af09e-186">Saiba como tootrigger capturas de pacotes com base em alertas visitando [usar pacote captura toodo pró-ativo monitoramento de rede com funções do Azure](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="af09e-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="af09e-187">Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="af09e-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
