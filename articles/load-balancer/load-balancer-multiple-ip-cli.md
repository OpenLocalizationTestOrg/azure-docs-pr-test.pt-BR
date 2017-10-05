---
title: "Balanceamento de carga em várias configurações de IP usando a CLI do Azure | Microsoft Docs"
description: "Saiba como atribuir vários endereços IP a uma máquina virtual usando a CLI do Azure | Resource Manager."
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
ms.openlocfilehash: bd15713752ea01ad403d8e3dcfed0c9a7adcc7fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="a795e-103">Balanceamento de carga em várias configurações de IP</span><span class="sxs-lookup"><span data-stu-id="a795e-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a795e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a795e-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="a795e-105">CLI</span><span class="sxs-lookup"><span data-stu-id="a795e-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="a795e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a795e-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="a795e-107">Este artigo descreve como usar o Azure Load Balancer com vários endereços IP em uma interface de rede secundária (NIC).</span><span class="sxs-lookup"><span data-stu-id="a795e-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="a795e-108">Para este cenário, temos duas VMs executando o Windows, cada uma com uma NIC principal e uma secundária.</span><span class="sxs-lookup"><span data-stu-id="a795e-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="a795e-109">Cada uma das NICs secundárias possui duas configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="a795e-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="a795e-110">Cada VM hospeda os sites contoso.com e fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="a795e-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="a795e-111">Cada site está associado a uma das configurações de IP na NIC secundária.</span><span class="sxs-lookup"><span data-stu-id="a795e-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="a795e-112">Usamos o Azure Load Balancer para expor dois endereços IP front-end, um para cada site, a fim de distribuir o tráfego para a respectiva configuração de IP do site.</span><span class="sxs-lookup"><span data-stu-id="a795e-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="a795e-113">Esse cenário usa o mesmo número de porta entre os front-ends, bem como os dois endereços IP do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="a795e-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Imagem de cenário do LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="a795e-115">Etapas para o balanceamento de carga em várias configurações de IP</span><span class="sxs-lookup"><span data-stu-id="a795e-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="a795e-116">Execute as etapas abaixo para obter o cenário descrito neste artigo:</span><span class="sxs-lookup"><span data-stu-id="a795e-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="a795e-117">[Instale e configure a CLI do Azure](../cli-install-nodejs.md) executando as etapas do artigo vinculado e faça logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a795e-117">[Install and Configure the Azure CLI](../cli-install-nodejs.md) the Azure CLI by following the steps in the linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="a795e-118">[Crie um grupo de recursos](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) chamado *contosofabrikam*, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="a795e-118">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="a795e-119">[Criar um conjunto de disponibilidade](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) para as duas VMs.</span><span class="sxs-lookup"><span data-stu-id="a795e-119">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) to for the two VMs.</span></span> <span data-ttu-id="a795e-120">Para esse cenário, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a795e-120">For this scenario, use the following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="a795e-121">[Crie uma rede virtual](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) chamada *myVNet*, e uma sub-rede chamada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a795e-121">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="a795e-122">[Crie o balanceador de carga](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) chamado *mylb*:</span><span class="sxs-lookup"><span data-stu-id="a795e-122">[Create the load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="a795e-123">Crie dois endereços IP públicos e dinâmicos para as configurações de IP de front-end de seu balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="a795e-123">Create two dynamic public IP addresses for the frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="a795e-124">Crie as duas configurações de IP de front-end, *contosofe* e *fabrikamfe*, respectivamente:</span><span class="sxs-lookup"><span data-stu-id="a795e-124">Create the two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="a795e-125">Crie seus pools de endereço back-end - *contosopool* e *fabrikampool*, uma [investigação](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, e suas regras de balanceamento de carga - *HTTPc* e *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="a795e-125">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="a795e-126">Execute o comando a seguir e, em seguida, verifique a saída para [verificar se o seu balanceador de carga](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) foi criado corretamente:</span><span class="sxs-lookup"><span data-stu-id="a795e-126">Run the following command below and then check the output to [verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="a795e-127">[Crie um IP público](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp* e uma [conta de armazenamento](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* para sua primeira máquina virtual VM1, conforme exibido abaixo:</span><span class="sxs-lookup"><span data-stu-id="a795e-127">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="a795e-128">[Crie as interfaces de rede](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) para a VM1 e adicione uma segunda configuração de IP, *VM1-ipconfig2* e [crie a VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) conforme exibido abaixo:</span><span class="sxs-lookup"><span data-stu-id="a795e-128">[Create the network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create the VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="a795e-129">Repita as etapas 10 a 11 para sua segunda VM:</span><span class="sxs-lookup"><span data-stu-id="a795e-129">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="a795e-130">Por fim, você deve configurar os registros de recurso DNS para apontar para o endereço IP do endereço IP front-end do Balanceador de Carga.</span><span class="sxs-lookup"><span data-stu-id="a795e-130">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="a795e-131">Você pode hospedar seus domínios no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="a795e-131">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="a795e-132">Para saber mais sobre como usar o DNS do Azure com o Load Balancer, confira [Usar o DNS do Azure com outros serviços do Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="a795e-132">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a795e-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a795e-133">Next steps</span></span>
- <span data-ttu-id="a795e-134">Saiba mais sobre como combinar os serviços de balanceamento de carga no Azure em [Usando os serviços de balanceamento de carga no Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a795e-134">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="a795e-135">Saiba como é possível usar diferentes tipos de logs no Azure para gerenciar e solucionar problemas do balanceador de carga em [Análise de log para o Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="a795e-135">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
