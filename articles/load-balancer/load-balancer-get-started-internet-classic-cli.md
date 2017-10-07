---
title: "aaaCreate um voltados para Internet carregar balanceador - clássico de CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga voltado para Internet no modelo de implantação clássico usando Olá CLI do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="2b40e-103">Introdução à criação de uma balanceador de carga (clássico) na Olá CLI do Azure da Internet</span><span class="sxs-lookup"><span data-stu-id="2b40e-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b40e-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="2b40e-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="2b40e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b40e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="2b40e-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2b40e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="2b40e-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="2b40e-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="2b40e-108">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico.</span><span class="sxs-lookup"><span data-stu-id="2b40e-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2b40e-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b40e-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="2b40e-110">Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2b40e-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="2b40e-111">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="2b40e-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="2b40e-112">Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2b40e-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="2b40e-113">Passo a passo para criação de um balanceador de carga para a Internet usando a CLI</span><span class="sxs-lookup"><span data-stu-id="2b40e-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="2b40e-114">Este guia mostra como toocreate um balanceador de carga de Internet com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="2b40e-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="2b40e-115">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="2b40e-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="2b40e-116">Executar Olá **modo de configuração do azure** tooswitch tooclassic modo de comando, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2b40e-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="2b40e-117">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="2b40e-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="2b40e-118">Criar ponto de extremidade e conjunto de balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="2b40e-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="2b40e-119">cenário de saudação pressupõe máquinas virtuais de hello "web1" e "web2" foi criado.</span><span class="sxs-lookup"><span data-stu-id="2b40e-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="2b40e-120">Este guia criará um conjunto de balanceadores de carga usando a porta 80 como porta pública e a porta 80 como porta local.</span><span class="sxs-lookup"><span data-stu-id="2b40e-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="2b40e-121">Uma porta de investigação também está configurada na porta 80 e balanceador de carga Olá nomeada definida "lbset".</span><span class="sxs-lookup"><span data-stu-id="2b40e-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="2b40e-122">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="2b40e-122">Step 1</span></span>

<span data-ttu-id="2b40e-123">Criar o primeiro ponto de extremidade de saudação e definir o uso do balanceador de carga `azure network vm endpoint create` para a máquina virtual "web1".</span><span class="sxs-lookup"><span data-stu-id="2b40e-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="2b40e-124">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="2b40e-124">Step 2</span></span>

<span data-ttu-id="2b40e-125">Adicione um segundo conjunto de Balanceador de carga de toohello máquina virtual "web2".</span><span class="sxs-lookup"><span data-stu-id="2b40e-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="2b40e-126">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="2b40e-126">Step 3</span></span>

<span data-ttu-id="2b40e-127">Verificar a configuração de Balanceador de carga de hello usando `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="2b40e-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="2b40e-128">saída de Hello serão:</span><span class="sxs-lookup"><span data-stu-id="2b40e-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="2b40e-129">Criar um ponto de extremidade da área de trabalho remota para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2b40e-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="2b40e-130">Você pode criar um tráfego de rede do ponto de extremidade da área de trabalho remota tooforward de uma porta local de tooa porta pública para uma máquina virtual específica usando `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="2b40e-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="2b40e-131">Remover máquina virtual do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="2b40e-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="2b40e-132">Você tem toodelete Olá ponto de extremidade associado toohello conjunto de Balanceador de carga da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b40e-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="2b40e-133">Depois que o ponto de extremidade de saudação for removido, máquina virtual de saudação não pertence balanceador de carga toohello definir mais.</span><span class="sxs-lookup"><span data-stu-id="2b40e-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="2b40e-134">Usando o exemplo hello acima, você pode remover ponto de extremidade de saudação criado para a máquina virtual "web1" do balanceador de carga usando o comando hello "lbset" `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="2b40e-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="2b40e-135">Você pode explorar mais opções toomanage pontos de extremidade usando o comando Olá`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="2b40e-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b40e-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b40e-136">Next steps</span></span>

[<span data-ttu-id="2b40e-137">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="2b40e-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="2b40e-138">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="2b40e-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="2b40e-139">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="2b40e-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
