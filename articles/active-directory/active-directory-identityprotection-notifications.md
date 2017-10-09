---
title: "notificações de proteção de identidade do Active Directory aaaAzure | Microsoft Docs"
description: "Saiba como as notificações dão suporte às suas atividades de investigação."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Notificações do Azure Active Directory Identity Protection
O Azure AD Identity Protection envia emails em dois tipos de notificação automatizado toohelp você gerenciar eventos de risco e risco do usuário:

* Email de alerta de usuário comprometido
* Email de resumo semanal

## <a name="user-compromised-alert-email"></a>Email de alerta de usuário comprometido
Um email de alerta de usuário comprometido é gerado quando o Azure AD Identity Protection identifica uma conta como comprometida. email de saudação inclui toohello um link que os usuários sinalizados para relatório de risco no painel de proteção de identidade de saudação. É recomendável investigar imediatamente as notificações das contas comprometidas.

## <a name="weekly-digest-email"></a>Email de resumo semanal
email de resumo semanal Olá contém um resumo dos novos eventos de risco.<br>
Ele inclui:

* Usuários em risco
* Atividades suspeitas
* Vulnerabilidades detectadas
* Toohello links relacionados a relatórios na proteção de identidade

<br>
![Correção](./media/active-directory-identityprotection-notifications/400.png "correção")
<br>

É possível desativar o envio de um email de resumo semanal.
<br><br>
![Riscos de usuário](./media/active-directory-identityprotection-notifications/62.png "riscos de usuário")
<br>

**caixa de diálogo de configuração relacionados de saudação tooopen**:

1. Em Olá **Azure AD Identity Protection** folha, clique em **configurações**.
   <br><br>
   ![Política de risco do usuário](./media/active-directory-identityprotection-notifications/401.png "política de risco do usuário")
   <br>
2. Em Olá **geral** seção, clique em **notificações**.
   <br><br>
   ![Política de risco do usuário](./media/active-directory-identityprotection-notifications/405.png "política de risco do usuário")
   <br>

## <a name="see-also"></a>Consulte também
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
