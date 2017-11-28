---
title: aaaCreate um Gateway de aplicativo do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um Application Gateway usando Olá 2.0 de CLI do Azure no Gerenciador de recursos"
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
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="ab558-103">Criar um gateway de aplicativo usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ab558-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab558-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ab558-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ab558-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab558-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ab558-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab558-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ab558-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab558-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ab558-108">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ab558-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="ab558-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ab558-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="ab558-110">O Gateway de Aplicativo é uma solução de virtualização dedicada que fornece o ADC (controlador de entrega de aplicativos) como serviço, oferecendo várias funcionalidades de balanceamento de carga de camada 7 para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab558-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ab558-111">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="ab558-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="ab558-112">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab558-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="ab558-113">[1.0 de CLI do Azure](application-gateway-create-gateway-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.</span><span class="sxs-lookup"><span data-stu-id="ab558-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="ab558-114">[2.0 do CLI do Azure](application-gateway-create-gateway-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="ab558-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="ab558-115">Pré-requisito: Instale Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ab558-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="ab558-116">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ab558-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="ab558-117">Se você não tiver uma conta do Azure, crie uma.</span><span class="sxs-lookup"><span data-stu-id="ab558-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="ab558-118">Inscreva-se em uma [avaliação gratuita aqui](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="ab558-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="ab558-119">Cenário</span><span class="sxs-lookup"><span data-stu-id="ab558-119">Scenario</span></span>

<span data-ttu-id="ab558-120">Nesse cenário, você aprenderá como toocreate um gateway de aplicativo usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab558-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="ab558-121">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="ab558-121">This scenario will:</span></span>

* <span data-ttu-id="ab558-122">Criará um Gateway de Aplicativo com duas instâncias.</span><span class="sxs-lookup"><span data-stu-id="ab558-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="ab558-123">Criará uma rede virtual chamada AdatumAppGatewayVNET, com um bloco CIDR 10.0.0.0/16 reservado.</span><span class="sxs-lookup"><span data-stu-id="ab558-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ab558-124">Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="ab558-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="ab558-125">Testes de configuração adicionais do gateway de aplicativo hello, incluindo integridade personalizado, endereços do pool de back-end e regras adicionais são configuradas após a configuração do gateway de aplicativo hello e não durante a implantação inicial.</span><span class="sxs-lookup"><span data-stu-id="ab558-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ab558-126">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ab558-126">Before you begin</span></span>

<span data-ttu-id="ab558-127">O Gateway de Aplicativo do Azure requer sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ab558-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="ab558-128">Ao criar uma rede virtual, certifique-se de que você deixe suficiente toohave de espaço de endereço várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="ab558-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="ab558-129">Depois de implantar um aplicativo gateway tooa de sub-rede, os gateways de aplicativos adicionais somente podem ser adicionados a sub-rede toohello.</span><span class="sxs-lookup"><span data-stu-id="ab558-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="ab558-130">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="ab558-130">Log in tooAzure</span></span>

<span data-ttu-id="ab558-131">Olá abrir **Prompt de comando do Microsoft Azure**e faça logon.</span><span class="sxs-lookup"><span data-stu-id="ab558-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="ab558-132">Você também pode usar `az login` sem comutador hello para logon de dispositivo que requer a inserção de um código em aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="ab558-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="ab558-133">Depois que você digitar Olá anterior de exemplo, um código é fornecido.</span><span class="sxs-lookup"><span data-stu-id="ab558-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="ab558-134">Navegue toohttps://aka.ms/devicelogin em um processo de logon do navegador toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="ab558-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd mostrando logon de dispositivo][1]

<span data-ttu-id="ab558-136">No navegador de hello, insira o código Olá recebido.</span><span class="sxs-lookup"><span data-stu-id="ab558-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="ab558-137">Você é redirecionado tooa na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab558-137">You are redirected tooa sign-in page.</span></span>

![código de tooenter do navegador][2]

<span data-ttu-id="ab558-139">Depois que o código de saudação foi inserido você entrou, Olá fechar navegador toocontinue com cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab558-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![conectado com êxito][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="ab558-141">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="ab558-141">Create hello resource group</span></span>

<span data-ttu-id="ab558-142">Antes de criar o gateway de aplicativo hello, um grupo de recursos é criado o gateway de aplicativo hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="ab558-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="ab558-143">Veja a seguir de Olá comando hello.</span><span class="sxs-lookup"><span data-stu-id="ab558-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="ab558-144">Criar hello application gateway</span><span class="sxs-lookup"><span data-stu-id="ab558-144">Create hello application gateway</span></span>

<span data-ttu-id="ab558-145">endereços IP de saudação usados para Olá back-end são endereços IP de saudação do servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="ab558-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="ab558-146">Esses valores podem ser qualquer IPs privados na rede virtual hello, ips públicos ou nomes de domínio totalmente qualificado para seus servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="ab558-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="ab558-147">Olá exemplo a seguir cria um application gateway com definições de configuração adicionais para as configurações de http, portas e regras.</span><span class="sxs-lookup"><span data-stu-id="ab558-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="ab558-148">Olá, exemplo anterior mostra várias propriedades que não são necessárias durante a criação de saudação de um application gateway.</span><span class="sxs-lookup"><span data-stu-id="ab558-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="ab558-149">Olá exemplo de código a seguir cria um application gateway com informações de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="ab558-149">hello following code example creates an application gateway with hello required information.</span></span>

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
> <span data-ttu-id="ab558-150">Para obter uma lista de parâmetros que podem ser fornecidas durante a saudação criação executar comando a seguir: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="ab558-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="ab558-151">Este exemplo cria um application gateway básico com configurações padrão para o ouvinte hello, pool de back-end, configurações de http de back-end e regras.</span><span class="sxs-lookup"><span data-stu-id="ab558-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="ab558-152">Você pode modificar essas configurações toosuit sua implantação quando Olá provisionamento é bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="ab558-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="ab558-153">Se você já tiver o aplicativo da web definido com o pool de back-end de saudação em Olá anterior etapas, uma vez criadas, balanceamento de carga começa.</span><span class="sxs-lookup"><span data-stu-id="ab558-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ab558-154">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ab558-154">Get application gateway DNS name</span></span>

<span data-ttu-id="ab558-155">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="ab558-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ab558-156">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="ab558-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ab558-157">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ab558-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="ab558-158">[Configurando um nome de domínio personalizado no Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ab558-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="ab558-159">tooconfigure um alias, recuperar detalhes do gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="ab558-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="ab558-160">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="ab558-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="ab558-161">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="ab558-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="ab558-162">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="ab558-162">Delete all resources</span></span>

<span data-ttu-id="ab558-163">toodelete todos os recursos criados neste artigo, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab558-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="ab558-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab558-164">Next steps</span></span>

<span data-ttu-id="ab558-165">Saiba como sondas de integridade personalizado toocreate visitando [criar um teste de integridade personalizado](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ab558-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="ab558-166">Saiba como tooconfigure descarregamento de SSL e take Olá cara SSL descriptografia desativada, os servidores web visitando [configurar descarregamento de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="ab558-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
