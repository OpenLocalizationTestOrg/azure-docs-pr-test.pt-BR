---
title: "aaaAzure Service Fabric as diferenças entre o Linux e Windows | Microsoft Docs"
description: "Diferenças entre hello visualização do Azure Service Fabric no Linux e do Azure Service Fabric no Windows."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="19e86-103">Diferenças entre o Service Fabric no Linux (visualização) e no Windows (geralmente disponível)</span><span class="sxs-lookup"><span data-stu-id="19e86-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="19e86-104">Como o Service Fabric no Linux é uma visualização, há alguns recursos que têm suporte no Windows, mas ainda não têm no Linux.</span><span class="sxs-lookup"><span data-stu-id="19e86-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="19e86-105">Eventualmente, Olá conjuntos de recursos será em paridade quando o serviço de malha no Linux se tornarem disponível.</span><span class="sxs-lookup"><span data-stu-id="19e86-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="19e86-106">Nas futuras versões, esse intervalo de recursos será reduzido.</span><span class="sxs-lookup"><span data-stu-id="19e86-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="19e86-107">Olá seguir existem diferenças entre as versões mais recentes disponíveis de hello (ou seja, entre a versão 5.6 no Windows e versão 5.5 no Linux):</span><span class="sxs-lookup"><span data-stu-id="19e86-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="19e86-108">Coleções Confiáveis (e Serviços Confiáveis com Estado)</span><span class="sxs-lookup"><span data-stu-id="19e86-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="19e86-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="19e86-109">ReverseProxy</span></span> 
* <span data-ttu-id="19e86-110">Instalador autônomo</span><span class="sxs-lookup"><span data-stu-id="19e86-110">Standalone installer</span></span> 
* <span data-ttu-id="19e86-111">Validação do esquema XML para os arquivos de manifesto</span><span class="sxs-lookup"><span data-stu-id="19e86-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="19e86-112">Redirecionamento do console</span><span class="sxs-lookup"><span data-stu-id="19e86-112">Console redirection</span></span> 
* <span data-ttu-id="19e86-113">Olá serviço de análise de falha (FAS)</span><span class="sxs-lookup"><span data-stu-id="19e86-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="19e86-114">Docker Compose, volume e drivers de log para contêineres</span><span class="sxs-lookup"><span data-stu-id="19e86-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="19e86-115">Governança de recursos para contêineres e serviços</span><span class="sxs-lookup"><span data-stu-id="19e86-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="19e86-116">Serviço DNS</span><span class="sxs-lookup"><span data-stu-id="19e86-116">DNS service</span></span>
* <span data-ttu-id="19e86-117">Suporte ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19e86-117">Azure Active Directory support</span></span>
* <span data-ttu-id="19e86-118">Equivalentes de comando da CLI de certos comandos do Powershell</span><span class="sxs-lookup"><span data-stu-id="19e86-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="19e86-119">Somente um subconjunto dos comandos do Powershell pode ser executado em um cluster do Linux (como expandido na próxima seção, Olá).</span><span class="sxs-lookup"><span data-stu-id="19e86-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="19e86-120">O redirecionamento de console não tem suporte em clusters de produção, mesmo no Windows.</span><span class="sxs-lookup"><span data-stu-id="19e86-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="19e86-121">As ferramentas de desenvolvimento também são diferente entre o Windows e o Linux.</span><span class="sxs-lookup"><span data-stu-id="19e86-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="19e86-122">VisualStudio, Powershell, VSTS e ETW são usados no Windows, enquanto Yeoman, Eclipse, Jenkins e LTTng são usados no Linux.</span><span class="sxs-lookup"><span data-stu-id="19e86-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="19e86-123">Cmdlets do PowerShell que não funcionam em um cluster Linux do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="19e86-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="19e86-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="19e86-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="19e86-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="19e86-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="19e86-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="19e86-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="19e86-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="19e86-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="19e86-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="19e86-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="19e86-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19e86-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="19e86-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19e86-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="19e86-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="19e86-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="19e86-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="19e86-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="19e86-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="19e86-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="19e86-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="19e86-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="19e86-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="19e86-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="19e86-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="19e86-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="19e86-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="19e86-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="19e86-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="19e86-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="19e86-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="19e86-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="19e86-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="19e86-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="19e86-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="19e86-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="19e86-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="19e86-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="19e86-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="19e86-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="19e86-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="19e86-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="19e86-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="19e86-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="19e86-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="19e86-146">Cmd</span></span>
* <span data-ttu-id="19e86-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19e86-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19e86-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="19e86-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="19e86-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="19e86-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="19e86-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="19e86-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="19e86-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="19e86-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="19e86-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="19e86-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="19e86-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19e86-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="19e86-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="19e86-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="19e86-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="19e86-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="19e86-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="19e86-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="19e86-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="19e86-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="19e86-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19e86-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19e86-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="19e86-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="19e86-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="19e86-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="19e86-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19e86-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19e86-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="19e86-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="19e86-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="19e86-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="19e86-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19e86-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19e86-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19e86-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19e86-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19e86-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19e86-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19e86-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19e86-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="19e86-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="19e86-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="19e86-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="19e86-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="19e86-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="19e86-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="19e86-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="19e86-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="19e86-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="19e86-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19e86-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19e86-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19e86-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19e86-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19e86-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19e86-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="19e86-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="19e86-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19e86-177">Next steps</span></span>
* [<span data-ttu-id="19e86-178">Preparar seu ambiente de desenvolvimento no Linux</span><span class="sxs-lookup"><span data-stu-id="19e86-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="19e86-179">Preparar seu ambiente de desenvolvimento no OSX</span><span class="sxs-lookup"><span data-stu-id="19e86-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="19e86-180">Criar e implantar seu primeiro aplicativo Java de do Service Fabric no Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="19e86-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="19e86-181">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in do Service Fabric para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="19e86-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="19e86-182">Criar seu primeiro aplicativo do CSharp no Linux</span><span class="sxs-lookup"><span data-stu-id="19e86-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="19e86-183">Usar Olá CLI de malha do serviço toomanage seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="19e86-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
