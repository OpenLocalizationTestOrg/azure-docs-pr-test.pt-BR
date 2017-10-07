---
title: "aaaCreate um interno carregar balanceador - clássico de CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga interno usando Olá CLI do Azure no modelo de implantação clássico Olá"
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
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="058d3-103">Introdução à criação de um balanceador de carga interno (clássico) usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="058d3-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="058d3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="058d3-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="058d3-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="058d3-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="058d3-106">Serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="058d3-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="058d3-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="058d3-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="058d3-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="058d3-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="058d3-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="058d3-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="058d3-110">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="058d3-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="058d3-111">toocreate um balanceador de carga interno definido para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="058d3-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="058d3-112">toocreate um balanceador de carga interno definido e Olá servidores que enviarão sua tooit de tráfego, você deve fazer a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="058d3-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="058d3-113">Crie uma instância de interno balanceamento de carga que será o ponto de extremidade de saudação da entrada tráfego toobe o balanceamento de carga servidores Olá de um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="058d3-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="058d3-114">Adicione pontos de extremidade correspondente máquinas virtuais toohello que irá receber tráfego de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="058d3-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="058d3-115">Configure servidores de saudação que enviará Olá tráfego toobe com balanceamento de carga toosend seu tráfego toohello endereço IP virtual (VIP) da instância de balanceamento de carga interno de saudação.</span><span class="sxs-lookup"><span data-stu-id="058d3-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="058d3-116">Passo a passo da criação de um balanceador de carga interno usando a CLI</span><span class="sxs-lookup"><span data-stu-id="058d3-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="058d3-117">Este guia mostra como toocreate um balanceador de carga interno com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="058d3-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="058d3-118">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="058d3-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="058d3-119">Executar Olá **modo de configuração do azure** tooswitch tooclassic modo de comando, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="058d3-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="058d3-120">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="058d3-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="058d3-121">Criar ponto de extremidade e conjunto de balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="058d3-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="058d3-122">cenário de saudação pressupõe Olá máquinas de virtuais "DB1" e "DB2" em um serviço de nuvem chamado "mytestcloud".</span><span class="sxs-lookup"><span data-stu-id="058d3-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="058d3-123">As duas máquinas virtuais estão usando uma rede virtual chamada minha "testvnet" com a sub-rede "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="058d3-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="058d3-124">Este guia criará um conjunto de balanceadores de carga internos usando a porta 1433 como a porta pública e 1433 como a porta local.</span><span class="sxs-lookup"><span data-stu-id="058d3-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="058d3-125">Este é um cenário comum em que máquinas virtuais SQL Olá o back-end usando que um servidores de banco de dados de carga interno balanceador tooguarantee Olá não seja exposto diretamente usando um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="058d3-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="058d3-126">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="058d3-126">Step 1</span></span>

<span data-ttu-id="058d3-127">Crie um conjunto do balanceador de carga interno usando o `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="058d3-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="058d3-128">Confira `azure service internal-load-balancer --help` para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="058d3-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="058d3-129">Você pode verificar as propriedades do balanceador de carga interno de saudação usando o comando Olá `azure service internal-load-balancer list` *nome do serviço de nuvem*.</span><span class="sxs-lookup"><span data-stu-id="058d3-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="058d3-130">A seguir, um exemplo de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="058d3-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="058d3-131">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="058d3-131">Step 2</span></span>

<span data-ttu-id="058d3-132">Configure o balanceador de carga interno Olá definida quando você adicionar o primeiro ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="058d3-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="058d3-133">Você associará Olá ponto de extremidade, a máquina virtual e a investigação porta toohello balanceador de carga interno definido nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="058d3-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="058d3-134">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="058d3-134">Step 3</span></span>

<span data-ttu-id="058d3-135">Verificar a configuração de Balanceador de carga de hello usando `azure vm show` *nome da máquina virtual*</span><span class="sxs-lookup"><span data-stu-id="058d3-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="058d3-136">saída de Hello serão:</span><span class="sxs-lookup"><span data-stu-id="058d3-136">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="058d3-137">Criar um ponto de extremidade da área de trabalho remota para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="058d3-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="058d3-138">Você pode criar um tráfego de rede do ponto de extremidade da área de trabalho remota tooforward de uma porta local de tooa porta pública para uma máquina virtual específica usando `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="058d3-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="058d3-139">Remover máquina virtual do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="058d3-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="058d3-140">Você pode remover uma máquina virtual de um balanceador de carga interno definido, excluindo o ponto de extremidade Olá associado.</span><span class="sxs-lookup"><span data-stu-id="058d3-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="058d3-141">Depois que o ponto de extremidade de saudação for removido, máquina virtual de saudação não pertencer balanceador de carga toohello definir mais.</span><span class="sxs-lookup"><span data-stu-id="058d3-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="058d3-142">Usando o exemplo hello acima, você pode remover ponto de extremidade de saudação criado para a máquina virtual "DB1" do balanceador de carga interno "ilbset" usando o comando Olá `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="058d3-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="058d3-143">Confira `azure vm endpoint --help` para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="058d3-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="058d3-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="058d3-144">Next steps</span></span>

[<span data-ttu-id="058d3-145">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="058d3-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="058d3-146">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="058d3-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
