---
title: "endereços IP privados de aaaConfigure para VMs (clássico) - 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais (clássico) usando hello Azure interface de linha de comando (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="4a4ca-103">Configurar endereços IP para uma máquina virtual (clássica) usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4a4ca-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4a4ca-104">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="4a4ca-105">Você também pode [gerenciar um endereço IP privado estático no modelo de implantação do Gerenciador de recursos de saudação](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a4ca-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="4a4ca-106">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="4a4ca-107">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a4ca-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="4a4ca-108">Como toospecify um particular de endereços IP estáticos ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="4a4ca-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="4a4ca-109">toocreate uma nova VM denominada *DNS01* em um novo serviço de nuvem chamado *TestService* com base no cenário de saudação acima, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="4a4ca-110">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4a4ca-111">Executar Olá **criar serviço do azure** toocreate serviço de nuvem de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="4a4ca-112">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="4a4ca-113">Executar Olá **azure criar vm** saudação do comando toocreate VM.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="4a4ca-114">Observe o valor de saudação para um endereço IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="4a4ca-115">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="4a4ca-116">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="4a4ca-117">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-117">**-l (or --location)**.</span></span> <span data-ttu-id="4a4ca-118">Região do Azure onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="4a4ca-119">Para o nosso cenário, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="4a4ca-120">**-n (ou --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="4a4ca-121">Nome da saudação VM toobe criado.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="4a4ca-122">**-w (ou --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="4a4ca-123">Nome da saudação redes onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="4a4ca-124">**-S (ou --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="4a4ca-125">Endereço IP privado estático para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="4a4ca-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-126">**TestService**.</span></span> <span data-ttu-id="4a4ca-127">Nome do serviço de nuvem Olá onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="4a4ca-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="4a4ca-129">Imagem usada toocreate hello VM.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="4a4ca-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-130">**adminuser**.</span></span> <span data-ttu-id="4a4ca-131">Administrador local para Olá VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="4a4ca-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="4a4ca-133">Senha de administrador local para Olá VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="4a4ca-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="4a4ca-134">Como informações de uma VM de endereço de IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="4a4ca-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="4a4ca-135">tooview Olá IP privado estático informações sobre endereço de saudação VM criada com o script de saudação acima, execute Olá após o comando CLI do Azure e observe o valor Olá *StaticIP rede*:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="4a4ca-136">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="4a4ca-137">Como tooremove um particular de endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="4a4ca-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="4a4ca-138">tooremove Olá endereço IP privado estático adicionados toohello VM script hello acima, Olá execução após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="4a4ca-139">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="4a4ca-140">Como tooadd uma tooan IP privado estático VM existente</span><span class="sxs-lookup"><span data-stu-id="4a4ca-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="4a4ca-141">tooadd um toohello de endereço IP de privado estático VM criada usando o script hello acima runt comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="4a4ca-142">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4a4ca-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="4a4ca-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a4ca-143">Next steps</span></span>
* <span data-ttu-id="4a4ca-144">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4a4ca-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4a4ca-145">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4a4ca-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4a4ca-146">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a4ca-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

