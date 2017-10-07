---
title: "Solução de problemas: Dados ausentes no hello baixado logs de atividade do Active Directory do Azure | Microsoft Docs"
description: "Fornece dados de toomissing uma resolução nos logs de atividade baixados do Active Directory do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Não é possível localizar nenhum dado nos logs de atividade do Active Directory do Azure Olá que eu tenha baixado


## <a name="symptoms"></a>Sintomas

Baixei logs de atividade hello (ou entradas de auditoria) e não vejo todos os registros de saudação para tempo de saudação que escolher. Por quê? 

 ![Relatórios](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Causa

Quando você baixa os logs de atividade no hello portal do Azure, estamos limitar os registros de too120K de escala hello, classificados por mais recente. 

## <a name="resolution"></a>Resolução

Você pode aproveitar [APIs de relatórios do Azure AD](active-directory-reporting-api-getting-started.md) toofetch tooa milhões de registros em qualquer momento específico. Nossa abordagem recomendada é toorun um script em uma base agendada que chama Olá reporting APIs toofetch registra de forma incremental em um período de tempo (por exemplo, diária ou semanalmente).

## <a name="next-steps"></a>Próximas etapas
Consulte Olá [reporting perguntas frequentes sobre o Active Directory do Azure](active-directory-reporting-faq.md).

