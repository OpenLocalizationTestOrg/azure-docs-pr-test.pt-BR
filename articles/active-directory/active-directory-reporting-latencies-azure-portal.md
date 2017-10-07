---
title: "latências de relatório de Active Directory aaaAzure | Microsoft Docs"
description: "Saiba mais sobre a quantidade de saudação de tempo que leva para relatar eventos tooshow backup no portal do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Latências de relatórios do Azure Active Directory

Com [reporting](active-directory-preview-explainer.md) em Olá Active Directory do Azure, você obter todas as informações de saudação necessário toodetermine como seu ambiente está fazendo. quantidade de saudação de tempo que leva para tooshow de dados para cima em Olá portal do Azure também é conhecido como latência de relatório. 

Este tópico lista informações de latência de saudação para Olá todas as categorias de relatório no hello portal do Azure. 


## <a name="activity-reports"></a>Relatórios de atividades

Há duas áreas de relatórios de atividade:

- **Atividades de entrada** – informações sobre o uso de saudação de aplicativos gerenciados e atividades de entrada do usuário
- **Logs de auditoria** - informações de auditoria sobre o gerenciamento de usuários e de grupos, os aplicativos gerenciados e as atividades de diretório

Olá a tabela a seguir lista as informações de latência de saudação para relatórios de atividade.

| Relatório | Mínimo | Média | Máximo |
| :-- | --- | --- | --- |
| Logs de auditoria             | 30 minutos  | 45 minutos | 1 hora     |
| Entradas               | 15 minutos  | 15 minutos | 2 horas*   |

>[!NOTE]
> Para alguns dados de atividade de entradas provenientes de aplicativos do office herdado, pode levar horas too8 Olá comunicando tooshow de dados. 


## <a name="security-reports"></a>Relatórios de segurança

Há duas áreas de relatórios de segurança:

- **Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário. 
- **Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida. 

Olá a tabela a seguir lista as informações de latência de saudação para relatórios de segurança.

| Relatório | Mínimo | Média | Máximo |
| :-- | --- | --- | --- |
| Usuários em risco          | 5 minutos   | 15 minutos  | 2 horas  |
| Entradas de risco         | 5 minutos   | 15 minutos  | 2 horas  |

## <a name="risk-events"></a>Eventos de risco

Active Directory do Azure usa algoritmos e heurística toodetect suspeitas ações relacionadas tooyour contas de usuário de aprendizado de máquina adaptável. Cada ação suspeita detectada é armazenada em um registro chamado evento de risco.

Olá a tabela a seguir lista as informações de latência de saudação para eventos de risco.

| Relatório | Mínimo | Média | Máximo |
| :-- | --- | --- | --- |
| Entradas de endereços IP anônimos |5 minutos |15 minutos |2 horas |
| Entradas de locais desconhecidos |5 minutos |15 minutos |2 horas |
| Usuários com credenciais vazadas |2 horas |4 horas |8 horas |
| Viagem impossível tooatypical locais |5 minutos |1 hora |8 horas  |
| Entradas de dispositivos infectados |2 horas |4 horas |8 horas  |
| Entradas de endereços IP com atividade suspeita |2 horas |4 horas |8 horas  |



## <a name="next-steps"></a>Próximas etapas

Se você quiser tooknow mais sobre relatórios de atividades de Olá Olá portal do Azure, consulte:

- [Relatórios de atividade de entrada no portal do Azure Active Directory Olá](active-directory-reporting-activity-sign-ins.md)
- [Relatórios de atividade no portal do Azure Active Directory Olá de auditoria](active-directory-reporting-activity-audit-logs.md)

Se você quiser tooknow mais sobre relatórios de segurança de Olá Olá portal do Azure, consulte:

- [Usuários no relatório de riscos de segurança no portal do Azure Active Directory Olá](active-directory-reporting-security-user-at-risk.md)
- [Relatório de entradas arriscados no portal do Azure Active Directory Olá](active-directory-reporting-security-risky-sign-ins.md)

Se você quiser tooknow mais informações sobre eventos de risco, consulte [eventos de risco do Active Directory do Azure](active-directory-reporting-risk-events.md).
