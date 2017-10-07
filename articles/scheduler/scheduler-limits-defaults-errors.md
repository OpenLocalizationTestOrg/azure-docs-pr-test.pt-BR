---
title: "Padrões e limites de aaaScheduler"
description: "Limites e padrões do Agendador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Limites e padrões do Agendador
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Aceleradores, limites, padrões e cotas do Agendador
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>Olá x-ms-request-id cabeçalho
Cada solicitação feita no hello serviço Agendador retorna um cabeçalho de resposta chamado**x-ms-request-id**. Esse cabeçalho contém um valor opaco que identifica exclusivamente a solicitação de saudação.

Se uma solicitação é consistente com falha e você tiver verificado que solicitação Olá formulada corretamente, você pode usar este tooMicrosoft de erro do valor tooreport hello. Em seu relatório, inclua o valor de saudação de tempo aproximado de saudação do x-ms-request-id, essa solicitação Olá foi feita, Olá identificador de assinatura hello, coleção de trabalhos e/ou trabalho e Olá o tipo de operação que Olá tentativa de solicitação.

## <a name="see-also"></a>Consulte também
 [O que é o Agendador?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Agendador do Azure](scheduler-concepts-terms.md)

 [Começar a usar o Agendador no hello portal do Azure](scheduler-get-started-portal.md)

 [Planos e Cobrança no Agendador do Azure](scheduler-plans-billing.md)

 [Referência da API REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador do Azure](scheduler-powershell-reference.md)

 [Alta disponibilidade e confiabilidade do Agendador do Azure](scheduler-high-availability-reliability.md)

 [Autenticação de saída do Agendador do Azure](scheduler-outbound-authentication.md)

