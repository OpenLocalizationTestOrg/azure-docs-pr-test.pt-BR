---
title: "Personalizar regras de firewall do aplicativo Web no Gateway de Aplicativo do Azure – Portal do Azure | Microsoft Docs"
description: "Este artigo fornece informações sobre como personalizar regras de firewall de aplicativo Web no Gateway de Aplicativo com o portal do Azure."
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
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="01219-103">Personalizar regras de firewall de aplicativo Web por do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="01219-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01219-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="01219-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="01219-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01219-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="01219-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="01219-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="01219-107">O WAF (firewall de aplicativo Web) do Gateway de Aplicativo do Azure fornece proteção para aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="01219-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="01219-108">Essas proteções são fornecidas pelo CRS (conjunto de regras principais) do OWASP (Open Web Application Security Project).</span><span class="sxs-lookup"><span data-stu-id="01219-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="01219-109">Algumas regras podem causar falsos positivos e bloquear o tráfego real.</span><span class="sxs-lookup"><span data-stu-id="01219-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="01219-110">Por esse motivo, o Gateway de Aplicativo possibilita que a capacidade personalize regras e grupos de regras.</span><span class="sxs-lookup"><span data-stu-id="01219-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="01219-111">Para obter mais informações sobre os grupos de regras e as regras específicas, consulte a [Lista de regras e grupos de regras de CRS do firewall de aplicativo Web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="01219-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="01219-112">Se o gateway de aplicativo não estiver usando a camada WAF, será exibida no painel direito a opção de atualizar o gateway de aplicativo para a camada WAF.</span><span class="sxs-lookup"><span data-stu-id="01219-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="01219-114">Exibir grupos de regras e regras</span><span class="sxs-lookup"><span data-stu-id="01219-114">View rule groups and rules</span></span>

<span data-ttu-id="01219-115">**Para exibir grupos de regras e regras**</span><span class="sxs-lookup"><span data-stu-id="01219-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="01219-116">Navegue até o gateway de aplicativo e selecione **Firewall do aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="01219-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="01219-117">Selecione **Configuração de regra avançada**.</span><span class="sxs-lookup"><span data-stu-id="01219-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="01219-118">Essa exibição mostra uma tabela na página com todos os grupos de regras fornecidos com o conjunto de regras escolhido.</span><span class="sxs-lookup"><span data-stu-id="01219-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="01219-119">Todas as caixas de seleção de regra são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="01219-119">All of the rule's check boxes are selected.</span></span>

![Configurar regras desabilitadas][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="01219-121">Pesquisar pelas regras a desabilitar</span><span class="sxs-lookup"><span data-stu-id="01219-121">Search for rules to disable</span></span>

<span data-ttu-id="01219-122">A folha **Configurações de firewall do aplicativo Web** possibilita que a capacidade filtre as regras usando uma pesquisa de texto.</span><span class="sxs-lookup"><span data-stu-id="01219-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="01219-123">O resultado exibe apenas grupos de regras e regras que contêm o texto que você pesquisou.</span><span class="sxs-lookup"><span data-stu-id="01219-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Pesquisar por regras][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="01219-125">Desabilitar regras e grupos de regras</span><span class="sxs-lookup"><span data-stu-id="01219-125">Disable rule groups and rules</span></span>

<span data-ttu-id="01219-126">Quando está desabilitando regras, você pode desabilitar um grupo de regras inteiro ou regras específicas em um ou mais grupos de regras.</span><span class="sxs-lookup"><span data-stu-id="01219-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="01219-127">**Para desabilitar regras específicas ou grupos de regras**</span><span class="sxs-lookup"><span data-stu-id="01219-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="01219-128">Pesquise pelas regras ou os grupos de regras que você deseja desabilitar.</span><span class="sxs-lookup"><span data-stu-id="01219-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="01219-129">Desmarque as caixas de seleção das regras que deseja desabilitar.</span><span class="sxs-lookup"><span data-stu-id="01219-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="01219-130">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="01219-130">Select **Save**.</span></span> 

![Salvar alterações][3]

## <a name="next-steps"></a><span data-ttu-id="01219-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01219-132">Next steps</span></span>

<span data-ttu-id="01219-133">Depois de configurar as regras desabilitadas, você pode aprender como exibir os logs de WAF.</span><span class="sxs-lookup"><span data-stu-id="01219-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="01219-134">Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="01219-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
