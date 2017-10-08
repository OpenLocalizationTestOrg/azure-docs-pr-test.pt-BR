---
title: "Tutorial: integração do Azure Active Directory ao Lifesize Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a nuvem Lifesize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>Tutorial: Integração do Azure Active Directory com o Lifesize Cloud

Neste tutorial, você aprenderá como toointegrate Lifesize nuvem com o Azure Active Directory (AD do Azure).

Integrando Lifesize nuvem com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLifesize nuvem
- Você pode habilitar seu usuários tooautomatically get conectado tooLifesize nuvem (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Lifesize nuvem, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Lifesize Cloud

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Lifesize nuvem da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-lifesize-cloud-from-hello-gallery"></a>Adicionando Lifesize nuvem da Galeria de saudação
integração de saudação tooconfigure da nuvem Lifesize no AD do Azure, você precisa tooadd Lifesize nuvem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Lifesize nuvem da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Lifesize nuvem**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. No painel de resultados de saudação, selecione **Lifesize nuvem**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Lifesize Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na nuvem Lifesize é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na nuvem Lifesize precisa toobe estabelecida.

Na nuvem Lifesize, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Lifesize nuvem, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de nuvem Lifesize](#creating-a-lifesize-cloud-test-user)**  -toohave um equivalente do Britta Simon na nuvem Lifesize que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de nuvem Lifesize.

**tooconfigure AD do Azure-logon único com Lifesize nuvem, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Lifesize nuvem** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. Em Olá **Lifesize nuvem domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.lifesizecloud.com/ls/?acs`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.lifesizecloud.com/<companyname>`

     
4. Verificar **Mostrar configurações de URL avançadas**, executar Olá etapa a seguir:  
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    Em Olá **estado de retransmissão** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com hello real URL de logon, o estado de retransmissão e identificador. Entre em contato com [equipe de suporte do cliente de nuvem Lifesize](https://www.lifesize.com/support) tooget URL de logon e valores de identificador e você pode obter o valor de estado de retransmissão de configuração de SSO é explicado posteriormente no tutorial de saudação.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. Em Olá **configuração de nuvem Lifesize** seção, clique em **configurar Lifesize nuvem** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. tooget SSO configurado para seu aplicativo, o logon em Olá aplicativos de nuvem Lifesize com privilégios de administrador.

8. No hello canto superior direito clique em seu nome e, em seguida, clique em Olá **configurações avançadas**.
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. Em Olá configurações avançadas agora, clique em Olá **configuração SSO** link. Ele abrirá a página de configuração de SSO de saudação para sua instância.
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. Configure agora Olá valores na interface de configuração de SSO Olá a seguir.    
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    a. Em **emissor do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.

    b.  Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.

    c. Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.
  
    d. Em Olá SAML atributo mapeamentos para a caixa de texto Nome hello insira o valor de saudação como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    e. No mapeamento de atributo de SAML Olá para Olá **Sobrenome** caixa de texto insira o valor de saudação como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. No mapeamento de atributo de SAML Olá para Olá **Email** caixa de texto insira o valor de saudação como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. configuração de saudação toocheck você pode clicar em Olá **teste** botão.
   
    >[!NOTE]
    >Para teste bem-sucedido, você precisa de Assistente de configuração de saudação toocomplete no AD do Azure e também fornecem acesso toousers ou grupos que podem executar o teste de saudação.

12. Habilitar Olá SSO verificando em Olá **habilitar SSO** botão.

13. Agora clique em Olá **atualização** botão para que todas as configurações de saudação são salvos. Isso irá gerar o valor de RelayState hello. Saudação de cópia RelayState valor, que é gerado na caixa de texto de saudação, cole-o em hello **retransmissão estado** textbox em **Lifesize nuvem domínio e URLs** seção. 

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-lifesize-cloud-test-user"></a>Criação de um usuário de teste do Lifesize Cloud

Nesta seção, você criará um usuário chamado Brenda Fernandes no Lifesize Cloud. O Lifesize Cloud oferece suporte ao provisionamento automático de usuário. Após a autenticação bem-sucedida no AD do Azure, usuário hello será provisionado no aplicativo hello automaticamente. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLifesize nuvem.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLifesize nuvem, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Lifesize nuvem**.

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em nuvem Lifesize bloco no painel de acesso de saudação do hello, você deve obter a página de logon do aplicativo de nuvem Lifesize.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

