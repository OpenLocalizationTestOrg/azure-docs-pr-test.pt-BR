---
title: "Tutorial: Integração do Azure Active Directory com o Mimecast Admin Console | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Console de Admin do Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Tutorial: Integração do Azure Active Directory com o Mimecast Admin Console

Neste tutorial, você aprenderá como toointegrate do Console de Admin do Mimecast com o Azure Active Directory (AD do Azure).

Integração do Console de Admin do Mimecast com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooMimecast Console de administração.
- Você pode habilitar seu usuários tooautomatically get conectado tooMimecast Console de administração (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Console de Admin do Mimecast, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Mimecast Admin Console com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar o Console de Admin do Mimecast da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a>Adicionar o Console de Admin do Mimecast da Galeria de saudação
integração de saudação tooconfigure do Console de Admin do Mimecast no AD do Azure, você precisa tooadd Console de Admin do Mimecast da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Console de Admin do Mimecast da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Console de Admin do Mimecast**, selecione **Console de Admin do Mimecast** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Console de Admin do Mimecast na lista de resultados de saudação](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Mimecast Admin Console, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Console de Admin do Mimecast é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Console de Admin do Mimecast precisa toobe estabelecida.

No Console de Admin do Mimecast, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Console de Admin do Mimecast, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Console de Admin do Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave um equivalente do Britta Simon no Console de Admin do Mimecast que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Console de Admin do Mimecast.

**tooconfigure logon único do AD do Azure com o Console de Admin do Mimecast, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Console de Admin do Mimecast** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. Em Olá **URLs e domínio de Console de Admin do Mimecast** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    Em Olá **URL de logon** caixa de texto, digite a URL de saudação:
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > a URL de logon Olá é a região específica.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. Em Olá **configuração de Console de Admin do Mimecast** seção, clique em **configurar o Console de Admin do Mimecast** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu Mimecast Admin Console como um administrador.

8. Vá muito**serviços \> aplicativo**.

    ![Serviços](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Serviços")

9. Clique em **Perfis de Autenticação**.

    ![Perfis de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Perfis de Autenticação")
    
10. Clique em **Novo Perfil de Autenticação**.

    ![Novos Perfis de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Novos Perfis de Autenticação")

11. Em Olá **o perfil de autenticação** , execute Olá etapas a seguir:

    ![Perfil de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Perfil de Autenticação")
    
    a. Em Olá **descrição** caixa de texto, digite um nome para a sua configuração.
    
    b. Selecione **Impor Autenticação SAML para o Mimecast Admin Console**.
    
    c. Como **Provedor**, selecione **Azure Active Directory**.
    
    d. Colar **ID da entidade SAML**, que você copiou de saudação portal do Azure em hello **URL do emissor** caixa de texto.
    
    e. Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de logon** caixa de texto.

    f. Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de Logout** caixa de texto.
    
    >[!NOTE]
    >Olá valor de URL de logon e o valor de URL de Logout de saudação são para hello Console de Admin do Mimecast Olá mesmo.
    
    g. Abra seu certificado de base 64 é baixado do portal do Azure no bloco de notas, remova a primeira linha de saudação ("*--*") e a última linha de saudação ("*--*"), Olá cópia restantes conteúdo dele na área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade (metadados)** caixa de texto.
    
    h. Selecione **Permitir Logon Único**.
    
    i. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-mimecast-admin-console-test-user"></a>Criar um usuário de teste do Mimecast Admin Console

Ordem tooenable AD do Azure usuários toolog no Console de Admin do Mimecast, eles devem ser provisionados no Console de Admin do Mimecast. No caso de saudação do Console de Admin do Mimecast, o provisionamento é uma tarefa manual.

* Antes de criar os usuários, você precisa tooregister um domínio.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Logon tooyour **Console de Admin do Mimecast** como administrador.
2. Vá muito**diretórios \> interno**.
   
   ![Diretórios](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Diretórios")
3. Clique em **Registrar Novo Domínio**.
   
   ![Registrar Novo Domínio](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Registrar Novo Domínio")
4. Depois de criar o novo domínio, clique em **Novo Endereço**.
   
   ![Novo Endereço](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Novo Endereço")
5. Na caixa de diálogo Olá de novo endereço, execute Olá etapas a seguir:
   
   ![Salvar](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Salvar")
   
   a. Saudação de tipo **endereço de Email**, **nome Global**, **senha**, e **Confirmar senha** atributos de um AD do Azure válidas de conta você deseja tooprovision em Olá relacionados caixas de texto.

   b. Clique em **Salvar**.

>[!NOTE]
>Você pode usar qualquer outra ferramenta de criação de conta de usuário do Console de Admin do Mimecast ou APIs fornecidas por contas de usuário do Console de Admin do Mimecast tooprovision AD do Azure. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMimecast Console de administração.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooMimecast Console de administração, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Console de Admin do Mimecast**.

    ![link do Console de Admin do Mimecast Olá na lista de aplicativos Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em um bloco de Console de Admin do Mimecast Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Console de Admin do Mimecast.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

