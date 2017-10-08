---
title: aaaHow tooconfigure senha single sign-on para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Como tooconfigure um aplicativo para proteger com base em senha de logon único quando ele estiver listado em Olá Galeria de aplicativos do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo da Galeria do AD do Azure

Quando você adicionar um aplicativo de saudação [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), você tem a opção de saudação de como você deseja que seu toosign usuários no aplicativo toothat. Você pode configurar essa opção a qualquer momento selecionando Olá **Single Sign-on** item de navegação em um aplicativo corporativo em Olá [Portal do Azure](https://portal.azure.com/).

Uma saudação métodos de logon único disponíveis tooyou é hello [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção. Isso é uma ótima maneira tooget iniciado integrando aplicativos no AD do Azure rapidamente e permite que você:

-   Habilitar **logon único para seus usuários** armazenando com segurança e repetição de nomes de usuário e senhas para o aplicativo hello integrado com o Azure AD

-   **Suporte a aplicativos que exigem vários campos de entrada** para aplicativos que exigem o nome de usuário e senha mais do que apenas toosign campos em

-   **Personalizar rótulos Olá** dos campos de entrada de usuário e senha Olá os usuários vejam no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando eles digitem suas credenciais

-   Permitir que seu **usuários** tooprovide seus próprios nomes de usuário e senhas para contas de aplicativo existente que estão digitando no manualmente no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Permitir que um **membro do grupo de negócios Olá** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando Olá [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) recurso

-   Permitir que um **administrador** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan do usuário](#assign-a-user-to-an-application-directly)

-   Permitir que um **administrador** toospecify Olá compartilhado nome do usuário ou senha usada por um grupo de pessoas, usando as credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan de grupo](#assign-an-application-to-a-group-directly)

A seguir descreve como você pode habilitar [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan aplicativo que já está em Olá [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

## <a name="overview-of-steps-required"></a>Visão geral das etapas necessárias
tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo da Galeria do Azure AD Olá](#add-an-application-from-the-azure-ad-gallery)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application-for-password-single-sign-on)

-   [Atribuir um grupo ou usuário de tooa de aplicativo hello](#assign-the-application-to-a-user-or-a-group)

    -   [Atribuir um aplicativo do usuário tooan diretamente](#assign-a-user-to-an-application-directly)

    -   [Atribuir um grupo de aplicativos tooa diretamente](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Adicionar um aplicativo da Galeria do Azure AD Olá

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha

6.  Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello

7.  Selecionar aplicativo hello desejar tooconfigure para logon único

8.  Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.

9.  Clique em **adicionar** botão, o aplicativo de hello tooadd.

Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar o aplicativo hello de senha single sign-on

tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  [Atribuir usuários toohello aplicativo](#assign-a-user-to-an-application-directly).

10. Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação. Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.

## <a name="assign-a-user-tooan-application-directly"></a>Atribuir um aplicativo do usuário tooan diretamente

tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.

13. Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.

15. Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.

## <a name="assign-an-application-tooa-group-directly"></a>Atribuir um grupo de aplicativos tooa diretamente

tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.

13. Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.

15. Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.

Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
