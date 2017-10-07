---
title: "aaaAzure cobrança Enterprise APIs - períodos de cobrança | Microsoft Docs"
description: "Saiba mais sobre Olá APIs de relatórios que permitem que os dados de consumo do Azure Enterprise clientes toopull programaticamente."
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>APIs de Relatórios para clientes Enterprise – Períodos de Cobrança

Olá cobrança períodos API retorna uma lista de cobrança períodos com dados de consumo para Olá especificado registro em ordem cronológica inversa. Cada período contém uma propriedade apontando toohello rota de API para Olá quatro conjuntos de dados - BalanceSummary, UsageDetails, Marktplace encargos e PriceSheet. Se o período de saudação não tiver dados, propriedade correspondente Olá é nula. 


##<a name="request"></a>Solicitação 
Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md). 

|Método | URI da solicitação|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.
>

## <a name="response"></a>Resposta
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Definições da propriedade de resposta**

|Nome da Propriedade| Tipo| Descrição
|-|-|-|
|billingPeriodId| string| Olá Id exclusiva que representa um determinado período de cobrança|
|billingStart| datetime| Cadeia de caracteres ISO 8601 que representa a data de início do período de saudação|
|billingEnd| datetime| Cadeia de caracteres ISO 8601 que representa a data de término do período de saudação|
|balanceSummary| string| caminho de URL de saudação que encaminha os dados de resumo de saldo de toohello para esse período|
|usageDetails| string| caminho de URL de saudação que roteia toohello dados de detalhes de uso para esse período|
|marketplaceCharges| string| caminho da URL Olá que encaminha dados de encargos do Marketplace toohello para esse período|
|priceSheet| string| caminho de URL de saudação que roteia toohello PriceSheet dados para esse período|

<br/>
## <a name="see-also"></a>Consulte também

* [API de saldo e resumo](billing-enterprise-api-balance-summary.md)

* [API de detalhes do uso](billing-enterprise-api-usage-detail.md) 

* [API do custo de armazenamento do Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API da folha de preço](billing-enterprise-api-pricesheet.md)