---
title: "aaaAdd novo tooAzure de usuários do Active Directory | Microsoft Docs"
description: "Explica como tooadd novos usuários no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Início rápido: Adicionar novo tooAzure de usuários do Active Directory
Este artigo explica como tooadd novos usuários em sua organização em hello Azure Active Directory (AD do Azure) uma por vez usando Olá portal do Azure ou sincronizando seu usuário do Windows Server AD local dados da conta. 

## <a name="add-cloud-based-users"></a>Adicionar usuários baseados em nuvem
1. Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **Azure Active Directory** e, em seguida, **Usuários e grupos**.
3. Em Olá **usuários e grupos** folha, selecione **todos os usuários**e, em seguida, selecione **novo usuário**.
   ![Selecionando o comando Add a saudação](./media/add-users-azure-active-directory/add-user.png)
4. Insira detalhes para usuário hello, como **nome** e **nome de usuário**. Olá parte do nome de domínio do nome de usuário Olá deve estar saudação inicial padrão domínio nome "[nome de domínio].onmicrosoft.com" ou verificado, não federado [nome de domínio personalizado](add-custom-domain.md) como "contoso.com".
5. Cópia ou caso contrário hello de Observação senha gerada pelo usuário para que você possa fornecê-lo toohello usuário depois que o processo seja concluído.
6. Opcionalmente, você pode abrir e preencha as informações de Olá Olá **perfil** folha, Olá **grupos** folha ou hello **função de diretório** folha para usuário hello. Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).
7. Em Olá **usuário** folha, selecione **criar**.
8. Com segurança distribua Olá gerado senha toohello novo usuário de forma que hello usuário possa acessar.

> [!TIP]
> Você também pode sincronizar dados de conta de usuário do Windows Server AD local. Soluções de identidade da Microsoft abrangem locais e recursos baseados em nuvem, criando uma identidade de usuário único para autenticação e autorização tooall recursos, independentemente do local. Chamamos isso de Identidade Híbrida. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) pode ser usado toointegrate seus diretórios locais com o Active Directory do Azure para cenários de identidade híbrida. Isso permite que você tooprovide uma identidade comum para os usuários para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure. 

## <a name="delete-users-from-azure-ad"></a>Excluir usuários do Azure AD
1. Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **Usuários e grupos**.
3. Em Olá **usuários e grupos** folha, selecione Olá toodelete de usuário na lista de saudação. 
4. Na folha de saudação do usuário selecionado hello, selecione **visão geral**e, em seguida, na barra de comandos hello, selecione **excluir**.
   ![Selecionando o comando Add a saudação](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Saiba mais 
* [Adicionar um usuário externo](active-directory-users-create-external-azure-portal.md)

* [Atribuir uma função de usuário tooa no AD do Azure](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Próximas etapas
Este guia de início rápido, você aprendeu como tooadd de novos usuários tooAzure AD Premium. 

Você pode usar o hello para seguir link toocreate um novo usuário no AD do Azure de saudação portal do Azure.

> [!div class="nextstepaction"]
> [Adicionar usuários tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
