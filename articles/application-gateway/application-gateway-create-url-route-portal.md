---
title: aaaCreate um caminho com base em regra - Gateway de aplicativo do Azure - Portal do Azure | Microsoft Docs
description: "Saiba como toocreate uma regra de caminho para um gateway de aplicativo usando Olá portal"
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="d6df5-103">Criar uma regra de caminho para um gateway de aplicativo usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="d6df5-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6df5-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d6df5-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="d6df5-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d6df5-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="d6df5-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="d6df5-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="d6df5-107">Roteamento baseado no caminho de URL permite que você tooassociate rotas com base no caminho de URL de saudação de solicitação Http.</span><span class="sxs-lookup"><span data-stu-id="d6df5-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="d6df5-108">Ele verifica se há um pool de back-end de tooa rota configurado para URL Olá listado no hello Application Gateway e envia Olá toohello de tráfego de rede definida pelo pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="d6df5-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="d6df5-109">Um uso comum para roteamento baseado em URL é equilibrar solicitações de tooload para pools de toodifferent de diferentes tipos de conteúdo do servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="d6df5-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="d6df5-110">Roteamento baseado em URL apresenta um novo gateway de tooapplication do tipo de regra.</span><span class="sxs-lookup"><span data-stu-id="d6df5-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="d6df5-111">O Gateway de Aplicativo tem dois tipos de regra: básica e com base no caminho.</span><span class="sxs-lookup"><span data-stu-id="d6df5-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="d6df5-112">Olá tipo de regra básica, fornece serviço de round-robin para Olá back-end pools ao regras com base no caminho de distribuição de rodízio tooround Além disso, também leva padrão de caminho da URL de solicitação de saudação em consideração ao escolher o pool de back-end apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6df5-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="d6df5-113">Cenário</span><span class="sxs-lookup"><span data-stu-id="d6df5-113">Scenario</span></span>

<span data-ttu-id="d6df5-114">Olá cenário a seguir passa por criar uma regra de caminho baseado em um gateway existente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6df5-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="d6df5-115">Olá cenário pressupõe que você já seguiu as etapas de saudação muito[criar um Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6df5-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![roteamento de url][scenario]

## <span data-ttu-id="d6df5-117"><a name="createrule"></a>Criar regra de caminho baseado Olá</span><span class="sxs-lookup"><span data-stu-id="d6df5-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="d6df5-118">Uma regra de caminho requer seu próprio ouvinte, antes de criar a regra de saudação ser tooverify se você tiver um ouvinte disponível toouse.</span><span class="sxs-lookup"><span data-stu-id="d6df5-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="d6df5-119">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="d6df5-119">Step 1</span></span>

<span data-ttu-id="d6df5-120">Navegue toohello [portal do Azure](http://portal.azure.com) e selecione um gateway existente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6df5-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="d6df5-121">Clique em **Regras**</span><span class="sxs-lookup"><span data-stu-id="d6df5-121">Click **Rules**</span></span>

![Visão geral do Gateway de Aplicativo][1]

### <a name="step-2"></a><span data-ttu-id="d6df5-123">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="d6df5-123">Step 2</span></span>

<span data-ttu-id="d6df5-124">Clique em **baseados no caminho** botão tooadd uma nova regra de caminho baseado.</span><span class="sxs-lookup"><span data-stu-id="d6df5-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="d6df5-125">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="d6df5-125">Step 3</span></span>

<span data-ttu-id="d6df5-126">Olá **Adicionar regra de caminho com base em** folha tem duas seções.</span><span class="sxs-lookup"><span data-stu-id="d6df5-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="d6df5-127">Olá primeira seção é onde você definiu o ouvinte Olá, nome de saudação da regra de saudação e configurações de caminho saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="d6df5-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="d6df5-128">configurações de caminho saudação padrão são para rotas que não pertencem a rota Olá personalizados baseados no caminho.</span><span class="sxs-lookup"><span data-stu-id="d6df5-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="d6df5-129">Olá a segunda seção do hello **Adicionar regra de caminho com base em** folha é onde você define regras baseadas no caminho Olá próprios.</span><span class="sxs-lookup"><span data-stu-id="d6df5-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="d6df5-130">**Configurações Básicas**</span><span class="sxs-lookup"><span data-stu-id="d6df5-130">**Basic Settings**</span></span>

* <span data-ttu-id="d6df5-131">**Nome** -este valor é uma regra de toohello nome amigável que pode ser acessada no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6df5-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="d6df5-132">**Ouvinte** -este valor é o ouvinte de saudação que é usado para a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6df5-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="d6df5-133">**Padrão de pool de back-end** -essa configuração é a configuração de saudação que define Olá toobe de back-end usado para a regra padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="d6df5-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="d6df5-134">**Configurações de HTTP padrão** -essa configuração é a configuração de saudação que define Olá toobe de configurações de HTTP usado para a regra padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6df5-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="d6df5-135">**Regras com base no caminho**</span><span class="sxs-lookup"><span data-stu-id="d6df5-135">**Path-based rules**</span></span>

* <span data-ttu-id="d6df5-136">**Nome** -este valor é uma regra de toopath com base no nome amigável.</span><span class="sxs-lookup"><span data-stu-id="d6df5-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="d6df5-137">**Caminhos** -essa configuração define Olá caminho Olá regra procura ao encaminhar o tráfego</span><span class="sxs-lookup"><span data-stu-id="d6df5-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="d6df5-138">**Pool de back-end** -essa configuração é a configuração de saudação que define Olá toobe de back-end usado para a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="d6df5-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="d6df5-139">**Configuração de HTTP** -essa configuração é a configuração de saudação que define Olá toobe de configurações de HTTP usado para a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6df5-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6df5-140">Caminhos: lista de saudação de toomatch de padrões de caminho.</span><span class="sxs-lookup"><span data-stu-id="d6df5-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="d6df5-141">Cada deve começar com / e coloque-Olá somente um "\*" é permitido é final hello.</span><span class="sxs-lookup"><span data-stu-id="d6df5-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="d6df5-142">Exemplos válidos são /xyz, /xyz* ou /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="d6df5-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Folha Adicionar regra com base no caminho com informações preenchidas][2]

<span data-ttu-id="d6df5-144">Adicionar uma regra de caminho com tooan gateway existente do aplicativo é um processo fácil por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="d6df5-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="d6df5-145">Depois que uma regra de caminho tiver sido criada, pode ser editado tooadd mais regras.</span><span class="sxs-lookup"><span data-stu-id="d6df5-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![adicionando mais regras com base no caminho][3]

<span data-ttu-id="d6df5-147">Essa etapa configura uma rota com base no caminho.</span><span class="sxs-lookup"><span data-stu-id="d6df5-147">This step configures a path-based route.</span></span> <span data-ttu-id="d6df5-148">É importante toounderstand que solicitações não são reconfiguradas, à medida que solicitações no gateway do aplicativo inspeciona solicitação hello e basic Olá url padrão envia Olá solicitação toohello apropriado back-end.</span><span class="sxs-lookup"><span data-stu-id="d6df5-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6df5-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6df5-149">Next steps</span></span>

<span data-ttu-id="d6df5-150">toolearn como tooconfigure descarregamento de SSL com o Gateway de aplicativo do Azure, consulte [configurar descarregamento de SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d6df5-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
