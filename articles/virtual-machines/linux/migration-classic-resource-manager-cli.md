---
title: Migrar VMs para o Resource Manager usando a CLI do Azure | Microsoft Docs
description: "Este artigo apresenta a migração de recursos com suporte da plataforma do modelo clássico para o Azure Resource Manager usando a CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="7288d-103">Migrar recursos de IaaS do modelo clássico para o Azure Resource Manager usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7288d-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="7288d-104">Estas etapas mostram como usar a CLI (interface de linha de comando) do Azure para migrar recursos de IaaS (infraestrutura como serviço) do modelo de implantação clássico para o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7288d-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7288d-105">O artigo exige a [CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7288d-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7288d-106">Todas as operações descritas aqui são idempotentes.</span><span class="sxs-lookup"><span data-stu-id="7288d-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="7288d-107">Caso você tenha algum problema que não seja um recurso sem suporte ou um erro de configuração, recomendamos que repita a operação de preparação, anulação ou confirmação.</span><span class="sxs-lookup"><span data-stu-id="7288d-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="7288d-108">Em seguida, a plataforma repetirá a ação.</span><span class="sxs-lookup"><span data-stu-id="7288d-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="7288d-109">Este é um fluxograma para identificar a ordem em que as etapas precisam ser executadas durante um processo de migração</span><span class="sxs-lookup"><span data-stu-id="7288d-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="7288d-111">Etapa 1: preparar para a migração</span><span class="sxs-lookup"><span data-stu-id="7288d-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="7288d-112">Veja a seguir algumas das práticas que recomendamos durante a avaliação de migração dos recursos de IaaS do modelo clássico para o Gerenciador de Recursos:</span><span class="sxs-lookup"><span data-stu-id="7288d-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="7288d-113">Leia a [lista de recursos ou de configurações sem suporte](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7288d-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="7288d-114">Caso você tenha máquinas virtuais que usam recursos ou configurações sem suporte, recomendamos que aguarde até que o suporte para o recurso/configuração seja anunciado.</span><span class="sxs-lookup"><span data-stu-id="7288d-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="7288d-115">Como alternativa, é possível remover esse recurso ou mudar a configuração para habilitar a migração, caso ela atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="7288d-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="7288d-116">Se você tiver scripts automatizados que implantam sua infraestrutura e aplicativos atualmente, tente criar uma configuração de teste semelhante usando esses scripts para migração.</span><span class="sxs-lookup"><span data-stu-id="7288d-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="7288d-117">Você também pode configurar ambientes de exemplo usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7288d-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7288d-118">Atualmente não ha suporte para Gateways de Aplicativo para a migração do clássico para o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7288d-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="7288d-119">Para migrar uma rede virtual clássica com um Gateway de Aplicativo, remova o gateway antes de executar uma operação de Preparação para mover a rede.</span><span class="sxs-lookup"><span data-stu-id="7288d-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="7288d-120">Depois de concluir a migração, reconecte o gateway no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7288d-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="7288d-121">Não é possível migrar automaticamente gateways de ExpressRoute conectando-se a circuitos de ExpressRoute em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="7288d-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="7288d-122">Nesses casos, remova o gateway de ExpressRoute, migre a rede virtual e recrie o gateway.</span><span class="sxs-lookup"><span data-stu-id="7288d-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="7288d-123">Confira [Migrar circuitos de ExpressRoute e redes virtuais associadas do modelo de implantação clássico para o Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="7288d-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="7288d-124">Etapa 2: Definir sua assinatura e registrar o provedor</span><span class="sxs-lookup"><span data-stu-id="7288d-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="7288d-125">Para cenários de migração, é necessário instalar seu ambiente tanto para o modelo clássico quanto para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="7288d-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="7288d-126">[Instale a CLI do Azure](../../cli-install-nodejs.md) e [selecione sua assinatura](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7288d-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="7288d-127">Entre em sua conta.</span><span class="sxs-lookup"><span data-stu-id="7288d-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="7288d-128">Selecione a assinatura do Azure usando o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="7288d-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="7288d-129">O registro é uma etapa única, mas é preciso executá-lo uma vez antes de tentar a migração.</span><span class="sxs-lookup"><span data-stu-id="7288d-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="7288d-130">Sem o registro, você verá a seguinte mensagem de erro</span><span class="sxs-lookup"><span data-stu-id="7288d-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="7288d-131">*BadRequest: a assinatura não está registrada para migração.*</span><span class="sxs-lookup"><span data-stu-id="7288d-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="7288d-132">Registre-se no provedor de recursos de migração usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="7288d-133">Observe que, em alguns casos, esse comando atinge o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="7288d-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="7288d-134">No entanto, o registro será bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="7288d-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="7288d-135">Aguarde cinco minutos para concluir o registro.</span><span class="sxs-lookup"><span data-stu-id="7288d-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="7288d-136">É possível verificar o status da aprovação usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="7288d-137">Verifique se RegistrationState é `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="7288d-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="7288d-138">Agora mude a CLI para o modo `asm` .</span><span class="sxs-lookup"><span data-stu-id="7288d-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="7288d-139">Etapa 3: Verifique se você tem uma quantidade suficiente de núcleos de Máquina Virtual do Azure Resource Manager na região do Azure de sua implantação atual ou VNET</span><span class="sxs-lookup"><span data-stu-id="7288d-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="7288d-140">Nesta etapa, você precisará alternar para o modo `arm` .</span><span class="sxs-lookup"><span data-stu-id="7288d-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="7288d-141">Faça isso com o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="7288d-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="7288d-142">Você pode usar o seguinte comando da CLI para verificar a quantidade atual de núcleos no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7288d-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="7288d-143">Para saber mais sobre cotas de núcleos, veja [Limites e o Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="7288d-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="7288d-144">Quando você terminar de verificar esta etapa, volte para o modo `asm` .</span><span class="sxs-lookup"><span data-stu-id="7288d-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="7288d-145">Etapa 4: Opção 1 – Migrar máquinas virtuais em um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="7288d-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="7288d-146">Obtenha a lista de serviços de nuvem usando o comando a seguir e escolha o serviço de nuvem que deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="7288d-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="7288d-147">Observe que, se as VMs no serviço de nuvem estiverem em uma rede virtual ou se tiverem funções web/de trabalho, você receberá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="7288d-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="7288d-148">Execute a comando a seguir para obter o nome da implantação do serviço de nuvem por meio da saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="7288d-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="7288d-149">Na maioria dos casos, o nome da implantação é igual ao nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7288d-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="7288d-150">Primeiro, valide se você pode migrar o serviço de nuvem usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7288d-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="7288d-151">Prepare as máquinas virtuais no serviço de nuvem para migração.</span><span class="sxs-lookup"><span data-stu-id="7288d-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="7288d-152">Você tem duas opções entre as quais escolher.</span><span class="sxs-lookup"><span data-stu-id="7288d-152">You have two options to choose from.</span></span>

<span data-ttu-id="7288d-153">Se quiser migrar as máquinas virtuais em uma rede virtual criada por plataforma, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="7288d-154">Se quiser migrar para uma rede virtual existente no modelo de implantação do Gerenciador de Recursos, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="7288d-155">Após uma operação de preparação bem-sucedida, você poderá examinar a saída detalhada para obter o estado de migração das VMs e assegurar que as elas estejam no estado `Prepared` .</span><span class="sxs-lookup"><span data-stu-id="7288d-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="7288d-156">Verifique a configuração dos recursos preparados usando a CLI ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7288d-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="7288d-157">Se você não estiver pronto para a migração e desejar voltar para o estado anterior, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="7288d-158">Se a configuração preparada estiver correta, será possível continuar e confirmar os recursos usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="7288d-159">Etapa 4: Opção 2 – Migrar máquinas virtuais em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="7288d-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="7288d-160">Selecione a rede virtual que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="7288d-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="7288d-161">Observe que, se a rede virtual contiver funções web/de trabalho ou VMs com configurações sem suporte, você receberá uma mensagem de erro de validação.</span><span class="sxs-lookup"><span data-stu-id="7288d-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="7288d-162">Obtenha todas as redes virtuais na assinatura usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="7288d-163">A saída será parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="7288d-163">The output will look something like this:</span></span>

![Captura de tela da linha de comando com o nome inteiro da rede virtual realçado.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="7288d-165">No exemplo acima, **virtualNetworkName** é o nome inteiro **“Grupo classicubuntu16 classicubuntu16”**.</span><span class="sxs-lookup"><span data-stu-id="7288d-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="7288d-166">Primeiro, valide se você pode migrar a rede virtual usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7288d-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="7288d-167">Prepare a rede virtual de sua preferência para migração usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="7288d-168">Verifique a configuração para as máquinas virtuais preparadas usando a CLI ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7288d-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="7288d-169">Se você não estiver pronto para a migração e desejar voltar para o estado anterior, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="7288d-170">Se a configuração preparada estiver correta, será possível continuar e confirmar os recursos usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="7288d-171">Etapa 5: Migrar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7288d-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="7288d-172">Depois de concluir a migração das máquinas virtuais, recomendamos a migração da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7288d-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="7288d-173">Prepare a conta de armazenamento para migração usando o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="7288d-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="7288d-174">Verifique a configuração da conta de armazenamento preparada usando a CLI ou o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7288d-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="7288d-175">Se você não estiver pronto para a migração e desejar voltar para o estado anterior, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="7288d-176">Se a configuração preparada estiver correta, será possível continuar e confirmar os recursos usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7288d-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="7288d-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7288d-177">Next steps</span></span>

* [<span data-ttu-id="7288d-178">Visão geral da migração de recursos de IaaS com suporte da plataforma do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7288d-178">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7288d-179">Análise técnica aprofundada sobre a migração com suporte da plataforma do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7288d-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7288d-180">Planejamento para a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7288d-180">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7288d-181">Usar o PowerShell para migrar recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7288d-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7288d-182">Ferramentas da comunidade para ajudar com a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7288d-182">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7288d-183">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="7288d-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7288d-184">Confira as perguntas mais frequentes sobre a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7288d-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
