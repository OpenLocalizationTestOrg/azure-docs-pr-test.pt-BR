---
title: gerenciamento de aplicativos do Azure Service Fabric do aaaAutomate | Microsoft Docs
description: Implantar, atualizar, testar e remover aplicativos do Service Fabric usando o PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>Automatizar o ciclo de vida do aplicativo hello usando o PowerShell
Muitos aspectos da saudação [ciclo de vida do aplicativo de malha do serviço](service-fabric-application-lifecycle.md) pode ser automatizada.  Este artigo mostra como as tarefas de toouse PowerShell tooautomate comum para implantar, atualizar, remover e testar aplicativos do Azure Service Fabric.  APIs gerenciadas e HTTP para gerenciamento de aplicativos também estão disponíveis. Consulte [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md) para obter mais informações.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de mover tarefas toohello artigo hello, certifique-se a:

* Familiarize-se com os conceitos do Service Fabric Olá descritos em [visão geral técnica do Service Fabric](service-fabric-technical-overview.md).
* [Instalar o tempo de execução hello, SDK e as ferramentas](service-fabric-get-started.md), que também instala Olá **ServiceFabric** módulo do PowerShell.
* [Habilitar a execução de script do PowerShell](service-fabric-get-started.md#enable-powershell-script-execution).
* Iniciar um cluster local.  Inicie uma nova janela do PowerShell como administrador e execute o script de instalação de cluster de saudação da pasta do SDK de saudação:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Antes de executar quaisquer comandos do PowerShell neste artigo, primeiro conecte-se toohello cluster de malha do serviço local usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Olá tarefas a seguir exige um toodeploy de pacote de aplicativo v1 e um pacote de aplicativo v2 para a atualização. Baixar Olá [ **WordCount** aplicativo de exemplo](http://aka.ms/servicefabricsamples) (localizado em exemplos de introdução de saudação). Compile e empacote o aplicativo hello no Visual Studio (com o botão direito em **WordCount** no Gerenciador de soluções e selecione **pacote**). Pacote de v1 Olá cópia no `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` muito`C:\Temp\WordCount`. Cópia `C:\Temp\WordCount` muito`C:\Temp\WordCountV2`, criação de pacote de aplicativo hello v2 para a atualização. Abra `C:\Temp\WordCountV2\ApplicationManifest.xml` em um editor de texto. Em Olá **ApplicationManifest** elemento, alteração Olá **ApplicationTypeVersion** de atributo de "1.0.0" muito "2.0.0" número de versão de aplicativo tooupdate hello. Salve o arquivo de ApplicationManifest.xml de saudação alterado.

## <a name="task-deploy-a-service-fabric-application"></a>Tarefa: Implantar um aplicativo do Service Fabric
Depois de criados e empacotados aplicativo hello (ou baixado o pacote de aplicativo hello), você pode implantar o aplicativo hello em um cluster de malha do serviço local. Implantação envolve a carregar o pacote de aplicativo hello, registrando o tipo de aplicativo hello e criação de instância de aplicativo hello. Use as instruções de saudação toodeploy esta seção um novo cluster de tooa do aplicativo.

### <a name="step-1-upload-hello-application-package"></a>Etapa 1: Carregar o pacote de aplicativo hello
Carregando toohello de pacote de aplicativo hello repositório de imagens coloca-o em um componentes da malha de serviço local toointernal acessível.  pacote de aplicativo Hello contém Olá manifesto do aplicativo, manifestos do serviço e o código, configuração necessárias e aplicativo de saudação de toocreate de pacote (s) de dados e instâncias de serviço. Se desejar que o pacote de aplicativo de saudação tooverify localmente, use Olá [ServiceFabricApplicationPackage teste](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.  Olá [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando Olá de carregamentos de pacote. Por exemplo:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Etapa 2: Registrar o tipo de aplicativo hello
Registrar pacote de aplicativo hello faz com tipo de aplicativo hello e versão declarados no manifesto de aplicativo hello disponível para uso. sistema Olá lê pacote hello carregado na etapa 1 do hello, verifique se o pacote de saudação (equivalente toorunning [ServiceFabricApplicationPackage teste](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) localmente), processar o conteúdo do pacote hello e copie Olá processado pacote tooan local do sistema interno.  Executar Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
toosee todos os tipos de aplicativo hello registrados no cluster de hello, executar Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Etapa 3: Criar a instância do aplicativo hello
Um aplicativo pode ser instanciado usando qualquer versão do tipo de aplicativo que foi registrado com êxito usando Olá [ServiceFabricApplication novo](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) comando. nome de saudação de cada aplicativo é declarada no tempo de implantação e deve começar com hello **malha:** esquema e ser exclusivo para cada instância do aplicativo. Olá nome do tipo de aplicativo e a versão do tipo de aplicativo são declarados no hello **ApplicationManifest.xml** arquivo hello do pacote de aplicativo. Se todos os serviços padrão foram definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino hello, aqueles são criados no momento.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Olá [ServiceFabricApplication Get](/powershell/servicefabric/vlatest/get-servicefabricapplication) comando lista todas as instâncias de aplicativo que foram criadas com êxito, juntamente com o respectivo status geral. Olá [ServiceFabricService Get](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) comando lista todas as instâncias de serviço Olá que foram criadas com êxito em uma instância de determinado aplicativo. Os serviços padrão (se houver) são listados.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Tarefa: Atualizar um aplicativo do Service Fabric
Você pode atualizar um aplicativo do Service Fabric implantado anteriormente com um pacote de aplicativos atualizado. Essa tarefa atualiza o aplicativo WordCount hello que foi implantado em "tarefa: implantar um aplicativo do Service Fabric." Leia [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md) para obter mais informações.

tookeep coisas simples para este exemplo, somente Olá aplicativo número de versão foi atualizada no pacote de aplicativo hello WordCountV2 criado nos pré-requisitos hello. Um cenário mais realista envolve atualizar seus arquivos de código, configuração ou dados de serviço e, em seguida, recriação e empacotar o aplicativo hello com números de versão atualizada.  

### <a name="step-1-upload-hello-updated-application-package"></a>Etapa 1: Carregar o pacote de aplicativo atualizado Olá
Olá WordCount v1 aplicativo está pronto toobe atualizado. Se você abrir uma janela do PowerShell como administrador e digite [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), consulte a versão 1.0.0 do hello WordCount tipo de aplicativo é implantado.  

Saudação de cópia atualizado repositório de imagens de malha do serviço do aplicativo pacote toohello (onde os pacotes de aplicativos Olá são armazenados pela malha do serviço). Olá parâmetro **ApplicationPackagePathInImageStore** informa onde ele pode localizar o pacote de aplicativo de saudação do Service Fabric. Olá cópias Olá pacote de aplicativo muito de comando a seguir**WordCountV2** no repositório de imagens de saudação:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Etapa 2: Registrar Olá atualizado o tipo de aplicativo
Olá, próxima etapa é tooregister Olá nova versão do aplicativo hello com o Service Fabric, que pode ser realizada usando Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Etapa 3: Iniciar a atualização de saudação
Vários parâmetros de atualização, tempos limite e critérios de integridade podem ser aplicado tooapplication atualizações. Leia Olá [parâmetros de atualização de aplicativo](service-fabric-application-upgrade-parameters.md) e [processo de atualização](service-fabric-application-upgrade.md) documentos toolearn mais. Todos os serviços e instâncias devem ser *Íntegro* após a atualização de saudação.  Saudação de conjunto **HealthCheckStableDuration** too60 segundos (de forma que os serviços de saudação estão íntegros pelo menos 20 segundos antes de atualização de saudação continua toohello próximo domínio de atualização).  Saudação de conjunto também **UpgradeDomainTimeout** too1200 segundos e Olá **UpgradeTimeout** too3000 segundos. Finalmente, defina Olá **UpgradeFailureAction** muito**reversão**que solicitações do Service Fabric reverte Olá versão anterior do aplicativo toohello se forem encontradas falhas durante a atualização.

Agora você pode começar a atualização do aplicativo hello usando Olá [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Observe que esse nome de aplicativo hello é Olá mesmo como Olá já implantou o nome do aplicativo v1.0.0 (fabric: / WordCount). Serviço de malha usa este tooidentify nome que o aplicativo está obtendo atualizado. Se você definir Olá toobe de tempos limite muito curto, você pode encontrar uma mensagem de falha de tempo limite estados Olá problema. Consulte também[solucionar problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md), ou aumente o tempo limite de saudação.

### <a name="step-4-check-upgrade-progress"></a>Etapa 4: verificar o andamento da atualização
Você pode monitorar o progresso de atualização do aplicativo usando [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), ou usando Olá [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

Em alguns minutos, Olá [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) mostra que todos os domínios de atualização foram atualizados (concluído).

## <a name="task-test-a-service-fabric-application"></a>Tarefa: testar um aplicativo do Service Fabric
Serviços de alta qualidade toowrite, os desenvolvedores precisam toobe tooinduce capaz de infraestrutura confiável falhas tootest Olá estabilidade de seus serviços. Service Fabric fornece aos desenvolvedores de ações de falha do hello capacidade tooinduce e testar os serviços na presença de saudação de falhas usando Olá caos e failover de cenários de teste.  Leia [toohello Introdução falhas Analysis Service](service-fabric-testability-overview.md) para obter informações adicionais.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Etapa 1: Execute o cenário de teste de caos Olá
cenário de teste de caos Hello gera falhas em cluster do Service Fabric inteira de saudação. cenário de saudação compacta falhas geralmente vistas em meses ou anos tooa algumas horas. combinação de saudação de falhas intercaladas com uma taxa alta de falhas de encontra casos de canto que outra forma seriam omitidos. Olá exemplo a seguir executa o cenário de teste de caos Olá por 60 minutos.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Etapa 2: Executar cenário de teste de failover Olá
Olá failover uma partição de serviço específico em vez de todo o cluster Olá de destinos de cenário de teste e deixa outros serviços afetados. cenário de saudação itera por meio de uma sequência de simulada falhas na validação de serviço durante a execução de sua lógica de negócios. Uma falha na validação do serviço indica um problema que precisa de mais investigação. teste de failover Olá induz somente uma falha de cada vez, como o cenário de teste do toohello contrário caos, que pode induzir a várias falhas. Olá exemplo a seguir executa teste de failover Olá por 60 minutos em relação a malha Olá: WordCount/serviço WordCountService.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Tarefa: remover um aplicativo do Service Fabric
Você pode excluir uma instância de um aplicativo implantado, remover o tipo de aplicativo hello provisionado de cluster de saudação e remova o pacote de aplicativo Olá Olá ImageStore.

### <a name="step-1-remove-an-application-instance"></a>Etapa 1: Remover uma instância de aplicativo
Quando uma instância de aplicativo não for mais necessário, você poderá removê-lo permanentemente usando Olá [ServiceFabricApplication remover](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. Isso remove automaticamente todos os serviços pertencentes toohello aplicativo, remover permanentemente todos os estados de serviço. Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Etapa 2: Cancelar o registro do tipo de aplicativo hello
Quando você não precisa mais uma versão específica de um tipo de aplicativo, cancelar seu registro usando Olá [ServiceFabricApplicationType Unregister](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Cancelando o registro tipos não utilizados versões espaço de armazenamento usado pelo pacote de aplicativo hello no repositório de imagens de saudação. Um tipo de aplicativo pode ter seu registro cancelado, desde que não existam aplicativos instanciados nele ou atualizações de aplicativo pendentes que façam referência a ele.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Etapa 3: Remover o pacote de aplicativo hello
Depois que o tipo de aplicativo hello for cancelado, o pacote de aplicativo de saudação pode ser removido saudação do repositório de imagens usando Olá [ServiceFabricApplicationPackage remover](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Próximas etapas
[Ciclo de vida do aplicativo do Service Fabric](service-fabric-application-lifecycle.md)

[Implantar um aplicativo](service-fabric-deploy-remove-applications.md)

[Atualização de aplicativo](service-fabric-application-upgrade.md)

[Cmdlets do Azure Service Fabric](/powershell/azure/overview?view=azureservicefabricps)

