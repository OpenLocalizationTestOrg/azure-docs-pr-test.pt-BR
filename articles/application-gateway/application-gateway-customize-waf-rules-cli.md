---
title: aaaCustomize regras de firewall de aplicativo web no Gateway do aplicativo do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Este artigo fornece informações sobre como o firewall do aplicativo web toocustomize as regras no Application Gateway com hello 2.0 do CLI do Azure."
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
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="4ab68-103">Personalizar regras de firewall do aplicativo web por meio de saudação 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab68-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ab68-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab68-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="4ab68-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ab68-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="4ab68-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab68-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="4ab68-107">firewall do aplicativo web do Hello Azure Application Gateway (WAF) fornece proteção para aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="4ab68-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="4ab68-108">Essas proteções são fornecidas pelo Olá Web aplicativo segurança projeto (OWASP) abra Core regra definida (CRS).</span><span class="sxs-lookup"><span data-stu-id="4ab68-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="4ab68-109">Algumas regras podem causar falsos positivos e bloquear o tráfego real.</span><span class="sxs-lookup"><span data-stu-id="4ab68-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="4ab68-110">Por esse motivo, o Application Gateway fornece regras e grupos de regras do hello recurso toocustomize.</span><span class="sxs-lookup"><span data-stu-id="4ab68-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="4ab68-111">Para obter mais informações sobre regras e grupos de regras específicas de hello, consulte [lista de regras e grupos de regras do web aplicativo firewall CRS](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="4ab68-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="4ab68-112">Exibir grupos de regras e regras</span><span class="sxs-lookup"><span data-stu-id="4ab68-112">View rule groups and rules</span></span>

<span data-ttu-id="4ab68-113">Olá, exemplos de código a seguir mostra como tooview regras e grupos que podem ser configurados de regras.</span><span class="sxs-lookup"><span data-stu-id="4ab68-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="4ab68-114">Exibir grupos de regras</span><span class="sxs-lookup"><span data-stu-id="4ab68-114">View rule groups</span></span>

<span data-ttu-id="4ab68-115">saudação de exemplo a seguir mostra como tooview Olá grupos de regras:</span><span class="sxs-lookup"><span data-stu-id="4ab68-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="4ab68-116">saudação de saída a seguir é uma resposta truncada da saudação anterior de exemplo:</span><span class="sxs-lookup"><span data-stu-id="4ab68-116">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="4ab68-117">Exibir regras em um grupo de regras</span><span class="sxs-lookup"><span data-stu-id="4ab68-117">View rules in a rule group</span></span>

<span data-ttu-id="4ab68-118">saudação de exemplo a seguir mostra como tooview as regras em um grupo de regras especificado:</span><span class="sxs-lookup"><span data-stu-id="4ab68-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="4ab68-119">saudação de saída a seguir é uma resposta truncada da saudação anterior de exemplo:</span><span class="sxs-lookup"><span data-stu-id="4ab68-119">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="4ab68-120">Desabilitar regras</span><span class="sxs-lookup"><span data-stu-id="4ab68-120">Disable rules</span></span>

<span data-ttu-id="4ab68-121">Olá, exemplo a seguir desabilita regras `910018` e `910017` em um gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="4ab68-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="4ab68-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ab68-122">Next steps</span></span>

<span data-ttu-id="4ab68-123">Depois de configurar as regras desabilitadas, você pode aprender como tooview seus logs de WAF.</span><span class="sxs-lookup"><span data-stu-id="4ab68-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="4ab68-124">Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="4ab68-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
