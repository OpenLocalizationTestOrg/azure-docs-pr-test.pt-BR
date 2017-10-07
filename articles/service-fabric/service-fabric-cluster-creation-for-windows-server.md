---
title: "aaaCreate um cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Crie um cluster do Azure Service Fabric em qualquer computador (físico ou virtual) executando o Windows Server, seja ele local ou em qualquer nuvem."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Criar um cluster autônomo em execução no Windows Server
Você pode usar clusters de malha do serviço do Azure Service Fabric toocreate em quaisquer máquinas virtuais ou computadores que executam o Windows Server. Isso significa que você pode implantar e executar os aplicativos do Service Fabric em qualquer ambiente que tenha um conjunto de computadores com o Windows Server interconectados, seja localmente ou em qualquer provedor de nuvem. Serviço de malha fornece um toocreate de pacote de instalação que do Service Fabric clusters chamado de pacote do hello autônomo do Windows Server.

Este artigo o orienta pelas etapas de saudação para a criação de um cluster do Service Fabric autônomo.

> [!NOTE]
> Este pacote autônomo do Windows Server está disponível para venda e pode ser usado para implantações de produção. Este pacote pode conter novos recursos do Service Fabric que estão em “Visualização”. Role para baixo demais"[incluídos neste pacote de recursos de visualização](#previewfeatures_anchor)." seção para obter lista de saudação de recursos de visualização de saudação. Você pode [baixar uma cópia do EULA da saudação](http://go.microsoft.com/fwlink/?LinkID=733084) agora.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Obter suporte para o pacote de malha do serviço para o Windows Server Olá
* Perguntar comunidade Olá pacote do hello Service Fabric autônomo para o Windows Server em Olá [Fórum do Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Abra um tíquete de [Suporte Profissional para o Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).  Saiba mais sobre o Suporte Profissional da Microsoft [aqui](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* Você também pode obter suporte para este pacote como parte do [Suporte Premier da Microsoft](https://support.microsoft.com/en-us/premier).
* Para obter mais detalhes, consulte as [Opções de suporte do Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* logs de toocollect para fins de suporte, executados Olá [coletor de Log do serviço do Fabric autônomo](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Baixar pacote de malha do serviço para o Windows Server Olá
cluster de Olá toocreate, use o pacote de malha do serviço para o Windows Server hello (Windows Server 2012 R2 e mais recente) encontradas aqui: <br>
[Link de Download – pacote autônomo do Service Fabric – Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

Encontrar detalhes sobre o conteúdo do pacote de saudação [aqui](service-fabric-cluster-standalone-package-contents.md).

pacote de tempo de execução do Service Fabric Olá é baixado automaticamente no momento da criação do cluster. Se a implantação de um computador não conectado toohello internet, baixe o pacote de tempo de execução de saudação fora da banda em aqui: <br>
[Link de Download – Tempo de Execução do Service Fabric – Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

Encontre amostras de configuração de cluster autônomo em: <br>
[Amostras de configuração de cluster autônomo](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Criar cluster Olá
Malha do serviço pode ser implantado tooa cluster de desenvolvimento de um computador usando Olá *ClusterConfig.Unsecure.DevCluster.json* arquivo incluído no [exemplos](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Desempacotar máquina do hello autônoma pacote tooyour, cópia Olá exemplo config arquivo toohello máquina local e execução Olá *CreateServiceFabricCluster.ps1* script por meio de uma sessão do PowerShell de administrador, do hello autônomo pasta do pacote:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Etapa 1A: criar um cluster de desenvolvimento local desprotegido
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Consulte Olá a seção de configuração do ambiente no [planejar e preparar a implantação de cluster](service-fabric-cluster-standalone-deployment-preparation.md) para obter detalhes de solução de problemas.

Se você concluiu os cenários de desenvolvimento em execução, você pode remover o cluster do Service Fabric Olá da máquina Olá referindo toosteps na seção "[remover um cluster](#removecluster_anchor)". 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Etapa 1B: criar um cluster com vários computadores
Depois de você ter feito Olá planejamento e etapas de preparação detalhadas em Olá abaixo do link, você está pronto toocreate seu cluster de produção usando o arquivo de configuração do cluster. <br>
[Planejar e preparar a implantação do cluster](service-fabric-cluster-standalone-deployment-preparation.md)

1. Validar o arquivo de configuração Olá escrevê executando Olá *TestConfiguration.ps1* script hello autônomo da pasta do pacote:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Você deverá ver uma saída como a abaixo. Se o campo de último hello "Aprovado" é retornado como "True", verificações de integridade tiveram passado e cluster Olá parece com base na configuração de entrada hello toobe implantável.

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. Criar cluster Olá: executar Olá *CreateServiceFabricCluster.ps1* cluster do script toodeploy saudação do Service Fabric em cada computador na configuração de saudação. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Os rastreamentos de implantação são gravados toohello VM/máquina em que você executou o script do PowerShell CreateServiceFabricCluster.ps1 hello. Eles podem ser encontrados na subpasta Olá DeploymentTraces, com base no diretório de saudação do qual Olá script foi executado. toosee se a malha do serviço foi implantado corretamente tooa máquina, localizar arquivos de Olá instalado no diretório de FabricDataRoot hello, conforme detalhado no arquivo de configuração de cluster Olá FabricSettings seção (por padrão c:\ProgramData\SF). Além disso, processos FabricHost.exe e Fabric.exe podem ser vistos em execução no Gerenciador de Tarefas.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Etapa 1C: Criar um cluster offline (desconectado da Internet)
pacote de tempo de execução do Service Fabric Olá é baixado automaticamente na criação do cluster. Ao implantar um cluster toomachines não conectado toohello internet, você precisará Olá toodownload Service Fabric runtime separadamente do pacote e fornecer Olá caminho tooit na criação do cluster.
Olá pacote de tempo de execução pode ser baixado separadamente, de outro computador conectado toohello internet, em [o Link de Download - tempo de execução do serviço de malha - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Copiar Olá toowhere de pacote em tempo de execução você está implantando o cluster offline de saudação do e cria cluster Olá executando `CreateServiceFabricCluster.ps1` com hello `-FabricRuntimePackagePath` parâmetro incluído, conforme mostrado abaixo: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
onde `.\ClusterConfig.json` e `.\MicrosoftAzureServiceFabric.cab` são configuração de cluster Olá caminhos toohello e CAB de tempo de execução-Olá, respectivamente.


### <a name="step-2-connect-toohello-cluster"></a>Etapa 2: Conectar toohello cluster
tooconnect tooa o cluster seguro, consulte [do Service fabric se conectar a cluster toosecure](service-fabric-connect-to-secure-cluster.md).

tooconnect tooan não segura cluster, execute Olá comando PowerShell a seguir:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Exemplo:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Etapa 3: abrir o Service Fabric Explorer
Agora você pode se conectar toohello cluster Service Fabric Explorer diretamente de uma das máquinas Olá http://localhost:19080/Explorer/index.html ou remotamente com http://<;*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Adicionar e remover nós
Você pode adicionar ou remover o cluster do Service Fabric de nós tooyour autônomo conforme suas necessidades comerciais mudarem. Consulte [adicionar ou remover nós tooa Service Fabric autônomo cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) para obter etapas detalhadas.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Remover um cluster
tooremove um cluster, execute Olá *RemoveServiceFabricCluster.ps1* script do PowerShell na pasta de pacote de saudação e passe o arquivo de configuração do hello caminho toohello JSON. Opcionalmente, você pode especificar um local para o log de saudação de exclusão de saudação.

Esse script pode ser executado em qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós em um arquivo de configuração de cluster de saudação. máquina de saudação que esse script é executado no não tem toobe parte do cluster de saudação.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Dados de telemetria coletados e como tooopt fora dele
Por padrão, produto Olá coleta a telemetria no hello Service Fabric uso tooimprove Olá de produto. Olá analisador de práticas recomendadas que é executado como parte da instalação Olá verifica a conectividade muito[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Se não estiver acessível, a instalação de saudação falhará a menos que você recusar a telemetria.

1. pipeline de telemetria Hello tenta Olá tooupload seguintes dados muito[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) uma vez por dia. Ele é um carregamento de melhor esforço e não tem nenhum impacto sobre a funcionalidade do cluster hello. Telemetria de saudação é enviada apenas do nó Olá executa Olá principal do Gerenciador de failover. Nenhum outro nó envia telemetria.
2. Telemetria Olá consiste em seguir hello:

* Número de serviços
* Número de ServiceTypes
* Número de Aplicativos
* Número de ApplicationUpgrades
* Número de FailoverUnits
* Número de InBuildFailoverUnits
* Número de UnhealthyFailoverUnits
* Número de Réplicas
* Número de InBuildReplicas
* Número de StandByReplicas
* Número de OfflineReplicas
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Número de Nós
* IsContextComplete: True/False
* ClusterId: esse é um GUID gerado aleatoriamente para cada cluster
* ServiceFabricVersion
* Endereço IP da máquina virtual de saudação ou máquina na qual Olá telemetria é carregada

Telemetria toodisable, adicionar Olá seguir muito*propriedades* na sua configuração de cluster: *enableTelemetry: false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Recursos de preview incluídos neste pacote
Nenhuma.


> [!NOTE]
> Começando com hello novo [versão GA do cluster do hello autônomo para o Windows Server (versão 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), você pode atualizar versões toofuture cluster, manual ou automaticamente. Consulte também[atualizar uma versão de cluster do Service Fabric autônomo](service-fabric-cluster-upgrade-windows-server.md) documento para obter detalhes.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Implantar e remover aplicativos usando o PowerShell](service-fabric-deploy-remove-applications.md)
* [Definições de configuração para o cluster autônomo no Windows](service-fabric-cluster-manifest.md)
* [Adicionar ou remover nós tooa autônomo do Service Fabric cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Atualizar uma versão autônoma de cluster do Service Fabric](service-fabric-cluster-upgrade-windows-server.md)
* [Criar um cluster do Service Fabric autônomo com VMs do Azure executando o Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Proteger um cluster autônomo no Windows usando a segurança](service-fabric-windows-cluster-windows-security.md)
* [Proteger um cluster autônomo no Windows usando os certificados X509](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
