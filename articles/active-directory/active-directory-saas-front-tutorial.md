---
title: "Tutorial: integração do Azure Active Directory ao Front | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e frontal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a>Tutorial: integração do Azure Active Directory ao Front

Neste tutorial, você aprenderá como toointegrate frente com o Azure Active Directory (AD do Azure).

Integrando frente com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooFront.
- Você pode habilitar seu usuários tooautomatically get conectado tooFront (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração de tooconfigure AD do Azure com início, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura de Front habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando a frente da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-front-from-hello-gallery"></a>Adicionando a frente da Galeria de saudação
integração de Olá tooconfigure da frente no AD do Azure, você precisa tooadd frente da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd frente da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Front**, selecione **Front** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Início da lista de resultados de saudação](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Front, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá na frente é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá na frente precisa toobe estabelecida.

No futuro, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com início, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de frente](#create-a-front-test-user)**  -toohave um equivalente de Britta Simon na frente, o que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal do Azure de saudação e configurar o logon único em seu aplicativo de início.

**tooconfigure logon único do AD do Azure com início, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Front** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. Em Olá **domínio Front e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.frontapp.com`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.frontapp.com/sso/saml/callback`

4. Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.frontapp.com`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de entrada que são explicadas posteriormente no tutorial ou entre em contato com [equipe de suporte de cliente Front](mailto:support@frontapp.com) tooget esses valores. 

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. Em Olá **configuração Front** seção, clique em **configurar Front** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. Locatário de frente tooyour logon como administrador.

9. Vá muito**configurações (ícone de engrenagem na parte inferior de saudação do lateral esquerda Olá) > Preferências**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. Clique no link **Logon Único** .
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. Selecione **SAML** na lista suspensa de saudação do **Single Sign On**.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. Em Olá **ponto de entrada** caixa de texto colocar o valor de saudação de **o URL de serviço de logon único** do Assistente de configuração de aplicativo do AD do Azure.
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. Abra seu baixado **Certificate(Base64)** no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado de autenticação** caixa de texto.
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. Em Olá **as configurações do provedor de serviço** , execute Olá etapas a seguir:

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    a. Copie o valor de saudação do **ID da entidade** e cole-a saudação **identificador** textbox em **domínio Front e URLs** seção no portal do Azure.

    b. Copie o valor de saudação do **URL do ACS** e cole-a saudação **URL de logon** textbox em **domínio Front e URLs** seção no portal do Azure.
    
15. Clique no botão **Salvar** .

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-front-test-user"></a>Criar um usuário de teste do Front

Nesta seção, você criará uma usuária chamada Britta Simon no Front. Trabalhar com [equipe de suporte de cliente Front](mailto:support@frontapp.com) para adicionar usuários de saudação na plataforma de frente hello. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFront.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooFront, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Front**.

    ![link de início Olá na lista de aplicativos Olá](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest usando o Azure AD SSOconfiguration Olá painel de acesso.

Quando você clica em um bloco de frente Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado em aplicativo de início. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

