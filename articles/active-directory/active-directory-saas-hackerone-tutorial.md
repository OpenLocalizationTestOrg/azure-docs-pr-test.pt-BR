---
title: "Tutorial: integração do Azure Active Directory ao HackerOne | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Hackerone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a>Tutorial: Integração do Azure Active Directory ao HackerOne

Neste tutorial, você aprenderá como toointegrate HackerOne com o Azure Active Directory (AD do Azure).

Integrando HackerOne com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHackerOne
- Você pode habilitar seu usuários tooautomatically get conectado tooHackerOne (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com HackerOne, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do HackerOne

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando HackerOne da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-hackerone-from-hello-gallery"></a>Adicionando HackerOne da Galeria de saudação
integração de saudação tooconfigure de HackerOne no AD do Azure, você precisa tooadd HackerOne da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd HackerOne da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **HackerOne**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. No painel de resultados de saudação, selecione **HackerOne**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure

Nesta seção, você configurará e testará o logon único do Azure AD com o HackerOne, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em HackerOne é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em HackerOne precisa toobe estabelecida.

HackerOne, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com HackerOne, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste HackerOne](#creating-a-hackerone-test-user)**  -toohave um equivalente do Britta Simon em HackerOne é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo HackerOne.

**tooconfigure AD do Azure-logon único com HackerOne, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **HackerOne** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. Em Olá **HackerOne única URL de logon e o identificador** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://hackerone.com/<company name>/authentication`

    b. Em Olá **identificador** caixa de texto, digite um URL como:`https://hackerone.com/users/saml/metadata`
    
    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Entre em contato com [HackerOne a equipe de suporte](mailto:support@hackerone.com) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. Em Olá **HackerOne configuração** seção, clique em **configurar HackerOne** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. Logon o tooyour HackerOne locatário como um administrador.

8. No menu de saudação na parte superior do hello, clique hello "**configurações**."
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. Navegue muito"**autenticação**"e clique em"**adicionar configurações SAML**."
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. Em Olá **configurações SAML** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    a. Em Olá **domínio de Email** caixa de texto, digite um domínio registrado.

    b. Em **URL de logon único** caixas de texto, cole o valor de saudação do **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.

    c. Abra o **arquivo de certificado** no bloco de notas baixado do portal do Azure, copie o conteúdo de saudação para sua área de transferência e, em seguida, cole-o toohello **certificado X509** caixa de texto.
    
    d. Clique em **Salvar**.

11. Na caixa de diálogo de configurações de autenticação hello, execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    a. Clique em **Executar teste**.

    b. Se Olá valor Olá **Status** campo é igual a **último status do teste: criado**, entre em contato com seu [HackerOne a equipe de suporte](mailto:support@hackerone.com) toorequest uma revisão da sua configuração.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-hackerone-test-user"></a>Criação de um usuário de teste do HackerOne

Em seguida, você criará um usuário chamado Brenda Fernandes no HackerOne. O HackerOne dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Quando você acessar HackerOne, um novo usuário será criado caso ele ainda não exista.

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, é necessário a equipe de suporte de certificar toocontact hello. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHackerOne.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHackerOne, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **HackerOne**.

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Por fim, você pode testar seu AD do Azure única configuração de logon usando o painel de acesso de saudação.  

Quando você clica em bloco HackerOne Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour HackerOne aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

