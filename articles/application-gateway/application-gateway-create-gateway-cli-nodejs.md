---
title: Criar um Gateway de Aplicativo do Azure - CLI do Azure 1.0 | Microsoft Docs
description: Saiba como criar um Gateway de Aplicativo usando a CLI do Azure 1.0 no Resource Manager
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
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="ea68f-103">Criar um gateway de aplicativo usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ea68f-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea68f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ea68f-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ea68f-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ea68f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ea68f-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea68f-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ea68f-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ea68f-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ea68f-108">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ea68f-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="ea68f-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ea68f-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="ea68f-110">O Azure Gateway de Aplicativo é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="ea68f-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ea68f-111">Ele fornece o failover e solicitações HTTP de roteamento de desempenho entre diferentes servidores, estejam eles na nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="ea68f-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="ea68f-112">O Gateway de Aplicativo tem os seguintes recursos de entrega de aplicativo: balanceamento de carga HTTP, afinidade de sessão baseada em cookie e descarregamento SSL (protocolo SSL), investigações de integridade personalizadas e suporte para vários sites.</span><span class="sxs-lookup"><span data-stu-id="ea68f-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="ea68f-113">Pré-requisito: instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ea68f-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="ea68f-114">Para executar as etapas deste artigo, será necessário [instalar a Interface de Linha de Comando do Azure para Mac, Linux e Windows (CLI do Azure)](../xplat-cli-install.md) e você precisará fazer [logon no Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ea68f-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="ea68f-115">Se você não tiver uma conta do Azure, crie uma.</span><span class="sxs-lookup"><span data-stu-id="ea68f-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="ea68f-116">Inscreva-se em uma [avaliação gratuita aqui](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="ea68f-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="ea68f-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="ea68f-117">Scenario</span></span>

<span data-ttu-id="ea68f-118">Nesse cenário, você aprenderá como criar um Gateway de Aplicativo usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea68f-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="ea68f-119">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="ea68f-119">This scenario will:</span></span>

* <span data-ttu-id="ea68f-120">Criará um Gateway de Aplicativo com duas instâncias.</span><span class="sxs-lookup"><span data-stu-id="ea68f-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="ea68f-121">Criar uma rede virtual chamada ContosoVNET com um bloco CIDR 10.0.0.0/16 reservado.</span><span class="sxs-lookup"><span data-stu-id="ea68f-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ea68f-122">Crie uma sub-rede chamada subnet01 que use 10.0.0.0/28 como bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="ea68f-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="ea68f-123">A configuração adicional do Gateway de Aplicativo, incluindo investigações de integridade personalizadas, endereços de pool de back-end e regras adicionais são configuradas após o Gateway de Aplicativo ser configurado e não durante a implantação inicial.</span><span class="sxs-lookup"><span data-stu-id="ea68f-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ea68f-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ea68f-124">Before you begin</span></span>

<span data-ttu-id="ea68f-125">O Gateway de Aplicativo do Azure requer sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ea68f-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="ea68f-126">Ao criar uma rede virtual, certifique-se de deixar espaço de endereço suficiente para ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="ea68f-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="ea68f-127">Depois de implantar um gateway de aplicativo a uma sub-rede, apenas gateway de aplicativos adicionais poderão ser adicionados à sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ea68f-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="ea68f-128">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="ea68f-128">Log in to Azure</span></span>

<span data-ttu-id="ea68f-129">Abra o **Prompt de comando do Microsoft Azure**e faça logon.</span><span class="sxs-lookup"><span data-stu-id="ea68f-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="ea68f-130">Depois de digitar o exemplo anterior, um código será fornecido.</span><span class="sxs-lookup"><span data-stu-id="ea68f-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="ea68f-131">Navegue até https://aka.ms/devicelogin em um navegador para continuar o processo de logon.</span><span class="sxs-lookup"><span data-stu-id="ea68f-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd mostrando logon de dispositivo][1]

<span data-ttu-id="ea68f-133">No navegador, digite o código recebido.</span><span class="sxs-lookup"><span data-stu-id="ea68f-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="ea68f-134">Você será redirecionado para uma página de entrada.</span><span class="sxs-lookup"><span data-stu-id="ea68f-134">You are redirected to a sign-in page.</span></span>

![navegador para inserir código][2]

<span data-ttu-id="ea68f-136">Depois que o código foi inserido, você estará conectado. Feche o navegador para continuar com o cenário.</span><span class="sxs-lookup"><span data-stu-id="ea68f-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![conectado com êxito][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="ea68f-138">Alternar para o modo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ea68f-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="ea68f-139">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ea68f-139">Create the resource group</span></span>

<span data-ttu-id="ea68f-140">Antes de criar o gateway de aplicativo, um grupo de recursos é criado para conter o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea68f-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="ea68f-141">O código a seguir mostra o comando.</span><span class="sxs-lookup"><span data-stu-id="ea68f-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="ea68f-142">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ea68f-142">Create a virtual network</span></span>

<span data-ttu-id="ea68f-143">Após a criação do grupo de recursos, uma rede virtual é criada para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea68f-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="ea68f-144">No exemplo a seguir, o espaço de endereço foi 10.0.0.0/16, conforme definido nas anotações do cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="ea68f-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="ea68f-145">Criar uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="ea68f-145">Create a subnet</span></span>

<span data-ttu-id="ea68f-146">Após a criação da rede virtual, uma sub-rede é adicionada ao gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea68f-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="ea68f-147">Se você planeja usar o gateway de aplicativo com um aplicativo Web hospedado na mesma rede virtual do que o gateway de aplicativo, não se esqueça de deixar espaço suficiente para outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ea68f-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="ea68f-148">Criar o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ea68f-148">Create the application gateway</span></span>

<span data-ttu-id="ea68f-149">Depois que a rede virtual e a sub-rede forem criadas, os pré-requisitos para o gateway de aplicativo estarão completos.</span><span class="sxs-lookup"><span data-stu-id="ea68f-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="ea68f-150">Além disso, um certificado .pfx exportado anteriormente e a senha do certificado são necessários para a etapa seguinte: os endereços IP usados para o back-end são os endereços IP para seu servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="ea68f-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="ea68f-151">Esses valores podem ser IPs privados na rede virtual, ips públicos ou nomes de domínio totalmente qualificados para seus servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="ea68f-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="ea68f-152">Para obter uma lista de parâmetros que podem ser fornecidos durante a criação, execute o seguinte comando: **azure network application-gateway create --help**.</span><span class="sxs-lookup"><span data-stu-id="ea68f-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="ea68f-153">Este exemplo cria um Gateway de Aplicativo básico com configurações padrão para o ouvinte, pool de back-end, configurações de http de back-end e regras.</span><span class="sxs-lookup"><span data-stu-id="ea68f-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="ea68f-154">Você pode modificar essas configurações de acordo com sua implantação quando o provisionamento for bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="ea68f-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="ea68f-155">Se você já tiver seu aplicativo Web definido com o pool de back-end nas etapas anteriores, o balanceamento de carga começará depois que ele for criado.</span><span class="sxs-lookup"><span data-stu-id="ea68f-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea68f-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea68f-156">Next steps</span></span>

<span data-ttu-id="ea68f-157">Saiba como criar investigações de integridade personalizados visitando [Criar uma investigação de integridade personalizada](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ea68f-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="ea68f-158">Saiba como configurar o Descarregamento de SSL e levar a descriptografia SSL cara longe dos seus servidores Web visitando [Configurar Descarregamento de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="ea68f-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
