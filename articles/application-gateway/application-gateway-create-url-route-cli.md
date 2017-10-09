---
title: aaaCreate um application gateway usando a URL de roteamento regras - 2.0 do CLI do Azure | Microsoft Docs
description: "Esta página fornece instruções toocreate, configure um gateway de aplicativo do Azure usando regras de roteamento de URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="5bbac-103">Criar um Gateway de Aplicativo usando roteamento com base em caminho com a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5bbac-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bbac-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5bbac-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="5bbac-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5bbac-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="5bbac-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="5bbac-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="5bbac-107">Roteamento baseado no caminho de URL permite que você tooassociate rotas com base no caminho de URL de saudação de uma solicitação Http.</span><span class="sxs-lookup"><span data-stu-id="5bbac-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="5bbac-108">Ele verifica se há um pool de back-end de tooa rota configurado para URL Olá apresentado em Olá Application Gateway e envia Olá toohello de tráfego de rede definida pelo pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bbac-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="5bbac-109">Um uso comum para roteamento baseado em URL é equilibrar solicitações de tooload para pools de toodifferent de diferentes tipos de conteúdo do servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bbac-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="5bbac-110">Roteamento baseado em URL apresenta um novo gateway de tooapplication do tipo de regra.</span><span class="sxs-lookup"><span data-stu-id="5bbac-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="5bbac-111">O gateway de aplicativo tem dois tipos de regra: básica e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="5bbac-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="5bbac-112">Tipo de regra básica fornece serviço de round-robin para Olá back-end pools ao PathBasedRouting distribuição de rodízio tooround Além disso, também leva padrão de caminho da URL de solicitação de saudação em consideração ao escolher o pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bbac-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="5bbac-113">Cenário</span><span class="sxs-lookup"><span data-stu-id="5bbac-113">Scenario</span></span>

<span data-ttu-id="5bbac-114">Em Olá exemplo a seguir, o Application Gateway está servindo tráfego para contoso.com com dois grupos de servidor back-end: um pool de servidor padrão e um pool de servidores de imagem.</span><span class="sxs-lookup"><span data-stu-id="5bbac-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="5bbac-115">As solicitações para http://contoso.com/image * são roteadas pool de servidores tooimage (imagesBackendPool), se hello não correspondência de padrão de caminho, um pool de servidores padrão (appGatewayBackendPool) está selecionado.</span><span class="sxs-lookup"><span data-stu-id="5bbac-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![roteamento de url](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="5bbac-117">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="5bbac-117">Log in tooAzure</span></span>

<span data-ttu-id="5bbac-118">Olá abrir **Prompt de comando do Microsoft Azure**e faça logon.</span><span class="sxs-lookup"><span data-stu-id="5bbac-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="5bbac-119">Você também pode usar `az login` sem comutador hello para logon de dispositivo que requer a inserção de um código em aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="5bbac-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="5bbac-120">Depois que você digitar Olá anterior de exemplo, um código é fornecido.</span><span class="sxs-lookup"><span data-stu-id="5bbac-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="5bbac-121">Navegue toohttps://aka.ms/devicelogin em um processo de logon do navegador toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="5bbac-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd mostrando logon de dispositivo][1]

<span data-ttu-id="5bbac-123">No navegador de hello, insira o código Olá recebido.</span><span class="sxs-lookup"><span data-stu-id="5bbac-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="5bbac-124">Você é redirecionado tooa na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="5bbac-124">You are redirected tooa sign-in page.</span></span>

![código de tooenter do navegador][2]

<span data-ttu-id="5bbac-126">Depois que o código de saudação foi inserido você entrou, Olá fechar navegador toocontinue com cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bbac-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![conectado com êxito][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="5bbac-128">Adicionar um gateway de aplicativos existentes baseados no caminho de regra tooan</span><span class="sxs-lookup"><span data-stu-id="5bbac-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="5bbac-129">Criar um Gateway de Aplicativo com uma regra com base em caminho definida</span><span class="sxs-lookup"><span data-stu-id="5bbac-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="5bbac-130">Criar um novo pool de back-end</span><span class="sxs-lookup"><span data-stu-id="5bbac-130">Create a new back-end pool</span></span>

<span data-ttu-id="5bbac-131">Definir configuração de gateway do aplicativo **imagesBackendPool** Olá com balanceamento de carga de tráfego de rede no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bbac-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="5bbac-132">Neste exemplo, você deve configurar as configurações de pool de back-end diferente para o novo pool de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="5bbac-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="5bbac-133">Cada pool de back-end pode ter sua própria configuração de pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bbac-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="5bbac-134">Configurações de HTTP de back-end são usadas por membros do pool regras tooroute tráfego toohello correto de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bbac-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="5bbac-135">Isso determina o protocolo de saudação e a porta que é usada ao enviar tráfego toohello membros do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bbac-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="5bbac-136">Sessões baseada em cookie também são determinadas pelas configurações de HTTP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bbac-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="5bbac-137">Se habilitada, a afinidade de sessão baseada em cookie envia tráfego toohello mesmo back-end como solicitações anteriores para cada pacote.</span><span class="sxs-lookup"><span data-stu-id="5bbac-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="5bbac-138">Criar uma nova porta de front-end</span><span class="sxs-lookup"><span data-stu-id="5bbac-138">Create a new front-end port</span></span>

<span data-ttu-id="5bbac-139">Configure portas de front-end Olá para o application gateway.</span><span class="sxs-lookup"><span data-stu-id="5bbac-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="5bbac-140">objeto de configuração de porta de front-end de saudação é usado por um ouvinte toodefine qual porta Olá Application Gateway escuta para o tráfego no ouvinte Olá.</span><span class="sxs-lookup"><span data-stu-id="5bbac-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="5bbac-141">Criar um novo ouvinte</span><span class="sxs-lookup"><span data-stu-id="5bbac-141">Create a new listener</span></span>

<span data-ttu-id="5bbac-142">Configure o ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bbac-142">Configure hello listener.</span></span> <span data-ttu-id="5bbac-143">Esta etapa configura um ouvinte de Olá para o endereço IP público de saudação e a porta usada tooreceive tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="5bbac-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="5bbac-144">saudação de exemplo a seguir usa a configuração de IP de front-end de Olá configurado anteriormente, a configuração de porta de front-end e um protocolo (http ou https) e configura o ouvinte hello.</span><span class="sxs-lookup"><span data-stu-id="5bbac-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="5bbac-145">Neste exemplo, o ouvinte de saudação escuta tooHTTP tráfego na porta 82 no endereço IP público Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5bbac-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="5bbac-146">Criar um mapa de caminho de Url Olá</span><span class="sxs-lookup"><span data-stu-id="5bbac-146">Create hello Url path map</span></span>

<span data-ttu-id="5bbac-147">Configure caminhos de regra de URL para pools de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bbac-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="5bbac-148">Esta etapa configura o caminho relativo do hello usado pelo mapeamento de saudação do aplicativo gateway toodefine entre o caminho da URL e qual pool de back-end recebe o tráfego de entrada hello toohandle.</span><span class="sxs-lookup"><span data-stu-id="5bbac-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bbac-149">Cada caminho deve começar com / e coloque-Olá somente um "\*" é permitido, está na extremidade hello.</span><span class="sxs-lookup"><span data-stu-id="5bbac-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="5bbac-150">Exemplos válidos são /xyz, /xyz* ou /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="5bbac-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="5bbac-151">Olá alimentada correspondente do caminho toohello de cadeia de caracteres não inclui qualquer texto após Olá primeiro "?" ou "#" e os caracteres não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="5bbac-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="5bbac-152">Olá, exemplo a seguir cria uma regra para "imagens / *" caminho de roteamento de tráfego tooback-end "imagesBackendPool".</span><span class="sxs-lookup"><span data-stu-id="5bbac-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="5bbac-153">Essa regra garante que o tráfego para cada conjunto de urls é roteado toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="5bbac-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="5bbac-154">Por exemplo, http://adatum.com/images/figure1.jpg fica muito "imagesBackendPool".</span><span class="sxs-lookup"><span data-stu-id="5bbac-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="5bbac-155">Se o caminho Olá não corresponde a qualquer uma das regras de caminho predefinido Olá, configuração de mapa de caminho de regra Olá também configura um pool de endereços de back-end do padrão.</span><span class="sxs-lookup"><span data-stu-id="5bbac-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="5bbac-156">Por exemplo, http://adatum.com/shoppingcart/test.html irá toopool1 conforme ele é definido como o pool padrão de saudação para tráfego não correspondente.</span><span class="sxs-lookup"><span data-stu-id="5bbac-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="5bbac-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bbac-157">Next steps</span></span>

<span data-ttu-id="5bbac-158">Se você quiser toolearn sobre descarregamento de Secure Sockets Layer (SSL), consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5bbac-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
