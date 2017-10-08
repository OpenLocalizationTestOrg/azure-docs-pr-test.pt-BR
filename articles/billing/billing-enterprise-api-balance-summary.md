---
title: "aaaAzure cobrança Enterprise APIs - saldo e resumo | Microsoft Docs"
description: "Saiba mais sobre o uso de cobrança do Azure e APIs RateCard, que são insights tooprovide usados para consumo de recursos do Azure e tendências."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>APIs de Relatórios para clientes Enterprise – Saldo e Resumo

Olá equilíbrio e a API de resumo oferece um resumo mensal de informações sobre saldos, novas aquisições, tarifas do serviço Azure Marketplace, ajustes e encargos de excedentes.


##<a name="request"></a>Solicitação 
Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md). Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados.

|Método | URI da solicitação|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary|

> [!Note]
> versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.
>

## <a name="response"></a>Resposta

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Definições da propriedade de resposta**

|Nome da Propriedade| Tipo| Descrição
|-|-|-|
|ID|string|Olá Id exclusiva para um determinado período de cobrança e registro|
|billingPeriodId|string |Olá Id do período de cobrança|
|currencyCode|string |código de moeda Olá|
|beginningBalance|decimal| saldo inicial de Olá Olá período de faturamento|
|endingBalance|decimal| Olá saldo final para o período de cobrança hello (para períodos abertos que isso será atualizado diariamente)|
|newPurchases|decimal| Valor total da nova compra|
|adjustments|decimal| Valor total do ajuste|
|utilized|decimal| Uso total do compromisso|
|serviceOverage|decimal| Excedente dos serviços do Azure|
|chargesBilledSeparately|decimal| Encargos cobrados separadamente|
|totalOverage|decimal| serviceOverage + chargesBilledSeparately|
|totalUsage|decimal| Compromisso do serviço do Azure + excedente total|
|azureMarketplaceServiceCharges|decimal| Total de encargos do Azure Marketplace|
|newPurchasesDetails|Matriz de cadeias de caracteres JSON de pares de nome e valor|Lista de novas compras|
|adjustmentDetails|Matriz de cadeias de caracteres JSON de pares de nome e valor|Lista de ajustes (crédito de promoção, crédito SIE etc.) |


<br/>
## <a name="see-also"></a>Consulte também

* [API dos períodos de cobrança](billing-enterprise-api-billing-periods.md)

* [API de detalhes do uso](billing-enterprise-api-usage-detail.md) 

* [API do custo de armazenamento do Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API da folha de preço](billing-enterprise-api-pricesheet.md)