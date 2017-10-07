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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Visualizar logs de fluxo NSG do Observador de Rede do Azure usando ferramentas de código aberto

Os logs de fluxo do Grupo de Segurança de Rede fornecem informações que podem ser usadas para entender a entrada e a saída de tráfego IP em Grupos de Segurança de Rede. Esses logs de fluxo Mostrar saídas e fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, informações de tupla 5 sobre o fluxo de saudação (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego de saudação é permitido ou negado.

Esses logs de fluxo podem ser difícil toomanually análise e obter ideias de. No entanto, há várias ferramentas de código livre que podem ajudar a visualizar esses dados. Este artigo fornecem uma solução toovisualize esses logs usando Olá pilha Elástico, que permitem que você tooquickly índice e visualizar seus logs de fluxo em um painel Kibana.

## <a name="scenario"></a>Cenário

Neste artigo, podemos configurar uma solução que permitirá que você toovisualize logs de fluxo de grupo de segurança de rede usando Olá pilha Elástico.  Um plug-in de entrada de Logstash obterá logs de fluxo Olá diretamente saudação do blob de armazenamento configurada para que contém os logs de fluxo de saudação. Em seguida, os logs de fluxo hello usando Olá pilha Elástico, serão indexados e usado toocreate um Kibana painel toovisualize Olá de informações.

![cenário][scenario]

## <a name="steps"></a>Etapas

### <a name="enable-network-security-group-flow-logging"></a>Habilitar os registros em logs do fluxo do Grupo de Segurança de Rede
Nessa situação, você deve habilitar o Registro em Log do Fluxo do Grupo de Segurança de Rede em um ou mais Grupos de Segurança de Rede em sua conta. Para obter instruções sobre como ativar Logs de fluxo de segurança de rede, consulte toohello artigo a seguir [registro em log tooflow de Introdução para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Configurar Olá pilha Elástico
Conectando-se NSG fluxo de logs com hello pilha Elástico, podemos criar um painel Kibana o que permite toosearch, gráfico, analisar e derivar informações de nossos logs.

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
1. Em seguida precisamos tooconfigure Logstash tooaccess e analise logs de fluxo de saudação. Crie um arquivo logstash.conf usando:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Adicione Olá toohello conteúdo de arquivo a seguir:

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

Para obter mais informações sobre como instalar Logstash, consulte toohello [documentação oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Instalar Olá Logstash entrada plug-in para o armazenamento de BLOBs do Azure

Este plug-in Logstash permitirá que você os logs de fluxo de saudação do acesso toodirectly da sua conta de armazenamento designadas. tooinstall este plug-in do diretório de instalação de Logstash saudação padrão (em /usr/share/logstash/bin neste caso) execute Olá comando:

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash executar comando hello:

```
sudo /etc/init.d/logstash start
```

Para obter mais informações sobre este plug-in, consulte toodocumentation [aqui](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

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
1. Para este cenário, o padrão de índice de saudação usado para logs de fluxo de saudação é "logs de fluxo nsg". Você pode alterar o padrão de índice Olá Olá "saída" seção do arquivo logstash.conf.

1. Se você quiser o painel de Kibana Olá tooview remotamente, criar uma regra NSG entrada permitindo acesso muito**porta 5601**.

### <a name="create-a-kibana-dashboard"></a>Criar um painel Kibana

Neste artigo, nós fornecemos um painel de exemplo para você tooview tendências e os detalhes de alertas.

![figura 1][1]

1. Baixar o arquivo do painel Olá [aqui](https://aka.ms/networkwatchernsgflowlogdashboard), arquivo de visualização de saudação [aqui](https://aka.ms/networkwatchernsgflowlogvisualizations)e o arquivo de pesquisa Olá salvada [aqui](https://aka.ms/networkwatchernsgflowlogsearch).

1. Em Olá **gerenciamento** guia de Kibana, navegue muito**objetos salvos** e importar todos os três arquivos. Depois de saudação **painel** guia você pode abrir e carga Olá painel de exemplo.

Você também pode criar suas próprias visualizações e painéis personalizados para métricas de seu próprio interesse. Leia mais sobre como criar visualizações do Kibana a partir da [documentação oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) do Kibana.

### <a name="visualize-nsg-flow-logs"></a>Visualizar logs de fluxo NSG

Painel de exemplo Hello fornece várias visualizações de saudação fluxo logs:

1. Fluxos por decisão/direção ao longo do tempo - gráficos de série de tempo mostrando o número de saudação de fluxos em Olá período de tempo. Você pode editar unidade Olá de tempo e o intervalo de ambas as essas visualizações. Fluxos de decisão mostra Olá proporção de permitem ou negar as decisões tomadas durante fluxos por direção mostra Olá proporção do tráfego de entrada e saída. Com esses elementos visuais, você pode examinar as tendências de tráfego ao longo do tempo e procure por picos ou padrões incomuns.

  ![figura2][2]

1. Fluxos por porta de origem/destino – gráficos de pizza mostrando a divisão de saudação de fluxos tootheir respectivas portas. Nesta exibição, você pode ver as portas usadas com mais frequência. Se você clicar em uma porta específica no gráfico de pizza hello, restante de saudação do painel Olá filtrará para baixo tooflows da porta.

  ![figura3][3]

1. Número de fluxos e a hora de Log mais antigo – métricas mostrando Olá o número de fluxos registradas e data de saudação do log mais antigo Olá capturada.

  ![figura4][4]

1. Fluxos de NSG e regra – um gráfico de barras mostrando a distribuição de saudação de fluxos em cada NSG, bem como distribuição Olá regras dentro de cada NSG. Aqui você pode ver quais NSG e as regras geradas Olá a maior parte do tráfego.

  ![figura5][5]

1. 10 principais origem/destino IPs – gráficos de barras, mostrando a fonte de 10 principais hello e IPs de destino. Você pode ajustar essas tooshow gráficos IPs superior mais ou menos. Aqui você pode consulte hello mais comumente ocorrendo IPs bem como Olá decisão de tráfego (permitir ou negar) que estão sendo feitas para cada IP.

  ![figura6][6]

1. Tuplas de fluxo – esta tabela mostra Olá informações contidas em cada tupla de fluxo, bem como seu NGS correspondente e a regra.

  ![figura7][7]

Usando a barra de consulta de saudação na parte superior de saudação do painel de saudação, você pode filtrar para baixo do painel de saudação com base em qualquer parâmetro de fluxos de saudação, como ID de assinatura, grupos de recursos, regra ou qualquer outra variável de interesse. Para obter mais informações sobre filtros e consultas do Kibana, consulte toohello [documentação oficial](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Conclusão

Combinando registros de fluxo de grupo de segurança de rede Olá com hello pilha Elástico, ter obtemos toovisualize de maneira eficiente e personalizável o tráfego de rede. Esses painéis permitem que você obtenha tooquickly e compartilhem informações sobre o tráfego de rede, bem como filtro para baixo e investigar em qualquer anomalias em potencial. Usando Kibana, você pode personalizar esses painéis e criar visualizações específicas toomeet necessidades de segurança, auditoria e conformidade.

## <a name="next-steps"></a>Próximas etapas

Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
