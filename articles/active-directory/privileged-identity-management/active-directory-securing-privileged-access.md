---
title: aaaSecuring acesso privilegiado no AD do Azure | Microsoft Docs
description: "Um tópico que explica Olá abordagens para proteger o acesso privilegiado no Azure, Active Directory do Azure e serviços Online da Microsoft."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Protegendo o acesso privilegiado no Azure AD
Com privilégios de proteger o acesso é a primeira etapa crítica toohelp proteger ativos de negócios em uma organização moderno. As contas privilegiadas são aquelas que administram e gerenciam sistemas de TI. Essas contas toogain acesso tooan organização dados e sistemas de destino invasores virtuais. acesso privilegiado do toosecure, você deve isolar as contas de saudação e sistemas de risco de saudação do que está sendo exposto usuário mal-intencionado tooa.

Mais usuários estão começando tooget privilegiado acesso por meio de serviços de nuvem. Isso pode incluir os administradores globais do Office365, administradores de assinatura do Azure e os usuários que têm acesso administrativo nas VMs ou em aplicativos SaaS.

A Microsoft recomenda que você siga este roteiro em [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx)(Proteger o acesso privilegiado).

Para clientes que usam o Azure Active Directory, o Office 365 ou outros serviços e aplicativos da Microsoft, esses princípios se aplicarão se as contas de usuário forem gerenciadas e autenticadas tanto pelo Active Directory quanto pelo Azure Active Directory. Olá seções a seguir fornecem mais informações sobre toosupport de recursos do AD do Azure protegendo o acesso privilegiado.

## <a name="azure-multi-factor-authentication"></a>Autenticação Multifator do Azure
segurança de saudação tooincrease de autenticação de administrador, você deve exigir verificação em duas etapas antes de conceder privilégios. Verificação em duas etapas é um método de verificação que você tiver que requer o uso de saudação de mais do que apenas um nome de usuário e senha. Ele fornece uma segunda camada de segurança toouser entradas e transações.

Azure multi-Factor Authentication (MFA) é uma solução de verificação em duas etapas da Microsoft, que ajuda a proteger aplicativos e acesso toodata atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de opções de verificação fácil, incluindo:

- chamadas telefônicas
- mensagens de texto
- notificações de aplicativo móvel
- códigos de verificação de aplicativo móvel
- tokens OATH de terceiros

Para obter uma visão geral de como funciona o Azure multi-Factor Authentication, consulte Olá vídeo a seguir:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Para obter mais informações, consulte [MFA para Office 365 e MFA para Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).

## <a name="time-bound-privileges"></a>Privilégios de limite de tempo
Algumas organizações podem acreditar que elas têm muitos usuários em funções altamente privilegiadas. Um usuário pode ter sido adicionado toohello função para uma atividade específica, como toosign um serviço, mas não use esses privilégios frequentemente posteriormente.

tempo de exposição de saudação toolower de privilégios e aumentar sua visibilidade sobre seu uso, limite os usuários tooonly levando em seus privilégios "just in time" (JIT), quando eles precisarem de tooperform uma tarefa. Para o Azure Active Directory e Microsoft Online Services, você pode usar o [Azure AD PIM (Privileged Identity Management)](http://aka.ms/AzurePIM).

![Painel PIM][2]

## <a name="attack-detection"></a>Detecção de ataque
O [Azure Active Directory Identity Protection](../active-directory-identityprotection.md) fornece uma exibição consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades da sua organização. Com base em eventos de risco, proteção de identidade calcula um nível de risco do usuário para cada usuário, permitindo que você tooconfigure risco políticas tooautomatically proteger Olá identidades da sua organização. Essas políticas, juntamente com outros controles de acesso condicional fornecidos pelo Active Directory do Azure e o EMS, automaticamente podem bloquear usuário hello ou oferecer sugestões que incluem as redefinições de senha e a imposição de autenticação multifator.

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a>Acesso condicional
Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas de saudação que escolha ao autenticar um usuário, antes de permitir acesso tooan aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado.

![Configurando regras de acesso condicional com MFA][4]

## <a name="related-articles"></a>Artigos relacionados
* Habilitar o [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Habilitar o [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Habilitar o [Azure AD Identity Protection](../active-directory-identityprotection.md)
* Habilitar os [controles de acesso condicionais](../active-directory-conditional-access.md)

Para obter mais informações sobre a criação de um roteiro de segurança completa, consulte a seção "responsabilidades do cliente e roteiro" Olá Olá [Microsoft Cloud Security para arquitetos de Enterprise](http://aka.ms/securecustomer) documento. Para obter mais informações sobre a interação Microsoft services tooassist com qualquer um destes tópicos, entre em contato com o representante da Microsoft ou visite nossa [página de soluções de segurança cibernética](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
