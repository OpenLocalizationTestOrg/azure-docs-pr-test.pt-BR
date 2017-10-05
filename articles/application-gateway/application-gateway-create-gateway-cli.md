---
title: Criar um Gateway de Aplicativo do Azure - CLI do Azure 2.0 | Microsoft Docs
description: Saiba como criar um Gateway de Aplicativo usando a CLI do Azure 2.0 no Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="71b62-103">Criar um gateway de aplicativo usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="71b62-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="71b62-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="71b62-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="71b62-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71b62-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="71b62-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="71b62-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="71b62-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71b62-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="71b62-108">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="71b62-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="71b62-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="71b62-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="71b62-110">O Gateway de Aplicativo é uma solução de virtualização dedicada que fornece o ADC (controlador de entrega de aplicativos) como serviço, oferecendo várias funcionalidades de balanceamento de carga de camada 7 para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71b62-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="71b62-111">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="71b62-111">CLI versions to complete the task</span></span>

<span data-ttu-id="71b62-112">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="71b62-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="71b62-113">[CLI do Azure 1.0](application-gateway-create-gateway-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e do resource manager.</span><span class="sxs-lookup"><span data-stu-id="71b62-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="71b62-114">[CLI do Azure 2.0](application-gateway-create-gateway-cli.md) – nossa próxima geração de CLI para o modelo de implantação do resource manager</span><span class="sxs-lookup"><span data-stu-id="71b62-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="71b62-115">Pré-requisito: instalar a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="71b62-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="71b62-116">Para executar as etapas deste artigo, será necessário [instalar a Interface de Linha de Comando do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="71b62-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="71b62-117">Se você não tiver uma conta do Azure, crie uma.</span><span class="sxs-lookup"><span data-stu-id="71b62-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="71b62-118">Inscreva-se em uma [avaliação gratuita aqui](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="71b62-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="71b62-119">Cenário</span><span class="sxs-lookup"><span data-stu-id="71b62-119">Scenario</span></span>

<span data-ttu-id="71b62-120">Nesse cenário, você aprenderá como criar um Gateway de Aplicativo usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="71b62-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="71b62-121">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="71b62-121">This scenario will:</span></span>

* <span data-ttu-id="71b62-122">Criará um Gateway de Aplicativo com duas instâncias.</span><span class="sxs-lookup"><span data-stu-id="71b62-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="71b62-123">Criará uma rede virtual chamada AdatumAppGatewayVNET, com um bloco CIDR 10.0.0.0/16 reservado.</span><span class="sxs-lookup"><span data-stu-id="71b62-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="71b62-124">Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="71b62-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="71b62-125">A configuração adicional do Gateway de Aplicativo, incluindo investigações de integridade personalizadas, endereços de pool de back-end e regras adicionais são configuradas após o Gateway de Aplicativo ser configurado e não durante a implantação inicial.</span><span class="sxs-lookup"><span data-stu-id="71b62-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="71b62-126">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="71b62-126">Before you begin</span></span>

<span data-ttu-id="71b62-127">O Gateway de Aplicativo do Azure requer sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="71b62-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="71b62-128">Ao criar uma rede virtual, certifique-se de deixar espaço de endereço suficiente para ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="71b62-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="71b62-129">Depois de implantar um Gateway de Aplicativo a uma sub-rede, apenas Gateways de Aplicativo adicionais podem ser adicionados à sub-rede.</span><span class="sxs-lookup"><span data-stu-id="71b62-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="71b62-130">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="71b62-130">Log in to Azure</span></span>

<span data-ttu-id="71b62-131">Abra o **Prompt de comando do Microsoft Azure**e faça logon.</span><span class="sxs-lookup"><span data-stu-id="71b62-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="71b62-132">Você também pode usar `az login` sem a opção de logon de dispositivo que exige a inserção de um código em aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="71b62-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="71b62-133">Depois de digitar o exemplo anterior, um código será fornecido.</span><span class="sxs-lookup"><span data-stu-id="71b62-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="71b62-134">Navegue até https://aka.ms/devicelogin em um navegador para continuar o processo de logon.</span><span class="sxs-lookup"><span data-stu-id="71b62-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd mostrando logon de dispositivo][1]

<span data-ttu-id="71b62-136">No navegador, digite o código recebido.</span><span class="sxs-lookup"><span data-stu-id="71b62-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="71b62-137">Você será redirecionado para uma página de entrada.</span><span class="sxs-lookup"><span data-stu-id="71b62-137">You are redirected to a sign-in page.</span></span>

![navegador para inserir código][2]

<span data-ttu-id="71b62-139">Depois que o código foi inserido, você estará conectado. Feche o navegador para continuar com o cenário.</span><span class="sxs-lookup"><span data-stu-id="71b62-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![conectado com êxito][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="71b62-141">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="71b62-141">Create the resource group</span></span>

<span data-ttu-id="71b62-142">Antes de criar o gateway de aplicativo, um grupo de recursos é criado para conter o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71b62-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="71b62-143">O código a seguir mostra o comando.</span><span class="sxs-lookup"><span data-stu-id="71b62-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="71b62-144">Criar o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="71b62-144">Create the application gateway</span></span>

<span data-ttu-id="71b62-145">Os endereços IP usados para o back-end são os endereços IP para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="71b62-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="71b62-146">Esses valores podem ser IPs privados na rede virtual, ips públicos ou nomes de domínio totalmente qualificados para seus servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="71b62-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="71b62-147">O exemplo a seguir cria um Gateway de Aplicativo com definições de configuração adicionais para as configurações HTTP, de portas e de regras.</span><span class="sxs-lookup"><span data-stu-id="71b62-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="71b62-148">O exemplo anterior mostra várias propriedades que não são necessárias durante a criação de um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71b62-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="71b62-149">O exemplo de código a seguir cria um Gateway de Aplicativo com as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="71b62-149">The following code example creates an application gateway with the required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="71b62-150">Para obter uma lista de parâmetros que podem ser fornecidos durante a criação, execute o seguinte comando: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="71b62-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="71b62-151">Este exemplo cria um Gateway de Aplicativo básico com configurações padrão para o ouvinte, pool de back-end, configurações de http de back-end e regras.</span><span class="sxs-lookup"><span data-stu-id="71b62-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="71b62-152">Você pode modificar essas configurações de acordo com sua implantação quando o provisionamento for bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="71b62-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="71b62-153">Se você já tiver seu aplicativo Web definido com o pool de back-end nas etapas anteriores, o balanceamento de carga começará depois que ele for criado.</span><span class="sxs-lookup"><span data-stu-id="71b62-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="71b62-154">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="71b62-154">Get application gateway DNS name</span></span>

<span data-ttu-id="71b62-155">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="71b62-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="71b62-156">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="71b62-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="71b62-157">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71b62-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="71b62-158">[Configurando um nome de domínio personalizado no Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="71b62-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="71b62-159">Para configurar um alias, recupere os detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71b62-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="71b62-160">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="71b62-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="71b62-161">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71b62-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="71b62-162">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="71b62-162">Delete all resources</span></span>

<span data-ttu-id="71b62-163">Para excluir todos os recursos criados neste artigo, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="71b62-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="71b62-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71b62-164">Next steps</span></span>

<span data-ttu-id="71b62-165">Saiba como criar investigações de integridade personalizados visitando [Criar uma investigação de integridade personalizada](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="71b62-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="71b62-166">Saiba como configurar o Descarregamento de SSL e levar a descriptografia SSL cara longe dos seus servidores Web visitando [Configurar Descarregamento de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="71b62-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
