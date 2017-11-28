---
title: "Atualizar um cluster autônomo do Azure Service Fabric no Windows Server | Microsoft Docs"
description: "Atualize o código do Azure Service Fabric e/ou a configuração que executa um cluster do Service Fabric autônomo, incluindo a configuração de modo de atualização de cluster."
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
ms.openlocfilehash: ac40775ca62362a32184207857a0b965a798e135
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="e0886-103">Atualize seu cluster autônomo do Azure Service Fabric no Windows Server</span><span class="sxs-lookup"><span data-stu-id="e0886-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0886-104">Cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="e0886-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="e0886-105">Cluster Independente</span><span class="sxs-lookup"><span data-stu-id="e0886-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="e0886-106">Para qualquer sistema moderno, a capacidade de atualização é uma chave para o sucesso de seu produto a longo prazo.</span><span class="sxs-lookup"><span data-stu-id="e0886-106">For any modern system, the ability to upgrade is a key to the long-term success of your product.</span></span> <span data-ttu-id="e0886-107">Um cluster do Azure Service Fabric é um recurso que pertence a você.</span><span class="sxs-lookup"><span data-stu-id="e0886-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="e0886-108">Este artigo descreve como garantir que o cluster sempre execute versões com suporte do código do Service Fabric e de configurações.</span><span class="sxs-lookup"><span data-stu-id="e0886-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="e0886-109">Controlar a versão do Service Fabric em execução no cluster</span><span class="sxs-lookup"><span data-stu-id="e0886-109">Control the Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="e0886-110">Para configurar o cluster para baixar atualizações do Service Fabric quando a Microsoft lançar uma nova versão, defina a configuração **fabricClusterAutoupgradeEnabled** do cluster para true.</span><span class="sxs-lookup"><span data-stu-id="e0886-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the **fabricClusterAutoupgradeEnabled** cluster configuration to true.</span></span> <span data-ttu-id="e0886-111">Para selecionar uma versão com suporte do Service Fabric em que você deseja que o seu cluster esteja, defina a configuração **fabricClusterAutoupgradeEnabled** do cluster para false.</span><span class="sxs-lookup"><span data-stu-id="e0886-111">To select a supported version of Service Fabric that you want your cluster to be on, set the **fabricClusterAutoupgradeEnabled** cluster configuration to false.</span></span>

> [!NOTE]
> <span data-ttu-id="e0886-112">Certifique-se de que o cluster sempre esteja executando uma versão do Service Fabric com suporte.</span><span class="sxs-lookup"><span data-stu-id="e0886-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="e0886-113">Quando a Microsoft anuncia o lançamento de uma nova versão do Service Fabric, a versão anterior é programada para encerrar sua vida útil após um mínimo de 60 dias a partir da data do comunicado.</span><span class="sxs-lookup"><span data-stu-id="e0886-113">When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement.</span></span> <span data-ttu-id="e0886-114">Novas versões são anunciadas [no blog da equipe do Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="e0886-114">New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="e0886-115">Nesse momento, a nova versão está disponível para escolha.</span><span class="sxs-lookup"><span data-stu-id="e0886-115">The new release is available to choose at that point.</span></span>
>
>

<span data-ttu-id="e0886-116">Será possível atualizar o cluster para a nova versão apenas se você estiver usando uma configuração de nó de estilo de produção, em que cada nó do Service Fabric é alocado em uma máquina virtual ou física separada.</span><span class="sxs-lookup"><span data-stu-id="e0886-116">You can upgrade your cluster to the new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="e0886-117">Se você tiver um cluster de desenvolvimento no qual exista mais de um nó do Service Fabric em uma única máquina virtual ou física, você deverá recriar o cluster com a nova versão.</span><span class="sxs-lookup"><span data-stu-id="e0886-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span></span>

<span data-ttu-id="e0886-118">Dois fluxos de trabalho distintos podem atualizar o cluster para a versão mais recente ou uma versão do Service Fabric com suporte.</span><span class="sxs-lookup"><span data-stu-id="e0886-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="e0886-119">Um fluxo de trabalho é para clusters com conectividade para baixar a versão mais recente automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e0886-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span></span> <span data-ttu-id="e0886-120">O outro fluxo de trabalho é para clusters sem conectividade para baixar a versão mais recente do Service Fabric automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e0886-120">The other workflow is for clusters that do not have connectivity to download the latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="e0886-121">Atualizar os clusters com conectividade para baixar o código e a configuração mais recentes</span><span class="sxs-lookup"><span data-stu-id="e0886-121">Upgrade clusters that have connectivity to download the latest code and configuration</span></span>
<span data-ttu-id="e0886-122">Use estas etapas para atualizar seu cluster para uma versão com suporte se os nós de cluster tiverem conectividade com a Internet para [http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e0886-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="e0886-123">Para clusters que tenham conectividade com [http://download.microsoft.com](http://download.microsoft.com), a Microsoft verifica periodicamente a disponibilidade de novas versões do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e0886-123">For clusters that have connectivity to [http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span></span>

<span data-ttu-id="e0886-124">Quando uma nova versão do Service Fabric estiver disponível, o pacote será baixado localmente para o cluster e provisionado para atualização.</span><span class="sxs-lookup"><span data-stu-id="e0886-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span></span> <span data-ttu-id="e0886-125">Além de informar o cliente sobre essa nova versão, o sistema colocará um aviso explícito de integridade do cluster semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="e0886-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span></span>

<span data-ttu-id="e0886-126">"O suporte à versão atual do cluster, [version#], termina em [Data]."</span><span class="sxs-lookup"><span data-stu-id="e0886-126">“The current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="e0886-127">Depois que o cluster estiver executando a versão mais recente, o aviso será removido.</span><span class="sxs-lookup"><span data-stu-id="e0886-127">After the cluster is running the latest version, the warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="e0886-128">Fluxo de trabalho de atualização do cluster</span><span class="sxs-lookup"><span data-stu-id="e0886-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="e0886-129">Ao ver o aviso de integridade do cluster, você deve fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e0886-129">After you see the cluster health warning, do the following:</span></span>

1. <span data-ttu-id="e0886-130">Conecte-se ao cluster de qualquer computador que tenha acesso de administrador a todos os computadores listados como nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="e0886-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="e0886-131">O computador no qual este script é executado não precisa fazer parte do cluster.</span><span class="sxs-lookup"><span data-stu-id="e0886-131">The machine that this script is run on does not have to be part of the cluster.</span></span>

    ```powershell

    ###### connect to the secure cluster using certs
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

2. <span data-ttu-id="e0886-132">Obtenha a lista de versões do Service Fabric para as quais você pode atualizar.</span><span class="sxs-lookup"><span data-stu-id="e0886-132">Get the list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="e0886-133">Você deverá receber uma saída semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="e0886-133">You should get an output similar to this:</span></span>

    ![obter versões de malha][getfabversions]
3. <span data-ttu-id="e0886-135">Inicie uma atualização de cluster para uma versão disponível usando o comando [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0886-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="e0886-136">Você pode monitorar o progresso da atualização no Service Fabric Explorer ou executando o comando do Windows PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0886-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="e0886-137">Se as políticas de integridade do cluster não forem atendidas, a atualização será revertida.</span><span class="sxs-lookup"><span data-stu-id="e0886-137">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="e0886-138">Para especificar as políticas de integridade personalizadas para o comando **Start-ServiceFabricClusterUpgrade**, consulte a documentação para [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0886-138">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="e0886-139">Depois de corrigir os problemas que resultaram na reversão, você precisará iniciar a atualização novamente, seguindo as mesmas etapas descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e0886-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="e0886-140">Atualizar os clusters <U>sem conectividade</u> para baixar o código e a configuração mais recentes</span><span class="sxs-lookup"><span data-stu-id="e0886-140">Upgrade clusters that have <U>no connectivity</u> to download the latest code and configuration</span></span>
<span data-ttu-id="e0886-141">Use estas etapas para atualizar seu cluster para uma versão com suporte se os nós de cluster não tiverem conectividade com a Internet para [http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e0886-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes do not have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="e0886-142">Se estiver executando um cluster que não esteja conectado à Internet, você precisará monitorar o blog da equipe do Service Fabric para saber sobre uma novo lançamento.</span><span class="sxs-lookup"><span data-stu-id="e0886-142">If you are running a cluster that is not connected to the Internet, you will have to monitor the Service Fabric team blog to learn about a new release.</span></span> <span data-ttu-id="e0886-143">O sistema não mostra nenhum aviso de integridade do cluster para alertá-lo a respeito.</span><span class="sxs-lookup"><span data-stu-id="e0886-143">The system does not show a cluster health warning to alert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="e0886-144">Provisionamento automático vs provisionamento manual</span><span class="sxs-lookup"><span data-stu-id="e0886-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="e0886-145">Para permitir o download automático e o registro para a versão mais recente do código, configure o Serviço de Atualização do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e0886-145">To enable automatic downloading and registration for the latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="e0886-146">Consulte Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro do [Pacote Autônomo](service-fabric-cluster-standalone-package-contents.md) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="e0886-146">Refer to the Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="e0886-147">Para o processo manual, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="e0886-147">For manual process, follow the instructions below.</span></span>

<span data-ttu-id="e0886-148">Modifique a configuração do cluster para definir a propriedade a seguir como false antes de iniciar uma atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="e0886-148">Modify your cluster configuration to set the following property to false before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="e0886-149">Consulte [cmd do PS Start-ServiceFabricClusterConfigurationUpgrade](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para obter detalhes de uso.</span><span class="sxs-lookup"><span data-stu-id="e0886-149">Refer to [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="e0886-150">Certifique-se de atualizar “clusterConfigurationVersion” no JSON antes de iniciar a atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="e0886-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="e0886-151">Fluxo de trabalho de atualização do cluster</span><span class="sxs-lookup"><span data-stu-id="e0886-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="e0886-152">Execute Get-ServiceFabricClusterUpgrade em um de nós no cluster e observe o TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="e0886-152">Run Get-ServiceFabricClusterUpgrade from one of the nodes in the cluster and note the TargetCodeVersion.</span></span>
2. <span data-ttu-id="e0886-153">Execute o seguinte de uma máquina conectada à internet para listar todas as versões compatíveis com atualização com a versão atual e baixar o pacote correspondente dos links de download associados.</span><span class="sxs-lookup"><span data-stu-id="e0886-153">Run the following from an internet connected machine to list all upgrade compatible versions with the current version and download the corresponding package from the associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="e0886-154">Conecte-se ao cluster de qualquer computador que tenha acesso de administrador a todos os computadores listados como nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="e0886-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="e0886-155">O computador no qual este script é executado não precisa fazer parte do cluster</span><span class="sxs-lookup"><span data-stu-id="e0886-155">The machine that this script is run on does not have to be part of the cluster</span></span>

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="e0886-156">Copie o pacote baixado para o repositório de imagens do cluster.</span><span class="sxs-lookup"><span data-stu-id="e0886-156">Copy the downloaded package into the cluster image store.</span></span>

5. <span data-ttu-id="e0886-157">Registre o pacote copiado.</span><span class="sxs-lookup"><span data-stu-id="e0886-157">Register the copied package.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="e0886-158">Inicie uma atualização do cluster para uma versão disponível.</span><span class="sxs-lookup"><span data-stu-id="e0886-158">Start a cluster upgrade to an available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="e0886-159">Você pode monitorar o progresso da atualização no Service Fabric Explorer ou executando o comando do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0886-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="e0886-160">Se as políticas de integridade do cluster não forem atendidas, a atualização será revertida.</span><span class="sxs-lookup"><span data-stu-id="e0886-160">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="e0886-161">Para especificar as políticas de integridade personalizadas para o comando **Start-ServiceFabricClusterUpgrade**, consulte a documentação para [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0886-161">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="e0886-162">Depois de corrigir os problemas que resultaram na reversão, você precisará iniciar a atualização novamente, seguindo as mesmas etapas descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e0886-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>


## <a name="upgrade-the-cluster-configuration"></a><span data-ttu-id="e0886-163">Atualizar a configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="e0886-163">Upgrade the cluster configuration</span></span>
<span data-ttu-id="e0886-164">Antes de iniciar a atualização de configuração, você pode testar seu novo json de configuração de cluster executando o script do powershell no pacote autônomo.</span><span class="sxs-lookup"><span data-stu-id="e0886-164">Before you initiate the configuration upgrade, you can test your new cluster configuration json by running the powershell script in the standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
<span data-ttu-id="e0886-165">ou</span><span class="sxs-lookup"><span data-stu-id="e0886-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

<span data-ttu-id="e0886-166">Algumas configurações não podem ser atualizadas, como pontos de extremidade, nome do cluster, nó IP, etc. Isso testará o json de configuração do cluster novo contra antigo e gerar erros na janela do Powershell, se houver qualquer problema.</span><span class="sxs-lookup"><span data-stu-id="e0886-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test the new cluster configuration json against the old one and throw errors in the Powershell window if there is any issue.</span></span>

<span data-ttu-id="e0886-167">Para atualizar a configuração do cluster, execute o comando **Start-ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="e0886-167">To upgrade the cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="e0886-168">A atualização de configuração é processada domínio de atualização por domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="e0886-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="e0886-169">Atualização da configuração do certificado do cluster</span><span class="sxs-lookup"><span data-stu-id="e0886-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="e0886-170">O certificado do cluster é usado para autenticação entre nós de cluster, para que a distribuição do certificado seja executada com muito cuidado, pois a falha bloqueará a comunicação entre nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0886-170">Cluster certificate is used for authentication between cluster nodes, so the certificate roll over should be performed with extra caution because failure will block the communication among cluster nodes.</span></span>  
<span data-ttu-id="e0886-171">Tecnicamente, há três opções com suporte:</span><span class="sxs-lookup"><span data-stu-id="e0886-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="e0886-172">Atualização de um certificado: o caminho de atualização é 'Certificado A (Primário)-> Certificado B (Primário)-> Certificado C (Primário)->...'.</span><span class="sxs-lookup"><span data-stu-id="e0886-172">Single certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="e0886-173">Atualização de dois certificados: o caminho de atualização é 'Certificado A (Primário) - > Certificado A (Primário) e B (Secundário) -> Certificado B (Primário) -> Certificado B (Primário) e C (Secundário) -> Certificado C (Primário)->...'.</span><span class="sxs-lookup"><span data-stu-id="e0886-173">Double certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="e0886-174">Atualização do tipo de certificado: configuração de certificados com base em CommonName configuração <-> com base em impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="e0886-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="e0886-175">Por exemplo, impressão digital do certificado (primária) e a impressão digital B (secundários) -> certificado CommonName C.</span><span class="sxs-lookup"><span data-stu-id="e0886-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0886-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0886-176">Next steps</span></span>
* <span data-ttu-id="e0886-177">Saiba como personalizar algumas das [configurações de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="e0886-177">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="e0886-178">Saiba como [reduzir e escalar horizontalmente seu cluster](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="e0886-178">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="e0886-179">Saiba mais sobre [atualizações de aplicativo](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="e0886-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
