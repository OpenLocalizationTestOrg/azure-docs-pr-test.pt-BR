---
title: "aaaUsing Elasticsearch como um repositório de rastreamento de aplicativo do Service Fabric | Microsoft Docs"
description: "Descreve como aplicativos de serviço de malha podem usar toostore Elasticsearch e Kibana, índice e pesquisa por meio de rastreamentos do aplicativo (registros)"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Usar o Elasticsearch como um repositório de rastreamento do aplicativo Service Fabric
## <a name="introduction"></a>Introdução
Este artigo descreve como os aplicativos do [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) podem usar o **Elasticsearch** e o **Kibana** para armazenamento de rastreamento do aplicativo, indexação e pesquisa. [Elasticsearch](https://www.elastic.co/guide/index.html) é um mecanismo de análise e pesquisa em tempo real escalonável, distribuído de software livre adequado para essa tarefa. Ele pode ser instalado em máquinas virtuais Windows ou Linux em execução no Microsoft Azure. O Elasticsearch pode processar de maneira eficiente os rastreamentos *estruturados* produzidos usando tecnologias como **ETW (Rastreamento de Eventos para Windows)**.

O ETW é usado pelo Service Fabric runtime toosource informações de diagnóstico (rastreamentos). É Olá recomendado suas informações de diagnóstico de método para toosource de aplicativos do Service Fabric muito. Usando o mesmo mecanismo permite a correlação entre fornecidas pelo aplicativo e fornecidos pelo tempo de execução de rastreamentos e torna a solução de problemas de saudação. Modelos de projeto de malha do serviço no Visual Studio incluem uma API de registro em log (com base em Olá .NET **EventSource** classe) que emite rastreamentos ETW por padrão. Para obter uma visão geral do rastreamento de aplicativo do Service Fabric usando o ETW, consulte [Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Para rastreamentos de saudação tooshow backup em Elasticsearch, eles precisam toobe capturados em nós de cluster do Service Fabric Olá em tempo real (enquanto o aplicativo hello está sendo executado) e enviadas tooan Elasticsearch endpoint. Há duas opções principais para a captura de rastreamento:

* **Captura de rastreamento dentro do processo**  
  aplicativo Hello, ou mais precisamente, processo de serviço, é responsável pelo envio de repositório de rastreamento de toohello de dados de diagnóstico de saudação (Elasticsearch).
* **Captura de rastreamento fora do processo**  
  Um agente separado é capturar rastreamentos de processo do serviço hello ou processos e enviá-los toohello repositório de rastreamento.

Abaixo descrevemos como tooset backup Elasticsearch no Azure, discuta profissionais hello e contras tanto para capturar as opções e explicam como tooconfigure uma malha de serviço serviço toosend tooElasticsearch de dados.

## <a name="set-up-elasticsearch-on-azure"></a>Configurar o Elasticsearch no Azure
Olá tooset de maneira mais direta o serviço de Elasticsearch Olá no Azure é por meio de [ **modelos do Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Um [modelo do Gerenciador de Recursos do Azure de início rápido para Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) abrangente está disponível no repositório de modelos de início rápido do Azure. Este modelo usa contas de armazenamento separada para as unidades de escala (grupos de nós). Ele também pode provisionar nós de cliente e servidor separados com configurações diferentes e vários números de discos de dados anexados.

Aqui, podemos usar outro modelo, chamado **ES-vários nós** de saudação [repositório de ferramentas de diagnóstico do Azure](https://github.com/Azure/azure-diagnostics-tools). Este modelo é mais fácil toouse e cria um cluster Elasticsearch protegido pela autenticação básica HTTP. Antes de prosseguir, baixe repositório de saudação do GitHub tooyour máquina (por clonagem do repositório de saudação ou baixar um arquivo zip). modelo de saudação ES-vários nós está localizado na pasta de saudação com hello mesmo nome.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Preparar uma máquina toorun Elasticsearch scripts de instalação
Olá modelo de saudação ES-vários nós de toouse de maneira mais fácil é através de um script do PowerShell do Azure fornecido chamado `CreateElasticSearchCluster`. toouse esse script, você precisa de módulos do PowerShell tooinstall e uma ferramenta chamada **openssl**. Olá este último é necessário para criar uma chave SSH que pode ser usado tooadminister cluster Elasticsearch remotamente.

`CreateElasticSearchCluster`script destina-se a facilidade de uso com o modelo de saudação ES-vários nós de um computador Windows. É possível toouse Olá modelo em um computador diferente do Windows, mas esse cenário está além do escopo deste artigo hello.

1. Se você ainda não os tiver instalado, instale os [**módulos do Azure PowerShell**](http://aka.ms/webpi-azps). Quando solicitado, clique em **Executar** e em **Instalar**. O Azure PowerShell 1.3 ou mais recente é necessário.
2. Olá **openssl** ferramenta está incluída na distribuição de saudação de [ **Git para Windows**](http://www.git-scm.com/downloads). Se ainda não tiver feito isso, instale agora o [Git para Windows](http://www.git-scm.com/downloads) . (opções de instalação padrão Olá são Okey).
3. Supondo que Git foi instalado, mas não incluído no caminho do sistema hello, abra uma janela do Microsoft Azure PowerShell e execute Olá comandos a seguir:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Substituir saudação `<Git installation folder>` com o local do Git de saudação em seu computador; padrão Olá é **"C:\Program Files\Git"**. Observe o caractere de ponto e vírgula Olá no início de saudação do caminho de saudação primeiro.
4. Certifique-se de que você está conectado tooAzure (via [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) e que você selecionou a assinatura de saudação que deve ser usado toocreate cluster pesquisa Elástico. Você pode verificar se a assinatura correta foi selecionada usando os cmdlets `Get-AzureRmContext` e `Get-AzureRmSubscription`.
5. Se você ainda não tiver feito isso, altere a pasta de toohello ES-vários nós de diretório atual do hello.

### <a name="run-hello-createelasticsearchcluster-script"></a>Executar script de CreateElasticSearchCluster Olá
Antes de executar o script hello, abra Olá `azuredeploy-parameters.json` de arquivo e verificar ou fornecer valores para parâmetros de script hello. Olá parâmetros a seguir é fornecido:

| Nome do Parâmetro | Descrição |
| --- | --- |
| dnsNameForLoadBalancerIP |Olá nome que seja toocreate usado Olá publicamente visível DNS de cluster de pesquisa Elástico Olá (acrescentando nome de toohello fornecido Olá região do Azure domínio). Por exemplo, se esse valor de parâmetro é "myBigCluster" e a região do Azure Olá escolhido é Oeste dos EUA, o nome DNS resultante do Olá para cluster Olá é myBigCluster.westus.cloudapp.azure.com. <br /><br />Esse nome também serve como um nome de raiz para muitos artefatos associados Olá pesquisa Elástico cluster, como nomes de nó de dados. |
| adminUsername |nome de Olá Olá da conta de administrador para o gerenciamento de cluster de pesquisa Elástico hello (chaves SSH correspondentes são geradas automaticamente). |
| dataNodeCount |número de saudação de nós no cluster de pesquisa Elástico hello. versão atual de saudação do script hello não faz distinção entre nós de dados e consultas. todos os nós de executar as duas funções. Padrões too3 nós. |
| dataDiskSize |tamanho de saudação de discos de dados (em GB) que é alocado para cada nó de dados. Cada nó recebe 4 discos de dados, tooElastic dedicado exclusivamente o serviço de pesquisa. |
| region |nome de saudação da região do Azure em que o cluster de pesquisa Elástico Olá deve estar localizado. |
| esUserName |Olá, nome do usuário de saudação que é configurado cluster tooES de acesso toohave (autenticação básica do assunto tooHTTP). Olá senha não é parte do arquivo de parâmetros e deve ser fornecida quando `CreateElasticSearchCluster` script é invocado. |
| vmSizeDataNodes |Olá tamanho de máquina virtual do Azure para nós de cluster de pesquisa Elástico. TooStandard_D2 padrões. |

Agora você está pronto toorun script de saudação. Saudação de problema comando a seguir:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

onde 

| Nome do parâmetro do script | Descrição |
| --- | --- |
| `<es-group-name>` |nome de Olá Olá do Azure do grupo de recursos que contém todos os recursos de cluster de pesquisa Elástico. |
| `<azure-region>` |nome de saudação do hello região do Azure, onde o cluster de pesquisa Elástico Olá deve ser criado. |
| `<es-password>` |senha Olá Olá Elástico pesquisar usuário. |

> [!NOTE]
> Se você receber uma NullReferenceException de cmdlet Olá AzureResourceGroup de teste, você esqueceu toolog em tooAzure (`Add-AzureRmAccount`).
> 
> 

Se você receber um erro de execução de script hello e você determinar que o erro de saudação foi causado por um valor de parâmetro incorreto de modelo, corrija o arquivo de parâmetro hello e execute o script hello novamente com um nome de grupo de recursos diferente. Também é possível reutilizar Olá o mesmo nome do grupo de recursos e têm o script hello limpar Olá antigo adicionando Olá `-RemoveExistingResourceGroup` invocação de script do parâmetro toohello.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Resultado da execução do script de CreateElasticSearchCluster Olá
Depois de executar Olá `CreateElasticSearchCluster` script hello artefatos principais a seguir será criado. Para este exemplo, vamos supor que você usou "myBigCluster" como valor de saudação do hello `dnsNameForLoadBalancerIP` parâmetro e região Olá em que você criou o cluster Olá é Oeste dos EUA.

| Artefato | Nome, local e comentários |
| --- | --- |
| Chave SSH para administração remota |arquivo myBigCluster.key (no diretório de saudação de quais Olá CreateElasticSearchCluster foi executada). <br /><br />Esse arquivo pode ser usado tooconnect toohello admin nó e (por meio do nó de administração de saudação) toodata nós no cluster de saudação. |
| Nó de Admin |myBigCluster-admin.westus.cloudapp.azure.com  <br /><br />Uma VM dedicada para administração remota do cluster Elasticsearch - Olá apenas um que permita conexões externas do SSH. Ele é executado em Olá mesma rede virtual, como todos os nós de cluster Elasticsearch hello, mas não execute todos os serviços Elasticsearch. |
| Nós de dados |myBigCluster1 ... myBigCluster*N* <br /><br />Os nós de dados que estão executando os serviços Elasticsearch e Kibana. Você pode se conectar via SSH tooeach nó, mas apenas por meio do nó de administração de saudação. |
| Cluster Elasticsearch |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />Olá ponto de extremidade primário para o cluster de Elasticsearch de saudação (sufixo do Observação Olá /es). Ele é protegido por autenticação HTTP básica (credenciais Olá foram Olá especificado esUserName/esPassword parâmetros de modelo Olá ES-vários nós). cluster Olá também tem Olá head plug-in instalado (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) para a administração de cluster básico. |
| Serviço Kibana |http://myBigCluster.westus.cloudapp.azure.com <br /><br />Olá Kibana serviço é configurar os dados de tooshow de saudação criada cluster Elasticsearch. Ele é protegido por Olá mesmas credenciais de autenticação de saudação do cluster em si. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Captura de rastreamento dentro do processo versus fora do processo
Introdução de saudação mencionamos duas maneiras fundamentais de coleta de dados de diagnóstico: em processo e fora de processo. Cada uma tem suas vantagens e desvantagens.

Vantagens da saudação **-processo de captura de rastreamento** incluem:

1. *Fácil Configuração e implantação*
   
   * configuração de saudação da coleta de dados de diagnóstico é apenas parte da configuração de aplicativo hello. É fácil tooalways manter "sincronizado" com hello-rest do aplicativo hello.
   * A configuração por aplicativo ou por serviço é facilmente realizável.
   * Captura de rastreamento de saída do processo normalmente requer uma implantação separada e a configuração do agente de diagnóstico hello, que é uma tarefa administrativa adicional e uma fonte de erros em potencial. a tecnologia de determinado agente Olá geralmente permite apenas uma instância do agente de saudação por máquina virtual (nó). Isso significa que a configuração para a coleção de saudação da configuração de diagnóstico de saudação é compartilhada entre todos os aplicativos e serviços em execução nesse nó.
2. *Flexibilidade*
   
   * aplicativo Hello pode enviar dados Olá sempre que ele precisa toogo, enquanto há uma biblioteca de cliente que oferece suporte ao sistema de armazenamento de dados Olá direcionado. Novos coletores podem ser adicionados conforme desejado.
   * Regras de captura complexa, filtragem e agregação de dados podem ser implementadas.
   * Capturar um rastreamento de saída do processo geralmente é limitado pelo Coletores de dados de saudação que Olá agent dá suporte a. Alguns agentes são extensíveis.
3. *Contexto e acessar dados de aplicativo toointernal*
   
   * subsistema de diagnóstico Olá em execução no processo de aplicativo/serviço Olá facilmente pode aumentar rastreamentos Olá com informações contextuais.
   * Na abordagem de fora do processo Olá, dados saudação devem ser enviados tooan agent por meio de um mecanismo de comunicação entre processos, como o rastreamento de eventos do Windows. Esse mecanismo pode impor limitações adicionais.

Vantagens da saudação **rastreamento fora do processo de captura** incluem:

1. *Olá capacidade toomonitor Olá aplicativos e coletar despejos de memória*
   
   * Captura de rastreamento em processo pode ser bem-sucedida se o aplicativo hello falha toostart ou falha. Um agente independente tem muito mais chances de capturar informações de solução de problemas cruciais.<br /><br />
2. *Maturidade, eficiência e desempenho comprovados*
   
   * Um agente desenvolvido por um fornecedor de plataforma (como um agente de diagnóstico do Microsoft Azure) foi toorigorous assunto de teste e otimização batalha.
   * Com o rastreamento em processo captura, tome cuidado tooensure atividade de saudação do envio de dados de diagnóstico de um processo de aplicativo não interferir com tarefas principal do aplicativo hello ou introduzir problemas de desempenho ou de tempo. Um agente de forma independente em execução é diminui a probabilidade de problemas de toothese e é especificamente projetado toolimit seu impacto no sistema de saudação.

É possível toocombine e se beneficiam de ambas as abordagens. Na verdade, talvez seja melhor solução Olá para muitos aplicativos.

Aqui, podemos usar Olá **Microsoft.Diagnostic.Listeners biblioteca** e Olá em processo rastreamento captura dados toosend de um cluster do Service Fabric application tooan Elasticsearch.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Use Olá ouvintes biblioteca toosend dados de diagnóstico tooElasticsearch
a biblioteca de Microsoft.Diagnostic.Listeners Olá é parte do aplicativo de serviço de malha de exemplo PartyCluster. toouse-lo:

1. Baixar [exemplo de PartyCluster hello](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) do GitHub.
2. Copiar projetos Olá Microsoft.Diagnostics.Listeners e Microsoft.Diagnostics.Listeners.Fabric (pastas inteiros) de saudação PartyCluster exemplo diretório toohello pasta de solução de aplicativo hello que supostamente toosend Olá dados tooElasticsearch .
3. Abrir a solução de destino hello, clique nó solução Olá Olá Gerenciador de soluções e escolha **Adicionar projeto existente**. Adicione Olá Microsoft.Diagnostics.Listeners projeto toohello solução. Repetir hello mesmo para projeto de Microsoft.Diagnostics.Listeners.Fabric hello.
4. Adicione uma referência de projeto de seus projetos toohello dois adicionados projetos de serviço. (Cada serviço que supostamente toosend dados tooElasticsearch deve fazer referência Microsoft.Diagnostics.EventListeners e Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Bibliotecas de Microsoft.Diagnostics.EventListeners.Fabric e tooMicrosoft.Diagnostics.EventListeners de referências de projeto][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>A versão de Disponibilidade Geral do Service Fabric e o pacote Nuget Microsoft.Diagnostics.Tracing
Os aplicativos criados com a versão de Disponibilidade Geral do Service Fabric (2.0.135, lançada em 31 de março de 2016) são voltados para o **.NET Framework 4.5.2**. Esta versão é a versão mais recente de saudação do hello suportada pelo Azure no momento de saudação da versão GA de saudação do .NET Framework. Infelizmente, essa versão do framework de saudação não tem determinadas APIs EventListener que Olá Microsoft.Diagnostics.Listeners precisa de biblioteca. Como EventSource (componente do hello que constitui a base saudação do log de APIs em aplicativos de malha) e EventListener estreitamente ligado, cada projeto que usa a biblioteca de Microsoft.Diagnostics.Listeners Olá deve usar uma implementação alternativa de EventSource. Essa implementação é fornecida pelo Olá **pacote Microsoft.Diagnostics.Tracing Nuget**, criados pela Microsoft. pacote de saudação é totalmente compatível com EventSource incluído na estrutura de hello, portanto, nenhuma alteração de código deve ser necessária que não sejam as alterações de namespace referenciado.

toostart usando Olá Microsoft.Diagnostics.Tracing implementação da classe de EventSource hello, siga estas etapas para cada projeto de serviço que precisa toosend dados tooElasticsearch:

1. Clique com botão direito no projeto de serviço hello e escolha **gerenciar pacotes Nuget**.
2. Alternar toohello nuget.org origem do pacote (se não já estiver selecionada) e procure "**Microsoft.Diagnostics.Tracing**".
3. Instalar Olá `Microsoft.Diagnostics.Tracing.EventSource` pacote (e suas dependências).
4. Olá abrir **ServiceEventSource.cs** ou **ActorEventSource.cs** do arquivo em seu projeto de serviço e substitua Olá `using System.Diagnostics.Tracing` diretiva na parte superior do arquivo hello com hello `using Microsoft.Diagnostics.Tracing` diretiva.

Essas etapas não será necessárias uma vez Olá **do .NET Framework 4.6** é suportado pelo Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Configuração e instanciação de ouvinte de Elasticsearch
Olá etapa final para enviar dados de diagnóstico tooElasticsearch é toocreate uma instância de `ElasticSearchListener` e configurá-lo com dados de conexão Elasticsearch. ouvinte de saudação captura automaticamente todos os eventos gerados por meio de classes de EventSource definidas no projeto de serviço de saudação. Ele precisa toobe ativo durante o tempo de vida de saudação do serviço hello, então Olá melhor colocar toocreate está no código de inicialização do serviço de saudação. Aqui está como código de inicialização de saudação para um serviço sem monitoração de estado pode parecer após as alterações necessárias hello (adições indicadas em comentários, começando com `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Dados de conexão Elasticsearch devem ser colocados em uma seção separada no arquivo de configuração do serviço de saudação (**PackageRoot\Config\Settings.xml**). nome de saudação da seção de saudação deve corresponder toohello valor passado toohello `FabricConfigurationProvider` construtor, por exemplo:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Olá valores de `serviceUri`, `userName` e `password` parâmetros correspondem endereço de ponto de extremidade de cluster toohello Elasticsearch Elasticsearch nome de usuário e senha, respectivamente. `indexNamePrefix`é o prefixo Olá para índices de Elasticsearch; biblioteca de Microsoft.Diagnostics.Listeners Olá cria um novo índice para seus dados diariamente.

### <a name="verification"></a>Verificação
É isso! Agora, sempre que o serviço de saudação é executado, ele começa a enviar o serviço de Elasticsearch toohello rastreamentos especificado na configuração de saudação. Você pode verificar isso Olá abertura que kibana UI associado com a instância do hello destino Elasticsearch. Em nosso exemplo, o endereço da página Olá é http://myBigCluster.westus.cloudapp.azure.com/. Verifique se os índices com prefixo de nome de saudação escolhido para hello `ElasticSearchListener` instância realmente foram criados e preenchidos com dados.

![Kibana mostrando os eventos do aplicativo PartyCluster][2]

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre o diagnóstico e monitoramento de um serviço da Malha de Serviço](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
