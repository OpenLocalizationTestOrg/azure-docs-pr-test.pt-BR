---
title: aaaConfigure do Azure AD Privileged Identity Management | Microsoft Docs
description: "Um tópico que explica o que é o Azure AD Privileged Identity Management e como toouse PIM tooimprove a segurança de nuvem."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>O que é o Azure AD Privileged Identity Management?
Com o Privileged Identity Management do Azure Active Directory (AD), você pode gerenciar, controlar e monitorar o acesso em sua organização. Isso inclui tooresources de acesso no AD do Azure e outros Microsoft online services como Office 365 ou Microsoft Intune.  

> [!NOTE]
> Privileged Identity Management é toda a organização tooyour disponíveis quando você licenciar seus administradores com edição de Olá P2 Premium do Active Directory do Azure. Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).

As organizações preferir que o número de saudação toominimize das pessoas que têm acesso toosecure informações ou recursos, porque o que reduz a chance de saudação de um usuário mal-intencionado obter acesso. No entanto, os usuários ainda precisam toocarry operações privilegiadas em aplicativos do Azure, Office 365 ou SaaS. As organizações dão aos usuários acesso privilegiado no Azure AD sem monitorar o que esses usuários estão fazendo com seus privilégios de administrador. O Azure AD Privileged Identity Management ajuda tooresolve esse risco.  

O Azure AD Privileged Identity Management ajuda você a:  

* Ver quais usuários são administradores do Azure AD
* Habilitar sob demanda "just in time" tooMicrosoft acesso administrativo a serviços Online como o Office 365 e Intune
* Obter relatórios sobre o histórico de acesso de administrador e as alterações nas atribuições de administrador
* Receber alertas sobre a função de tooa de acesso privilegiado
* Exigir aprovação tooactivate (visualização)

Azure AD Privileged Identity Management pode gerenciar funções de organizacional Olá interna do AD do Azure, incluindo (mas não limitado a):  

* Administrador global
* Administrador de cobrança
* Administrador de serviços  
* Administrador de usuários
* Administrador de senha

## <a name="just-in-time-administrator-access"></a>Administrador de acesso just in time
Historicamente, você pode atribuir uma função de administrador do usuário tooan por meio de saudação portal clássico do Azure ou o Windows PowerShell. Como resultado, ele se torna um **administrador permanente**sempre ativa na função hello atribuído. Azure AD Privileged Identity Management apresenta o conceito de saudação de um **admin qualificado**. Administradores elegíveis devem ser usuários que precisam de acesso privilegiado às vezes, mas não todos os dias. função Hello está inativa até que o usuário Olá precisa de acesso, em seguida, eles concluir um processo de ativação e se tornar um administrador ativo para uma quantidade predeterminada de tempo.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Habilitar o Privileged Identity Management para seu diretório
Você pode começar a usar o Azure AD Privileged Identity Management em hello [portal do Azure](https://portal.azure.com/).

> [!NOTE]
> Você deve ser um administrador global com uma conta organizacional (por exemplo, @yourdomain.com), não uma conta da Microsoft (por exemplo, @outlook.com), tooenable do Azure AD Privileged Identity Management para um diretório.

1. Entrar toohello [portal do Azure](https://portal.azure.com/) como um administrador global do seu diretório.
2. Se sua organização tiver mais de um diretório, selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure. Selecione o diretório de saudação onde você usará o Azure AD Privileged Identity Management.
3. Selecione **mais serviços** e usar Olá toosearch de caixa de texto de filtro para **do Azure AD Privileged Identity Management**.
4. Verificar **Pin toodashboard** e, em seguida, clique em **criar**. Olá aplicativo Privileged Identity Management é aberto.

Se você estiver hello primeira pessoa toouse Azure AD Privileged Identity Management em seu diretório, Olá [Assistente segurança](active-directory-privileged-identity-management-security-wizard.md) orienta a experiência de atribuição inicial hello. Depois que você se torna automaticamente Olá primeiro **administrador de segurança** e **administrador com privilégios de função** do diretório de saudação.

Somente um administrador com função com privilégios pode gerenciar o acesso de outros administradores. Você pode [dar toomanage de capacidade de saudação outros usuários de PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Painel de administração do Privileged Identity Management
O Privileged Identity Manager do Azure AD oferece um painel de administração que fornece informações importantes, como:

* Alertas que o ponto de segurança de tooimprove de oportunidades
* número de saudação de usuários que recebem a função privilegiada tooeach  
* número de saudação do grupo administradores qualificados e permanentes
* Um gráfico de ativações de funções com privilégios em seu diretório

![painel PIM - captura de tela][2]

## <a name="privileged-role-management"></a>Gerenciamento de funções com privilégios
Com o Azure AD Privileged Identity Management, você pode gerenciar administradores Olá adicionando ou removendo a função de tooeach administradores permanentes ou qualificados.

![adicionar/remover administradores no PIM - captura de tela][3]

## <a name="configure-hello-role-activation-settings"></a>Definir configurações de ativação de função hello
Usando Olá [configurações de função](active-directory-privileged-identity-management-how-to-change-default-settings.md) você pode configurar propriedades de ativação de função qualificado Olá incluindo:

* duração de saudação do período de ativação de função hello
* notificação de ativação de função Hello
* informações de saudação um usuário precisa tooprovide durante o processo de ativação de função hello
* Tíquete de serviço ou número do incidente
* [Requisitos do fluxo de trabalho de aprovação – Versão prévia](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![configurações do PIM - ativação do administrador - captura de tela][4]

Observe que, na imagem de Olá Olá botões para **multi-Factor Authentication** estão desabilitados. Certamente, funções com altos privilégios exigirão MFA para maior proteção.

## <a name="role-activation"></a>Ativação de função
muito[ativar uma função](active-directory-privileged-identity-management-how-to-activate-role.md), um administrador qualificado solicita um limite de tempo "ativação" para a função hello. ativação Olá pode ser solicitada Olá **ativar minha função** opção no Azure AD Privileged Identity Management.

Um administrador que deseja tooactivate uma função que precisa tooinitialize do Azure AD Privileged Identity Management no portal do Azure de saudação.

A ativação de função é personalizável. Nas configurações de PIM Olá, você pode determinar o comprimento de saudação de ativação hello e quais informações Olá administrador precisa de função de saudação do tooprovide tooactivate.

![ativação da função de solicitação do administrador do PIM - captura de tela][5]

## <a name="review-role-activity"></a>Examinar atividade de função
Há dois tootrack de maneiras como estão usando seus funcionários e os administradores com privilégios de funções. opção primeira Hello está usando [histórico de auditoria de funções de diretório](active-directory-privileged-identity-management-how-to-use-audit-log.md). histórico de auditoria Olá logs de controle de alterações em atribuições de função privilegiada e histórico de ativação de função.

![histórico da ativação do PIM - captura de tela][6]

Olá, segunda opção é tooset backup regular [acessar revisões](active-directory-privileged-identity-management-how-to-start-security-review.md). Essas análises de acesso podem ser executadas pelo e atribuídos revisor (como um gerente de equipe) ou funcionários Olá podem examinar a mesmos. Isso é Olá toomonitor de maneira melhor ainda, que requer acesso e que não faz.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM na expiração da assinatura
Tooreaching anterior geral disponibilidade do Azure AD PIM estava no modo de visualização e não houve nenhuma licença verifica toopreview um locatário Azure AD PIM.  Agora que o Azure AD PIM alcança disponibilidade geral, as licenças de avaliação ou pagas devem ser atribuídas a administradores toohello de saudação locatário toocontinue usar o PIM.  Se sua organização não comprar o Azure AD Premium P2 ou sua versão de avaliação expira, principalmente todos os recursos do Azure AD PIM Olá não estará disponíveis em seu locatário.  Você pode ler mais em Olá [requisitos de assinatura do Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
