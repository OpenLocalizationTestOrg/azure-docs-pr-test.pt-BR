---
title: "Tutorial: integração do Azure Active Directory com o BeeLine | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a>Tutorial: Integração do Azure Active Directory ao Beeline

Neste tutorial, você aprenderá como toointegrate BeeLine com o Azure Active Directory (AD do Azure).

Integrando BeeLine com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBeeLine
- Você pode habilitar seu usuários tooautomatically get conectado tooBeeLine (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com BeeLine, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do BeeLine

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando BeeLine da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-beeline-from-hello-gallery"></a>Adicionando BeeLine da Galeria de saudação
integração de saudação tooconfigure de BeeLine no AD do Azure, você precisa tooadd BeeLine da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd BeeLine da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **BeeLine**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. No painel de resultados de saudação, selecione **BeeLine**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o BeeLine, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em BeeLine é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em BeeLine precisa toobe estabelecida.

BeeLine, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com BeeLine, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste BeeLine](#creating-a-beeline-test-user)**  -toohave um equivalente do Britta Simon em BeeLine é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BeeLine.

**tooconfigure AD do Azure-logon único com BeeLine, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **BeeLine** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. Em Olá **BeeLine domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://projects.beeline.net/<instancename>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) tooget esses valores.
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. Seu aplicativo de Beeline espera as asserções SAML de saudação em um formato específico. Trabalhe com [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) tooidentify primeiro Olá identificador de usuário correta que será mapeada para o aplicativo hello. Também siga as diretrizes de saudação do [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) sobre Olá atributo que quiserem toouse para que esse mapeamento. Você pode gerenciar o valor deste atributo Olá de saudação **atributos de usuário** guia do aplicativo hello. Olá captura de tela a seguir mostra um exemplo. Aqui nós mapeou hello **identificador de usuário** declarações com hello **userprincipalname** atributo, que fornece a ID de usuário exclusivo, que será enviada toohello Beeline aplicativo hello cada SAML com êxito Resposta.

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. Em Olá **BeeLine configuração** seção, clique em **configurar BeeLine** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout** e **ID da entidade SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. tooconfigure logon único no **BeeLine** lado, você precisa toosend Olá baixado **Metadata XML** e **ID da entidade SAML**, **URL de logout**muito[a equipe de suporte BeeLine](https://www.beeline.com/contact-us/).

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-beeline-test-user"></a>Criação de um usuário de teste do BeeLine

Nesta seção, você criará um usuário chamado Brenda Fernandes no Beeline. Aplicativo de beeline precisa de todas as toobe de usuários Olá provisionado no aplicativo hello antes de fazer logon único. Para trabalhar com hello [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) tooprovision todos esses usuários para o aplicativo hello. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBeeLine.

![Atribuir usuário][200] 

**tooassign Britta Simon tooBeeLine, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **BeeLine**.

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação. Quando você clica em bloco Beeline Olá Olá painel de acesso, você deve obter o aplicativo de Beeline tooyour automaticamente conectado em.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

