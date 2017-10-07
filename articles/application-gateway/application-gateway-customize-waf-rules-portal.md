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
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Personalizar regras de firewall do aplicativo web por meio de saudação portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI 2.0 do Azure](application-gateway-customize-waf-rules-cli.md)

firewall do aplicativo web do Hello Azure Application Gateway (WAF) fornece proteção para aplicativos da web. Essas proteções são fornecidas pelo Olá Web aplicativo segurança projeto (OWASP) abra Core regra definida (CRS). Algumas regras podem causar falsos positivos e bloquear o tráfego real. Por esse motivo, o Application Gateway fornece regras e grupos de regras do hello recurso toocustomize. Para obter mais informações sobre regras e grupos de regras específicas de hello, consulte [lista de regras e grupos de regras do web aplicativo firewall CRS](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Se seu gateway de aplicativo não está usando a camada de WAF hello, Olá opção tooupgrade Olá gateway toohello WAF camada de aplicativo aparecerá no painel direito da saudação. 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>Exibir grupos de regras e regras

**regras e grupos de regras de tooview**
   1. Procurar toohello gateway de aplicativo e, em seguida, selecione **firewall do aplicativo Web**.  
   2. Selecione **Configuração de regra avançada**.  
   Essa exibição mostra uma tabela na página de saudação de todos os grupos de regras de saudação fornecido com hello escolhido o conjunto de regras. Todas as caixas de seleção da regra Olá são selecionadas.

![Configurar regras desabilitadas][1]

## <a name="search-for-rules-toodisable"></a>Procure regras toodisable

Olá **configurações de firewall do aplicativo da Web** folha fornece a capacidade de saudação regras de saudação toofilter por meio de uma pesquisa de texto. resultado de saudação exibe apenas grupos de regras de saudação e regras que contêm o texto de saudação procurado.

![Pesquisar por regras][2]

## <a name="disable-rule-groups-and-rules"></a>Desabilitar regras e grupos de regras

Quando está desabilitando regras, você pode desabilitar um grupo de regras inteiro ou regras específicas em um ou mais grupos de regras. 

**grupos de regras de toodisable ou regras específicas**

   1. Pesquisar regras hello ou grupos de regras que você deseja toodisable.
   2. Desmarque as caixas de seleção de saudação para Olá regras que você deseja toodisable. 
   2. Selecione **Salvar**. 

![Salvar alterações][3]

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as regras desabilitadas, você pode aprender como tooview seus logs de WAF. Para obter mais informações, consulte [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
