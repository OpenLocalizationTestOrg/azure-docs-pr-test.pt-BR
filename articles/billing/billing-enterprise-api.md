---
title: "aaaAzure cobrança Enterprise APIs | Microsoft Docs"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Visão geral das APIs de Relatórios para clientes Enterprise
Olá Reporting APIs permitem que o consumo do Azure Enterprise clientes tooprogrammatically pull e dados de cobrança em ferramentas de análise de dados preferencial. 

## <a name="enabling-data-access-toohello-api"></a>Habilitando a API toohello de acesso a dados
* **Gerar ou recuperar a chave de API de saudação** - Log toohello Enterprise portal e siga Olá tutorial em Ajuda - APIs de relatórios. a primeira seção Olá sob este artigo ajuda explica como toogenerate ou recuperar chave Olá API Olá especificado registro.
* **Passando chaves Olá API** -chave de API de saudação deve toobe passado para cada chamada para autenticação e autorização. propriedade a seguir Hello precisa toobe toohello HTTP cabeçalhos

|Chave de cabeçalho da solicitação | Valor|
|-|-|
|Autorização| Especifique o valor de saudação neste formato: **portador {API_KEY}** <br/> Exemplo: portador e... 09|

## <a name="consumption-apis"></a>APIs de consumo
Há um ponto de extremidade de Swagger [aqui](https://consumption.azure.com/swagger/ui/index) para Olá APIs descritas abaixo do qual deve introspecção fácil de habilitar da API de saudação e cliente toogenerate da capacidade Olá SDKs usando [AutoRest](https://github.com/Azure/AutoRest) ou [ Gerador de código de swagger](http://swagger.io/swagger-codegen/). Os dados a partir de 1º de maio de 2014 estão disponíveis por essa API. 

* **Saldo e resumo** - Olá [equilíbrio e a API de resumo](billing-enterprise-api-balance-summary.md) oferece um resumo mensal de informações sobre saldos, novas aquisições, taxas de serviço do Azure Marketplace, ajustes e encargos excedentes.

* **Detalhes de uso** - Olá [API de detalhes de uso](billing-enterprise-api-usage-detail.md) oferece um detalhamento diário das quantidades consumidas e encargos estimados por um registro. resultado de saudação também inclui informações sobre instâncias, medidores e departamentos. Olá API pode ser consultada por período de cobrança ou de início especificado e a data de término. 

* **Custos de armazenamento do Marketplace** - Olá [API de custos de armazenamento Marketplace](billing-enterprise-api-marketplace-storecharge.md) retorna divisão de encargos do marketplace baseada no uso de Olá por dia para Olá especificado o período de cobrança ou datas de início e término (taxas de uma vez não estão incluídas) .

* **Tabela de preços** - Olá [API de folha de preço](billing-enterprise-api-pricesheet.md) fornece taxa aplicável Olá para cada medidor para Olá dado registro e o período de cobrança. 

## <a name="helper-apis"></a>APIs auxiliares
 **Lista os períodos de cobrança** - Olá [API de períodos de cobrança](billing-enterprise-api-billing-periods.md) retorna uma lista de períodos que têm dados de consumo de saudação especificada registro em ordem cronológica inversa de cobrança. Cada período contém uma propriedade apontando toohello rota de API para Olá quatro conjuntos de dados - BalanceSummary, UsageDetails, encargos do Marketplace e tabela de preços.


## <a name="api-response-codes"></a>Códigos de resposta da API  
|Código de status de resposta|Mensagem|Descrição|
|-|-|-|
|200| OK|Nenhum erro|
|401| Não Autorizado| Chave de API não encontrada, inválida, expirada, etc.|
|404| Indisponível| Ponto de extremidade de relatório não encontrado|
|400| Solicitação incorreta| Parâmetros inválidos – intervalos de datas, números de EA, etc.|
|500| Erro de servidor| Solicitação de processamento de erro inesperada| 









