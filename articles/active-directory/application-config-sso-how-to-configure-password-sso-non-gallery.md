---
title: "aaaHow tooconfigure senha single sign-on para uma galeria não applicationn | Microsoft Docs"
description: "Como tooconfigure um aplicativo não Galeria personalizado para proteger com base em senha de logon único quando ele não estiver listado na Olá Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo não Galeria

Além disso toohello opções encontrado na Galeria de aplicativos de saudação do AD do Azure, você também tem Olá opção tooadd um **aplicativo Galeria não** ao aplicativo hello desejado não estiver listado. Usando esse recurso, você pode adicionar qualquer aplicativo que já existe em sua organização, ou qualquer aplicativo de terceiros que você pode usar de um fornecedor que não ainda faz parte do hello [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

Quando você adicionar um aplicativo não galeria, você pode configurar Olá único método de logon usa este aplicativo, selecionando Olá **Single Sign-on** item de navegação em um aplicativo corporativo em Olá [Portal do Azure ](https://portal.azure.com/).

Uma saudação SSO métodos disponível tooyou é hello [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção. Com hello **adicionar um aplicativo da Galeria não** experiência, você pode integrar qualquer aplicativo que processa um nome de usuário com base em HTML e a senha de entrada campo, mesmo se ele não está em nosso conjunto de aplicativos pré-integrados.

Olá acontece é por uma página de captura de tecnologia que faz parte da saudação extensão do painel de acesso que nos permite tooauto-detectar os campos de entrada de nome de usuário e senha, armazená-las com segurança para a instância do aplicativo específico. Em seguida, repetir com segurança os nomes de usuário e campos de toothose senhas quando um usuário navega toothat aplicativo no painel de acesso do aplicativo hello.

Isso é uma ótima maneira tooget iniciado a integração de qualquer tipo de aplicativo ao AD do Azure rapidamente e permite que você:

-   Integrar **qualquer aplicativo em Olá, mundo** com seu locatário de AD do Azure, contanto que ele renderiza um campo de chamadas entrada de usuário e senha HTML

-   Habilitar **logon único para seus usuários** armazenando com segurança e repetição de nomes de usuário e senhas para o aplicativo hello integrado com o Azure AD

-   **Detecção automática de entrada** campos para qualquer aplicativo e permitem que você toomanually detectar esses campos usando Olá extensão de navegador do painel de acesso, no caso de detecção automática não encontrá-los

-   **Suporte a aplicativos que exigem vários campos de entrada** para aplicativos que exigem o nome de usuário e senha mais do que apenas toosign campos em

-   **Personalizar rótulos Olá** dos campos de entrada de usuário e senha Olá os usuários vejam no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando eles digitem suas credenciais

-   Permitir que seu **usuários** tooprovide seus próprios nomes de usuário e senhas para contas de aplicativo existente que estão digitando no manualmente no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Permitir que um **membro do grupo de negócios Olá** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando Olá [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) recurso

-   Permitir que um **administrador** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan do usuário](#_How_to_configure_1)

-   Permitir que um **administrador** toospecify Olá compartilhado nome do usuário ou senha usada por um grupo de pessoas, usando as credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan de grupo](#assign-an-application-to-a-group-directly)

A seguir descreve como você pode habilitar [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany aplicativo que você adicione usando Olá **adicionar um aplicativo da Galeria não** experiência.

## <a name="overview-of-steps-required"></a>Visão geral das etapas necessárias

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo inexistente na galeria](#add-a-non-gallery-application)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application-for-password-single-sign-on)

-   [Atribuir um grupo ou usuário de tooa de aplicativo hello](#assign-the-application-to-a-user-or-a-group)

    -   [Atribuir um aplicativo do usuário tooan diretamente](#assign-a-user-to-an-application-directly)

    -   [Atribuir um grupo de aplicativos tooa diretamente](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>Adicionar um aplicativo inexistente na galeria

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha

6.  clique em **Aplicativo inexistente na galeria.**

7.  Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto. Selecione **Adicionar.**

Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar o aplicativo hello de senha single sign-on

tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  Digite hello **URL de logon**. Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para. Certifique-se de campos de entrada hello são visíveis na URL de saudação.

10. Atribua usuários toohello aplicativo.

11. Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação. Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.

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
