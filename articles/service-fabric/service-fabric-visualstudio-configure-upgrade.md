---
title: "Configurar a atualização de um aplicativo do Service Fabric | Microsoft Docs"
description: "Saiba como definir as configurações para atualizar um aplicativo do Service Fabric usando o Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="9f06d-103">Configurar a atualização de um aplicativo do Service Fabric no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f06d-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="9f06d-104">As ferramentas do Visual Studio para o Service Fabric do Azure dão suporte à atualização da publicação em clusters locais ou remotos.</span><span class="sxs-lookup"><span data-stu-id="9f06d-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="9f06d-105">Há três cenários onde você deseja atualizar seu aplicativo para uma versão mais recente em vez de substituir o aplicativo durante o teste e a depuração:</span><span class="sxs-lookup"><span data-stu-id="9f06d-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="9f06d-106">Os dados de aplicativos não serão perdidos durante a atualização.</span><span class="sxs-lookup"><span data-stu-id="9f06d-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="9f06d-107">A disponibilidade continua alta para que não haja nenhuma interrupção do serviço durante a atualização, se houver instâncias de serviço suficientes distribuídas entre os domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="9f06d-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="9f06d-108">Os testes podem ser executados em um aplicativo enquanto ele está sendo atualizado.</span><span class="sxs-lookup"><span data-stu-id="9f06d-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="9f06d-109">Parâmetros necessários para atualizar</span><span class="sxs-lookup"><span data-stu-id="9f06d-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="9f06d-110">Você pode escolher entre dois tipos de implantação: normal ou atualização.</span><span class="sxs-lookup"><span data-stu-id="9f06d-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="9f06d-111">Uma implantação normal apaga todas as informações e dados sobre a implantação anterior do cluster, enquanto uma implantação de atualização preserva-as.</span><span class="sxs-lookup"><span data-stu-id="9f06d-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="9f06d-112">Ao atualizar um aplicativo do Service Fabric no Visual Studio, você precisa fornecer políticas de verificação de integridade e parâmetros de atualização de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f06d-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="9f06d-113">Os parâmetros de atualização de aplicativo ajudam a controlar a atualização, enquanto as políticas de verificação de integridade determinam se a atualização foi bem-sucedida ou não.</span><span class="sxs-lookup"><span data-stu-id="9f06d-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="9f06d-114">Veja [Atualização do aplicativo Service Fabric: atualizar parâmetros](service-fabric-application-upgrade-parameters.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9f06d-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="9f06d-115">Existem três modos de atualização: *Monitored*, *UnmonitoredAuto* e *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="9f06d-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="9f06d-116">Uma atualização Monitorada automatiza a atualização e a verificação de integridade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f06d-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="9f06d-117">Uma atualização Não monitorada/Automática automatiza a atualização, mas ignora a verificação de integridade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f06d-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="9f06d-118">Ao fazer uma atualização Não monitorada/Manual, é necessário atualizar manualmente cada domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="9f06d-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="9f06d-119">Cada modo de atualização requer diferentes conjuntos de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9f06d-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="9f06d-120">Veja [Parâmetros de atualização de aplicativo](service-fabric-application-upgrade-parameters.md) para saber mais sobre as opções de atualização disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9f06d-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="9f06d-121">Atualizar um aplicativo do Service Fabric no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f06d-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="9f06d-122">Se você está usando as ferramentas do Service Fabric no Visual Studio para atualizar um aplicativo do Service Fabric, você pode especificar um processo de publicação como uma atualização em vez de uma implantação normal, marcando a caixa de seleção **Atualizar o aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="9f06d-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="9f06d-123">Para configurar os parâmetros de atualização</span><span class="sxs-lookup"><span data-stu-id="9f06d-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="9f06d-124">Clique no botão **Configurações** próximo à caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="9f06d-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="9f06d-125">A caixa de diálogo **Editar Parâmetros de Atualização** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9f06d-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="9f06d-126">A caixa de diálogo **Editar Parâmetros de Atualização** dá suporte aos modos de atualização Monitorada, Não monitorada/Automática e Não monitorada/Manual.</span><span class="sxs-lookup"><span data-stu-id="9f06d-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="9f06d-127">Selecione o modo de atualização que você deseja usar e preencha a grade de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9f06d-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="9f06d-128">Cada parâmetro tem valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9f06d-128">Each parameter has default values.</span></span> <span data-ttu-id="9f06d-129">O parâmetro opcional *DefaultServiceTypeHealthPolicy* tem uma entrada de tabela de hash.</span><span class="sxs-lookup"><span data-stu-id="9f06d-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="9f06d-130">Aqui está um exemplo do formato de entrada de tabela de hash para *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="9f06d-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="9f06d-131">*ServiceTypeHealthPolicyMap* é outro parâmetro opcional que utiliza uma entrada de tabela de hash no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9f06d-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="9f06d-132">Aqui está um exemplo da vida real:</span><span class="sxs-lookup"><span data-stu-id="9f06d-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="9f06d-133">Se selecionar o modo de atualização Não monitorada/Manual, você precisará iniciar manualmente um console do PowerShell para continuar e concluir o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="9f06d-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="9f06d-134">Consulte [Atualização de aplicativos do Service Fabric: tópicos avançados](service-fabric-application-upgrade-advanced.md) para saber como a atualização manual funciona.</span><span class="sxs-lookup"><span data-stu-id="9f06d-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="9f06d-135">Atualizar um aplicativo usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f06d-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="9f06d-136">Você pode usar os cmdlets do PowerShell para atualizar um aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9f06d-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="9f06d-137">Confira [Tutorial da atualização de aplicativos do Service Fabric](service-fabric-application-upgrade-tutorial.md) e [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="9f06d-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="9f06d-138">Especifique uma política de verificação de integridade no arquivo de manifesto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9f06d-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="9f06d-139">Cada serviço em um aplicativo do Service Fabric pode ter seus próprios parâmetros de política de integridade, que substituem os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9f06d-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="9f06d-140">Você pode fornecer esses valores de parâmetro no arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f06d-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="9f06d-141">O exemplo a seguir mostra como aplicar uma política de verificação de integridade exclusiva para cada serviço no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f06d-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="9f06d-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f06d-142">Next steps</span></span>
<span data-ttu-id="9f06d-143">Para saber mais sobre como implantar um aplicativo, confira [Implantar um aplicativo existente no Service Fabric do Azure](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f06d-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>