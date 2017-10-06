---
title: "aaaHow tooadd ou remover uma função de usuário | Microsoft Docs"
description: "Saiba como identidades de tooprivileged tooadd funções com hello aplicativo do Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Como tooadd ou remover uma função de usuário
Com o Azure AD (Active Directory), um administrador global (ou o administrador da empresa) pode atualizar os usuários que devem **permanentemente** atribuído tooroles no AD do Azure. Isso é feito com os cmdlets do PowerShell como `Add-MsolRoleMember` e `Remove-MsolRoleMember`. Ou eles podem usar Olá portal clássico do Azure conforme descrito em [atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles.md).

saudação de aplicativo do Azure AD Privileged Identity Management permite que os administradores de função privilegiada toomake permanente as atribuições de função, também. Além disso, os administradores de função com privilégios podem tornar os usuários **qualificados** para funções de administrador. Um administrador qualificado pode ativar a função hello quando necessário e, em seguida, suas permissões expirarem assim que estiverem concluídos.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Gerenciar funções PIM em Olá portal do Azure
Em sua organização, você pode atribuir usuários funções administrativas toodifferent no AD do Azure, aplicativos e serviços do Microsoft Office 365 e outros.  Mais detalhes sobre funções disponíveis Olá podem ser encontrados no [funções no Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd ou remover um usuário em uma função usando o gerenciamento de identidades com privilégios, coloque o painel PIM hello. Em seguida, clique em Olá **usuários em funções de administrador** botão, ou selecione uma função específica (por exemplo, o Administrador Global) da tabela de funções de saudação.

> [!NOTE]
> Se você não tiver habilitado o PIM em Olá portal do Azure, vá muito[Introdução ao Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) para obter detalhes.

Se você quiser que outra tooPIM de acesso de usuário em si, funções de saudação que requer o PIM Olá usuário toohave são descritos mais detalhadamente em toogive [como toogive acessar tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Adicionar uma função de usuário tooa
1. Em Olá [portal do Azure](https://portal.azure.com/), selecione Olá **do Azure AD Privileged Identity Management** bloco no painel de saudação.
2. Selecione **Gerenciar funções privilegiadas**.
3. Em Olá **Resumo da função** tabela, selecione Olá função toomanage.
4. Na folha de função hello, selecione **adicionar**.
5. Clique em **Selecione usuários** e pesquise o usuário Olá Olá **Selecione usuários** folha.  
6. Selecione usuário Olá Olá lista de resultados de pesquisa e, em seguida, clique em **feito**.
7. Clique em **Okey** toosave sua seleção. usuário Olá selecionados serão exibidos na lista de saudação como qualificado para a função hello.

> [!NOTE]
> Novos usuários em uma função só são elegíveis para a função hello por padrão. Se quiser toomake Olá função permanente, clique em usuário Olá na lista de saudação. informações de saudação do usuário serão exibida em uma nova folha. Selecione **Verifique perm** no menu de informações de usuário de saudação.  
> Se um usuário não é possível registrar para o Azure multi-Factor Authentication (MFA) ou está usando uma conta da Microsoft (geralmente @outlook.com), você precisa toomake-los permanente em todas as suas funções. Administradores qualificados serão solicitadas tooregister do MFA durante a ativação.

Agora que hello a usuário está qualificado para uma função, que eles saibam que eles podem ativá-lo de acordo com as instruções de toohello em [como tooactivate ou desativar uma função](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Remover um usuário de uma função
Você pode remover usuários de atribuições de função elegíveis, mas certifique-se de que sempre haja pelo menos um usuário que seja um administrador global permanente.

Siga essas etapas tooremove um usuário específico de uma função:

1. Navegue toohello função na lista de função hello selecionando uma função no painel do Azure AD PIM hello ou clicando no hello **usuários em funções de administrador** botão.
2. Clique no usuário Olá na lista de saudação do usuário.
3. Clique em **Remover**. Uma mensagem solicitará que você tooconfirm.
4. Clique em **Sim** tooremove função de saudação do usuário hello.

Se você não tiver certeza de que os usuários que ainda precisam as atribuições de função e, em seguida, você pode [iniciar uma revisão de acesso para a função hello](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

