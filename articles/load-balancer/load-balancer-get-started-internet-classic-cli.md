---
title: "Criar um balanceador de carga voltado para a Internet - CLI do Azure clássica | Microsoft Docs"
description: "Saiba como criar um balanceador de carga para a Internet no modelo de implantação clássico usando a CLI do Azure"
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
ms.openlocfilehash: da3a908f17ff5c6d3923549a884ecc0a13cb8e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-cli"></a><span data-ttu-id="388ec-103">Introdução à criação de um balanceador de carga para a Internet (clássico) na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="388ec-103">Get started creating an Internet facing load balancer (classic) in the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="388ec-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="388ec-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="388ec-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="388ec-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="388ec-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="388ec-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="388ec-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="388ec-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="388ec-108">Antes de trabalhar com os recursos do Azure, é importante entender que, no momento, o Azure apresenta dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="388ec-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="388ec-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="388ec-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="388ec-110">Você pode exibir a documentação para ferramentas diferentes clicando nas guias na parte superior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="388ec-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="388ec-111">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="388ec-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="388ec-112">Também é possível [Saber como criar um balanceador de carga para a Internet usando o Gerenciador de Recursos do Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="388ec-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="388ec-113">Passo a passo para criação de um balanceador de carga para a Internet usando a CLI</span><span class="sxs-lookup"><span data-stu-id="388ec-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="388ec-114">Este guia mostra como criar um balanceador de carga de Internet com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="388ec-114">This guide shows how to create an Internet load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="388ec-115">Se você nunca usou a CLI do Azure, consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="388ec-115">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="388ec-116">Execute o comando **azure config mode** para alternar para o modo clássico, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="388ec-116">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="388ec-117">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="388ec-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="388ec-118">Criar ponto de extremidade e conjunto de balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="388ec-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="388ec-119">O cenário pressupõe que as máquinas virtuais "web1" e "web2" foram criadas.</span><span class="sxs-lookup"><span data-stu-id="388ec-119">The scenario assumes the virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="388ec-120">Este guia criará um conjunto de balanceadores de carga usando a porta 80 como porta pública e a porta 80 como porta local.</span><span class="sxs-lookup"><span data-stu-id="388ec-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="388ec-121">Uma porta de investigação também é configurada na porta 80 e nomeou o conjunto de balanceadores de carga como "lbset".</span><span class="sxs-lookup"><span data-stu-id="388ec-121">A probe port is also configured on port 80 and named the load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="388ec-122">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="388ec-122">Step 1</span></span>

<span data-ttu-id="388ec-123">Criar o primeiro ponto de extremidade e conjunto de balanceadores de carga usando `azure network vm endpoint create` para a máquina virtual "web1".</span><span class="sxs-lookup"><span data-stu-id="388ec-123">Create the first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="388ec-124">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="388ec-124">Step 2</span></span>

<span data-ttu-id="388ec-125">Adicione uma segunda máquina virtual "web2" ao conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="388ec-125">Add a second virtual machine "web2" to the load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="388ec-126">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="388ec-126">Step 3</span></span>

<span data-ttu-id="388ec-127">Verificar a configuração do balanceador de carga usando `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="388ec-127">Verify the load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="388ec-128">A saída será:</span><span class="sxs-lookup"><span data-stu-id="388ec-128">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="388ec-129">Criar um ponto de extremidade da área de trabalho remota para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="388ec-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="388ec-130">Você pode criar um ponto de extremidade da área de trabalho remota para encaminhar o tráfego de rede de uma porta pública para uma porta local, para uma máquina virtual específica, usando `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="388ec-130">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="388ec-131">Remover máquina virtual do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="388ec-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="388ec-132">Você precisa excluir o ponto de extremidade associado ao conjunto de balanceadores de carga da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="388ec-132">You have to delete the endpoint associated to the load balancer set from the virtual machine.</span></span> <span data-ttu-id="388ec-133">Depois que o ponto de extremidade é removido, a máquina virtual não pertence mais ao conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="388ec-133">Once the endpoint is removed, the virtual machine doesn't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="388ec-134">Usando o exemplo acima, você pode remover o ponto de extremidade criado para a máquina virtual "web1" do balanceador de carga usando o comando "lbset" `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="388ec-134">Using the example above, you can remove the endpoint created for virtual machine "web1" from load balancer "lbset" using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="388ec-135">Você pode explorar mais opções para gerenciar pontos de extremidade usando o comando `azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="388ec-135">You can explore more options to manage endpoints using the command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="388ec-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="388ec-136">Next steps</span></span>

[<span data-ttu-id="388ec-137">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="388ec-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="388ec-138">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="388ec-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="388ec-139">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="388ec-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
