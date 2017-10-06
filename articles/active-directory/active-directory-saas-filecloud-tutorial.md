---
title: "Tutorial: integração do Azure Active Directory ao FileCloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a>Tutorial: integração do Azure Active Directory ao FileCloud

Neste tutorial, você aprenderá como toointegrate FileCloud com o Azure Active Directory (AD do Azure).

Integrando FileCloud com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooFileCloud.
- Você pode habilitar seu usuários tooautomatically get conectado tooFileCloud (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com FileCloud, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do FileCloud

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando FileCloud da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-filecloud-from-hello-gallery"></a>Adicionando FileCloud da Galeria de saudação
integração de saudação tooconfigure de FileCloud no AD do Azure, você precisa tooadd FileCloud da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd FileCloud da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **FileCloud**, selecione **FileCloud** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![FileCloud na lista de resultados de saudação](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o FileCloud, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em FileCloud é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em FileCloud precisa toobe estabelecida.

FileCloud, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com FileCloud, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste FileCloud](#create-a-filecloud-test-user)**  -toohave um equivalente do Britta Simon em FileCloud é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo FileCloud.

**tooconfigure AD do Azure-logon único com FileCloud, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **FileCloud** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. Em Olá **FileCloud domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único em Domínio e URLs do FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.filecloudhosted.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente FileCloud](mailto:support@codelathe.com) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. Em Olá **FileCloud configuração** seção, clique em **configurar FileCloud** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**

    ![Configuração do FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. Em uma janela de navegador web diferente, logon tooyour FileCloud locatário como um administrador.

8. No painel de navegação esquerdo hello, clique em **configurações**. 
   
    ![Seção Configurações no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. Clique na guia **SSO** na seção Configurações. 
   
    ![Guia Logon Único no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. Selecione **SAML** como **Tipo de SSO Padrão** em **Configurações de SSO (Logon Único)** painel.
   
    ![Painel de Configurações de Logon Único no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. Colar **ID da entidade SAML**, que você copiou do portal do Azure em Olá **URL de ponto de extremidade IdP** caixa de texto.

    ![Caixa de texto URL do Ponto de Extremidade do IDP](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. Abra o arquivo de metadados baixado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **metadados IdP** textbox em **configurações SAML** painel.

    ![Seção Metadados do IDP no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. Clique no botão **Salvar** .

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-filecloud-test-user"></a>Criar um usuário de teste do FileCloud

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no FileCloud. O FileCloud dá suporte ao provisionamento just-in-time, que está habilitado por padrão. Não há itens de ação para você nesta seção. Um novo usuário é criado durante uma tentativa tooaccess FileCloud se ele ainda não existir.

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do cliente FileCloud](mailto:support@codelathe.com). 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFileCloud.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooFileCloud, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **FileCloud**.

    ![link de FileCloud Olá na lista de aplicativos Olá](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco FileCloud Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour FileCloud aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

