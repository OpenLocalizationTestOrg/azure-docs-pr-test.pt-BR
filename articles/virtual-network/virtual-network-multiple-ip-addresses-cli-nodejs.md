---
title: "aaaVM com vários endereços IP usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa máquina virtual usando Olá 1.0 da CLI do Azure | Gerenciador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="2154c-103">Atribuir vários endereços IP toovirtual máquinas usando 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2154c-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="2154c-104">Este artigo explica como toocreate uma máquina virtual (VM) por meio de saudação do Azure Resource Manager implantação do modelo usando Olá 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2154c-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="2154c-105">Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="2154c-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="2154c-106">toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2154c-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="2154c-107"><a name = "create"></a>Criar uma VM com vários endereços IP</span><span class="sxs-lookup"><span data-stu-id="2154c-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="2154c-108">Você pode concluir essa tarefa usando Olá CLI do Azure 1.0 (Este artigo) ou hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2154c-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="2154c-109">etapas Olá que seguem explicam como toocreate um exemplo VM com IP vários endereços, conforme descrito no cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="2154c-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="2154c-110">Altere os nomes da variável e os tipos de endereço IP como exigido por sua implementação.</span><span class="sxs-lookup"><span data-stu-id="2154c-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="2154c-111">Instalar e configurar hello Azure CLI 1.0 por Olá seguir as etapas em Olá [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo e faça logon em sua conta do Azure com hello `azure-login` comando.</span><span class="sxs-lookup"><span data-stu-id="2154c-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="2154c-112">Crie um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2154c-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="2154c-113">Criar uma rede virtual:</span><span class="sxs-lookup"><span data-stu-id="2154c-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="2154c-114">Crie uma sub-rede na rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="2154c-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="2154c-115">Crie uma conta de armazenamento para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2154c-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="2154c-116">Antes de executar Olá após o comando, substitua *mystorageaccount* com um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="2154c-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="2154c-117">nome da saudação deve ser exclusivo no Azure:</span><span class="sxs-lookup"><span data-stu-id="2154c-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="2154c-118">Criar hello configurações de IP de uma NIC e atribuir Olá IP configurações toohello NIC em.</span><span class="sxs-lookup"><span data-stu-id="2154c-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="2154c-119">Você pode adicionar, remover ou alterar as configurações de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="2154c-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="2154c-120">Olá configurações a seguir é descrita no cenário de saudação:</span><span class="sxs-lookup"><span data-stu-id="2154c-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="2154c-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="2154c-121">**IPConfig-1**</span></span>

    <span data-ttu-id="2154c-122">Digite os comandos de saudação que seguem toocreate:</span><span class="sxs-lookup"><span data-stu-id="2154c-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="2154c-123">Um recurso de endereço IP público com um endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="2154c-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="2154c-124">Uma NIC, atribuição de endereço IP público de saudação e um tooit de endereço IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="2154c-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="2154c-125">Substituir *mypublicdns* com um nome que seja exclusivo dentro de saudação local do Azure.</span><span class="sxs-lookup"><span data-stu-id="2154c-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="2154c-126">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="2154c-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="2154c-127">toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="2154c-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="2154c-128">Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="2154c-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="2154c-129">mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="2154c-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="2154c-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="2154c-130">**IPConfig-2**</span></span>

     <span data-ttu-id="2154c-131">Um novo recurso de endereço IP público e uma nova configuração de IP com um endereço IP público estático e um endereço IP privado estático, digite Olá toocreate comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="2154c-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="2154c-132">**IPConfig-3**</span></span>

    <span data-ttu-id="2154c-133">Digite hello comandos toocreate uma configuração de IP com um endereço IP privado estático e nenhum endereço IP público a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="2154c-134">Embora este artigo atribui todos os tooa de configurações de IP NIC único, você também pode atribuir várias tooany de configurações de IP NIC em uma VM.</span><span class="sxs-lookup"><span data-stu-id="2154c-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="2154c-135">toolearn como ler de uma VM com várias NICs, toocreate Olá criar uma VM com o artigo de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="2154c-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="2154c-136">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="2154c-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="2154c-137">toochange Olá VM tamanho tooStandard DS2 v2, por exemplo, basta adicionar Olá propriedade a seguir `--vm-size Standard_DS3_v2` toohello `azure vm create` comando na etapa 6.</span><span class="sxs-lookup"><span data-stu-id="2154c-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="2154c-138">Insira Olá Olá do comando tooview NIC a seguir e Olá as configurações de IP associadas:</span><span class="sxs-lookup"><span data-stu-id="2154c-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="2154c-139">IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2154c-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="2154c-140"><a name="add"></a>Adicionar endereços IP tooa VM</span><span class="sxs-lookup"><span data-stu-id="2154c-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="2154c-141">Você pode adicionar adicionais pública e privada IP endereços tooan existente NIC completando as etapas de saudação que seguem.</span><span class="sxs-lookup"><span data-stu-id="2154c-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="2154c-142">exemplos de saudação incrementar Olá [cenário](#Scenario) descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2154c-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="2154c-143">Abra a CLI do Azure e completa hello restantes etapas nesta seção dentro de uma única sessão CLI.</span><span class="sxs-lookup"><span data-stu-id="2154c-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="2154c-144">Se você ainda não tiver a CLI do Azure instalado e configurado, Olá concluir etapas no hello [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo e faça logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2154c-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="2154c-145">Conclua as etapas de saudação em uma das seguintes seções, com base nas necessidades de saudação:</span><span class="sxs-lookup"><span data-stu-id="2154c-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="2154c-146">**Adicionar um endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="2154c-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="2154c-147">tooadd um tooa de endereço IP privado NIC, você deve criar uma configuração de IP usando o comando de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="2154c-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="2154c-148">endereço estático Olá deve ser um endereço não usado para a sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="2154c-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="2154c-149">Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).</span><span class="sxs-lookup"><span data-stu-id="2154c-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="2154c-150">**Adicionar um endereço IP público**</span><span class="sxs-lookup"><span data-stu-id="2154c-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="2154c-151">Um endereço IP público é adicionado ao associá-la tooeither uma nova configuração de IP ou uma configuração de IP existente.</span><span class="sxs-lookup"><span data-stu-id="2154c-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="2154c-152">Conclua as etapas de saudação em uma saudação próximas seções, você precisa.</span><span class="sxs-lookup"><span data-stu-id="2154c-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="2154c-153">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="2154c-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="2154c-154">toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="2154c-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="2154c-155">Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="2154c-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="2154c-156">mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="2154c-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="2154c-157">**Associar Olá recurso tooa nova configuração de IP**</span><span class="sxs-lookup"><span data-stu-id="2154c-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="2154c-158">Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="2154c-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="2154c-159">Você pode adicionar um recurso de endereço IP público existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="2154c-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="2154c-160">toocreate uma nova, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="2154c-161">toocreate uma nova configuração de IP com um endereço IP privado estático e Olá associados *myPublicIP3* IP público recurso de endereço, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="2154c-162">**Associar a configuração de IP existente do hello recursos tooan**</span><span class="sxs-lookup"><span data-stu-id="2154c-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="2154c-163">Um recurso de endereço IP público só pode ser a configuração de IP tooan associado que ainda não tiver um associado.</span><span class="sxs-lookup"><span data-stu-id="2154c-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="2154c-164">Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="2154c-165">Procure um toohello semelhante de linha que segue para 3 IPConfig no hello retornado de saída:</span><span class="sxs-lookup"><span data-stu-id="2154c-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="2154c-166">Desde Olá **IP público** coluna para *IpConfig 3* está em branco, nenhum recurso de endereço IP público é tooit atualmente associado.</span><span class="sxs-lookup"><span data-stu-id="2154c-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="2154c-167">Você pode adicionar um existente pública IP endereço recurso tooIpConfig-3, ou insira Olá toocreate comando um a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="2154c-168">Digite hello recurso toohello existente IP configuração denominada do endereço IP público do tooassociate Olá de comando a seguir *3 IPConfig*:</span><span class="sxs-lookup"><span data-stu-id="2154c-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="2154c-169">Exibir endereços IP privados de saudação e Olá pública IP endereço recursos atribuído toohello NIC inserindo Olá o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2154c-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="2154c-170">Olá retornado é de saída a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="2154c-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="2154c-171">Adicionar endereços IP privados Olá adicionado o sistema operacional do toohello NIC toohello VM seguindo instruções Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2154c-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="2154c-172">Não adicione Olá pública IP endereços toohello sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="2154c-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
