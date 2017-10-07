---
title: "aaaLoad balanceamento em várias configurações de IP usando a CLI do Azure | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa máquina de virtual usando a CLI do Azure | Gerenciador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="5961d-103">Balanceamento de carga em várias configurações de IP</span><span class="sxs-lookup"><span data-stu-id="5961d-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5961d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5961d-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="5961d-105">CLI</span><span class="sxs-lookup"><span data-stu-id="5961d-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="5961d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5961d-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="5961d-107">Este artigo descreve como toouse balanceador de carga do Azure com o IP de vários endereços em uma interface de rede secundária (NIC).</span><span class="sxs-lookup"><span data-stu-id="5961d-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="5961d-108">Para este cenário, temos duas VMs executando o Windows, cada uma com uma NIC principal e uma secundária.</span><span class="sxs-lookup"><span data-stu-id="5961d-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="5961d-109">Cada um dos secundários de saudação NICs têm duas configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="5961d-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="5961d-110">Cada VM hospeda os sites contoso.com e fabrikam.com. Cada site é associado tooone Olá de configurações de IP em uma NIC secundário. Olá</span><span class="sxs-lookup"><span data-stu-id="5961d-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="5961d-111">Usamos o balanceador de carga do Azure tooexpose dois front-end endereços IP, uma para cada site, toodistribute tráfego toohello respectiva configuração de IP para o site de saudação.</span><span class="sxs-lookup"><span data-stu-id="5961d-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="5961d-112">Esse cenário usa Olá o mesmo número de porta entre os front-ends, bem como os dois endereços IP do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="5961d-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Imagem de cenário do LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="5961d-114">Saldo de tooload etapas em várias configurações de IP</span><span class="sxs-lookup"><span data-stu-id="5961d-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="5961d-115">Siga as próximas etapas, Olá cenário de saudação tooachieve descritos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="5961d-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="5961d-116">[Instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) Olá CLI do Azure, seguindo as etapas de saudação no artigo vinculado hello e log em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5961d-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="5961d-117">[Crie um grupo de recursos](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) chamado *contosofabrikam*, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="5961d-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="5961d-118">[Criar um conjunto de disponibilidade](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor Olá duas VMs.</span><span class="sxs-lookup"><span data-stu-id="5961d-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="5961d-119">Para este cenário, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5961d-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="5961d-120">[Crie uma rede virtual](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) chamada *myVNet*, e uma sub-rede chamada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="5961d-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="5961d-121">[Criar o balanceador de carga Olá](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) chamado *mylb*:</span><span class="sxs-lookup"><span data-stu-id="5961d-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="5961d-122">Crie dois endereços do IP de públicos dinâmicos para as configurações de IP de front-end de saudação do balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="5961d-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="5961d-123">Criar front-end Olá duas configurações de IP, *contosofe* e *fabrikamfe* respectivamente:</span><span class="sxs-lookup"><span data-stu-id="5961d-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="5961d-124">Crie seus pools de endereço back-end - *contosopool* e *fabrikampool*, uma [investigação](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, e suas regras de balanceamento de carga - *HTTPc* e *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="5961d-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="5961d-125">Seguinte Olá executar comando abaixo e verifique a saída de hello muito[verificar seu balanceador de carga](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) foi criado corretamente:</span><span class="sxs-lookup"><span data-stu-id="5961d-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="5961d-126">[Crie um IP público](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp* e uma [conta de armazenamento](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* para sua primeira máquina virtual VM1, conforme exibido abaixo:</span><span class="sxs-lookup"><span data-stu-id="5961d-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="5961d-127">[Criar hello interfaces de rede](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) para VM1 e adicionar uma segunda configuração IP, *VM1 ipconfig2*, e [criar hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5961d-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="5961d-128">Repita as etapas 10 a 11 para sua segunda VM:</span><span class="sxs-lookup"><span data-stu-id="5961d-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="5961d-129">Por fim, você deve configurar o recurso registros toopoint toohello front-end respectivo endereço IP de DNS Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5961d-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="5961d-130">Você pode hospedar seus domínios no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="5961d-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="5961d-131">Para saber mais sobre como usar o DNS do Azure com o Load Balancer, confira [Usar o DNS do Azure com outros serviços do Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="5961d-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5961d-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5961d-132">Next steps</span></span>
- <span data-ttu-id="5961d-133">Saiba mais sobre como o balanceamento de carga de toocombine serviços no Azure em [usando os serviços de balanceamento de carga no Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5961d-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="5961d-134">Saiba como você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas de Balanceador de carga no [de análise de Log para o balanceador de carga do Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="5961d-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
