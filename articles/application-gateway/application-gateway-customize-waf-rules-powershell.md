---
title: aaaCustomize regras de firewall de aplicativo web no Gateway do aplicativo do Azure - PowerShell | Microsoft Docs
description: "Este artigo fornece informações sobre como as regras de firewall do aplicativo web toocustomize no Application Gateway com o PowerShell."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="6d7f5-103">Personalizar as regras de firewall de aplicativo Web por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d7f5-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d7f5-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f5-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="6d7f5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d7f5-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="6d7f5-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f5-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="6d7f5-107">firewall do aplicativo web do Hello Azure Application Gateway (WAF) fornece proteção para aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="6d7f5-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="6d7f5-108">Essas proteções são fornecidas pelo Olá Web aplicativo segurança projeto (OWASP) abra Core regra definida (CRS).</span><span class="sxs-lookup"><span data-stu-id="6d7f5-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="6d7f5-109">Algumas regras podem causar falsos positivos e bloquear o tráfego real.</span><span class="sxs-lookup"><span data-stu-id="6d7f5-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="6d7f5-110">Por esse motivo, o Application Gateway fornece regras e grupos de regras do hello recurso toocustomize.</span><span class="sxs-lookup"><span data-stu-id="6d7f5-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="6d7f5-111">Para obter mais informações sobre regras e grupos de regras específicas de hello, consulte [lista de grupos de CRS regra de firewall de aplicativos web e regras](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f5-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="6d7f5-112">Exibir grupos de regras e regras</span><span class="sxs-lookup"><span data-stu-id="6d7f5-112">View rule groups and rules</span></span>

<span data-ttu-id="6d7f5-113">Olá, exemplos de código a seguir mostra como tooview regras e grupos que podem ser configurados em um gateway do aplicativo habilitado para WAF de regras.</span><span class="sxs-lookup"><span data-stu-id="6d7f5-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="6d7f5-114">Exibir grupos de regras</span><span class="sxs-lookup"><span data-stu-id="6d7f5-114">View rule groups</span></span>

<span data-ttu-id="6d7f5-115">Olá mostrado no exemplo a seguir como tooview grupos de regras:</span><span class="sxs-lookup"><span data-stu-id="6d7f5-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="6d7f5-116">saudação de saída a seguir é uma resposta truncada da saudação anterior de exemplo:</span><span class="sxs-lookup"><span data-stu-id="6d7f5-116">hello following output is a truncated response from hello preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="6d7f5-117">Desabilitar regras</span><span class="sxs-lookup"><span data-stu-id="6d7f5-117">Disable rules</span></span>

<span data-ttu-id="6d7f5-118">Olá, exemplo a seguir desabilita regras `910018` e `910017` em um gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6d7f5-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="6d7f5-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d7f5-119">Next steps</span></span>

<span data-ttu-id="6d7f5-120">Depois de configurar as regras desabilitadas, você pode aprender como tooview seus logs de WAF.</span><span class="sxs-lookup"><span data-stu-id="6d7f5-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="6d7f5-121">Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="6d7f5-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
