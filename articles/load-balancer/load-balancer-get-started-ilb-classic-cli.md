---
title: "Criar um balanceador de carga interno - CLI do Azure clássica | Microsoft Docs"
description: "Saiba como criar um balanceador de carga interno no modelo de implantação clássico usando a CLI do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="8b322-103">Introdução à criação de um balanceador de carga interno (clássico) usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8b322-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b322-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b322-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="8b322-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8b322-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="8b322-106">Serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="8b322-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="8b322-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8b322-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8b322-108">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="8b322-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="8b322-109">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="8b322-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8b322-110">Saiba como [executar estas etapas usando o modelo do Resource Manager](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b322-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="8b322-111">Para criar um conjunto de balanceadores de carga internos para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8b322-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="8b322-112">Para criar um conjunto de balanceadores de carga internos e os servidores que enviarão o tráfego para ele, é necessário fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8b322-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="8b322-113">Crie uma instância do Balanceamento de Carga Interno que será o ponto de extremidade do tráfego de entrada a ser balanceado nos servidores de um conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="8b322-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="8b322-114">Adicione pontos de extremidade correspondentes às máquinas virtuais que receberão o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b322-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="8b322-115">Configure os servidores que enviarão o tráfego com a carga a ser balanceada para enviar o tráfego para o endereço VIP (IP Virtual) da instância do Balanceamento de Carga Interno.</span><span class="sxs-lookup"><span data-stu-id="8b322-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="8b322-116">Passo a passo da criação de um balanceador de carga interno usando a CLI</span><span class="sxs-lookup"><span data-stu-id="8b322-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="8b322-117">Este guia mostra como criar um balanceador de carga interno com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="8b322-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="8b322-118">Se você nunca usou a CLI do Azure, consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b322-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8b322-119">Execute o comando **azure config mode** para alternar para o modo clássico, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8b322-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="8b322-120">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="8b322-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="8b322-121">Criar ponto de extremidade e conjunto de balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="8b322-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="8b322-122">O cenário pressupõe a existência das máquinas virtuais “DB1” e “DB2” em um serviço de nuvem chamado “mytestcloud”.</span><span class="sxs-lookup"><span data-stu-id="8b322-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="8b322-123">As duas máquinas virtuais estão usando uma rede virtual chamada minha "testvnet" com a sub-rede "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="8b322-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="8b322-124">Este guia criará um conjunto de balanceadores de carga internos usando a porta 1433 como a porta pública e 1433 como a porta local.</span><span class="sxs-lookup"><span data-stu-id="8b322-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="8b322-125">Esse é um cenário comum em que você tem máquinas virtuais do SQL no back-end usando um balanceador de carga interno para garantir que os servidores de banco de dados não sejam expostos diretamente usando um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="8b322-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="8b322-126">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8b322-126">Step 1</span></span>

<span data-ttu-id="8b322-127">Crie um conjunto do balanceador de carga interno usando o `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="8b322-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="8b322-128">Confira `azure service internal-load-balancer --help` para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8b322-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="8b322-129">É possível verificar as propriedades do balanceador de carga interno usando o comando `azure service internal-load-balancer list` *nome do serviço de nuvem*.</span><span class="sxs-lookup"><span data-stu-id="8b322-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="8b322-130">Apresentamos a seguir um exemplo da saída:</span><span class="sxs-lookup"><span data-stu-id="8b322-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="8b322-131">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8b322-131">Step 2</span></span>

<span data-ttu-id="8b322-132">Você configura o conjunto de balanceadores de carga internos quando adicionar o primeiro ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="8b322-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="8b322-133">Você associará o ponto de extremidade, a máquina virtual e a porta de investigação ao conjunto de balanceador de carga interno nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="8b322-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="8b322-134">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="8b322-134">Step 3</span></span>

<span data-ttu-id="8b322-135">Verifique a configuração do balanceador de carga usando o `azure vm show` *nome da máquina virtual*</span><span class="sxs-lookup"><span data-stu-id="8b322-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="8b322-136">A saída será:</span><span class="sxs-lookup"><span data-stu-id="8b322-136">The output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="8b322-137">Criar um ponto de extremidade da área de trabalho remota para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8b322-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="8b322-138">Você pode criar um ponto de extremidade da área de trabalho remota para encaminhar o tráfego de rede de uma porta pública para uma porta local, para uma máquina virtual específica, usando `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="8b322-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="8b322-139">Remover máquina virtual do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8b322-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="8b322-140">É possível remover uma máquina virtual de um conjunto de balanceadores de carga internos excluindo o ponto de extremidade associado.</span><span class="sxs-lookup"><span data-stu-id="8b322-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="8b322-141">Depois que o ponto de extremidade for removido, a máquina virtual não pertencerá mais ao conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="8b322-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="8b322-142">Usando o exemplo acima, você pode remover o ponto de extremidade criado para a máquina virtual “DB1” do balanceador de carga interno usando o comando “lbset” `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="8b322-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="8b322-143">Confira `azure vm endpoint --help` para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8b322-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b322-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b322-144">Next steps</span></span>

[<span data-ttu-id="8b322-145">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="8b322-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8b322-146">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8b322-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
