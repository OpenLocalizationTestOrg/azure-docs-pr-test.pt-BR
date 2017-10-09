---
title: "Tutorial: Integração do Azure Active Directory com o Image Relay | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e retransmissão de imagem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a>Tutorial: Integração do Azure Active Directory com o Image Relay

Neste tutorial, você aprenderá como toointegrate retransmissão de imagem com o Azure Active Directory (AD do Azure).

Integração de retransmissão de imagem com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooImage retransmissão
- Você pode habilitar seu usuários tooautomatically get conectado tooImage retransmissão (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com retransmissão de imagem, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Image Relay

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando a retransmissão de imagem da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-image-relay-from-hello-gallery"></a>Adicionando a retransmissão de imagem da Galeria de saudação
integração de saudação tooconfigure de retransmissão de imagem no AD do Azure, você precisa tooadd retransmissão de imagem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd retransmissão de imagem da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **imagem retransmissão**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. No painel de resultados de saudação, selecione **imagem retransmissão**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Image Relay com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na imagem de retransmissão é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na imagem de retransmissão precisa toobe estabelecida.

Na imagem de retransmissão, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com a imagem de retransmissão, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de retransmissão de imagem](#creating-an-image-relay-test-user)**  -toohave um equivalente do Britta Simon na retransmissão de imagem que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de retransmissão de imagem.

**tooconfigure AD do Azure-logon único com retransmissão de imagem, executar Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **imagem retransmissão** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. Em Olá **domínio de retransmissão de imagem e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.imagerelay.com/`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.imagerelay.com/sso/metadata`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente de retransmissão de imagem](http://support.imagerelay.com/) tooget esses valores. 
 


4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. Em Olá **configuração de imagem de retransmissão** seção, clique em **configurar imagem retransmissão** tooopen **configurar o logon** janela. Saudação de cópia **URL do serviço de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. Em outra janela do navegador, entre no site da empresa tooyour retransmissão de imagem como um administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em Olá **usuários e permissões** carga de trabalho.
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. Clique em **Criar Nova Permissão**.
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. Em Olá **logon único** carga de trabalho, selecione Olá **este grupo pode apenas entrar por meio de logon único** caixa de seleção e, em seguida, clique em **salvar**.
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. Vá muito**configurações de conta**.
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. Vá toohello **logon único** carga de trabalho.
    
     ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. Em Olá **configurações SAML** caixa de diálogo, executar Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    a. Em **URL de logon** caixa de texto valor Olá colar **o URL de serviço de logon único** que você copiou do portal do Azure.

    b. Em **URL de Logout** caixa de texto valor Olá colar **URL do serviço de logon único** que você copiou do portal do Azure.

    c. Em **Formato da Id de Nome**, selecione **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.

    d. Como **opções de associação para solicitações de saudação (imagem de retransmissão) do provedor de serviços**, selecione **POST associação**.

    e. Em **Certificado x.509**, clique em **Atualizar Certificado**.

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    f. Abra o certificado de saudação baixado no bloco de notas, copie o conteúdo de hello e cole-o na caixa de texto de certificado de x. 509 hello.

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    g. Em **just-in-provisionamento de usuário** seção, selecione Olá **habilitar provisionamento de usuário just-in-**.

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    h. Grupo de permissão de Select hello (por exemplo, **SSO básico**) que é permitido toosign em apenas por meio de logon único.

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    i. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-image-relay-test-user"></a>Criar um usuário de teste do Image Relay

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon na imagem de retransmissão.

**toocreate um usuário chamado Britta Simon na imagem de retransmissão, execute Olá etapas a seguir:**

1. Site de empresa de retransmissão de imagem tooyour logon como administrador.

2. Vá muito**usuários e permissões** e selecione **criar usuário de SSO**.
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. Digite hello **Email**, **nome**, **Sobrenome**, e **empresa** de usuário Olá deseja tooprovision e grupo de permissão de select Olá (por exemplo, SSO básica) que é o grupo de saudação que possa entrar apenas por meio de logon único.
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. Clique em **Criar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooImage retransmissão.

![Atribuir usuário][200] 

**tooassign Britta Simon tooImage retransmissão, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **imagem retransmissão**.

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.    

Quando você clica em um bloco de imagem retransmissão Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de retransmissão de imagem.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

