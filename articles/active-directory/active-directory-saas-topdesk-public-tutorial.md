---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Público | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TOPdesk - público."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Tutorial: integração do Azure Active Directory com o TOPdesk – Public

Neste tutorial, você aprenderá como toointegrate TOPdesk - público com o Azure Active Directory (AD do Azure).

Integração do TOPdesk - público com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTOPdesk - público.
- Você pode habilitar seu usuários tooautomatically get conectado tooTOPdesk - público (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com TOPdesk - público, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do TOPdesk – Public habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando TOPdesk - público da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-topdesk---public-from-hello-gallery"></a>Adicionando TOPdesk - público da Galeria de saudação
integração de saudação do tooconfigure do TOPdesk - público no Azure AD, é necessário tooadd TOPdesk - público na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd TOPdesk - público da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **TOPdesk - público**, selecione **TOPdesk - público** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![TOPdesk - público na lista de resultados de saudação](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o TOPdesk – Public, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá no TOPdesk - público é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TOPdesk - público precisa toobe estabelecida.

No TOPdesk - público, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e testar o AD do Azure-logon único com TOPdesk - público, será necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um TOPdesk - público testar usuário](#create-a-topdesk---public-test-user)**  - toohave um equivalente do Britta Simon no TOPdesk - público que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no TOPdesk - público aplicativo.

**tooconfigure logon único do AD do Azure com TOPdesk - público, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **TOPdesk - público** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. Em Olá **TOPdesk - domínio público e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.topdesk.net`
    
    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. A URL de resposta é explicada posteriormente no tutorial. Entre em contato com [TOPdesk - a equipe de suporte de cliente público](https://help.topdesk.com/saas/enterprise/user/) tooget esses valores.  

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. Em Olá **TOPdesk - público configuração** seção, clique em **configurar TOPdesk - público** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Logon tooyour **TOPdesk - público** site da empresa como um administrador.

8. Em Olá **TOPdesk** menu, clique em **configurações**.
   
    ![Configurações](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configurações")

9. Clique em **Configurações de Logon**.
   
    ![Configurações de logon](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configurações de logon")

10. Expanda Olá **configurações de logon** menu e clique **geral**.
   
    ![Geral](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Geral")

11. Em Olá **pública** seção Olá **logon SAML** configuração, execute Olá etapas a seguir:
   
    ![Configurações técnicas](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configurações técnicas")
   
    a. Clique em **baixar** toodownload Olá arquivo de metadados público e, em seguida, salve-o localmente no seu computador.
   
    b. Abra o arquivo de metadados Olá baixado e localize Olá **AssertionConsumerService** nó.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Saudação de cópia **AssertionConsumerService** valor, cole esse valor Olá **URL de resposta** textbox em **TOPdesk - domínio público e URLs** seção.      
   
12. toocreate um arquivo de certificado, execute Olá etapas a seguir:
    
    ![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")
    
    a. Abra Olá baixou o arquivo de metadados do portal do Azure.
    
    b. Expanda Olá **RoleDescriptor** nó que possui um **xsi: Type** de **fed: ApplicationServiceType**.
    
    c. Copie o valor Olá Olá **X509Certificate** nó.
    
    d. Salvar Olá copiado **X509Certificate** valor localmente no seu computador em um arquivo.

13. Em Olá **pública** seção, clique em **adicionar**.
    
    ![Logon SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "logon SAML")

14. Em Olá **Assistente de configuração SAML** caixa de diálogo de página, execute Olá etapas a seguir:
    
    ![Assistente de configuração SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistente de configuração SAML")
    
    a. tooupload seus metadados de download de arquivo do portal do Azure, em **metadados de Federação**, clique em **procurar**.

    b. tooupload arquivo seu certificado, em **certificado (RSA)**, clique em **procurar**.

    c. arquivo de logotipo Olá tooupload você obteve da equipe de suporte do TOPdesk hello, em **ícone do logotipo**, clique em **procurar**.

    d. Em Olá **atributo de nome de usuário** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. Em Olá **nome de exibição** caixa de texto, digite um nome para a sua configuração.

    f. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-topdesk---public-test-user"></a>Criar um usuário de teste do TOPdesk – Public

Em ordem toolog de usuários tooenable AD do Azure no TOPdesk - público, eles devem ser provisionados no TOPdesk - público.  
No caso de saudação do TOPdesk - público, o provisionamento é uma tarefa manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisionamento de usuário, execute Olá etapas a seguir:
1. Logon tooyour **TOPdesk - público** site da empresa como administrador.

2. No menu de saudação na parte superior de saudação, clique em **TOPdesk \> novo \> arquivos de suporte \> pessoa**.
   
    ![Pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Pessoa")

3. Na caixa de diálogo de nova pessoa hello, execute Olá etapas a seguir:
   
    ![Nova pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nova pessoa")
   
    a. Clique em guia Geral hello.

    b. Em Olá **Sobrenome** caixa de texto, digite o sobrenome do usuário, Olá como Simon
 
    c. Selecione um **Site** conta hello.
 
    d. Clique em **Salvar**.

> [!NOTE]
> Você pode usar qualquer outra TOPdesk - ferramenta de criação de conta de usuário público ou APIs fornecidos pelo TOPdesk - público tooprovision AD do Azure contas de usuário.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTOPdesk - público.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooTOPdesk - público, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **TOPdesk - público**.

    ![Olá TOPdesk - público link na lista de aplicativos Olá](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá TOPdesk - público lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour TOPdesk - público aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

