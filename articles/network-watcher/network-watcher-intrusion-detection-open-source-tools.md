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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Executar a detecção de invasão de rede com o Observador de Rede e ferramentas de software livre

Captura de pacote é um componente-chave para implementar sistemas de detecção de invasão de rede (IDS) e executar o Monitoramento de Segurança de Rede (NSM). Há várias ferramentas de IDS de software livre que processam capturas de pacote e procuram assinaturas de possíveis invasões de rede e atividades mal-intencionadas. Usando capturas de pacote hello fornecidas pelo observador de rede, você pode analisar para qualquer invasões prejudiciais ou vulnerabilidades em sua rede.

Uma dessas ferramentas de software livre é Suricata, um mecanismo de IDS que usa o tráfego de rede de toomonitor conjuntos de regras e dispara alertas sempre que ocorrerem eventos suspeitos. O Suricata oferece um mecanismo de vários segmentos, o que significa que ele pode realizar análise de tráfego de rede com mais velocidade e eficiência. Para obter mais detalhes sobre o Suricata e seus recursos, visite o site em https://suricata-ids.org/.

## <a name="scenario"></a>Cenário

Este artigo explica como tooset backup tooperform seu ambiente de rede usando o observador de rede, Suricata, a detecção de intrusão e Olá pilha Elástico. Observador de rede oferece a que você com o pacote de saudação capturas usado tooperform detecção de intrusão de rede. Captura de pacote de saudação do Suricata processos e gatilho alertas com base nos pacotes que correspondem a seu conjunto de regras específico de ameaças. Esses alertas são armazenados em um arquivo de log no computador local. Usando Olá pilha Elástico, logs de saudação gerados pela Suricata podem ser indexados e usado toocreate um painel Kibana, fornecendo uma representação visual dos logs de saudação e uma vulnerabilidade de rede significa tooquickly ganho insights toopotential.  

![cenário de aplicativo Web simples][1]

Ambas as ferramentas do código-fonte aberto podem ser configuradas em uma VM do Azure, permitindo que você tooperform essa análise dentro de seu próprio ambiente de rede do Azure.

## <a name="steps"></a>Etapas

### <a name="install-suricata"></a>Instalar o Suricata

Para todos os outros métodos de instalação, visite http://suricata.readthedocs.io/en/latest/install.html

1. No terminal de linha de comando de saudação da VM execute Olá comandos a seguir:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify a instalação, execute o comando Olá `suricata -h` lista completa de saudação de toosee de comandos.

### <a name="download-hello-emerging-threats-ruleset"></a>Baixar o conjunto de regras de ameaças emergentes Olá

Neste estágio, não temos todas as regras para Suricata toorun. Se houver rede tooyour de ameaças específicas que deseja toodetect, ou você também pode usar desenvolvido conjuntos de regras de um número de provedores, como ameaças emergentes ou regras VRT Snort, você pode criar suas próprias regras. Usamos Olá livremente acessível ameaças emergentes ruleset aqui:

Baixar o conjunto de regras de saudação e copie-os no diretório hello:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Capturas de pacotes de processo com o Suricata

pacote de tooprocess captura usando Suricata, execute Olá comando a seguir:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck Olá resultante alertas, ler Olá fast.log arquivo:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Configurar Olá pilha Elástico

Enquanto os logs de saudação que produz Suricata contêm informações valiosas sobre o que está acontecendo na rede, esses arquivos de log não são tooread mais fácil hello e entenderem. Conectando Suricata com hello pilha Elástico, podemos criar um painel Kibana o que permite toosearch, gráfico, analisar e derivar informações de nossos logs.

#### <a name="install-elasticsearch"></a>Instalar Elasticsearch

1. Olá Elástico pilha de versão 5.0 e superior requer Java 8. Execute o comando Olá `java -version` toocheck sua versão. Se você não tiver java de instalação, consulte toodocumentation em [site da Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Baixe pacote de binário correto Olá para o seu sistema:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Outros métodos de instalação podem ser encontrados em [Instalação do Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)

1. Verifique se Elasticsearch está em execução com o comando hello:

    ```
    curl http://127.0.0.1:9200
    ```

    Você verá um toothis semelhante de resposta:

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

Para obter mais instruções sobre pesquisa elástica instalar, consulte a página de toohello [instalação](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Instalar Logstash

1. tooinstall Logstash execute Olá comandos a seguir:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Em seguida, nós precisamos tooconfigure Logstash tooread da saída de saudação do arquivo eve.json. Crie um arquivo logstash.conf usando:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Adicionar Olá toohello conteúdo de arquivo a seguir (Verifique se o arquivo hello caminho toohello eve.json está correto):

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

1. Fazer com certeza toogive Olá permissões corretas toohello eve.json arquivo para que Logstash pode incluir o arquivo hello.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash executar comando hello:

    ```
    sudo /etc/init.d/logstash start
    ```

Para obter mais informações sobre como instalar Logstash, consulte toohello [documentação oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-kibana"></a>Instalar Kibana

1. Execute Olá comandos tooinstall Kibana a seguir:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. toorun Kibana usar comandos de saudação:

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. tooview Kibana web interface, navegue até muito`http://localhost:5601`
1. Para este cenário, padrão de índice de Olá usado para Olá Suricata registra em log é "logstash-*"

1. Se você quiser o painel de Kibana Olá tooview remotamente, criar uma regra NSG entrada permitindo acesso muito**porta 5601**.

### <a name="create-a-kibana-dashboard"></a>Criar um painel Kibana

Neste artigo, nós fornecemos um painel de exemplo para você tooview tendências e os detalhes de alertas.

1. Baixar o arquivo do painel Olá [aqui](https://aka.ms/networkwatchersuricatadashboard), arquivo de visualização de saudação [aqui](https://aka.ms/networkwatchersuricatavisualization)e o arquivo de pesquisa Olá salvada [aqui](https://aka.ms/networkwatchersuricatasavedsearch).

1. Em Olá **gerenciamento** guia de Kibana, navegue muito**objetos salvos** e importar todos os três arquivos. Depois de saudação **painel** guia você pode abrir e carga Olá painel de exemplo.

Você também pode criar suas próprias visualizações e painéis personalizados para métricas de seu próprio interesse. Leia mais sobre como criar visualizações do Kibana na [documentação oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) do Kibana.

![painel kibana][2]

### <a name="visualize-ids-alert-logs"></a>Visualizar logs de alerta de IDS

Painel de exemplo Hello fornece várias visualizações dos logs de alertas de Suricata hello:

1. Alertas por GeoIP – um mapa mostrando a distribuição de saudação de alertas de seu país de origem com base na localização geográfica (determinada por IP)

    ![ip geográfico][3]

1. Principais 10 alertas – um resumo de alertas de saudação 10 mais frequentes disparada e sua descrição. Clicar em um alerta individual filtra informações de toohello painel Olá pertencentes alerta específico toothat.

    ![image 4][4]

1. Número de alertas – Olá a contagem total de alertas disparados pela Olá ruleset

    ![imagem 5][5]

1. IPs de origem/destino 20 principais/portas - gráficos de pizza mostrando Olá IPs 20 principais e portas que o alerta foram disparadas em. Você pode filtrar para baixo em toosee específico de IPs/portas quantos e qual tipos de alertas de seja iniciada.

    ![imagem 6][6]

1. Resumo de alertas – uma tabela de resumo de detalhes específicos de cada alerta individual. Você pode personalizar essa tabela tooshow outros parâmetros de interesse para cada alerta.

    ![imagem 7][7]

Para obter mais documentação sobre a criação de painéis e visualizações personalizadas, consulte [documentação oficial do Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Conclusão

Combinando pacote captura fornecida pelo Observador de Rede e ferramentas de IDS de código-fonte aberto como Suricata, você pode executar detecção de invasão de rede para uma ampla variedade de ameaças. Esses painéis permitem que você tooquickly identificar tendências e anomalias dentro de sua rede, também examinar Olá causas raiz de toodiscover de dados de alertas, como agentes de usuário mal-intencionado ou portas vulneráveis. Com esses dados extraídos, você pode tomar decisões informadas sobre como tooreact tooand proteger sua rede de qualquer tentativa de invasão prejudiciais e criar regras tooprevent invasões futuras tooyour rede.

## <a name="next-steps"></a>Próximas etapas

Saiba como tootrigger capturas de pacotes com base em alertas visitando [usar pacote captura toodo pró-ativo monitoramento de rede com funções do Azure](network-watcher-alert-triggered-packet-capture.md)

Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
