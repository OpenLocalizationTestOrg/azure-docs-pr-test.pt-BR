---
title: "aaaWhat é o Agendador do Azure? | Microsoft Docs"
description: "O Agendador do Azure permite que você toodeclaratively descrevem ações toorun na nuvem hello. Em seguida, ele agenda e executa essas ações automaticamente."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>O que é o Agendador do Azure?
O Agendador do Azure permite que você toodeclaratively descrevem ações toorun na nuvem hello. Em seguida, ele agenda e executa essas ações automaticamente.  Faz isso usando [Olá portal do Azure](scheduler-get-started-portal.md), código, [API REST](https://msdn.microsoft.com/library/mt629143.aspx), ou o Azure PowerShell.

O Agendador cria, mantém e invoca o trabalho agendado.  O Agendador não hospeda qualquer carga de trabalho ou executar qualquer código. Ele apenas *invoca* código hospedado em outro lugar—no Azure, no local ou em outro provedor. Ele invoca via HTTP, HTTPS, uma fila de armazenamento, uma fila do barramento de serviço ou um tópico do barramento de serviço.

Agendas de Agendador [trabalhos](scheduler-concepts-terms.md), mantém um histórico dos resultados da execução de trabalho que um pode examinar e forma determinista e confiável executar agendas toobe de cargas de trabalho. WebJobs do Azure (parte do recurso de aplicativos Web Olá no serviço de aplicativo do Azure) e outros recursos de agendamento do Azure usam o Agendador no plano de fundo de saudação. Olá [API REST do Agendador](https://msdn.microsoft.com/library/mt629143.aspx) ajuda a gerenciar a comunicação Olá para essas ações. Dessa forma, o Agendador oferece suporte para [agendas complexas e recorrência avançadas](scheduler-advanced-complexity.md) facilmente.

Há vários cenários que se prestam toohello uso do Agendador. Por exemplo:

* *Ações do aplicativo recorrente* : coleta periódica de dados do Twitter no feed.
* *Manutenção diária:* redução diária de logs, realização de backups e outras tarefas de manutenção. Por exemplo, um administrador pode escolher tooback o banco de dados de saudação à 1:00 A.M. todos os dias para Olá próximos nove meses.

Agendador permite toocreate, atualizar, excluir, exibir e gerenciar trabalhos e [coleções de trabalhos](scheduler-concepts-terms.md) programaticamente, usando scripts e no portal de saudação.

## <a name="see-also"></a>Consulte também
 [Conceitos, terminologia e hierarquia de entidades do Agendador do Azure](scheduler-concepts-terms.md)

 [Começar a usar o Agendador no hello portal do Azure](scheduler-get-started-portal.md)

 [Planos e Cobrança no Agendador do Azure](scheduler-plans-billing.md)

 [Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure](scheduler-advanced-complexity.md)

 [Referência da API REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador do Azure](scheduler-powershell-reference.md)

 [Alta disponibilidade e confiabilidade do Agendador do Azure](scheduler-high-availability-reliability.md)

 [Limites, padrões e códigos de erro do Agendador do Azure](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Agendador do Azure](scheduler-outbound-authentication.md)

