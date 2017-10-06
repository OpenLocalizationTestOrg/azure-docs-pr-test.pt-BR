---
title: aaaHow toogive acesso tooPrivileged Identity Management - Azure | Microsoft Docs
description: "Saiba como tooadd funções toousers com hello extensão do Azure Active Directory Privileged Identity Management para que eles possam PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Fornecendo acesso toomanage Azure AD Privileged Identity Management
administrador global Hello, que permite que o Azure AD Privileged Identity Management (PIM) para uma organização automaticamente obter atribuições de função e acesso tooPIM. Entretanto, ninguém mais obtém acesso de gravação por padrão, incluindo outros administradores globais. Outros administradores globais, administradores de segurança e leitores de segurança têm acesso somente leitura tooAzure AD PIM. toogive tooPIM de acesso, o usuário primeiro Olá pode atribuir outros toohello **administrador com privilégios de função** função. Essa atribuição deve ser feita no próprio PIM e não pode ser alterada por meio do PowerShell ou outros portais.

> [!NOTE]
> O gerenciamento do Azure AD PIM requer o Azure MFA. Como as contas da Microsoft não podem se registrar para o Azure MFA, um usuário que entra com uma conta da Microsoft não pode acessar o Azure AD PIM.
> 
> 

Certifique-se de que haja sempre pelo menos dois usuários em uma função de administrador de função com privilégios, no caso de um usuário estar bloqueado ou sua conta ser excluída.

## <a name="give-another-user-access-toomanage-pim"></a>Dê toomanage acesso de outro usuário PIM
1. Entrar toohello [portal do Azure](https://portal.azure.com/) e selecione hello **do Azure AD Privileged Identity Management** aplicativo no painel de saudação.
2. Selecione **Gerenciar funções com privilégios** > **Administrador com função com privilégios** > **Adicionar**.
   
    ![Adicionar administradores com função com privilégios – captura de tela][1]
3. Na folha de usuários gerenciados adicionar Olá, etapa 1 já está concluída. A etapa 2, selecione **Selecione usuários** e pesquisa para o usuário Olá você deseja tooadd.
   
    ![Selecionar usuários – captura de tela][2]
4. Selecione o usuário Olá Olá dos resultados da pesquisa e, em seguida, clique em **feito**.
5. Clique em **Okey** toosave sua seleção. usuário Olá selecionado será exibido na lista de saudação de administradores com privilégios de função.
   
   * Sempre que você atribui um novo toosomeone de função, eles são automaticamente configurados como função de saudação tooactivate qualificados. Se você quiser toomake permanente na função hello, clique em usuário Olá na lista de saudação. Selecione **fazer perm** no menu de informações de usuário de saudação.
6. Enviar link ao usuário Olá muito[guia de Introdução ao Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Remover direitos de acesso de outro usuário para o gerenciamento de PIM
Antes de você remove da função de administrador com privilégios de função hello, sempre Certifique-se de haver dois usuários atribuídos tooit.

1. No painel PIM hello, clique na função hello **administrador com privilégios de função**.  saudação de lista de usuários atualmente na função será exibida.
2. Clique no usuário Olá na lista de saudação do usuário.
3. Clique em **Remover**.  Será exibida uma mensagem de confirmação.
4. Clique em **Sim** tooremove usuário Olá função hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
