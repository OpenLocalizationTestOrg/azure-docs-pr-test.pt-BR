---
title: "aaaAzure cobrança Enterprise APIs - encargos do Marketplace | Microsoft Docs"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>APIs de Relatórios para clientes Enterprise – Custos de Armazenamento do Marketplace

Olá API de custos de armazenamento do Marketplace retorna Olá baseada no uso marketplace encargos divisão por dia para Olá especificado o período de cobrança ou datas de início e término (taxas de uma vez não estão incluídas).

##<a name="request"></a>Solicitação 
Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md). Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados. Intervalos de tempo personalizado podem ser especificados com o início do hello e terminar parâmetros de data que estão no tempo de saudação formato AAAA-MM-dd, Olá máximo com suporte intervalo é de 36 meses.  

|Método | URI da solicitação|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/billingPeriods/{períododeCobrança}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{númerodaInscrição}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.
>

## <a name="response"></a>Resposta
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Definições da propriedade de resposta**

|Nome da Propriedade| Tipo| Descrição
|-|-|-|
|ID|string|Id exclusiva para o item de cobrança do marketplace Olá|
|subscriptionGuid|Guid|Olá Guid de assinatura|
|subscriptionName|string|Olá, nome da assinatura|
|meterId|string|ID de saudação emitido medidor|
|usageStartDate|Datetime|Hora de início para o registro de uso de saudação|
|usageEndDate|Datetime|Hora de término para o registro de uso de saudação|
|offerName|string|nome da oferta Olá|
|resourceGroup|string|Grupo de recursos de saudação|
|instanceId|string|ID da instância|
|additionalInfo|string|Cadeia de caracteres JSON de informações adicionais|
|marcas|string|Cadeia de caracteres JSON da marca|
|orderNumber|string|número de ordem de saudação|
|unitOfMeasure|string|Unidade de medida para o medidor Olá|
|costCenter|string|Centro de custo de saudação|
|accountId|int|conta de saudação Id|
|accountName|string |Olá, nome da conta|
|accountOwnerId|string|Olá Id de proprietário de conta|
|departmentId|int|departamento de saudação Id|
|departmentName|string|nome do departamento de saudação|
|publisherName|string|nome do publicador Olá|
|planName|string|nome do plano de saudação|
|consumedQuantity|decimal|Quantidade consumida durante esse período|
|resourceRate|decimal|Preço unitário medidor Olá|
|extendedCost|decimal|Cobrança estimada com base na quantidade consumida e no custo estendido|
<br/>
## <a name="see-also"></a>Consulte também

* [API dos períodos de cobrança](billing-enterprise-api-billing-periods.md)

* [API de detalhes do uso](billing-enterprise-api-usage-detail.md) 

* [API de saldo e resumo](billing-enterprise-api-balance-summary.md)

* [API da folha de preço](billing-enterprise-api-pricesheet.md)