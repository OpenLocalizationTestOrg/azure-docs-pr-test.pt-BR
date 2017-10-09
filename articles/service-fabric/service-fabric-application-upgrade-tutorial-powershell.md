---
title: "atualização do aplicativo de malha aaaService usando o PowerShell | Microsoft Docs"
description: "Este artigo o orienta através da experiência de saudação de implantar um aplicativo de malha do serviço, alterar o código de saudação e implantar uma atualização usando o PowerShell."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Atualização do aplicativo do Service Fabric usando o PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Olá usados com mais frequência e a abordagem de atualização recomendada é atualização sem interrupção Olá monitorado.  Malha do serviço do Azure monitora a integridade do hello do aplicativo hello está sendo atualizado com base em um conjunto de políticas de integridade. Após a atualização de um domínio de atualização (UD), Service Fabric avalia a integridade do aplicativo hello e continua toohello próximo domínio de atualização ou falha de atualização Olá dependendo de diretivas de integridade de saudação.

Uma atualização do aplicativo monitorado pode ser realizada usando Olá gerenciados ou APIs nativas, PowerShell ou REST. Para obter instruções sobre como executar uma atualização usando o Visual Studio, confira [Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md).

Com atualizações sem interrupção do Service Fabric monitorados, administrador do aplicativo hello pode configurar a política de avaliação de integridade de saudação que o Service Fabric usa toodetermine se o aplicativo hello está íntegro. Além disso, o administrador de saudação pode configurar Olá toobe de ação executada quando a avaliação de integridade Olá falha (por exemplo, fazer uma reversão automática.) Esta seção orienta por meio de uma atualização monitorada por um dos exemplos do SDK Olá que usa o PowerShell. Olá seguinte vídeo Microsoft Virtual Academy também orienta você por meio de uma atualização do aplicativo:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Etapa 1: Criar e implantar o exemplo de objetos visuais hello
Criar e publicar o aplicativo hello clicando no projeto de aplicativo hello, **VisualObjectsApplication,** e selecionando Olá **publicar** comando.  Para obter mais informações, confira o [Tutorial de atualização de aplicativos do Service Fabric](service-fabric-application-upgrade-tutorial.md).  Como alternativa, você pode usar PowerShell toodeploy seu aplicativo.

> [!NOTE]
> Antes de qualquer um dos comandos do Service Fabric Olá podem ser usados no PowerShell, é necessário primeiro tooconnect toohello cluster usando Olá `Connect-ServiceFabricCluster` cmdlet. Da mesma forma, presume-se que Olá que cluster já foi configurado no computador local. Consulte o artigo Olá no [configurar seu ambiente de desenvolvimento do Service Fabric](service-fabric-get-started.md).
> 
> 

Depois de criar o projeto de saudação no Visual Studio, você pode usar o comando do PowerShell Olá [ServiceFabricApplicationPackage cópia](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy Olá aplicativo pacote toohello ImageStore. Se desejar que o pacote de aplicativo de saudação tooverify localmente, use Olá [ServiceFabricApplicationPackage teste](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet. Olá, próxima etapa é tooregister Olá toohello Service Fabric tempo de execução usando Olá [ServiceFabricApplicationPackage registro](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet. Olá etapa final é toostart uma instância do aplicativo hello usando Olá [ServiceFabricApplication novo](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.  Essas três etapas são análogos toousing Olá **implantar** item de menu no Visual Studio.

Agora, você pode usar [Service Fabric Explorer tooview Olá cluster e Olá o aplicativo](service-fabric-visualizing-your-cluster.md). aplicativo Hello tem um serviço web que pode ser navegado tooin Internet Explorer digitando [http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) na barra de endereços de saudação.  Você deve ver alguns objetos visual flutuantes mover-se na tela hello.  Além disso, você pode usar [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck status da saudação do aplicativo.

## <a name="step-2-update-hello-visual-objects-sample"></a>Etapa 2: Atualizar exemplo de objetos visuais hello
Você pode notar que com a versão de saudação que foi implantado na etapa 1, objetos visuais Olá não gire. Vamos atualizar esse tooone aplicativo onde objetos visuais Olá também girar.

Selecionar projeto VisualObjects.ActorService Olá Olá VisualObjects solução e abrir o arquivo de StatefulVisualObjectActor.cs hello. Dentro desse arquivo, navegue toohello método `MoveObject`, comente `this.State.Move()`e remova os `this.State.Move(true)`. Essa alteração gira objetos Olá depois que o serviço de saudação é atualizado.

Também precisamos Olá tooupdate *ServiceManifest.xml* arquivo (em PackageRoot) do projeto Olá **VisualObjects.ActorService**. Saudação de atualização *CodePackage* Olá too2.0 de versão do serviço e Olá linhas correspondentes na Olá *ServiceManifest.xml* arquivo.
Você pode usar o Visual Studio de saudação *editar arquivos de manifesto* opção após clicar em alterações no arquivo de manifesto Olá Olá solução toomake.

Depois que forem feitas alterações Olá, manifesto Olá deve ter aparência a seguir Olá (realçadas partes mostram alterações Olá):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Olá agora *ApplicationManifest.xml* arquivo (encontrado em Olá **VisualObjects** projeto sob Olá **VisualObjects** solução) é atualizada tooversion 2.0 de saudação  **VisualObjects.ActorService** projeto. Além disso, a versão do aplicativo hello é atualizada too2.0.0.0 de 1.0.0.0. Olá *ApplicationManifest.xml* deve aparência Olá trecho de código a seguir:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


Agora, crie o projeto de hello, selecionando apenas Olá **ActorService** de projeto e, em seguida, clicando duas vezes e selecionando Olá **criar** opção no Visual Studio. Se você selecionar **recompilar tudo**, você deve atualizar versões Olá para todos os projetos, como código Olá poderia ter sido alterada. Em seguida, vamos saudação do pacote atualizado o aplicativo clicando em ***VisualObjectsApplication***, selecionando Olá Menu de malha do serviço e escolhendo **pacote**. Essa ação cria um pacote de aplicativos que pode ser implantado.  Seu aplicativo atualizado está pronto toobe implantado.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Etapa 3: decida sobre diretivas de integridade e parâmetros de atualização
Familiarize-se com hello [parâmetros de atualização de aplicativo](service-fabric-application-upgrade-parameters.md) e hello [processo de atualização](service-fabric-application-upgrade.md) tooget um bom entendimento da saudação vários atualizar parâmetros, tempos limite e critérios de integridade aplicada . Para este passo a passo, critério de avaliação de integridade de serviço Olá é definir toohello padrão (e recomendável) valores, o que significa que todos os serviços e instâncias devem ser *Íntegro* após a atualização de saudação.  

No entanto, vamos aumentar Olá *HealthCheckStableDuration* too60 segundos (de forma que os serviços de saudação estão íntegros para pelo menos 20 segundos antes de atualização de saudação continua toohello próximo domínio de atualização).  Vamos definir também Olá *UpgradeDomainTimeout* toobe 1200 segundos e hello *UpgradeTimeout* toobe 3000 segundos.

Por fim, vamos também definir Olá *UpgradeFailureAction* toorollback. Essa opção requer a versão anterior do toohello de aplicativo de backup Olá do Service Fabric tooroll se encontrar problemas durante a atualização de saudação. Portanto, ao iniciar a atualização da saudação (na etapa 4), hello seguintes parâmetros são especificados:

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Etapa 4: preparar o aplicativo para atualização
Agora o aplicativo hello é criado e atualizado toobe pronto. Se você abrir uma janela do PowerShell como administrador e digitar [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), será informado de que o aplicativo tipo 1.0.0.0 do **VisualObjects** foi implantado.  

Olá pacote de aplicativo é armazenado na seguinte Olá caminho relativo onde você descompactou Olá SDK do Service Fabric - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. Você deve encontrar uma pasta de "Pacote" no diretório, onde o pacote de aplicativo hello está armazenado. Verifique Olá carimbos de hora tooensure que se trata de compilação mais recente do hello (talvez seja necessário toomodify Olá caminhos adequadamente).

Agora vamos Olá cópia atualizada toohello do pacote de aplicativo ImageStore de malha do serviço (onde os pacotes de aplicativos Olá são armazenados pela malha do serviço). Olá parâmetro *ApplicationPackagePathInImageStore* informa onde ele pode localizar o pacote de aplicativo de saudação do Service Fabric. Nós trabalhamos aplicativo hello atualizado "VisualObjects\_V2" com hello (talvez seja necessário toomodify caminhos novamente adequadamente) de comando a seguir.

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

próxima etapa do Hello é tooregister esse aplicativo com a malha do serviço, que pode ser realizada usando Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Se hello comando anterior não for bem-sucedida, é provável que você precisa de uma recompilação de todos os serviços. Conforme mencionado na etapa 2, você pode ter tooupdate sua versão do serviço Web.

## <a name="step-5-start-hello-application-upgrade"></a>Etapa 5: Iniciar a atualização do aplicativo hello
Agora, estamos todos os aplicativos de saudação do conjunto toostart atualização usando Olá [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) comando:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Olá nome do aplicativo é Olá mesmo conforme descrito em Olá *ApplicationManifest.xml* arquivo. Serviço de malha usa este tooidentify nome que o aplicativo está obtendo atualizado. Se você definir Olá toobe de tempos limite muito curto, você pode encontrar uma mensagem de falha que estados Olá problema. Consulte a seção de solução de problemas de toohello ou aumentar o tempo limite de saudação.

Agora, como hello prossegue de atualização do aplicativo, você poderá monitorá-lo usando o Gerenciador do Service Fabric, ou usando Olá [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) comando do PowerShell: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

Em alguns minutos, status de saudação que você obteve usando Olá precede o comando do PowerShell, deverá indicar que todos os domínios de atualização foram atualizados (concluído). E você deve encontrar que objetos de saudação do visual na janela do navegador iniciaram girando!

Você pode tentar a atualização de versão 2 tooversion 3 ou de versão 2 tooversion 1 como um exercício. Mudança de versão 2 tooversion 1 também é considerada uma atualização. Experimentar tempos limite e toomake de diretivas de integridade por conta própria familiarizados com eles. Quando você estiver implantando tooan cluster do Azure, Olá parâmetros necessidade toobe conjunto adequadamente. É tooset bons tempos-limite Olá impedidas.

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.

Controle como seu aplicativo é atualizado usando [parâmetros de atualização](service-fabric-application-upgrade-parameters.md).

Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).

Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).

Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [Solucionando problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).

