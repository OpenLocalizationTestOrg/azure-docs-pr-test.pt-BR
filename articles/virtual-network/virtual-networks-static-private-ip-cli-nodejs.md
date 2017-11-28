---
title: "endereços IP privados de aaaConfigure para VMs - 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais usando hello Azure interface de linha de comando (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="ddfeb-103">Configurar endereços IP para uma máquina virtual usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ddfeb-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ddfeb-104">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="ddfeb-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ddfeb-105">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ddfeb-106">[1.0 de CLI do Azure](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="ddfeb-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ddfeb-107">[2.0 do CLI do Azure](virtual-networks-static-private-ip-arm-cli.md) -nosso CLI de última geração para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="ddfeb-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ddfeb-108">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="ddfeb-109">Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ddfeb-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="ddfeb-110">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="ddfeb-111">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ddfeb-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="ddfeb-112">Como toospecify um particular de endereços IP estáticos ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="ddfeb-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="ddfeb-113">toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="ddfeb-114">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ddfeb-115">Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="ddfeb-116">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="ddfeb-117">Executar Olá **public-ip de rede do azure criar** toocreate um IP público para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="ddfeb-118">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="ddfeb-119">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="ddfeb-120">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="ddfeb-121">Nome do IP público do Olá Olá recurso grupo será criado no.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="ddfeb-122">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-122">**-n (or --name)**.</span></span> <span data-ttu-id="ddfeb-123">Nome do IP público hello.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="ddfeb-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-124">**-l (or --location)**.</span></span> <span data-ttu-id="ddfeb-125">Região do Azure onde IP público Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="ddfeb-126">Para o nosso cenário, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="ddfeb-127">Executar Olá **nic de rede do azure criar** comando toocreate uma NIC com um endereço IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="ddfeb-128">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="ddfeb-129">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="ddfeb-130">**- a (ou --private-ip-address)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="ddfeb-131">Endereço IP privado estático para Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="ddfeb-132">**-m (ou --subnet-vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="ddfeb-133">Nome da saudação redes onde Olá NIC será criada.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="ddfeb-134">**-k (ou --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="ddfeb-135">Nome da sub-rede Olá onde Olá NIC será criada.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="ddfeb-136">Executar Olá **criar vm do azure** saudação do comando toocreate VM usando o IP público hello e NIC criado acima.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="ddfeb-137">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="ddfeb-138">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="ddfeb-139">**-y (ou --os-type)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="ddfeb-140">Tipo de operando sistema Olá VM, ou *Windows* ou *Linux*.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="ddfeb-141">**-f (ou --nic-name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="ddfeb-142">Nome da saudação NIC Olá VM usará.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="ddfeb-143">**-i (ou --public-ip-name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="ddfeb-144">Nome da saudação IP pública Olá VM usará.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="ddfeb-145">**-F (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="ddfeb-146">Nome da saudação redes onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="ddfeb-147">**-j (ou --vnet-subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="ddfeb-148">Nome da sub-rede Olá onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="ddfeb-149">Como informações de uma VM de endereço de IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="ddfeb-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="ddfeb-150">tooview Olá IP privado estático informações sobre endereço de saudação VM criada com o script de saudação acima, execute Olá após o comando CLI do Azure e observar os valores de saudação para *método de alocação de IP privado* e *endereço IP privado*:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="ddfeb-151">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="ddfeb-152">Como tooremove um particular de endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="ddfeb-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="ddfeb-153">Você não pode remover um endereço IP privado estático de uma NIC no CLI do Azure para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="ddfeb-154">Você deve criar uma nova NIC que usa um IP dinâmico, remova Olá NIC anterior de saudação VM e depois adicione toohello NIC Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="ddfeb-155">toochange hello NIC para Olá VM usado int eh comandos acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="ddfeb-156">Executar Olá **nic de rede do azure criar** comando toocreate uma nova NIC usando a alocação de IP dinâmico.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="ddfeb-157">Observe como você não precisa toospecify Olá endereço IP neste momento.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="ddfeb-158">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="ddfeb-159">Executar Olá **conjunto de vm do azure** saudação do comando toochange NIC usada por Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="ddfeb-160">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="ddfeb-161">Se quiser, execute Olá **nic de rede do azure excluir** comando toodelete Olá antigo placa de rede.</span><span class="sxs-lookup"><span data-stu-id="ddfeb-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="ddfeb-162">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="ddfeb-163">Como tooadd um endereço IP privado estático endereço tooan existente VM</span><span class="sxs-lookup"><span data-stu-id="ddfeb-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="ddfeb-164">tooadd um toohello de endereço IP de privado estático NIC usada para a máquina virtual criada usando o script de saudação acima, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="ddfeb-165">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ddfeb-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="ddfeb-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ddfeb-166">Next steps</span></span>
* <span data-ttu-id="ddfeb-167">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="ddfeb-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ddfeb-168">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="ddfeb-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ddfeb-169">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddfeb-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

