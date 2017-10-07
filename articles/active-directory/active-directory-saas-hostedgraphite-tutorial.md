---
title: "Tutorial: integração do Azure Active Directory com o Hosted Graphite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e grafite hospedado."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a>Tutorial: integração do Azure Active Directory ao Hosted Graphite

Neste tutorial, você aprenderá como toointegrate grafite hospedado no Azure Active Directory (AD do Azure).

Integrando grafite hospedado do Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHosted grafite
- Você pode habilitar seu usuários tooautomatically get conectado tooHosted grafite (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com grafite hospedado, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Hosted Graphite habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando hospedado grafite da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-hosted-graphite-from-hello-gallery"></a>Adicionando hospedado grafite da Galeria de saudação
integração de saudação tooconfigure do grafite hospedado no Azure AD, é necessário tooadd grafite hospedado na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd grafite hospedado na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **hospedado grafite**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. No painel de resultados de saudação, selecione **hospedado grafite**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Hosted Graphite com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte de saudação em grafite hospedado é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em grafite hospedado precisa toobe estabelecida.

Grafite hospedado, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com grafite hospedado, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste hospedado grafite](#creating-a-hosted-graphite-test-user)**  -toohave um equivalente do Britta Simon em grafite hospedado que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo hospedado grafite.

**tooconfigure AD do Azure-logon único com grafite hospedado, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **hospedado grafite** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. Em Olá **hospedado grafite domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, executar Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.hostedgraphite.com/metadata/<user id>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.hostedgraphite.com/complete/saml/<user id>`

4. Em Olá **hospedado grafite domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    a. Clique em Olá **Mostrar configurações de URL avançadas** opção

    b. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.hostedgraphite.com/login/saml/<user id>/`   

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com hello identificador real, a URL de resposta e URL de logon. tooget esses valores, você pode ir tooAccess -> Configuração SAML no lado do aplicativo ou entre em contato com [a equipe de suporte hospedado grafite](mailto:help@hostedgraphite.com).
    >
 
5. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. Em Olá **hospedado grafite configuração** seção, clique em **configurar grafite hospedado** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. Locatário de grafite hospedado tooyour logon como administrador.

9. Vá toohello **página de instalação do SAML** na lateral da saudação (**acesso -> instalação do SAML**).
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. Confirmar essas URls corresponderá à configuração feita na Olá **hospedado grafite domínio e URLs** seção Olá portal do Azure.
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. Em **entidade ou ID do emissor** e **URL de logon SSO** caixas de texto, cole o valor de saudação do **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure. 
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. Selecione "**Somente leitura**" como a **Função de usuário padrão**.
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. Clique no botão **Salvar** .

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-hosted-graphite-test-user"></a>Criação de um usuário de teste no Hosted Graphite

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no grafite hospedado. O Hosted Graphite dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Será criado um novo usuário durante uma tentativa tooaccess hospedado grafite se ele ainda não existir.

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, você precisa toocontact Olá grafite hospedado a equipe de suporte via < mailto:help@hostedgraphite.com >. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHosted grafite.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHosted grafite, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **hospedado grafite**.

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco hospedado grafite Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de grafite hospedado.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

