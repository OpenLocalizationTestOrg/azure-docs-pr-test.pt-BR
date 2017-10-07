---
title: "atualização de saudação aaaConfigure de um aplicativo de malha do serviço | Microsoft Docs"
description: "Saiba como tooconfigure Olá configurações para atualizar um aplicativo de malha do serviço usando o Microsoft Visual Studio."
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
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="befd8-103">Configurar a atualização de saudação de um aplicativo de malha do serviço no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="befd8-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="befd8-104">Visual Studio tools para o Azure Service Fabric oferecem suporte à atualização para publicação toolocal ou clusters remotos.</span><span class="sxs-lookup"><span data-stu-id="befd8-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="befd8-105">Há três cenários em que você deseja tooupgrade sua versão mais recente do aplicativo tooa em vez de substituir o aplicativo hello durante o teste e depuração:</span><span class="sxs-lookup"><span data-stu-id="befd8-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="befd8-106">Dados de aplicativo não serão perdidos durante a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="befd8-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="befd8-107">Disponibilidade permanece alta para não haver qualquer interrupção do serviço durante a atualização de hello, se houver que instâncias suficientes serviço espalham em domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="befd8-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="befd8-108">Os testes podem ser executados em um aplicativo enquanto ele está sendo atualizado.</span><span class="sxs-lookup"><span data-stu-id="befd8-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="befd8-109">Parâmetros necessários tooupgrade</span><span class="sxs-lookup"><span data-stu-id="befd8-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="befd8-110">Você pode escolher entre dois tipos de implantação: normal ou atualização.</span><span class="sxs-lookup"><span data-stu-id="befd8-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="befd8-111">Uma implantação regular apaga quaisquer informações de implantação anterior e os dados no cluster hello, enquanto preserva a ele uma implantação de atualização.</span><span class="sxs-lookup"><span data-stu-id="befd8-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="befd8-112">Quando você atualizar um aplicativo de malha do serviço no Visual Studio, você precisa parâmetros de atualização de aplicativo tooprovide e políticas de verificação de integridade.</span><span class="sxs-lookup"><span data-stu-id="befd8-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="befd8-113">Atualização do aplicativo parâmetros ajudam a controlar a atualização de hello, enquanto as políticas de verificação de integridade determinam se a atualização de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="befd8-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="befd8-114">Veja [Atualização do aplicativo Service Fabric: atualizar parâmetros](service-fabric-application-upgrade-parameters.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="befd8-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="befd8-115">Existem três modos de atualização: *Monitored*, *UnmonitoredAuto* e *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="befd8-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="befd8-116">Uma atualização monitorado automatiza a atualização hello e aplicativo verificação de integridade.</span><span class="sxs-lookup"><span data-stu-id="befd8-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="befd8-117">Uma atualização UnmonitoredAuto automatiza a atualização hello, mas ignora Olá verificação de integridade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="befd8-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="befd8-118">Quando você faz uma atualização UnmonitoredManual, você precisa toomanually atualizar cada domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="befd8-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="befd8-119">Cada modo de atualização requer diferentes conjuntos de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="befd8-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="befd8-120">Consulte [parâmetros de atualização de aplicativo](service-fabric-application-upgrade-parameters.md) toolearn mais sobre as opções de atualização disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="befd8-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="befd8-121">Atualizar um aplicativo do Service Fabric no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="befd8-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="befd8-122">Se você estiver usando saudação do Visual Studio Service Fabric ferramentas tooupgrade um aplicativo de malha do serviço, você pode especificar uma atualização em vez de uma implantação regular um toobe do processo de publicação, verificando Olá **atualizar o aplicativo hello** verificar caixa.</span><span class="sxs-lookup"><span data-stu-id="befd8-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="befd8-123">parâmetros de atualização de saudação tooconfigure</span><span class="sxs-lookup"><span data-stu-id="befd8-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="befd8-124">Clique em Olá **configurações** caixa de seleção do botão próxima toohello.</span><span class="sxs-lookup"><span data-stu-id="befd8-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="befd8-125">Olá **Editar parâmetros de atualização** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="befd8-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="befd8-126">Olá **Editar parâmetros de atualização** caixa de diálogo oferece suporte a modos de atualização monitorado, UnmonitoredAuto e UnmonitoredManual hello.</span><span class="sxs-lookup"><span data-stu-id="befd8-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="befd8-127">Selecione o modo de atualização de Olá que você deseja toouse e, em seguida, preencha a grade de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="befd8-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="befd8-128">Cada parâmetro tem valores padrão.</span><span class="sxs-lookup"><span data-stu-id="befd8-128">Each parameter has default values.</span></span> <span data-ttu-id="befd8-129">Olá parâmetro opcional *DefaultServiceTypeHealthPolicy* utiliza uma entrada da tabela de hash.</span><span class="sxs-lookup"><span data-stu-id="befd8-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="befd8-130">Aqui está um exemplo de formato de tabela entrada de hash Olá para *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="befd8-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="befd8-131">*ServiceTypeHealthPolicyMap* é outro parâmetro opcional que usa uma entrada de tabela de hash no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="befd8-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="befd8-132">Aqui está um exemplo da vida real:</span><span class="sxs-lookup"><span data-stu-id="befd8-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="befd8-133">Se você selecionar o modo de atualização UnmonitoredManual, manualmente deve iniciar um toocontinue do console do PowerShell e concluir o processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="befd8-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="befd8-134">Consulte também[atualização do aplicativo do Service Fabric: tópicos avançados](service-fabric-application-upgrade-advanced.md) toolearn manual como atualizar funciona.</span><span class="sxs-lookup"><span data-stu-id="befd8-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="befd8-135">Atualizar um aplicativo usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="befd8-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="befd8-136">Você pode usar o PowerShell cmdlets tooupgrade um aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="befd8-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="befd8-137">Confira [Tutorial da atualização de aplicativos do Service Fabric](service-fabric-application-upgrade-tutorial.md) e [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="befd8-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="befd8-138">Especificar uma política de verificação de integridade no arquivo de manifesto de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="befd8-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="befd8-139">Cada serviço em um aplicativo de malha do serviço pode ter seus próprios parâmetros de política de integridade que substituem os valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="befd8-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="befd8-140">Você pode fornecer esses valores de parâmetro no arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="befd8-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="befd8-141">Olá exemplo a seguir mostra como verificar a diretiva de para cada serviço no manifesto de aplicativo hello tooapply exclusivos de integridade.</span><span class="sxs-lookup"><span data-stu-id="befd8-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="befd8-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="befd8-142">Next steps</span></span>
<span data-ttu-id="befd8-143">Para saber mais sobre como implantar um aplicativo, confira [Implantar um aplicativo existente no Service Fabric do Azure](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="befd8-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>