---
title: aaaCustomize regras de firewall de aplicativo web no Gateway do aplicativo do Azure - portal do Azure | Microsoft Docs
description: "Este artigo fornece informações sobre como o firewall do aplicativo web toocustomize as regras no Application Gateway com hello portal do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="e8cb3-103">Personalizar regras de firewall do aplicativo web por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8cb3-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8cb3-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8cb3-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="e8cb3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8cb3-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="e8cb3-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="e8cb3-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="e8cb3-107">firewall do aplicativo web do Hello Azure Application Gateway (WAF) fornece proteção para aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="e8cb3-108">Essas proteções são fornecidas pelo Olá Web aplicativo segurança projeto (OWASP) abra Core regra definida (CRS).</span><span class="sxs-lookup"><span data-stu-id="e8cb3-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="e8cb3-109">Algumas regras podem causar falsos positivos e bloquear o tráfego real.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="e8cb3-110">Por esse motivo, o Application Gateway fornece regras e grupos de regras do hello recurso toocustomize.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="e8cb3-111">Para obter mais informações sobre regras e grupos de regras específicas de hello, consulte [lista de regras e grupos de regras do web aplicativo firewall CRS](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e8cb3-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="e8cb3-112">Se seu gateway de aplicativo não está usando a camada de WAF hello, Olá opção tooupgrade Olá gateway toohello WAF camada de aplicativo aparecerá no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="e8cb3-114">Exibir grupos de regras e regras</span><span class="sxs-lookup"><span data-stu-id="e8cb3-114">View rule groups and rules</span></span>

<span data-ttu-id="e8cb3-115">**regras e grupos de regras de tooview**</span><span class="sxs-lookup"><span data-stu-id="e8cb3-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="e8cb3-116">Procurar toohello gateway de aplicativo e, em seguida, selecione **firewall do aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="e8cb3-117">Selecione **Configuração de regra avançada**.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="e8cb3-118">Essa exibição mostra uma tabela na página de saudação de todos os grupos de regras de saudação fornecido com hello escolhido o conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="e8cb3-119">Todas as caixas de seleção da regra Olá são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-119">All of hello rule's check boxes are selected.</span></span>

![Configurar regras desabilitadas][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="e8cb3-121">Procure regras toodisable</span><span class="sxs-lookup"><span data-stu-id="e8cb3-121">Search for rules toodisable</span></span>

<span data-ttu-id="e8cb3-122">Olá **configurações de firewall do aplicativo da Web** folha fornece a capacidade de saudação regras de saudação toofilter por meio de uma pesquisa de texto.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="e8cb3-123">resultado de saudação exibe apenas grupos de regras de saudação e regras que contêm o texto de saudação procurado.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Pesquisar por regras][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="e8cb3-125">Desabilitar regras e grupos de regras</span><span class="sxs-lookup"><span data-stu-id="e8cb3-125">Disable rule groups and rules</span></span>

<span data-ttu-id="e8cb3-126">Quando está desabilitando regras, você pode desabilitar um grupo de regras inteiro ou regras específicas em um ou mais grupos de regras.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="e8cb3-127">**grupos de regras de toodisable ou regras específicas**</span><span class="sxs-lookup"><span data-stu-id="e8cb3-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="e8cb3-128">Pesquisar regras hello ou grupos de regras que você deseja toodisable.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="e8cb3-129">Desmarque as caixas de seleção de saudação para Olá regras que você deseja toodisable.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="e8cb3-130">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-130">Select **Save**.</span></span> 

![Salvar alterações][3]

## <a name="next-steps"></a><span data-ttu-id="e8cb3-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8cb3-132">Next steps</span></span>

<span data-ttu-id="e8cb3-133">Depois de configurar as regras desabilitadas, você pode aprender como tooview seus logs de WAF.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="e8cb3-134">Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="e8cb3-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
