---
title: "aaaAdd novo tooAzure de usuários do Active Directory | Microsoft Docs"
description: "Explica como tooadd novos usuários ou alterar informações de usuário no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Adicionar novos usuários ou usuários com tooAzure de contas do Microsoft Active Directory
Adicione usuários toopopulate seu diretório. Este artigo explica como tooadd novos usuários em sua organização e como os usuários de tooadd com contas da Microsoft. Para saber mais sobre como adicionar usuários de outros diretórios ao Azure Active Directory ou como adicionar usuários de empresas parceiras, veja [Adicionar usuários de outros diretórios ou de empresas parceiras ao Azure Active Directory](active-directory-create-users-external.md). Usuários adicionados não tem permissões de administrador, por padrão, mas você pode atribuir funções toothem a qualquer momento.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como tooadd um usuário no Centro de administração de saudação do AD do Azure, consulte [adicionar nova tooAzure de usuários do Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Adicionar um usuário
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **do Active Directory**e, em seguida, selecione o nome de saudação do diretório de sua organização.
3. Selecione Olá **usuários** guia e, em seguida, na barra de comandos hello, selecione **adicionar usuário**.
4. Em Olá **Conte-nos sobre este usuário** página em **tipo de usuário**, selecione:

   * **Novo usuário em sua organização** – adiciona uma nova conta de usuário a seu diretório.
   * **Usuário com uma conta existente do Microsoft** – adiciona um Microsoft consumidor conta tooyour diretório existente (por exemplo, uma conta do Outlook)
5. Dependendo da **Tipo de usuário**, insira um nome de usuário (para o novo usuário) ou um endereço de email (para um usuário com uma conta da Microsoft).
6. Usuário Olá **perfil** , forneça um nome e sobrenome, um nome amigável e uma função de usuário do hello **funções** lista. Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md). Especifique se muito**habilitar autenticação multifator** para usuário hello.
7. Em Olá **obter senha temporária** página, selecione **criar**.

> [!IMPORTANT]
> Se sua organização usa mais de um domínio, você deve saber sobre Olá problemas a seguir quando você adicionar uma conta de usuário:
>
> * contas de usuário tooadd com hello mesmo nome principal de usuário (UPN) entre domínios, **primeiro** adicionar, por exemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido por** geoffgrisso@contoso.com.
> * **Não** adicione geoffgrisso@contoso.com antes de adicionar geoffgrisso@contoso.onmicrosoft.com. Essa ordem é importante e pode ser complicado tooundo.
>
>

## <a name="change-user-information"></a>Alterar as informações do usuário
Você pode alterar qualquer atributo de usuário, exceto Olá ID de objeto.

1. Abra seu diretório.
2. Selecione Olá **usuários** guia e nome para exibição, em seguida, selecione Olá do hello usuário a ser toochange.
3. Conclua suas alterações e, em seguida, clique em **Salvar**.

Se o usuário de saudação que você está alterando está sincronizado com o serviço do Active Directory local, você não pode alterar informações do usuário hello usando esse procedimento. usuário de saudação toochange, use as ferramentas de gerenciamento do Active Directory local.

## <a name="guest-user-management-and-limitations"></a>Limitações e gerenciamento de usuário convidado
As contas de convidados são usuários de outros diretórios que foram convidados tooyour directory tooaccess SharePoint documentos, aplicativos ou outros recursos do Azure. Uma conta de convidado em seu diretório tem o atributo de UserType subjacente definido muito "convidado". Usuários regulares (especificamente, os membros do diretório) tem o atributo de UserType do hello "Member".

Os convidados têm um conjunto limitado de direitos no diretório de saudação. Esses direitos limitam a capacidade de saudação para obter informações sobre outros usuários no diretório Olá toodiscover convidados. No entanto, os usuários convidados ainda podem interagir com usuários hello e grupos associados a recursos hello está trabalhando. Os usuários convidados podem:

* Ver outros usuários e grupos associados a um toowhich de assinatura do Azure que estão atribuídas
* Consulte Olá membros de grupos toowhich pertencem
* Pesquisar outros usuários no diretório hello, se eles saibam o endereço de email completo de saudação do usuário Olá
* Consulte apenas um conjunto limitado de atributos de usuários Olá que eles pesquisar – toodisplay limitado nome, endereço de email, nome de usuário principal (UPN) e foto em miniatura
* Obter uma lista de domínios verificados no diretório Olá
* Consentimento tooapplications, conceder-lhes Olá mesmo acesso que os membros têm em seu diretório

## <a name="set-guest-user-access-policies"></a>Definir políticas de acesso de usuário convidado
Olá **configurar** guia de um diretório inclui opções toocontrol acesso para usuários convidados. Essas opções só podem ser alteradas no portal clássico do Azure por um administrador global. Atualmente, não existe um método de API ou do PowerShell.

Olá tooopen **configurar** guia Olá select de portal clássico do Azure **do Active Directory**e, em seguida, selecione nome de saudação do diretório de saudação.

![Configurar a guia no Azure Active Directory][1]

Em seguida, você pode editar Olá opções toocontrol acesso para usuários convidados.

![opções de controle de acesso para usuários convidados][2]

## <a name="whats-next"></a>O que vem a seguir
* [Adicionar usuários de outros diretórios ou de empresas parceiras no Azure Active Directory](active-directory-create-users-external.md)
* [Administrando o Azure AD](active-directory-administer.md)
* [Gerenciar senhas no Azure AD](active-directory-manage-passwords.md)
* [Gerenciar grupos no Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
