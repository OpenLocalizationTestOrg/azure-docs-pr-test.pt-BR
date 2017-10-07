---
title: "configurações de ativação de função aaaHow toomanage | Microsoft Docs"
description: "Saiba como toochange Olá configurações padrão de identidades com privilégios com hello extensão do Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Como configurações de ativação de função toomanage no Azure AD Privileged Identity Management
Um administrador com privilégios de função pode personalizar o Azure AD Privileged Identity Management (PIM) em sua organização, incluindo alterar a experiência de saudação para um usuário que está sendo ativado uma atribuição de função qualificado.

## <a name="manage-hello-role-activation-settings"></a>Gerenciar configurações de ativação de função hello
1. Vá toohello [portal do Azure](https://portal.azure.com) e selecione hello **do Azure AD Privileged Identity Management** aplicativo a partir do painel de saudação.
2. Selecione **Gerenciar funções privilegiadas** > **Configurações** > **Funções Privilegiadas**.
3. Escolha a função hello cujas configurações você deseja toomanage.

Na página de configurações de saudação para cada função, há uma série de configurações que você pode configurar. Essas configurações afetam apenas os usuários que são administradores elegíveis, mas não os administradores permanentes.

**Ativações**: tempo de saudação, em horas, que uma função permanece ativa antes de expirar. Isso pode ser entre 1 e 72 horas.

**Notificações**: você pode escolher se ou não o sistema de Olá envia emails tooadmins confirmando que eles ativou a uma função. Isso pode ser útil para detectar ativações não autorizadas ou ilegítimas.

**Tíquete de solicitação deincidente/**: você pode escolher se ou não toorequire administradores qualificados tooinclude um tíquete de número quando elas ativaram sua função. Isso pode ser útil ao realizar auditorias de acesso à função.

**Autenticação multifator**: você pode escolher se ou não toorequire usuários tooverify sua identidade com MFA antes de poder ativar suas funções. Eles apenas têm tooverify isso vez por sessão, não toda vez que eles ativaram uma função. Há dois tookeep de dicas em mente quando você habilitar a MFA:

* Os usuários que têm contas da Microsoft para seus endereços de email (normalmente @outlook.com, mas nem sempre) não é possível registrar para o Azure MFA. Se você quiser tooassign funções toousers com contas da Microsoft, torná-los administradores permanentes ou desabilite o MFA para essa função.
* Você não pode desabilitar o MFA para funções com altos privilégios do Azure AD e do Office365. Esse é um recurso de segurança, porque estas funções devem ser protegidas com cuidado:  
  
  * Administrador de aplicativos
  * Administrador do servidor de Proxy de Aplicativo
  * Administrador de cobrança  
  * Administrador de conformidade  
  * Administrador de serviços do CRM
  * Aprovador de acesso do Sistema de Proteção de Dados do Cliente
  * Gravador de diretório  
  * Administrador do Exchange  
  * Administrador global
  * Administrador de serviço do Intune
  * Administrador de caixa de correio  
  * Suporte de camada 1 do parceiro  
  * Suporte de camada 2 do parceiro  
  * Administrador de função com privilégios   
  * Administrador de segurança  
  * Administrador do SharePoint  
  * Administrador do Skype for Business  
  * Administrador da conta de usuário  

Para obter mais informações sobre como usar MFA com PIM consulte [como tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

