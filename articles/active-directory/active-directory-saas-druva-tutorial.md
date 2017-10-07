---
title: "Tutorial: integração do Azure Active Directory com Druva | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a>Tutorial: integração do Azure Active Directory com o Druva

Neste tutorial, você aprenderá como toointegrate Druva com o Azure Active Directory (AD do Azure).

Integrando o Druva com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooDruva.
- Você pode habilitar seu usuários tooautomatically get conectado tooDruva (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Druva, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Druva

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Druva da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-druva-from-hello-gallery"></a>Adicionando Druva da Galeria de saudação
integração de saudação tooconfigure do Druva no AD do Azure, você precisa tooadd Druva da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Druva da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Druva**, selecione **Druva** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Druva na lista de resultados de saudação](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Druva, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Druva é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Druva precisa toobe estabelecida.

No Druva, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Druva, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Druva](#create-a-druva-test-user)**  -toohave um equivalente do Britta Simon no Druva é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu aplicativo Druva.

**tooconfigure AD do Azure-logon único com o Druva, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Druva** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. Em Olá **Druva domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://cloud.druva.com/home`

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. Seu aplicativo Druva espera as asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens SAML** configuração. 

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, como mostrado no hello anterior a imagem e executar Olá etapas a seguir:

    | Nome do atributo      | Valor do atributo      |
    | ------------------- | -------------------- |
    | insync\_auth\_token |Insira o valor gerado do token Olá |
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.
    
    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha. Olá valor do token gerado é explicado posteriormente no tutorial.
    
    d. Clique em **OK**.    

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. Em Olá **Druva configuração** seção, clique em **configurar Druva** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Druva como um administrador.

10. Vá muito**gerenciar \> configurações**.

    ![Configurações](./media/active-directory-saas-druva-tutorial/ic795091.png "Configurações")

11. Na caixa de diálogo de configurações de logon único hello, execute Olá etapas a seguir:

    ![Configurações de Logon Único](./media/active-directory-saas-druva-tutorial/ic795092.png "Configurações de Logon Único")
    
    a. Colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de logon do provedor de identidade** caixa de texto.
    
    b. Colar **URL de logout** valor que você copiou de saudação portal do Azure em hello **URL de Logout do provedor de identidade** caixa de texto.
    
     c. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de ID** caixa de texto
     
     d. Olá tooopen **configurações** , clique em **salvar**.

12. Em Olá **configurações** , clique em **gerar Token do SSO**.

    ![Configurações](./media/active-directory-saas-druva-tutorial/ic795093.png "Configurações")

13. Em Olá **único logon no Token de autenticação** caixa de diálogo, executar Olá etapas a seguir:

    ![Token SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token SSO")
    
    a. Clique em **cópia**, colar copiados valor em Olá **valor** textbox em Olá **Adicionar atributo** seção.
    
    b. Clique em **fechar**

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-druva-test-user"></a>Criar um usuário de teste do Druva

Ordem tooenable AD do Azure usuários toolog em tooDruva, eles devem ser provisionados no Druva. No caso de saudação do Druva, o provisionamento é uma tarefa manual.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Druva** site da empresa como administrador.

2. Vá muito**gerenciar \> usuários**.
   
   ![Gerenciar Usuários](./media/active-directory-saas-druva-tutorial/ic795097.png "Gerenciar Usuários")

3. Clique em **Criar Novo**.
   
   ![Gerenciar Usuários](./media/active-directory-saas-druva-tutorial/ic795098.png "Gerenciar Usuários")

4. Na caixa de diálogo de criar novo usuário hello, execute Olá etapas a seguir:
   
   ![Criar Novo Usuário](./media/active-directory-saas-druva-tutorial/ic795099.png "Criar Novo Usuário")
   
   a. Em Olá **endereço de Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .
   
   b. Em Olá **nome** caixa de texto, insira o nome de saudação do usuário, como **BrittaSimon**.
   
   c. Clique em **Criar Usuário**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Druva usuário conta ou APIs fornecidas pelo Druva tooprovision contas de usuário do AD do Azure.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDruva.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooDruva, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Druva**.

    ![link do Druva Olá na lista de aplicativos Olá](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Druva Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Druva aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

