---
title: "aaaAzure cobrança Enterprise APIs - PriceSheet | Microsoft Docs"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>APIs de Relatórios para clientes Enterprise – PriceSheet

Olá API de folha de preço fornece taxa aplicável Olá para cada medidor para Olá dado registro e o período de cobrança.

##<a name="request"></a>Solicitação
Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md). Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados.

|Método | URI da solicitação|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|GET|https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/billingPeriods/{períododeCobrança}/pricesheet|

> [!Note]
> versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.
>

## <a name="response"></a>Resposta

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Se você estiver usando Olá API da visualização, o campo meterId não está disponível.
>

**Definições da propriedade de resposta**

|Nome da Propriedade| Tipo| Descrição
|-|-|-|
|ID| string| Olá Id exclusiva que representa um item específico do PriceSheet (medidor por período de cobrança)|
|billingPeriodId| string| Olá Id exclusiva que representa um determinado período de cobrança|
|meterId| string| Identificador Olá medidor hello. Ele pode ser mapeado toohello meterId de uso.|
|meterName| string| nome do medidor Olá|
|unitOfMeasure| string| saudação de unidade de medida para medir o serviço Olá|
|includedQuantity| decimal| Quantidade incluída |
|partNumber| string| número de peça Olá associado Olá medidor|
|unitPrice| decimal| preço unitário Olá medidor Olá|
|currencyCode| string| código de moeda Olá para unitPrice Olá|
<br/>
## <a name="see-also"></a>Consulte também

* [API dos períodos de cobrança](billing-enterprise-api-billing-periods.md)

* [API de detalhes do uso](billing-enterprise-api-usage-detail.md)

* [API de saldo e resumo](billing-enterprise-api-balance-summary.md)

* [API do custo de armazenamento do Marketplace](billing-enterprise-api-marketplace-storecharge.md)
