---
title: "Adicionar ou excluir usuários no Azure Active Directory | Microsoft Docs"
description: "Explica como adicionar novos usuários no Azure Active Directory ou excluir usuários existentes dele"
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/08/2018
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: f0f18f377f194e78c05e63e9b6cbc31c1b945335
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a>Início rápido: adicionar novos usuários ao Azure Active Directory
Este artigo explica como usuários em sua organização podem ser excluídos do locatário do Azure AD (Azure Active Directory) dessa organização ou adicionados a ele, usando o Portal do Azure ou sincronizando os dados da conta de usuário do Windows Server AD local. 

## <a name="add-cloud-based-users"></a>Adicionar usuários baseados em nuvem
1. Entre no [Centro de administração do Azure Active Directory](https://aad.portal.azure.com) com uma conta que seja um administrador global do diretório.
2. Selecione **Azure Active Directory** e, em seguida, **Usuários e grupos**.
3. Em **Usuários e grupos**, selecione **Todos os usuários** e, em seguida, selecione **Novo usuário**.
   ![Selecionando o comando Adicionar](./media/add-users-azure-active-directory/add-user.png)
4. Insira os detalhes do usuário, como **Nome** e **Nome de usuário**. A parte de nome de domínio do nome de usuário deve ser o nome de domínio padrão inicial "[nome de domínio].onmicrosoft.com" ou um [nome de domínio personalizado](add-custom-domain.md) verificado e não federado, como "contoso.com".
5. Copie ou anote a senha de usuário gerada para que você possa fornecê-la ao usuário depois que esse processo estiver concluído.
6. Opcionalmente, você pode abrir e preencher as informações em **Perfil**, **Grupos** ou **Função do diretório** para o usuário. Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles-azure-portal.md).
7. Em **Usuário**, selecione **Criar**.
8. Distribua com segurança a senha gerada para o novo usuário para que ele possa entrar.

> [!TIP]
> Você também pode sincronizar dados de conta de usuário do Windows Server AD local. As soluções de identidade da Microsoft abrangem locais e recursos baseados em nuvem, criando uma identidade de usuário único para autenticação e autorização em todos os recursos, independentemente do local. Chamamos isso de Identidade Híbrida. O [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) pode ser usado para integrar seus diretórios locais ao Azure Active Directory para cenários de identidade híbrida. Isso permite que você forneça uma identidade comum para os usuários dos aplicativos do Office 365, Azure e SaaS integrados ao AD do Azure. 

## <a name="delete-users-from-azure-ad"></a>Excluir usuários do Azure AD
1. Entre no [Centro de administração do Azure Active Directory](https://aad.portal.azure.com) com uma conta que seja um administrador global do diretório.
2. Selecione **Usuários e grupos**.
3. Na folha **Usuários e grupos**, selecione o usuário a ser excluído na lista. 
4. Na folha para o usuário selecionado, escolha **Visão geral** e, na barra de comandos, escolha **Excluir**.
   ![Selecionando o comando Adicionar](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Saiba mais 
* [Adicionar usuários convidados de outro diretório](active-directory-b2b-what-is-azure-ad-b2b.md) 
* [Atribuir um usuário a uma função no Azure AD](active-directory-users-assign-role-azure-portal.md)
* [Gerenciar perfis de usuário](active-directory-users-profile-azure-portal.md)
* [Restaurar um usuário excluído](active-directory-users-restore.md)



## <a name="next-steps"></a>Próximas etapas
Neste guia de início rápido, você aprendeu como adicionar novos usuários ao Azure AD Premium. 

Você pode usar o link a seguir para criar um novo usuário no Azure AD usando o portal do Azure.

> [!div class="nextstepaction"]
> [Adicionar usuários ao Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 