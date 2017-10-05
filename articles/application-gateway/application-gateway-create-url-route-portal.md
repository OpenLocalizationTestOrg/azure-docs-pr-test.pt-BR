---
title: Criar uma regra com base no caminho - Gateway de Aplicativo do Azure - Portal do Azure | Microsoft Docs
description: Saiba como criar uma regra com base no caminho para um gateway de aplicativo usando o portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="01b65-103">Criar uma regra baseada em caminho para um gateway de aplicativo usando o portal</span><span class="sxs-lookup"><span data-stu-id="01b65-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01b65-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="01b65-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="01b65-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01b65-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="01b65-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="01b65-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="01b65-107">O Roteamento com base em caminho de URL permite que você associe rotas com base no caminho de URL da solicitação Http.</span><span class="sxs-lookup"><span data-stu-id="01b65-107">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="01b65-108">Ele verifica se há uma rota para um pool de back-end configurado para a URL listada no Gateway de Aplicativo e envia o tráfego de rede para o pool de back-end definido.</span><span class="sxs-lookup"><span data-stu-id="01b65-108">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="01b65-109">Um uso comum para o roteamento com base em URL é balancear a carga das solicitações para tipos de conteúdo diferentes para pools de servidores back-end diferentes.</span><span class="sxs-lookup"><span data-stu-id="01b65-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="01b65-110">O roteamento com base em URL apresenta um novo tipo de regra ao gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01b65-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="01b65-111">O Gateway de Aplicativo tem dois tipos de regra: básica e com base no caminho.</span><span class="sxs-lookup"><span data-stu-id="01b65-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="01b65-112">O tipo de regra básica fornece o serviço de round robin para os pools de back-end, enquanto as regras com base no caminho também leva em consideração, além da distribuição round robin, o padrão de caminho da URL da solicitação ao escolher o pool de back-end apropriado.</span><span class="sxs-lookup"><span data-stu-id="01b65-112">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="01b65-113">Cenário</span><span class="sxs-lookup"><span data-stu-id="01b65-113">Scenario</span></span>

<span data-ttu-id="01b65-114">O cenário a seguir passa pela criação de uma regra com base no caminho em um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="01b65-114">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="01b65-115">O cenário pressupõe que você já seguiu as etapas para [Criar um Gateway de Aplicativo](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="01b65-115">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![roteamento de url][scenario]

## <span data-ttu-id="01b65-117"><a name="createrule"></a>Criar a regra com base no caminho</span><span class="sxs-lookup"><span data-stu-id="01b65-117"><a name="createrule"></a>Create the Path-based rule</span></span>

<span data-ttu-id="01b65-118">Uma regra com base no caminho exige seu próprio ouvinte. Antes da criação da regra, não se esqueça de verificar se você tem um ouvinte disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="01b65-118">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="01b65-119">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="01b65-119">Step 1</span></span>

<span data-ttu-id="01b65-120">Navegue até o [Portal do Azure](http://portal.azure.com) e selecione um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="01b65-120">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="01b65-121">Clique em **Regras**</span><span class="sxs-lookup"><span data-stu-id="01b65-121">Click **Rules**</span></span>

![Visão geral do Gateway de Aplicativo][1]

### <a name="step-2"></a><span data-ttu-id="01b65-123">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="01b65-123">Step 2</span></span>

<span data-ttu-id="01b65-124">Clique no botão **Com base no caminho** para adicionar uma nova regra com base em caminho.</span><span class="sxs-lookup"><span data-stu-id="01b65-124">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="01b65-125">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="01b65-125">Step 3</span></span>

<span data-ttu-id="01b65-126">A folha **Adicionar regra com base no caminho** tem duas seções.</span><span class="sxs-lookup"><span data-stu-id="01b65-126">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="01b65-127">A primeira seção é onde você definiu o ouvinte, o nome da regra e as configurações de caminho padrão.</span><span class="sxs-lookup"><span data-stu-id="01b65-127">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="01b65-128">As configurações do caminho padrão são para rotas que não se ajustam à rota com base no caminho personalizada.</span><span class="sxs-lookup"><span data-stu-id="01b65-128">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="01b65-129">A segunda seção da folha **Adicionar regra com base no caminho** é onde você define as regras com base no caminho em si.</span><span class="sxs-lookup"><span data-stu-id="01b65-129">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="01b65-130">**Configurações Básicas**</span><span class="sxs-lookup"><span data-stu-id="01b65-130">**Basic Settings**</span></span>

* <span data-ttu-id="01b65-131">**Nome** – esse valor é um nome amigável para a regra que está acessível no portal.</span><span class="sxs-lookup"><span data-stu-id="01b65-131">**Name** - This value is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="01b65-132">**Ouvinte** – esse valor é o ouvinte usado para a regra.</span><span class="sxs-lookup"><span data-stu-id="01b65-132">**Listener** - This value is the listener that is used for the rule.</span></span>
* <span data-ttu-id="01b65-133">**Pool de back-end padrão** : essa configuração é a que define o back-end a ser usado para a regra padrão</span><span class="sxs-lookup"><span data-stu-id="01b65-133">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="01b65-134">**Configurações HTTP padrão** : essa configuração é a que define as configurações HTTP a serem usadas para a regra padrão.</span><span class="sxs-lookup"><span data-stu-id="01b65-134">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="01b65-135">**Regras com base no caminho**</span><span class="sxs-lookup"><span data-stu-id="01b65-135">**Path-based rules**</span></span>

* <span data-ttu-id="01b65-136">**Nome** – esse valor é um nome amigável para a regra com base no caminho.</span><span class="sxs-lookup"><span data-stu-id="01b65-136">**Name** - This value is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="01b65-137">**Caminhos** – essa configuração define o caminho que a regra procura ao encaminhar o tráfego</span><span class="sxs-lookup"><span data-stu-id="01b65-137">**Paths** - This setting defines the path the rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="01b65-138">**Pool de back-end** : essa configuração é a que define o back-end a ser usado para a regra padrão</span><span class="sxs-lookup"><span data-stu-id="01b65-138">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="01b65-139">**Configuração HTTP** : essa configuração é a que define as configurações HTTP a serem usadas para a regra.</span><span class="sxs-lookup"><span data-stu-id="01b65-139">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01b65-140">Caminhos: a lista de padrões de caminho para correspondência.</span><span class="sxs-lookup"><span data-stu-id="01b65-140">Paths: The list of path patterns to match.</span></span> <span data-ttu-id="01b65-141">Cada um deve começar com /, e o único lugar no qual um "\*" é permitido é no final.</span><span class="sxs-lookup"><span data-stu-id="01b65-141">Each must start with / and the only place a "\*" is allowed is at the end.</span></span> <span data-ttu-id="01b65-142">Exemplos válidos são /xyz, /xyz* ou /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="01b65-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Folha Adicionar regra com base no caminho com informações preenchidas][2]

<span data-ttu-id="01b65-144">Adicionar uma regra com base no caminho a um gateway de aplicativo existente é um processo fácil por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="01b65-144">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="01b65-145">Após uma regra com base no caminho ser sido criada, ela poderá ser editada para adicionar mais regras.</span><span class="sxs-lookup"><span data-stu-id="01b65-145">After a path-based rule has been created, it can be edited to add additional rules.</span></span> 

![adicionando mais regras com base no caminho][3]

<span data-ttu-id="01b65-147">Essa etapa configura uma rota com base no caminho.</span><span class="sxs-lookup"><span data-stu-id="01b65-147">This step configures a path-based route.</span></span> <span data-ttu-id="01b65-148">É importante entender que as solicitações não são reescritas; à medida que as solicitações chegam, o Gateway de Aplicativo inspeciona a solicitação e a regra básica no padrão de URL envia a solicitação para o back-end apropriado.</span><span class="sxs-lookup"><span data-stu-id="01b65-148">It is important to understand that requests are not rewritten, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01b65-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01b65-149">Next steps</span></span>

<span data-ttu-id="01b65-150">Para saber como configurar o descarregamento SSL com o Gateway de Aplicativo do Azure, veja [Configurar descarregamento SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="01b65-150">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
