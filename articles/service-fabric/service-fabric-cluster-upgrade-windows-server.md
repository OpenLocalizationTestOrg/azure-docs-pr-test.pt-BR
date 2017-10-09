---
title: aaaUpgrade independente do Azure Service Fabric do cluster no Windows Server | Microsoft Docs
description: "Atualize o código do Azure Service Fabric hello e/ou configuração que é executado de um cluster de malha do serviço autônomo, incluindo a definição do modo de atualização de cluster hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="71507-103">Atualize seu cluster autônomo do Azure Service Fabric no Windows Server</span><span class="sxs-lookup"><span data-stu-id="71507-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71507-104">Cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="71507-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="71507-105">Cluster Independente</span><span class="sxs-lookup"><span data-stu-id="71507-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="71507-106">Para qualquer sistema moderno, Olá capacidade tooupgrade é um sucesso a longo prazo toohello chave do produto.</span><span class="sxs-lookup"><span data-stu-id="71507-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="71507-107">Um cluster do Azure Service Fabric é um recurso que pertence a você.</span><span class="sxs-lookup"><span data-stu-id="71507-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="71507-108">Este artigo descreve como você pode verificar se as que versões com suporte do código de malha do serviço e configurações de cluster Olá sempre é executado.</span><span class="sxs-lookup"><span data-stu-id="71507-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="71507-109">Versão do Service Fabric do controle Olá que é executado em seu cluster</span><span class="sxs-lookup"><span data-stu-id="71507-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="71507-110">tooset toodownload seu cluster de atualizações de malha do serviço quando a Microsoft lança uma nova versão, conjunto Olá **fabricClusterAutoupgradeEnabled** tootrue de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="71507-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="71507-111">uma versão com suporte de malha do serviço que você deseja que seu toobe de cluster no conjunto de saudação do tooselect **fabricClusterAutoupgradeEnabled** toofalse de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="71507-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="71507-112">Certifique-se de que o cluster sempre esteja executando uma versão do Service Fabric com suporte.</span><span class="sxs-lookup"><span data-stu-id="71507-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="71507-113">Quando a Microsoft anuncia versão saudação de uma nova versão do Service Fabric, versão anterior do hello está marcado para fim do suporte depois que um mínimo de 60 dias da data de saudação do anúncio de saudação.</span><span class="sxs-lookup"><span data-stu-id="71507-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="71507-114">Novas versões são anunciadas [no blog da equipe do Service Fabric Olá](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="71507-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="71507-115">Olá nova versão está disponível toochoose nesse ponto.</span><span class="sxs-lookup"><span data-stu-id="71507-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="71507-116">Você pode atualizar a nova versão do cluster toohello somente se você estiver usando uma configuração de nó de estilo de produção, onde cada nó do Service Fabric é alocado em uma máquina virtual ou física separada.</span><span class="sxs-lookup"><span data-stu-id="71507-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="71507-117">Se você tiver um cluster de desenvolvimento, onde mais de um nó de malha do serviço estiver em um único computador físico ou virtual, você deve recriar Olá cluster com a nova versão de hello.</span><span class="sxs-lookup"><span data-stu-id="71507-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="71507-118">Dois fluxos de trabalho distintos podem atualizar sua versão mais recente do cluster toohello ou uma versão com suporte do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="71507-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="71507-119">Um fluxo de trabalho é para clusters que têm a versão mais recente da conectividade toodownload Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="71507-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="71507-120">Olá outro fluxo de trabalho é para clusters que não têm conectividade toodownload hello mais recente do Service Fabric versão.</span><span class="sxs-lookup"><span data-stu-id="71507-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="71507-121">Atualizar clusters que têm a configuração e o código mais recente da conectividade toodownload Olá</span><span class="sxs-lookup"><span data-stu-id="71507-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="71507-122">Usar essas etapas tooupgrade sua versão de tooa com suporte de cluster se os nós de cluster tem conectividade com a Internet muito[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="71507-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="71507-123">Para clusters que têm conectividade muito[http://download.microsoft.com](http://download.microsoft.com), Microsoft verifica periodicamente se há disponibilidade de saudação de novas versões do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="71507-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="71507-124">Quando uma nova versão do Service Fabric está disponível, o pacote de saudação seja baixado localmente toohello cluster e provisionado para atualização.</span><span class="sxs-lookup"><span data-stu-id="71507-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="71507-125">Além disso, tooinform Prezado cliente dessa nova versão, o sistema Olá mostra um aviso de integridade do cluster explícita é toohello semelhante a seguir:</span><span class="sxs-lookup"><span data-stu-id="71507-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="71507-126">"suporte de versão [versão #] do cluster atual Olá termina [Date]."</span><span class="sxs-lookup"><span data-stu-id="71507-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="71507-127">Depois que o cluster de saudação está executando a versão mais recente do hello, aviso Olá desaparece.</span><span class="sxs-lookup"><span data-stu-id="71507-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="71507-128">Fluxo de trabalho de atualização do cluster</span><span class="sxs-lookup"><span data-stu-id="71507-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="71507-129">Depois de ver o aviso de integridade do cluster hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="71507-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="71507-130">Conecte o cluster de toohello de qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="71507-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="71507-131">máquina de saudação que esse script é executado no não tem toobe parte do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="71507-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="71507-132">Obter lista de saudação de versões de malha do serviço que você pode atualizar para.</span><span class="sxs-lookup"><span data-stu-id="71507-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="71507-133">Você deve obter um toothis semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="71507-133">You should get an output similar toothis:</span></span>

    ![obter versões de malha][getfabversions]
3. <span data-ttu-id="71507-135">Inicie uma versão disponível do tooan de atualização de cluster usando o [ServiceFabricClusterUpgrade início](https://msdn.microsoft.com/library/mt125872.aspx) cmd do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71507-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="71507-136">progresso de saudação do toomonitor de atualização de hello, você pode usar o Service Fabric Explorer ou Olá executar comando do Windows PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="71507-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="71507-137">Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida.</span><span class="sxs-lookup"><span data-stu-id="71507-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="71507-138">toospecify diretivas de integridade personalizado para Olá **início ServiceFabricClusterUpgrade** command, consulte a documentação para [ServiceFabricClusterUpgrade início](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="71507-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="71507-139">Depois de corrigir problemas de saudação que resultaram em reversão Olá, inicie novamente a atualização de saudação Olá seguir as mesmas etapas conforme descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="71507-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="71507-140">Atualizar clusters que têm <U>nenhuma conectividade</u> toodownload hello mais recente código e configuração</span><span class="sxs-lookup"><span data-stu-id="71507-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="71507-141">Usar essas etapas tooupgrade sua versão de tooa com suporte de cluster se os nós de cluster não tem conectividade com a Internet muito[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="71507-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="71507-142">Se você estiver executando um cluster que não seja toohello conectado à Internet, você terá toomonitor Olá Service Fabric team blog toolearn sobre uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="71507-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="71507-143">Olá sistema não mostrar um tooalert de aviso de integridade do cluster de uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="71507-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="71507-144">Provisionamento automático vs provisionamento manual</span><span class="sxs-lookup"><span data-stu-id="71507-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="71507-145">download automático de tooenable e o registro para a versão mais recente do código Olá, configurar o serviço de atualização de malha.</span><span class="sxs-lookup"><span data-stu-id="71507-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="71507-146">Consulte toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro Olá [pacote autônomo](service-fabric-cluster-standalone-package-contents.md) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="71507-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="71507-147">Processo manual, siga as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="71507-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="71507-148">Modifique seu Olá de tooset de configuração de cluster toofalse de propriedade a seguir antes de iniciar uma atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="71507-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="71507-149">Consulte também[ServiceFabricClusterConfigurationUpgrade início PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para obter detalhes de uso.</span><span class="sxs-lookup"><span data-stu-id="71507-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="71507-150">Verifique se tooupdate 'clusterConfigurationVersion' em seu JSON antes de iniciar a atualização de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="71507-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="71507-151">Fluxo de trabalho de atualização do cluster</span><span class="sxs-lookup"><span data-stu-id="71507-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="71507-152">Execute Get-ServiceFabricClusterUpgrade em um de nós de saudação em cluster hello e anote Olá TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="71507-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="71507-153">Seguinte Olá execução de um toolist de computador conectado à internet todas as versões compatíveis com a versão atual do hello de atualização e baixar Olá correspondente do pacote de links de download associadas hello.</span><span class="sxs-lookup"><span data-stu-id="71507-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="71507-154">Conecte o cluster de toohello de qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="71507-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="71507-155">máquina de saudação que esse script é executado no não tem toobe parte do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="71507-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="71507-156">Copie o pacote de saudação baixada no repositório de imagens de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="71507-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="71507-157">Registre pacote hello copiado.</span><span class="sxs-lookup"><span data-stu-id="71507-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="71507-158">Inicie uma versão disponível do tooan de atualização de cluster.</span><span class="sxs-lookup"><span data-stu-id="71507-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="71507-159">Você pode monitorar o progresso de saudação de atualização de saudação no Gerenciador do Service Fabric, ou você pode executar Olá comando PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="71507-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="71507-160">Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida.</span><span class="sxs-lookup"><span data-stu-id="71507-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="71507-161">políticas de integridade personalizado toospecify para hello **ServiceFabricClusterUpgrade início** command, consulte a documentação de saudação do [ServiceFabricClusterUpgrade início](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="71507-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="71507-162">Depois de corrigir problemas de saudação que resultaram em reversão Olá, inicie novamente a atualização de saudação Olá seguir as mesmas etapas conforme descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="71507-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="71507-163">Atualizar a configuração de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="71507-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="71507-164">Antes de iniciar a atualização de configuração hello, você pode testar o json de configuração do cluster novo, executando o script do powershell Olá no pacote autônomo de saudação.</span><span class="sxs-lookup"><span data-stu-id="71507-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="71507-165">ou o</span><span class="sxs-lookup"><span data-stu-id="71507-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="71507-166">Algumas configurações não podem ser atualizadas, como pontos de extremidade, nome do cluster, nó IP, etc. Isso testará Olá novo cluster configuração json contra Olá antigo e geram erros na janela do Powershell hello, se houver qualquer problema.</span><span class="sxs-lookup"><span data-stu-id="71507-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="71507-167">atualização de configuração de cluster de saudação tooupgrade, execute **ServiceFabricClusterConfigurationUpgrade início**.</span><span class="sxs-lookup"><span data-stu-id="71507-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="71507-168">atualização de configuração de saudação é processado domínio de atualização por domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="71507-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="71507-169">Atualização da configuração do certificado do cluster</span><span class="sxs-lookup"><span data-stu-id="71507-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="71507-170">Certificado de cluster é usado para autenticação entre os nós de cluster, para o certificado de saudação sobrepor deve ser executada com muito cuidado porque falha bloqueará a comunicação de saudação entre nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="71507-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="71507-171">Tecnicamente, há três opções com suporte:</span><span class="sxs-lookup"><span data-stu-id="71507-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="71507-172">Atualização de certificado único: caminho de atualização de saudação é ' certificado (primária) -> B de certificado (primária) -> C de certificado (primária) ->... '.</span><span class="sxs-lookup"><span data-stu-id="71507-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="71507-173">Atualização de certificado duplo: Olá caminho de atualização é ' -> (primário) do certificado do certificado (primária) e B (secundários) -> B de certificado (primária) -> B de certificado (primária) e C (secundários) -> C de certificado (primária) ->... '.</span><span class="sxs-lookup"><span data-stu-id="71507-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="71507-174">Atualização do tipo de certificado: configuração de certificados com base em CommonName configuração <-> com base em impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="71507-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="71507-175">Por exemplo, impressão digital do certificado (primária) e a impressão digital B (secundários) -> certificado CommonName C.</span><span class="sxs-lookup"><span data-stu-id="71507-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="71507-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71507-176">Next steps</span></span>
* <span data-ttu-id="71507-177">Saiba como toocustomize alguns [configurações de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="71507-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="71507-178">Saiba como muito[escalar horizontalmente o seu cluster](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="71507-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="71507-179">Saiba mais sobre [atualizações de aplicativo](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="71507-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
