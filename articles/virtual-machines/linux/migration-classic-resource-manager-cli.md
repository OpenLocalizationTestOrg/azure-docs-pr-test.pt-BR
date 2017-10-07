---
title: aaaMigrate VMs tooResource Manager usando a CLI do Azure | Microsoft Docs
description: "Este artigo o orienta por meio da migração de suporte de plataforma de saudação de recursos de tooAzure clássico Gerenciador de recursos usando a CLI do Azure"
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
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="b91dd-103">Migrar recursos de IaaS de tooAzure clássico Gerenciador de recursos usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b91dd-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="b91dd-104">Estas etapas mostram como toouse interface de linha de comando (CLI) do Azure comandos toomigrate infraestrutura como um recurso de serviço (IaaS) do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91dd-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b91dd-105">artigo Olá requer Olá [CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b91dd-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b91dd-106">Todas as operações de saudação descritas aqui são idempotentes.</span><span class="sxs-lookup"><span data-stu-id="b91dd-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="b91dd-107">Se você tiver um problema que não seja um recurso sem suporte ou um erro de configuração, é recomendável que você repita Olá preparar, anular ou confirmar a operação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="b91dd-108">plataforma de saudação tente novamente a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="b91dd-109">Aqui está uma ordem de saudação do fluxograma tooidentify nos quais etapas precisam toobe executado durante o processo de migração</span><span class="sxs-lookup"><span data-stu-id="b91dd-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Captura de tela que mostra as etapas de migração de saudação](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="b91dd-111">Etapa 1: preparar para a migração</span><span class="sxs-lookup"><span data-stu-id="b91dd-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="b91dd-112">Aqui estão algumas práticas recomendadas que recomendamos durante a avaliação de migração de recursos de IaaS do clássico tooResource Manager:</span><span class="sxs-lookup"><span data-stu-id="b91dd-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="b91dd-113">Leia Olá [lista de configurações sem suporte ou recursos](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b91dd-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="b91dd-114">Se você tiver máquinas virtuais que usam recursos ou configurações sem suporte, é recomendável que você aguarde toobe de suporte de configuração do recurso Olá anunciada.</span><span class="sxs-lookup"><span data-stu-id="b91dd-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="b91dd-115">Como alternativa, você pode remover esse recurso ou sai migração configuração tooenable se ele atende às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="b91dd-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="b91dd-116">Se você tiver automatizado scripts que implantar a infraestrutura e os aplicativos de hoje, tente toocreate uma configuração de teste semelhante usando esses scripts para a migração.</span><span class="sxs-lookup"><span data-stu-id="b91dd-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="b91dd-117">Como alternativa, você pode configurar ambientes de exemplo usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91dd-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b91dd-118">Os Gateways de aplicativos não têm suporte atualmente para a migração de clássico tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="b91dd-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="b91dd-119">toomigrate uma rede virtual clássica com um gateway de aplicativo, remova gateway Olá antes de executar uma rede Olá de toomove de operação de preparação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="b91dd-120">Depois de concluir a migração de hello, reconecte gateway Olá no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91dd-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="b91dd-121">Gateways de rota expressa conectando tooExpressRoute circuitos em outra assinatura não podem ser migrados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b91dd-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="b91dd-122">Nesses casos, remover o gateway de rota expressa hello, migrar a rede virtual hello e recrie o gateway hello.</span><span class="sxs-lookup"><span data-stu-id="b91dd-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="b91dd-123">Consulte [ExpressRoute migrar circuitos e associadas a redes virtuais do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../../expressroute/expressroute-migration-classic-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b91dd-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="b91dd-124">Etapa 2: Definir sua assinatura e registrar o provedor de saudação</span><span class="sxs-lookup"><span data-stu-id="b91dd-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="b91dd-125">Para cenários de migração, você precisa tooset seu ambiente para ambos os clássico e o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b91dd-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="b91dd-126">[Instale a CLI do Azure](../../cli-install-nodejs.md) e [selecione sua assinatura](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b91dd-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="b91dd-127">Conta de logon tooyour.</span><span class="sxs-lookup"><span data-stu-id="b91dd-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="b91dd-128">Selecione Olá assinatura do Azure usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="b91dd-129">O registro é uma hora de uma etapa mas precisa toobe feito uma vez antes de tentar a migração.</span><span class="sxs-lookup"><span data-stu-id="b91dd-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="b91dd-130">Sem registrar, você verá Olá a seguinte mensagem de erro</span><span class="sxs-lookup"><span data-stu-id="b91dd-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="b91dd-131">*BadRequest: a assinatura não está registrada para migração.*</span><span class="sxs-lookup"><span data-stu-id="b91dd-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="b91dd-132">Registrar com o provedor de recursos de migração de saudação usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="b91dd-133">Observe que, em alguns casos, esse comando atinge o tempo limite. No entanto, o registro de saudação será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="b91dd-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="b91dd-134">Aguarde cinco minutos para Olá toofinish de registro.</span><span class="sxs-lookup"><span data-stu-id="b91dd-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="b91dd-135">Você pode verificar o status de saudação de aprovação de saudação usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="b91dd-136">Verifique se RegistrationState é `Registered` antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="b91dd-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="b91dd-137">Agora, alterne CLI toohello `asm` modo.</span><span class="sxs-lookup"><span data-stu-id="b91dd-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="b91dd-138">Etapa 3: Verifique se que você tem suficiente núcleos de máquina Virtual do Azure Resource Manager no hello região do Azure de sua implantação atual ou a rede virtual</span><span class="sxs-lookup"><span data-stu-id="b91dd-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="b91dd-139">Para esta etapa será necessário tooswitch muito`arm` modo.</span><span class="sxs-lookup"><span data-stu-id="b91dd-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="b91dd-140">Fazer isso com o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="b91dd-141">Você pode usar o hello CLI comando toocheck Olá quantidade atual de núcleos que você tem no Gerenciador de recursos do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="b91dd-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="b91dd-142">toolearn mais sobre cotas de core, consulte [limites e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="b91dd-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="b91dd-143">Quando terminar de verificar se esta etapa, você pode alternar de volta muito`asm` modo.</span><span class="sxs-lookup"><span data-stu-id="b91dd-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="b91dd-144">Etapa 4: Opção 1 – Migrar máquinas virtuais em um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="b91dd-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="b91dd-145">Obter uma lista de serviços de nuvem usando o comando a seguir de saudação e, em seguida, escolha Olá serviço em nuvem que você deseja toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="b91dd-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="b91dd-146">Observe que se Olá VMs no serviço de nuvem Olá está em uma rede virtual ou se eles têm funções web/de trabalho, você receberá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="b91dd-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="b91dd-147">Olá execução após o nome da implantação do comando tooget Olá Olá serviço de nuvem de saída detalhada hello.</span><span class="sxs-lookup"><span data-stu-id="b91dd-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="b91dd-148">Na maioria dos casos, nome da implantação Olá é Olá igual ao nome do serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b91dd-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="b91dd-149">Primeiro, valide se você pode migrar o serviço de nuvem hello usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b91dd-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="b91dd-150">Prepare Olá VMs no serviço de nuvem Olá para migração.</span><span class="sxs-lookup"><span data-stu-id="b91dd-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="b91dd-151">Você tem dois toochoose de opções do.</span><span class="sxs-lookup"><span data-stu-id="b91dd-151">You have two options toochoose from.</span></span>

<span data-ttu-id="b91dd-152">Se você quiser toomigrate Olá VMs tooa criado plataforma rede virtual, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b91dd-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="b91dd-153">Se você quiser tooan toomigrate existentes de rede virtual no modelo de implantação do Gerenciador de recursos de hello, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b91dd-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="b91dd-154">Depois de preparar Olá operação for bem-sucedida, você pode examinar o estado de migração de Olá Olá saída detalhada tooget de saudação VMs e certifique-se de que eles estejam em Olá `Prepared` estado.</span><span class="sxs-lookup"><span data-stu-id="b91dd-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="b91dd-155">Verifique a configuração de saudação para Olá preparado recursos usando a CLI ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91dd-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="b91dd-156">Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b91dd-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="b91dd-157">Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="b91dd-158">Etapa 4: Opção 2 – Migrar máquinas virtuais em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="b91dd-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="b91dd-159">Escolha Olá rede virtual que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="b91dd-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="b91dd-160">Observe que, se a rede virtual Olá contém funções web/de trabalho ou máquinas virtuais com configurações sem suporte, você obterá uma mensagem de erro de validação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="b91dd-161">Obter todas as redes virtuais de saudação na assinatura de saudação usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="b91dd-162">saída de Hello será parecida com isto:</span><span class="sxs-lookup"><span data-stu-id="b91dd-162">hello output will look something like this:</span></span>

![Captura de tela hello da linha de comando com o nome de toda a rede virtual Olá realçado.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="b91dd-164">Em Olá exemplo acima, Olá **virtualNetworkName** é o nome completo da saudação **"Grupo classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="b91dd-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="b91dd-165">Primeiro, valide se migrar Olá rede virtual usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b91dd-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="b91dd-166">Prepare a rede virtual Olá de sua escolha para a migração usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="b91dd-167">Verifique a configuração de saudação para Olá preparado máquinas virtuais usando a CLI ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91dd-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="b91dd-168">Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b91dd-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="b91dd-169">Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="b91dd-170">Etapa 5: Migrar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b91dd-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="b91dd-171">Quando terminar de migração de máquinas virtuais Olá, é recomendável que migrar a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="b91dd-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="b91dd-172">Preparar a conta de armazenamento Olá para a migração usando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="b91dd-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="b91dd-173">Verifique a configuração de saudação para Olá preparado conta de armazenamento usando a CLI ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b91dd-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="b91dd-174">Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b91dd-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="b91dd-175">Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b91dd-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="b91dd-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b91dd-176">Next steps</span></span>

* [<span data-ttu-id="b91dd-177">Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b91dd-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b91dd-178">Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b91dd-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b91dd-179">Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b91dd-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b91dd-180">Usar recursos de IaaS PowerShell toomigrate de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b91dd-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b91dd-181">Ferramentas de comunidade para ajudar com a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b91dd-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b91dd-182">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="b91dd-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b91dd-183">Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b91dd-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
