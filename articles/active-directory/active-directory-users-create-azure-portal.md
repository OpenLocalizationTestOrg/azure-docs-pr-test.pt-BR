---
title: "Adicionar novos usuários ao Azure Active Directory | Microsoft Docs"
description: "Explica como adicionar novos usuários ou como alterar informações do usuário no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a>Adicionar novos usuários ao Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-users-create-azure-portal.md)
> * [Portal clássico do Azure](active-directory-create-users.md)
>
>

Este artigo explica como adicionar novos usuários em sua organização no Azure AD (Azure Active Directory). 

1. Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.
2. Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.

   ![Abrir usuários e grupos](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. Na folha **Usuários e grupos**, selecione **Todos os usuários**, em seguida, selecione **Adicionar**.

   ![Selecionando o comando Adicionar](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. Insira os detalhes do usuário, como **Nome** e **Nome de usuário**. A parte do nome do domínio do nome do usuário deve ser o nome do domínio padrão inicial "foo.onmicrosoft.com", ou um nome de domínio verificado não federado, como "contoso.com".
5. Copie ou anote a senha de usuário gerada para que você possa fornecê-la ao usuário depois que esse processo estiver concluído.
6. Opcionalmente, você pode abrir e preencher as informações na folha **Perfil**, folha **Grupos** ou folha **Função de diretório** para o usuário. Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).
7. Na folha **Usuário**, selecione **Criar**.
8. Distribua com segurança a senha gerada para o novo usuário para que ele possa entrar.

### <a name="next-steps"></a>Próximas etapas
* [Adicionar um usuário externo](active-directory-users-create-external-azure-portal.md)
* [Redefinir a senha do usuário no novo Portal do Azure](active-directory-users-reset-password-azure-portal.md)
* [Alterar as informações de trabalho do usuário](active-directory-users-work-info-azure-portal.md)
* [Gerenciar perfis de usuário](active-directory-users-profile-azure-portal.md)
* [Excluir um usuário no Azure AD](active-directory-users-delete-user-azure-portal.md)
* [Atribuir um usuário a uma função no Azure AD](active-directory-users-assign-role-azure-portal.md)
