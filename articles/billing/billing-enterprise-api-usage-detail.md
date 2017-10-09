---
title: "aaaAzure cobrança Enterprise APIs - detalhes de uso | Microsoft Docs"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>APIs de Relatórios para clientes Enterprise – detalhes de uso

API de detalhes de uso de saudação oferece um detalhamento diário das quantidades consumidas e encargos estimados por um registro. resultado de saudação também inclui informações sobre instâncias, medidores e departamentos. Olá API pode ser consultada por período de cobrança ou de início especificado e a data de término. 
## <a name="consumption-apis"></a>APIs de consumo


##<a name="request"></a>Solicitação 
Propriedades de cabeçalho comuns que precisam toobe adicionado são especificadas [aqui](billing-enterprise-api.md). Se não for especificado um período de cobrança, em seguida, dados de cobrança atual Olá período são retornados. Intervalos de tempo personalizado podem ser especificados com o início do hello e terminar parâmetros de data que estão em Olá formato AAAA-MM-DD. intervalo de tempo com suporte máximo Olá é 36 meses.  

|Método | URI da solicitação|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> versão de visualização de saudação toouse da API, substitua v2 v1 no hello acima URL.
>

## <a name="response"></a>Resposta

> Devido a toohello potencialmente grande volume de resultado da saudação dados conjunto é paginado. propriedade de nextLink Olá, se presente, especifica o link de saudação para a próxima página Olá de dados. Se o link de saudação estiver vazio, indica que que é Olá última página. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Definições da propriedade de resposta**

|Nome da Propriedade| Tipo| Descrição
|-|-|-|
|ID| string| Olá Id exclusiva para a chamada de API de saudação. |
|data| Matriz JSON| Olá matriz de detalhes de uso diário para cada instance\meter.|
|nextLink| string| Quando há mais páginas de dados Olá nextLink toohello URL tooreturn Olá próxima página pontos de dados. |
|accountId| int| Campo obsoleto. Presente para a compatibilidade com versões anteriores. |
|productId| int| Campo obsoleto. Presente para a compatibilidade com versões anteriores. |
|resourceLocationId| int| Campo obsoleto. Presente para a compatibilidade com versões anteriores. |
|consumedServiceID| int| Campo obsoleto. Presente para a compatibilidade com versões anteriores. |
|departmentId| int| Campo obsoleto. Presente para a compatibilidade com versões anteriores. |
|accountOwnerEmail| string| Conta de email do proprietário da conta de saudação. |
|accountName| string| Nome de cliente informado da conta de saudação. |
|serviceAdministratorId| string| Endereço de email do Administrador de serviços. |
|subscriptionId| int| Campo obsoleto. Presente para a compatibilidade com versões anteriores. |
|subscriptionGuid| string| Identificador global exclusivo para a assinatura de saudação. |
|subscriptionName| string| Nome da assinatura de saudação. |
|data| string| Data de saudação em que ocorreu o consumo. |
|product| string| Detalhes adicionais no medidor hello. Exemplo: A1(VM)Windows – Leste do Pacífico Asiático|
|meterId| string| Identificador Olá medidor Olá que emitidos de uso. |
|meterCategory| string| Olá serviços da plataforma Azure que foi usado. |
|meterSubCategory| string| Define o tipo de serviço do Azure de saudação que pode afetar a taxa de saudação. Exemplo: VM A1 (não Windows|
|meterRegion| string| Identifica o local de saudação do datacenter Olá para determinados serviços que são cobradas com base na localização do datacenter. |
|meterName| string| Nome do medidor de saudação. |
|consumedQuantity| double| quantidade de saudação do medidor de saudação que foi consumido. |
|resourceRate| double| taxa de saudação aplicável unitário faturável. |
|cost| double| encargo de saudação incorrido para medidor hello. |
|resourceLocation| string| Identifica Olá datacenter onde medidor hello está sendo executado. |
|consumedService| string| Olá serviços da plataforma Azure que foi usado. |
|instanceId| string| Esse identificador é o nome de saudação do recurso de saudação ou Olá totalmente qualificados ID de recurso. Para saber mais, confira [API do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources) |
|serviceInfo1| string| Metadados de serviço interno do Azure. |
|serviceInfo2| string| Por exemplo, um tipo de imagem para uma máquina virtual e o nome do ISP para o ExpressRoute. |
|additionalInfo| string| Metadados específicos ao serviço. Por exemplo, um tipo de imagem para uma máquina virtual. |
|marcas| string| Marcas adicionadas pelo cliente. Para saber mais, confira [Organizar os recursos do Azure com marcas](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| string| Essa coluna não é usada. Presente para a compatibilidade com versões anteriores. |
|departmentName| string| Nome do departamento de saudação. |
|costCenter| string| Centro de custo de saudação uso hello está associado. |
|unitOfMeasure| string| Identifica a unidade Olá cobrado no serviço de saudação. Por exemplo, GB, horas, 10.000 s. |
|resourceGroup| string| grupo de recursos Olá no qual hello está sendo executado no medidor implantado. Para saber mais, consulte [Visão geral do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Consulte também

* [API dos períodos de cobrança](billing-enterprise-api-billing-periods.md)

* [API de saldo e resumo](billing-enterprise-api-balance-summary.md)

* [API do custo de armazenamento do Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [API da folha de preço](billing-enterprise-api-pricesheet.md)
