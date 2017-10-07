---
title: "aaaAzure notificações de relatório do Active Directory"
description: "Como toouse Olá notificações de relatório do Active Directory do Azure para logon suspeitos ins."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Notificações de Relatórios do Active Directory do Azure
## <a name="what-reports-generate-email-notifications"></a>Quais relatórios geram notificações por email
Neste momento, as notificações por email somente Olá entradas irregulares em gatilhos de relatório de atividade.

## <a name="what-is-an-irregular-sign-in"></a>O que é uma "Entrada irregular"?
Entradas irregulares são aquelas que foram identificados pelos nossos algoritmos com base Olá uma condição "viagem impossível" combinada com um local de entrada anormal e o dispositivo de aprendizado de máquina. Isso pode indicar que um hacker tem tentado toosign usando essa conta.

## <a name="who-receives-hello-email-notifications"></a>Quem recebe notificações de email Olá?
email de saudação é enviado tooall administradores globais que tem sido atribuídos uma licença do Active Directory Premium. tooensure é entregue, podemos enviar-toohello admins. do endereço de Email alternativo também. Os administradores devem incluir aad-alerts-noreply@mail.windowsazure.com em suas listas de remetentes confiáveis para que eles não perderem o email de saudação.

## <a name="how-often-are-these-emails-sent"></a>Com que frequência esses emails são enviados?
email de saudação é enviado se 10 novas irregulares entrar atividades ocorrem em Olá últimos 30 dias, ou desde o envio de email última hello, o que for menor.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Como acessar o relatório Olá mencionado no email Olá?
Quando você clica no link Olá, você será redirecionado toohello página de relatório em Olá portal clássico do Azure. Em ordem tooaccess Olá relatório, é necessário toobe ambos:

* Um administrador ou coadministrador de sua assinatura do Azure
* Um administrador global no diretório de saudação e atribuída uma licença do Active Directory Premium. Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>Posso desativar esses emails?
Sim, tooturn desativar as notificações relacionadas tooanomalous entradas em Olá portal clássico do Azure, clique em **configurar**e, em seguida, selecione **desabilitado** em Olá **notificações**seção.

## <a name="whats-next"></a>O que vem a seguir
* Curioso sobre que relatórios de segurança, auditoria e atividade estão disponíveis? Verifique [Relatórios de segurança, auditoria e atividade do AD do Azure](active-directory-view-access-usage-reports.md)
* [Introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Adicionar identidade visual tooyour páginas entrar e painel de acesso da empresa](active-directory-add-company-branding.md)

