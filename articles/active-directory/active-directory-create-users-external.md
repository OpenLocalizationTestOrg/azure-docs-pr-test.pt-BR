---
title: "os usuários aaaAdd outros diretórios ou empresas parceiras no Active Directory do Azure | Microsoft Docs"
description: "Explica como os usuários de tooadd ou alterar informações de usuário no Active Directory do Azure, incluindo usuários externos e convidados."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Adicionar usuários de outros diretórios ou de empresas parceiras no Azure Active Directory

Este artigo explica como tooadd usuários de outros diretórios no Azure Active Directory ou adicionar usuários de empresas parceiras. Para obter informações sobre a adição de novos usuários em sua organização e adição de usuários que têm contas da Microsoft, consulte [adicionar nova tooAzure de usuários do Active Directory](active-directory-create-users.md). 

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como centralizar tooadd B2B colaboração guest users na administração de saudação do AD do Azure, consulte [novidades colaboração B2B do Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)

Usuários adicionados não tem permissões de administrador, por padrão, mas você pode atribuir funções toothem a qualquer momento.

## <a name="add-a-user"></a>Adicionar um usuário
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **Active Directory**e abra seu diretório.
3. Selecione Olá **usuários** guia e, em seguida, na barra de comandos hello, selecione **adicionar usuário**.
4. Em Olá **Conte-nos sobre este usuário** página em **tipo de usuário**, selecione:

   * **Usuário em outro diretório do AD do Azure** – adiciona um diretório de tooyour de conta de usuário que é originado em outro diretório do AD do Azure. Você só poderá selecionar um usuário em outro diretório se também for membro desse diretório.
   * **Os usuários em empresas parceiras** -tooinvite e autorizar o diretório de tooyour parceiros da empresa de usuários (consulte [colaboração B2B do Azure Active Directory](active-directory-b2b-what-is-azure-ad-b2b.md)). Você precisará de muito[carregar um arquivo CSV especificar endereços de email](active-directory-b2b-references-csv-file-format.md).
5. Usuário Olá **perfil** , forneça um nome e sobrenome, um nome amigável e uma função de usuário do hello **funções** lista. Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md). Especifique se muito**habilitar autenticação multifator** para usuário hello.
6. Em Olá **obter senha temporária** página, selecione **criar**.

> [!IMPORTANT]
> Se sua organização usa mais de um domínio, você deve saber sobre Olá problemas a seguir quando você adicionar uma conta de usuário:
>
> * contas de usuário tooadd com hello mesmo nome principal de usuário (UPN) entre domínios, **primeiro** adicionar, por exemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido por** geoffgrisso@contoso.com.
> * **Não** adicione geoffgrisso@contoso.com antes de adicionar geoffgrisso@contoso.onmicrosoft.com.
>

Se você alterar as informações para um usuário cuja identidade é sincronizada com o serviço do Active Directory local, você não pode alterar informações de usuário Olá Olá portal clássico do Azure. toochange Olá informações do usuário, use as ferramentas de gerenciamento do Active Directory local.

## <a name="add-external-users"></a>Adicionar usuários externos
Você também pode adicionar usuários a partir de outro toowhich de diretório do AD do Azure que você pertence, ou empresas parceiras carregando um arquivo CSV. tooadd um usuário externo, para **tipo de usuário**, especifique **usuário em outro diretório do AD do Microsoft Azure** ou **usuários em empresas parceiras**.

Os usuários de ambos os tipos são originados de outro diretório e adicionados como **usuários externos**. Os usuários externos podem colaborar com outros usuários em um diretório sem qualquer requisito tooadd novas contas e o credenciais. Autenticação de usuários externos com seu diretório inicial quando entrarem no e que a autenticação funciona para qualquer toowhich de diretórios que eles foram adicionados.

## <a name="external-user-management-and-limitations"></a>Limitações e gerenciamento de usuários externos
Quando você adicionar um usuário de outro diretório de tooyour, esse usuário é um usuário externo em seu diretório. nome de usuário e o nome de exibição de saudação são copiados do seu diretório inicial e usados para usuário externo de saudação em seu diretório. Daí em seguida diante, as propriedades da conta de usuário externo Olá são completamente independentes. Se forem feitas alterações de propriedade toohello usuário em seu diretório inicial, essas alterações não sejam propagadas toohello conta de usuário externo no diretório.

Olá única ligação entre duas contas de saudação é que o usuário Olá sempre se autentica em seu diretório inicial ou com sua conta da Microsoft. É por isso que você não ver uma senha de saudação tooreset opção ou habilitar autenticação multifator para um usuário externo. Atualmente, política de autenticação de saudação do diretório de saudação inicial ou conta da Microsoft é hello apenas um que é avaliada quando o usuário Olá entrar.

> [!NOTE]
> Você ainda pode desabilitar o usuário externo de saudação no diretório de saudação, que bloqueia tooyour acessar o diretório.
>
>

Se um usuário for excluído do seu diretório inicial ou cancelar a sua conta da Microsoft, o usuário externo Olá ainda existe no seu diretório. No entanto, o usuário de saudação em seu diretório não pode acessar recursos porque eles não poderão autenticar com um diretório inicial ou a conta da Microsoft.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Serviços que oferecem suporte ao acesso por usuários externos do AD do Azure:
* **Portal clássico do Azure**: permite que um usuário externo que seja um administrador de vários diretórios toomanage cada desses diretórios.
* **O SharePoint Online**: se compartilhamento externo está habilitado, permite que um usuário externo tooaccess recursos do SharePoint Online autorizado.
* **Dynamics CRM**: se o usuário Olá é licenciado por meio do PowerShell, permite que um usuário externo tooaccess autorizado a recursos do Dynamics CRM.
* **Dynamics AX**: se o usuário Olá é licenciado por meio do PowerShell, permite que um usuário externo tooaccess autorizado a recursos no Dynamics AX. Olá limitações para [usuários externos do AD do Azure](#known-limitations-of-azure-ad-external-users) aplicar tooexternal usuários do Dynamics AX.

## <a name="next-steps"></a>Próximas etapas
* [Adicionar novo tooAzure de usuários do Active Directory](active-directory-create-users.md)
* [Administrando o Azure AD](active-directory-administer.md)
* [Gerenciar senhas no Azure AD](active-directory-manage-passwords.md)
* [Gerenciar grupos no Azure AD](active-directory-manage-groups.md)
