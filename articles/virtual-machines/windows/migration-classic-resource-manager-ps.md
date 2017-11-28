---
title: aaaMigrate tooResource Manager com o PowerShell | Microsoft Docs
description: "Este artigo o orienta por meio da migração de suporte de plataforma de saudação de recursos de IaaS como máquinas virtuais (VMs), redes virtuais (VNETs) e contas de armazenamento do clássico tooAzure Resource Manager (ARM) usando comandos do PowerShell do Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="db047-103">Migrar recursos de IaaS de tooAzure clássico Gerenciador de recursos usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="db047-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="db047-104">Estas etapas mostram como os toouse do Azure PowerShell comandos toomigrate infraestrutura como um recurso de serviço (IaaS) do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="db047-105">Se desejar, você também pode migrar recursos usando Olá [Interface de linha de comando (CLI do Azure) do Azure](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="db047-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="db047-106">Para obter informações sobre cenários de migração com suporte, consulte [plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db047-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="db047-107">Para obter orientações detalhadas e um passo a passo de migração, consulte [técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="db047-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="db047-108">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="db047-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="db047-109">Aqui está uma ordem de saudação do fluxograma tooidentify nos quais etapas precisam toobe executado durante o processo de migração</span><span class="sxs-lookup"><span data-stu-id="db047-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Captura de tela que mostra as etapas de migração de saudação](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="db047-111">Etapa 1: Planejar a migração</span><span class="sxs-lookup"><span data-stu-id="db047-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="db047-112">Aqui estão algumas práticas recomendadas que recomendamos durante a avaliação de migração de recursos de IaaS do clássico tooResource Manager:</span><span class="sxs-lookup"><span data-stu-id="db047-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="db047-113">Leia Olá [com e sem suporte a recursos e configurações](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db047-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="db047-114">Se você tiver máquinas virtuais que usam recursos ou configurações sem suporte, é recomendável que você aguarde Olá configuração/recurso suporte toobe anunciada.</span><span class="sxs-lookup"><span data-stu-id="db047-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="db047-115">Como alternativa, se ele atende às suas necessidades, remover esse recurso ou mover para fora da migração tooenable configuração.</span><span class="sxs-lookup"><span data-stu-id="db047-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="db047-116">Se você tiver automatizado scripts que implantar a infraestrutura e os aplicativos de hoje, tente toocreate uma configuração de teste semelhante usando esses scripts para a migração.</span><span class="sxs-lookup"><span data-stu-id="db047-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="db047-117">Como alternativa, você pode configurar ambientes de exemplo usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db047-118">Os Gateways de aplicativos não têm suporte atualmente para a migração de clássico tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="db047-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="db047-119">toomigrate uma rede virtual clássica com um gateway de aplicativo, remova gateway Olá antes de executar uma rede Olá de toomove de operação de preparação.</span><span class="sxs-lookup"><span data-stu-id="db047-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="db047-120">Depois de concluir a migração de hello, reconecte gateway Olá no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="db047-121">Gateways de rota expressa conectando tooExpressRoute circuitos em outra assinatura não podem ser migrados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="db047-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="db047-122">Nesses casos, remover o gateway de rota expressa hello, migrar a rede virtual hello e recrie o gateway hello.</span><span class="sxs-lookup"><span data-stu-id="db047-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="db047-123">Consulte [ExpressRoute migrar circuitos e associadas a redes virtuais do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../../expressroute/expressroute-migration-classic-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="db047-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="db047-124">Etapa 2: Instalar a versão mais recente de saudação do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="db047-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="db047-125">Há duas opções principais tooinstall PowerShell do Azure: [Galeria do PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) ou [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="db047-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="db047-126">WebPI recebe atualizações mensais.</span><span class="sxs-lookup"><span data-stu-id="db047-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="db047-127">A Galeria do PowerShell receberá atualizações continuamente.</span><span class="sxs-lookup"><span data-stu-id="db047-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="db047-128">Este artigo tem base no Azure PowerShell versão 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="db047-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="db047-129">Para obter instruções de instalação, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db047-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="db047-130">Etapa 3: Verifique se você for um administrador de assinatura de saudação no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="db047-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="db047-131">tooperform a migração, você deve ser adicionado como coadministrador da assinatura Olá Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db047-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="db047-132">O logon no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db047-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="db047-133">No menu de Hub hello, selecione **assinatura**.</span><span class="sxs-lookup"><span data-stu-id="db047-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="db047-134">Caso não visualize essa opção, selecione **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="db047-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="db047-135">Localizar a entrada de assinatura apropriada hello, examinar Olá **minha função** campo.</span><span class="sxs-lookup"><span data-stu-id="db047-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="db047-136">Para um coadministrador, o valor de saudação deve ser _administrador da conta_.</span><span class="sxs-lookup"><span data-stu-id="db047-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="db047-137">Se você não for capaz de tooadd um coadministrador, contate um administrador de serviço ou coadministrador para Olá assinatura tooget por conta própria adicionado.</span><span class="sxs-lookup"><span data-stu-id="db047-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="db047-138">Etapa 4: Definir a assinatura e se inscrever para a migração</span><span class="sxs-lookup"><span data-stu-id="db047-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="db047-139">Primeiro, inicie um prompt do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db047-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="db047-140">Para a migração, você precisa tooset seu ambiente para ambos os clássico e o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="db047-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="db047-141">Entre na conta de tooyour para o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="db047-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="db047-142">Obter assinaturas disponíveis hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="db047-143">Defina sua assinatura do Azure para Olá a sessão atual.</span><span class="sxs-lookup"><span data-stu-id="db047-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="db047-144">Este exemplo define Olá nome da assinatura padrão muito**minha assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="db047-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="db047-145">Substitua o nome de inscrição do exemplo hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="db047-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="db047-146">O registro é uma etapa única, mas é preciso executá-lo uma vez antes de tentar a migração.</span><span class="sxs-lookup"><span data-stu-id="db047-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="db047-147">Sem registrar, você verá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="db047-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="db047-148">*BadRequest: a assinatura não está registrada para migração.*</span><span class="sxs-lookup"><span data-stu-id="db047-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="db047-149">Registrar com o provedor de recursos de migração de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="db047-150">Aguarde cinco minutos para Olá toofinish de registro.</span><span class="sxs-lookup"><span data-stu-id="db047-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="db047-151">Você pode verificar o status de saudação de aprovação de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="db047-152">Verifique se RegistrationState é `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="db047-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="db047-153">Agora, entre na conta de tooyour para o modelo clássico hello.</span><span class="sxs-lookup"><span data-stu-id="db047-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="db047-154">Obter assinaturas disponíveis hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="db047-155">Defina sua assinatura do Azure para Olá a sessão atual.</span><span class="sxs-lookup"><span data-stu-id="db047-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="db047-156">Este exemplo define a assinatura de padrão de saudação muito**minha assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="db047-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="db047-157">Substitua o nome de inscrição do exemplo hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="db047-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="db047-158">Etapa 5: Verifique se que você tem suficiente núcleos de máquina Virtual do Azure Resource Manager no hello região do Azure de sua implantação atual ou a rede virtual</span><span class="sxs-lookup"><span data-stu-id="db047-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="db047-159">Você pode usar o hello PowerShell comando toocheck Olá número atual de núcleos que você tem no Gerenciador de recursos do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="db047-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="db047-160">toolearn mais sobre cotas de core, consulte [limites e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="db047-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="db047-161">Este exemplo verifica a disponibilidade Olá Olá **Oeste dos EUA** região.</span><span class="sxs-lookup"><span data-stu-id="db047-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="db047-162">Substitua o nome da região exemplo hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="db047-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="db047-163">Etapa 6: Executar comandos toomigrate seus recursos de IaaS</span><span class="sxs-lookup"><span data-stu-id="db047-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="db047-164">Todas as operações de saudação descritas aqui são idempotentes.</span><span class="sxs-lookup"><span data-stu-id="db047-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="db047-165">Se você tiver um problema que não seja um recurso sem suporte ou um erro de configuração, é recomendável que você repita Olá preparar, anular ou confirmar a operação.</span><span class="sxs-lookup"><span data-stu-id="db047-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="db047-166">plataforma de saudação tentará novamente a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="db047-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="db047-167">Etapa 6.1: Opção 1 - Migrar máquinas virtuais em um serviço de nuvem (não em uma rede virtual)</span><span class="sxs-lookup"><span data-stu-id="db047-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="db047-168">Obter uma lista de serviços de nuvem usando o comando a seguir de saudação e, em seguida, escolha Olá serviço em nuvem que você deseja toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="db047-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="db047-169">Se Olá VMs no serviço de nuvem Olá está em uma rede virtual ou se eles têm funções web ou de trabalho, o comando Olá retorna uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="db047-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="db047-170">Obter o nome de implantação Olá Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="db047-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="db047-171">Neste exemplo, o nome do serviço de saudação é **meu serviço**.</span><span class="sxs-lookup"><span data-stu-id="db047-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="db047-172">Substitua o nome do serviço de exemplo hello com seu próprio nome de serviço.</span><span class="sxs-lookup"><span data-stu-id="db047-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="db047-173">Prepare Olá VMs no serviço de nuvem Olá para migração.</span><span class="sxs-lookup"><span data-stu-id="db047-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="db047-174">Você tem dois toochoose de opções do.</span><span class="sxs-lookup"><span data-stu-id="db047-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="db047-175">**Opção 1. Migrar Olá VMs tooa criado plataforma rede virtual**</span><span class="sxs-lookup"><span data-stu-id="db047-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="db047-176">Primeiro, valide se você pode migrar o serviço de nuvem hello usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="db047-177">Olá comando anterior exibe avisos e erros que bloqueiam a migração.</span><span class="sxs-lookup"><span data-stu-id="db047-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="db047-178">Se a validação for bem-sucedida, você pode mover toohello **preparar** etapa:</span><span class="sxs-lookup"><span data-stu-id="db047-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="db047-179">**Opção 2. Migrar a rede virtual existente do tooan no modelo de implantação do Gerenciador de recursos de saudação**</span><span class="sxs-lookup"><span data-stu-id="db047-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="db047-180">Este exemplo define Olá nome do grupo de recursos muito**myResourceGroup**, Olá muito o nome de rede virtual**myVirtualNetwork** e Olá nome da sub-rede muito**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="db047-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="db047-181">Substitua os nomes de saudação no exemplo hello com nomes de saudação de seus próprios recursos.</span><span class="sxs-lookup"><span data-stu-id="db047-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="db047-182">Primeiro, valide se migrar Olá rede virtual usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="db047-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="db047-183">Olá comando anterior exibe avisos e erros que bloqueiam a migração.</span><span class="sxs-lookup"><span data-stu-id="db047-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="db047-184">Se a validação for bem-sucedida, você pode prosseguir com hello etapa de preparação a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="db047-185">Depois de Olá operação preparar for bem-sucedida com o hello anterior opções, consulte o estado de migração de saudação do hello VMs.</span><span class="sxs-lookup"><span data-stu-id="db047-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="db047-186">Certifique-se de que eles estejam em Olá `Prepared` estado.</span><span class="sxs-lookup"><span data-stu-id="db047-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="db047-187">Este exemplo define Olá nome da VM muito**myVM**.</span><span class="sxs-lookup"><span data-stu-id="db047-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="db047-188">Substitua o nome do exemplo hello com seu próprio nome VM.</span><span class="sxs-lookup"><span data-stu-id="db047-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="db047-189">Verifique a configuração de saudação para Olá preparado recursos usando o PowerShell ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="db047-190">Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="db047-191">Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="db047-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="db047-192">Etapa 6.1: Opção 2 - Migrar máquinas virtuais em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="db047-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="db047-193">máquinas virtuais de toomigrate em uma rede virtual, você migrar a rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="db047-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="db047-194">máquinas virtuais de saudação migrar automaticamente com a rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="db047-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="db047-195">Escolha Olá rede virtual que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="db047-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="db047-196">[Migrar máquina virtual clássica](migrate-single-classic-to-resource-manager.md) criando uma nova máquina virtual Gerenciador de recursos com discos gerenciados usando os arquivos hello (sistema operacional e dados) de VHD de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="db047-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="db047-197">nome da rede virtual Olá pode ser diferente do que é exibido no hello novo Portal.</span><span class="sxs-lookup"><span data-stu-id="db047-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="db047-198">Olá, novo Portal do Azure exibe nome hello como `[vnet-name]` mas o nome de rede virtual real Olá é do tipo `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="db047-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="db047-199">Antes de migrar, nome da pesquisa Olá real de rede virtual usando o comando Olá `Get-AzureVnetSite | Select -Property Name` ou exibi-lo no hello antigo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="db047-200">Este exemplo define Olá nome de rede virtual muito**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="db047-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="db047-201">Substitua o nome de rede virtual do exemplo hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="db047-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="db047-202">Se a rede virtual Olá contém web ou funções de trabalho ou máquinas virtuais com configurações sem suporte, você receberá uma mensagem de erro de validação.</span><span class="sxs-lookup"><span data-stu-id="db047-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="db047-203">Primeiro, valide se você pode migrar a rede virtual Olá usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="db047-204">Olá comando anterior exibe avisos e erros que bloqueiam a migração.</span><span class="sxs-lookup"><span data-stu-id="db047-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="db047-205">Se a validação for bem-sucedida, você pode prosseguir com hello etapa de preparação a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="db047-206">Verifique a configuração de saudação para Olá preparado máquinas virtuais usando o Azure PowerShell ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="db047-207">Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="db047-208">Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="db047-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="db047-209">Etapa 6.2 Migrar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="db047-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="db047-210">Quando terminar de migração de máquinas virtuais Olá, é recomendável que migrar as contas de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="db047-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="db047-211">Antes de migrar uma conta de armazenamento hello, execute anterior verificações de pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="db047-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="db047-212">**Migrar máquinas virtuais clássicas cujos discos são armazenados na conta de armazenamento Olá**</span><span class="sxs-lookup"><span data-stu-id="db047-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="db047-213">Precede o comando retorna propriedades de RoleName e DiskName de todos os discos VM clássicos Olá na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="db047-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="db047-214">RoleName é o nome de saudação do hello toowhich de máquina virtual em um disco está anexado.</span><span class="sxs-lookup"><span data-stu-id="db047-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="db047-215">Se precede o comando retorna discos, em seguida, certifique-se de que toowhich de máquinas virtuais que esses discos anexados são migrados antes de migrar Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="db047-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="db047-216">**Excluir desanexada clássicos discos VM armazenados na conta de armazenamento Olá**</span><span class="sxs-lookup"><span data-stu-id="db047-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="db047-217">Localize desanexada clássicos discos de VM no armazenamento de saudação de conta usando a seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="db047-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="db047-218">Se o comando acima retornar discos, exclua-os usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="db047-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="db047-219">**Excluir imagens da VM armazenadas na conta de armazenamento Olá**</span><span class="sxs-lookup"><span data-stu-id="db047-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="db047-220">Precede o comando retorna todas as imagens VM Olá com armazenados na conta de armazenamento de saudação de disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="db047-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="db047-221">Precede o comando retorna todas as imagens VM Olá com discos de dados armazenados na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="db047-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="db047-222">Exclua todas as imagens VM Olá retornadas por acima comandos usando o comando anterior:</span><span class="sxs-lookup"><span data-stu-id="db047-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="db047-223">Valide cada conta de armazenamento para a migração usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="db047-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="db047-224">Neste exemplo, é o nome de conta de armazenamento Olá **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="db047-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="db047-225">Substitua o nome do exemplo hello com nome de saudação do sua própria conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="db047-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="db047-226">Próxima etapa é a conta de armazenamento tooPrepare Olá para migração</span><span class="sxs-lookup"><span data-stu-id="db047-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="db047-227">Verifique a configuração de saudação para Olá preparada a conta de armazenamento usando o Azure PowerShell ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="db047-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="db047-228">Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="db047-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="db047-229">Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="db047-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="db047-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db047-230">Next steps</span></span>
* [<span data-ttu-id="db047-231">Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="db047-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="db047-232">Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="db047-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="db047-233">Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="db047-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="db047-234">Usar recursos de IaaS toomigrate CLI do clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="db047-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="db047-235">Ferramentas de comunidade para ajudar com a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="db047-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="db047-236">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="db047-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="db047-237">Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="db047-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
