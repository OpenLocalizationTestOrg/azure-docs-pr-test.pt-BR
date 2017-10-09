---
title: "aaaAzure aplicativo de orquestração de patch do Service Fabric | Microsoft Docs"
description: Tooautomate aplicativo operacional patches do sistema em um cluster do Service Fabric.
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Patch do sistema de operacional do Windows hello no cluster do Service Fabric

aplicativo de orquestração de patch Hello é um aplicativo do Azure Service Fabric que automatiza o sistema operacional a aplicação de patch em um cluster do Service Fabric no Azure sem tempo de inatividade.

Olá patch orquestração aplicativo fornece a seguir hello:

- **Instalação da atualização automática do sistema operacional**. Atualizações do sistema operacional são baixadas e instaladas automaticamente. Nós de cluster são reiniciados conforme necessário, sem tempo de inatividade do cluster.

- **Aplicação de patch com suporte a cluster e integração de integridade**. Durante a aplicação de atualizações, Olá patch orquestração aplicativo monitora a integridade de Olá Olá de nós de cluster. Os nós de cluster fazem upgrade de um nó ou um domínio de atualização por vez. Se a integridade de saudação do cluster Olá falhar devido a processo de aplicação de patch toohello, aplicação de patch é interrompido tooprevent aggravating problema hello.

## <a name="internal-details-of-hello-app"></a>Detalhes internos de aplicativo hello

aplicativo de orquestração de patch Olá é composto de saudação subcomponentes a seguir:

- **Serviço de Coordenador**: este serviço com estado é responsável por:
    - Coordenar o trabalho de atualização do Windows hello em todo o cluster hello.
    - Armazena o resultado de saudação das operações concluídas do Windows Update.
- **Serviço de Agente do Nó**: é um serviço sem estado, executado em todos os nós de cluster do Service Fabric. serviço de saudação é responsável por:
    - Olá NTService de agente do nó de inicialização.
    - Olá NTService do nó do agente de monitoramento.
- **NTService do Agente do Nó**: este serviço Windows NT é executado em um privilégio de nível superior (SISTEMA). Por outro lado, Olá nó serviço de agente e hello serviço Coordenador de execute em um nível mais baixo de privilégio (serviço de rede). serviço de saudação é responsável pela execução Olá trabalhos de atualização do Windows a seguir em todos os nós de cluster hello:
    - Desabilitar atualização automática do Windows no nó de saudação.
    - Baixando e instalando o Windows Update de acordo com o usuário de saudação do toohello política foi fornecido.
    - Postagem de máquina Olá reiniciar a instalação do Windows Update.
    - Carregando resultados de saudação do toohello de atualizações do Windows o serviço de coordenador.
    - Relatórios de integridade de relatórios no caso de falha na operação após esgotar todas as novas tentativas.

> [!NOTE]
> Olá patch orquestração aplicativo usa Olá Service Fabric reparar toodisable de serviço de sistema do Gerenciador ou habilitar nó hello e realiza verificações de integridade. tarefa de reparo do Hello criada pelo Olá Olá patch orquestração aplicativo rastreia andamento da atualização do Windows para cada nó.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="minimum-supported-service-fabric-runtime-version"></a>Versão de tempo de execução do Service Fabric com suporte mínimo

#### <a name="azure-clusters"></a>Clusters do Azure
Olá patch orquestração aplicativo deve ser executado no Azure clusters que têm v 5.5 do Service Fabric runtime versão ou posterior.

#### <a name="standalone-on-premises-clusters"></a>Clusters locais autônomos
Olá patch orquestração aplicativo deve ser executado em clusters autônomo com v 5.6 de versão de tempo de execução do Service Fabric ou posterior.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Habilitar o serviço de Gerenciador de reparo do hello (se ele não está funcionando)

Olá patch orquestração aplicativo requer Olá reparo manager sistema serviço toobe habilitada no cluster hello.

#### <a name="azure-clusters"></a>Clusters do Azure

Clusters do Azure na camada de durabilidade prata Olá tem Olá reparar service manager habilitado por padrão. Clusters do Azure na camada de durabilidade gold Olá podem ou não podem ter o serviço de Gerenciador de reparo do hello habilitado, dependendo de quando os clusters foram criados. Clusters do Azure na camada de durabilidade bronze hello, por padrão, não têm Olá reparar service manager habilitado. Se o serviço de saudação já estiver habilitado, você pode ver em execução na seção de serviços de sistema Olá em Olá Service Fabric Explorer.

##### <a name="azure-portal"></a>Portal do Azure
Você pode habilitar o Gerenciador de reparo do portal do Azure em tempo de saudação de configuração de cluster. Selecione `Include Repair Manager` opção em `Add on features` no tempo de saudação da configuração de Cluster.
![Imagem do Gerenciador de reparo de habilitação do portal do Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Modelo do Azure Resource Manager
Como alternativa, você pode usar Olá [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) serviço de Gerenciador de reparo tooenable Olá em clusters de malha de serviço novos e existentes. Obter modelo Olá cluster Olá que você deseja toodeploy. Você pode usar modelos de exemplo hello ou criar um modelo personalizado do Gerenciador de recursos. 

serviço tooenable Olá reparo Gerenciador usando [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Primeiro, verifique que Olá `apiversion` está definido muito`2017-07-01-preview` para Olá `Microsoft.ServiceFabric/clusters` recurso, conforme mostrado no hello trecho de código a seguir. Se ele for diferente, você precisará Olá tooupdate `apiVersion` toohello valor `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Agora habilitar o serviço de Gerenciador de reparo do hello adicionando Olá seguintes `addonFeatures` seção após Olá `fabricSettings` seção:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Depois de atualizar o modelo de cluster com essas alterações, aplicá-las e que a atualização de saudação concluir. Agora você pode ver o serviço do sistema Olá reparo manager em execução no cluster. Ele é chamado `fabric:/System/RepairManagerService` na seção de serviços de sistema Olá em Olá Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Clusters locais autônomos

Você pode usar o hello [definições de configuração para o cluster do Windows autônoma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) serviço de Gerenciador de reparo tooenable Olá no cluster do Service Fabric novo e existente.

serviço de Gerenciador de reparo do hello tooenable:

1. Primeiro, verifique que Olá `apiversion` na [configurações de cluster geral](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) está definido muito`04-2017` ou superior:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Agora ativar o serviço de Gerenciador de reparo adicionando Olá seguintes `addonFeaturres` seção após Olá `fabricSettings` seção conforme mostrado abaixo:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Atualizar o manifesto do cluster com essas alterações, usando o manifesto do cluster Olá atualizado [criar um novo cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) ou [configuração de cluster de atualização Olá](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Depois que o cluster hello está sendo executado com o manifesto de cluster atualizado, agora você pode ver em execução no seu cluster, que é chamado de serviço do sistema Olá reparo Gerenciador `fabric:/System/RepairManagerService`, em serviços de sistema seção no Gerenciador do Service Fabric hello.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Desabilite o Windows Update automático em todos os nós

Atualizações automáticas do Windows podem causar perda de tooavailability porque vários nós de cluster podem reiniciar Olá mesmo tempo. aplicativo de orquestração de patch Hello, por padrão, as tentativas toodisable Olá atualização automática do Windows em cada nó de cluster. No entanto, se as configurações de saudação são gerenciadas por um administrador ou a diretiva de grupo, é recomendável Olá configuração Windows Update política muito "notificar antes de baixar" explicitamente.

### <a name="optional-enable-azure-diagnostics"></a>Opcional: habilitar o Diagnóstico do Microsoft Azure

Clusters que executam a versão de tempo de execução do Service Fabric `5.6.220.9494` e acima de logs de aplicativo de orquestração patch coletar como parte da malha do serviço de logs.
Você pode ignorar esta etapa se o cluster está em execução na versão de tempo de execução do Service Fabric `5.6.220.9494` e acima.

Para clusters que executam a versão de tempo de execução do Service Fabric menor `5.6.220.9494`, logs do aplicativo de orquestração de patch Olá são coletados localmente em cada um de nós de cluster de saudação.
É recomendável que você configurar logs de tooupload de diagnóstico do Azure de todos os local central tooa de nós.

Para obter mais informações sobre o Diagnóstico do Microsoft Azure, consulte [Coletar logs usando o Diagnóstico do Microsoft Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Logs do aplicativo de orquestração de patch Olá são gerados no hello provedor fixa IDs a seguir:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

No Gerenciador de recursos modelo goto `EtwEventSourceProviderConfiguration` seção em `WadCfg` e adicione Olá entradas a seguir:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Se o cluster do Service Fabric tem vários tipos de nó, seção anterior Olá deve ser adicionada para Olá todos os `WadCfg` seções.

## <a name="download-hello-app-package"></a>Baixe o pacote do aplicativo hello

Baixar o aplicativo hello da saudação [link de download](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Configurar aplicativo hello

Olá o comportamento do aplicativo de orquestração de patch Olá pode ser configurado toomeet suas necessidades. Substitua valores de padrão de saudação pela passagem de parâmetro de saudação do aplicativo durante a criação do aplicativo ou atualização. Parâmetros do aplicativo podem ser fornecidos especificando `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` ou `New-ServiceFabricApplication` cmdlets.

|**Parâmetro**        |**Tipo**                          | **Detalhes**|
|:-|-|-|
|MaxResultsToCache    |long                              | Número máximo de resultados do Windows Update, que devem ser armazenados em cache. <br>O valor padrão é 3000, supondo que o: <br> - Número de nós é 20. <br> - Número de atualizações acontecendo em um nó por mês seja de cinco. <br> – Número de resultados por operação possa ser de 10. <br> -Resultados de saudação últimos três meses devem ser armazenados. |
|TaskApprovalPolicy   |Enum <br> { NodeWise, UpgradeDomainWise }                          |TaskApprovalPolicy indica a diretiva de saudação toobe usada por atualizações do Windows hello serviço tooinstall em nós de cluster do Service Fabric hello.<br>                         Valores permitidos são: <br>                                                           <b>NodeWise</b>. O Windows Update é instalado em um nó por vez. <br>                                                           <b>UpgradeDomainWise</b>. O Windows Update é instalado em um domínio de atualização por vez. (No máximo de hello, todos os nós de saudação pertencentes tooan domínio de atualização podem ir para o Windows Update).
|LogsDiskQuotaInMB   |long  <br> (Padrão: 1024)               |Tamanho máximo dos logs do aplicativo de orquestração de patch em MB, que pode ser mantido localmente no nó.
| WUQuery               | string<br>(Padrão: "IsInstalled=0")                | Consulta tooget atualizações do Windows. Para obter mais informações, consulte [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)
| InstallWindowsOSOnlyUpdates | Bool <br> (padrão: True)                 | Esse sinalizador permite que o Windows operacional toobe de atualizações do sistema instalado.            |
| WUOperationTimeOutInMinutes | int <br>(Padrão: 90)                   | Especifica o tempo limite de saudação para qualquer operação de atualização do Windows (Pesquisar ou baixar ou instalar). Se a operação de saudação não foi concluída dentro de Olá tempo limite especificado, ele será anulado.       |
| WURescheduleCount     | int <br> (Padrão: 5)                  | o número de vezes que serviço Olá reagenda Olá máximo Olá Windows update no caso de uma operação falha de maneira persistente.          |
| WURescheduleTimeInMinutes | int <br>(Padrão: 30) | intervalo de saudação em qual Olá serviço reagenda Olá Windows update no caso de falha persistir. |
| WUFrequency           | Cadeia de caracteres separada por vírgula (padrão: "Semanalmente, quarta-feira, 7:00:00")     | frequência de saudação para instalar o Windows Update. Olá formato e os valores possíveis são: <br>-   Mensal, DD, HH:MM:SS, por exemplo, Mensal, 5, 12:22:32. <br> -   Semanal, DIA, HH:MM:SS, por exemplo, Semanal, terça-feira, 12:22:32.  <br> -   Diário, HH:MM:SS, por exemplo, Diário, 12:22:32.  <br> -  Nenhum indica que o Windows Update não deve ser executado.  <br><br> Observe que todos os tempos de saudação estão em UTC.|
| AcceptWindowsUpdateEula | Bool <br>(Padrão: true) | Ao definir esse sinalizador, o aplicativo hello aceita saudação do usuário final licença contrato para o Windows Update em nome do proprietário de saudação da máquina de saudação.              |

> [!TIP]
> Se você quiser Windows Update toohappen imediatamente, defina `WUFrequency` toohello relativo tempo de implantação de aplicativo. Por exemplo, suponha que você tenha um aplicativo teste de nó de cinco cluster e planejar toodeploy Olá em cerca de 5:00 PM UTC. Se você presumir que a implantação ou atualização do aplicativo hello leva 30 minutos no Olá Olá máximo, defina WUFrequency como "Diariamente, 17:30:00."

## <a name="deploy-hello-app"></a>Implantar o aplicativo hello

1. Conclua todos os cluster de Olá Olá etapas de pré-requisito tooprepare.
2. Implante o aplicativo de orquestração de patch de saudação como qualquer outro aplicativo de malha do serviço. Você pode implantar o aplicativo hello usando o PowerShell. Siga as etapas de saudação em [implantar e remover aplicativos usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. aplicativo de Olá tooconfigure em tempo de saudação de implantação, passe Olá `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet. Para sua conveniência, fornecemos script hello Deploy.ps1 juntamente com o aplicativo hello. script de saudação toouse:

    - Conecte-se o cluster do Service Fabric tooa usando `Connect-ServiceFabricCluster`.
    - Executar script do PowerShell Olá Deploy.ps1 com hello apropriado `ApplicationParameter` valor.

> [!NOTE]
> Manter script hello e pasta de aplicativo hello PatchOrchestrationApplication em Olá mesmo diretório.

## <a name="upgrade-hello-app"></a>Atualizar o aplicativo hello

tooupgrade um aplicativo de orquestração de patch existente usando o PowerShell, execute as etapas de saudação em [atualização do aplicativo do Service Fabric usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Remover o aplicativo hello

aplicativo do tooremove hello, siga etapas de saudação em [implantar e remover aplicativos usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Para sua conveniência, fornecemos script hello Undeploy.ps1 juntamente com o aplicativo hello. script de saudação toouse:

  - Conecte-se o cluster do Service Fabric tooa usando ```Connect-ServiceFabricCluster```.

  - Execute o script do PowerShell Olá Undeploy.ps1.

> [!NOTE]
> Manter script hello e pasta de aplicativo hello PatchOrchestrationApplication em Olá mesmo diretório.

## <a name="view-hello-windows-update-results"></a>Exibir resultados da atualização do Windows hello

Olá patch orquestração aplicativo expõe o usuário de toohello APIs REST toodisplay Olá resultados históricos. Um exemplo de resultado de saudação JSON:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Se nenhuma atualização estiver agendada ainda, o resultado de saudação JSON está vazio.

Registrar resultados em toohello cluster tooquery Windows Update. Em seguida, descobrir Olá endereço de réplica para o primário Olá Olá serviço Coordenador de e pressione Olá URL do navegador de saudação: http://&lt;IP de réplica&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

Olá o ponto de extremidade REST para Olá serviço tem uma porta dinâmica. toocheck Olá URL exata, consulte toohello Service Fabric Explorer. Por exemplo, os resultados de saudação estão disponíveis em `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Imagem do ponto de extremidade REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Se o proxy reverso Olá estiver habilitado no cluster Olá, você pode acessar Olá a URL de fora do cluster hello.
Olá ponto de extremidade que precisa toobe ocorrências é http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

proxy reverso do tooenable Olá no cluster hello, siga as etapas de saudação em [proxy no Azure Service Fabric reverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Após a configuração de proxy reverso hello, todos os serviços em cluster Olá micro que expõem um ponto de extremidade HTTP são endereçáveis da fora Olá cluster.

## <a name="diagnosticshealth-events"></a>Eventos de diagnóstico/integridade

### <a name="collect-patch-orchestration-app-logs"></a>Colete logs do aplicativo de orquestração de patch

Os logs do aplicativo de orquestração de patch são coletados como parte dos logs do Service Fabric a partir da versão de tempo de execução `5.6.220.9494` e superior.
Para clusters que executam a versão de tempo de execução do Service Fabric menor `5.6.220.9494`, logs podem ser coletados usando um dos métodos a seguir de saudação.

#### <a name="locally-on-each-node"></a>Localmente em cada nó

Logs são coletados localmente em cada nó de cluster do Service Fabric se a versão de tempo de execução do Service Fabric é menor que `5.6.220.9494`. Olá local tooaccess Olá logs é \[Service Fabric\_instalação\_unidade\]:\\PatchOrchestrationApplication\\logs.

Por exemplo, se o serviço de malha é instalada na unidade D, caminho de saudação é d:\\PatchOrchestrationApplication\\logs.

#### <a name="central-location"></a>Local central

Se o diagnóstico do Azure é configurado como parte das etapas de pré-requisito, logs do aplicativo de orquestração de patch Olá estão disponíveis no armazenamento do Azure.

### <a name="health-reports"></a>Relatórios de integridade

aplicativo de orquestração de patch Olá também publica relatórios de integridade em relação a saudação serviço coordenador ou Olá serviço de agente do nó no Olá casos a seguir:

#### <a name="a-windows-update-operation-failed"></a>Uma falha na operação do Windows Update

Se uma operação de atualização do Windows falhar em um nó, um relatório de integridade é gerado em relação a saudação serviço de agente do nó. Detalhes do relatório de integridade de saudação contém nome de nó problemáticos de saudação.

Após a aplicação de patch é concluída com êxito no nó problemático hello, relatório Olá será desmarcado automaticamente.

#### <a name="hello-node-agent-ntservice-is-down"></a>Olá NTService de agente do nó está inoperante

Se Olá NTService de agente do nó estiver inativo em um nó, um relatório de integridade do nível de aviso é gerado em relação a saudação serviço de agente do nó.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>serviço de Gerenciador de reparo do Hello não está habilitado

Se o serviço de Gerenciador de reparo do hello não foi encontrado no cluster hello, um relatório de integridade do nível de aviso é gerado para Olá serviço de coordenador.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

P. **Por que vejo o cluster em um estado de erro quando Olá patch orquestração aplicativo está em execução?**

R. Durante o processo de instalação hello, Olá patch orquestração aplicativo desabilita ou reinicia nós, o que podem resultar temporariamente a integridade de saudação do cluster Olá ficar inativo.

Com base na política de saudação para o aplicativo hello, ou um nó pode ser reduzidos durante uma operação de aplicação de patch *ou* todo um domínio de atualização pode ser reduzidos simultaneamente.

Final de saudação do hello instalação do Windows Update, Olá nós são habilitados novamente após a reinicialização.

Em Olá exemplo a seguir, o cluster Olá entrou estado de erro tooan temporariamente porque dois nós foram para baixo e Olá MaxPercentageUnhealthNodes política foi violado. Erro de saudação é temporário até Olá operação de patch está em andamento.

![Imagem do cluster não íntegro](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Se Olá problema persistir, consulte a seção de solução de problemas de toohello.

P. **O aplicativo de orquestração de patch está em estado de aviso**

R. Verifique toosee se um relatório de integridade lançado contra o aplicativo hello causa hello. Normalmente, o aviso de saudação contém detalhes do problema de saudação. Se o problema de saudação é transitório, o aplicativo hello é esperada tooauto recuperação desse estado.

P. **O que fazer se o cluster está íntegro e precisa de uma atualização do sistema de operacional urgentes de toodo?**

R. Olá patch orquestração aplicativo não instala atualizações ao cluster Olá não está íntegro. Tente toobring seu cluster tooa Íntegro toounblock Olá patch orquestração aplicativo fluxo de trabalho.

P. **Por que a aplicação de patch em clusters leva muito tempo toorun?**

R. tempo de saudação necessário pelo aplicativo de orquestração de patch Olá depende principalmente Olá fatores a seguir:

- política de saudação do hello serviço coordenador. 
  - Olá política padrão, `NodeWise`, resulta na aplicação de patch apenas um nó por vez. Especialmente no caso de saudação de clusters maiores, é recomendável que você use Olá `UpgradeDomainWise` política tooachieve mais rápido de aplicação de patch em clusters.
- número de saudação de atualizações disponíveis para download e instalação. 
- Olá toodownload tempo médio necessário e instalar uma atualização, que não deve exceder a algumas horas.
- desempenho de saudação de largura de banda de rede e máquinas virtuais de saudação.

P. **Por que vejo algumas atualizações no Windows Update resultados obtidos por meio da api REST, mas não em Olá histórico do Windows Update no computador?**

R. Algumas atualizações do produto necessário toobe check-in de seu histórico de atualização/patch do respectivos. Por exemplo: Atualizações do Windows Defender não aparecem no histórico do Windows Update no Windows Server 2016.

## <a name="disclaimers"></a>Avisos de Isenção de Responsabilidade

- aplicativo de orquestração de patch Olá aceita saudação do usuário final licença contrato do Windows Update em nome de usuário de saudação. Opcionalmente, configuração de saudação pode ser desativada na configuração de saudação do aplicativo hello.

- aplicativo de orquestração de patch Olá coleta telemetria tootrack uso e desempenho. Telemetria do aplicativo Hello segue a configuração de saudação da configuração de telemetria de saudação do Service Fabric runtime (que é ativado por padrão).

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="a-node-is-not-coming-back-tooup-state"></a>Um nó não voltará tooup estado

**nó de saudação pode estar paralisada em um estado de desabilitação porque**:

Uma verificação de segurança está pendente. tooremedy nessa situação, certifique-se de que nós suficientes estejam disponíveis em um estado íntegro.

**nó de saudação pode estar paralisada em um estado desabilitado porque**:

- nó de saudação foi desativado manualmente.
- nó de saudação foi desabilitada devido tooan trabalho de infraestrutura do Azure em andamento.
- nó Olá foi desativado temporariamente pelo nó de saudação toopatch do aplicativo de orquestração de patch hello.

**Olá nó pode estar paralisado em um estado inativo porque**:

- nó de saudação foi colocado em um estado inativo manualmente.
- nó de saudação está passando por uma reinicialização (que pode ser disparada por aplicativo de orquestração de patch Olá).
- nó de saudação está inoperante devido tooa defeituoso VM ou máquina ou rede problemas de conectividade.

### <a name="updates-were-skipped-on-some-nodes"></a>As atualizações foram ignoradas em alguns nós

Olá patch orquestração aplicativo tenta tooinstall uma acordo toohello reagendar diretiva do Windows update. serviço de Olá tenta nó de saudação toorecover e ignorar a política de aplicativo de toohello acordo do hello update.

Nesse caso, um relatório de integridade do nível de aviso é gerado em relação a saudação serviço de agente do nó. resultado de saudação para o Windows Update também contém um motivo possível para falha de Olá Olá.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>integridade de saudação do cluster Olá vai tooerror enquanto a instalação da atualização de saudação

Uma atualização com falha do Windows pode desativar a integridade de saudação de um aplicativo ou o cluster em um nó específico ou um domínio de atualização. Olá patch orquestração aplicativo interrompe qualquer operação subsequente do Windows Update até que o cluster Olá estiver íntegra novamente.

Um administrador deve intervir e determinar por que aplicativo hello ou cluster se tornou Íntegro devido tooWindows atualização.

## <a name="release-notes-"></a>Notas de Versão:

### <a name="version-110"></a>Version 1.1.0
- Versão pública

### <a name="version-111"></a>Versão 1.1.1
- Correção de bug no SetupEntryPoint de NodeAgentService que impediu a instalação de NodeAgentNTService.

### <a name="version-120-latest"></a>Versão 1.2.0 (mais recente)

- Correções de bugs em torno do fluxo de trabalho de reinício do sistema.
- Correção de bug na criação de tarefas do RM devido a verificação de integridade toowhich durante a preparação de tarefas de reparo não estava acontecendo conforme o esperado.
- Modo de inicialização alterada Olá para o serviço do windows POANodeSvc de auto toodelayed-auto.
