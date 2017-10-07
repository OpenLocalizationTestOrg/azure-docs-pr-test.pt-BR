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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>Personalizar regras de firewall do aplicativo web por meio de saudação 2.0 do CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI 2.0 do Azure](application-gateway-customize-waf-rules-cli.md)

firewall do aplicativo web do Hello Azure Application Gateway (WAF) fornece proteção para aplicativos da web. Essas proteções são fornecidas pelo Olá Web aplicativo segurança projeto (OWASP) abra Core regra definida (CRS). Algumas regras podem causar falsos positivos e bloquear o tráfego real. Por esse motivo, o Application Gateway fornece regras e grupos de regras do hello recurso toocustomize. Para obter mais informações sobre regras e grupos de regras específicas de hello, consulte [lista de regras e grupos de regras do web aplicativo firewall CRS](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Exibir grupos de regras e regras

Olá, exemplos de código a seguir mostra como tooview regras e grupos que podem ser configurados de regras.

### <a name="view-rule-groups"></a>Exibir grupos de regras

saudação de exemplo a seguir mostra como tooview Olá grupos de regras:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

saudação de saída a seguir é uma resposta truncada da saudação anterior de exemplo:

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

### <a name="view-rules-in-a-rule-group"></a>Exibir regras em um grupo de regras

saudação de exemplo a seguir mostra como tooview as regras em um grupo de regras especificado:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

saudação de saída a seguir é uma resposta truncada da saudação anterior de exemplo:

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

## <a name="disable-rules"></a>Desabilitar regras

Olá, exemplo a seguir desabilita regras `910018` e `910017` em um gateway de aplicativo:

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as regras desabilitadas, você pode aprender como tooview seus logs de WAF. Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
