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
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Personalizar as regras de firewall de aplicativo Web por meio do PowerShell

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI 2.0 do Azure](application-gateway-customize-waf-rules-cli.md)

firewall do aplicativo web do Hello Azure Application Gateway (WAF) fornece proteção para aplicativos da web. Essas proteções são fornecidas pelo Olá Web aplicativo segurança projeto (OWASP) abra Core regra definida (CRS). Algumas regras podem causar falsos positivos e bloquear o tráfego real. Por esse motivo, o Application Gateway fornece regras e grupos de regras do hello recurso toocustomize. Para obter mais informações sobre regras e grupos de regras específicas de hello, consulte [lista de grupos de CRS regra de firewall de aplicativos web e regras](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Exibir grupos de regras e regras

Olá, exemplos de código a seguir mostra como tooview regras e grupos que podem ser configurados em um gateway do aplicativo habilitado para WAF de regras.

### <a name="view-rule-groups"></a>Exibir grupos de regras

Olá mostrado no exemplo a seguir como tooview grupos de regras:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

saudação de saída a seguir é uma resposta truncada da saudação anterior de exemplo:

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

## <a name="disable-rules"></a>Desabilitar regras

Olá, exemplo a seguir desabilita regras `910018` e `910017` em um gateway de aplicativo:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as regras desabilitadas, você pode aprender como tooview seus logs de WAF. Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
