---
title: aaaCreate um Gateway de aplicativo do Azure - 1.0 da CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um Application Gateway usando Olá 1.0 de CLI do Azure no Gerenciador de recursos"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="b2dfb-103">Criar um gateway de aplicativo usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b2dfb-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2dfb-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b2dfb-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="b2dfb-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2dfb-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="b2dfb-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2dfb-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="b2dfb-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2dfb-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="b2dfb-108">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b2dfb-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="b2dfb-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b2dfb-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="b2dfb-110">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b2dfb-111">Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="b2dfb-112">Gateway de aplicativo tem Olá recursos de entrega de aplicativos a seguir: HTTP carregar testes de integridade personalizado de balanceamento, afinidade de sessão baseada em cookie e descarregamento de Secure Sockets Layer (SSL) e suporte para vários locais.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="b2dfb-113">Pré-requisito: Instale Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b2dfb-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="b2dfb-114">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](../xplat-cli-install.md) e você precisa de muito[logon tooAzure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b2dfb-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="b2dfb-115">Se você não tiver uma conta do Azure, crie uma.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="b2dfb-116">Inscreva-se em uma [avaliação gratuita aqui](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="b2dfb-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="b2dfb-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="b2dfb-117">Scenario</span></span>

<span data-ttu-id="b2dfb-118">Nesse cenário, você aprenderá como toocreate um gateway de aplicativo usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="b2dfb-119">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="b2dfb-119">This scenario will:</span></span>

* <span data-ttu-id="b2dfb-120">Criará um Gateway de Aplicativo com duas instâncias.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="b2dfb-121">Criar uma rede virtual chamada ContosoVNET com um bloco CIDR 10.0.0.0/16 reservado.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="b2dfb-122">Crie uma sub-rede chamada subnet01 que use 10.0.0.0/28 como bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="b2dfb-123">Testes de configuração adicionais do gateway de aplicativo hello, incluindo integridade personalizado, endereços do pool de back-end e regras adicionais são configuradas após a configuração do gateway de aplicativo hello e não durante a implantação inicial.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b2dfb-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b2dfb-124">Before you begin</span></span>

<span data-ttu-id="b2dfb-125">O Gateway de Aplicativo do Azure requer sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="b2dfb-126">Ao criar uma rede virtual, certifique-se de que você deixe suficiente toohave de espaço de endereço várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="b2dfb-127">Depois de implantar um aplicativo gateway tooa de sub-rede, os gateways de aplicativos adicionais só são toobe capaz de adicionar sub-rede toohello.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="b2dfb-128">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2dfb-128">Log in tooAzure</span></span>

<span data-ttu-id="b2dfb-129">Olá abrir **Prompt de comando do Microsoft Azure**e faça logon.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="b2dfb-130">Depois que você digitar Olá anterior de exemplo, um código é fornecido.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="b2dfb-131">Navegue toohttps://aka.ms/devicelogin em um processo de logon do navegador toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd mostrando logon de dispositivo][1]

<span data-ttu-id="b2dfb-133">No navegador de hello, insira o código Olá recebido.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="b2dfb-134">Você é redirecionado tooa na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-134">You are redirected tooa sign-in page.</span></span>

![código de tooenter do navegador][2]

<span data-ttu-id="b2dfb-136">Depois que o código de saudação foi inserido você entrou, Olá fechar navegador toocontinue com cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![conectado com êxito][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="b2dfb-138">Alternar tooResource modo Manager</span><span class="sxs-lookup"><span data-stu-id="b2dfb-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="b2dfb-139">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="b2dfb-139">Create hello resource group</span></span>

<span data-ttu-id="b2dfb-140">Antes de criar o gateway de aplicativo hello, um grupo de recursos é criado o gateway de aplicativo hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="b2dfb-141">Veja a seguir de Olá comando hello.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="b2dfb-142">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="b2dfb-142">Create a virtual network</span></span>

<span data-ttu-id="b2dfb-143">Depois de criar o grupo de recursos hello, uma rede virtual é criada para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="b2dfb-144">Olá exemplo a seguir, o espaço de endereço Olá foi como 10.0.0.0/16 conforme definido na saudação anterior anotações de cenário.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="b2dfb-145">Criar uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="b2dfb-145">Create a subnet</span></span>

<span data-ttu-id="b2dfb-146">Após a criação de rede virtual hello, uma sub-rede é adicionada para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="b2dfb-147">Se você planejar toouse gateway de aplicativo com um aplicativo web hospedado no hello mesmo virtual de rede como gateway de aplicativo hello, ser tooleave se espaço suficiente para outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="b2dfb-148">Criar hello application gateway</span><span class="sxs-lookup"><span data-stu-id="b2dfb-148">Create hello application gateway</span></span>

<span data-ttu-id="b2dfb-149">Após a criação de sub-rede e a rede virtual hello, Olá os pré-requisitos para o gateway de aplicativo hello forem concluídos.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="b2dfb-150">Além de uma senha de certificado e hello. pfx exportado anteriormente para o certificado de saudação são necessários para Olá etapa a seguir: endereços IP de saudação usados para Olá back-end são endereços IP de saudação do servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="b2dfb-151">Esses valores podem ser qualquer IPs privados na rede virtual hello, ips públicos ou nomes de domínio totalmente qualificado para seus servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="b2dfb-152">Para obter uma lista de parâmetros que podem ser fornecidas durante a criação da execução Olá comando a seguir: **criar gateway de aplicativo de rede do azure – ajuda**.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="b2dfb-153">Este exemplo cria um application gateway básico com configurações padrão para o ouvinte hello, pool de back-end, configurações de http de back-end e regras.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="b2dfb-154">Você pode modificar essas configurações toosuit sua implantação quando Olá provisionamento é bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="b2dfb-155">Se você já tiver o aplicativo da web definido com o pool de back-end de saudação em Olá anterior etapas, uma vez criadas, balanceamento de carga começa.</span><span class="sxs-lookup"><span data-stu-id="b2dfb-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2dfb-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2dfb-156">Next steps</span></span>

<span data-ttu-id="b2dfb-157">Saiba como sondas de integridade personalizado toocreate visitando [criar um teste de integridade personalizado](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b2dfb-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="b2dfb-158">Saiba como tooconfigure descarregamento de SSL e take Olá cara SSL descriptografia desativada, os servidores web visitando [configurar descarregamento de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="b2dfb-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
