---
title: "Tutorial: Integração do Azure Active Directory ao Hightail | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Tutorial: Integração do Azure Active Directory ao Hightail

Neste tutorial, você aprenderá como toointegrate Hightail com o Azure Active Directory (AD do Azure).

Integrando Hightail com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHightail
- Você pode habilitar seu usuários tooautomatically get conectado tooHightail (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Hightail, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Hightail

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Hightail da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-hightail-from-hello-gallery"></a>Adicionando Hightail da Galeria de saudação
integração de saudação tooconfigure de Hightail no AD do Azure, você precisa tooadd Hightail da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Hightail da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Hightail**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. No painel de resultados de saudação, selecione **Hightail**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com Hightail com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Hightail é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Hightail precisa toobe estabelecida.

Hightail, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Hightail, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Hightail](#creating-a-hightail-test-user)**  -toohave um equivalente do Britta Simon em Hightail é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Hightail.

**tooconfigure AD do Azure-logon único com Hightail, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Hightail** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. Em Olá **Hightail domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     Em Olá **URL de resposta** caixa de texto, digite a URL hello como:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE] 
    > Olá valor anterior não é um valor real. Você atualizará o valor de saudação com hello real URL de resposta, que é explicada posteriormente no tutorial de saudação.
 
4. Em Olá **Hightail domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    a. Clique em Olá **Mostrar configurações de URL avançadas**.

    b. Em Olá **URL de logon** caixa de texto, digite a URL hello como:`https://www.hightail.com/loginSSO`

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. Hightail aplicativo espera as asserções SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de saudação **"Atributo"** guia do aplicativo hello. Olá captura de tela a seguir mostra um exemplo. 

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | ------------------- | -------------------- |
    | Nome | user.givenname |
    | Sobrenome | user.surname |
    | Email | user.mail |    
    | UserIdentity | user.mail |
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.

    d. Deixe Olá **Namespace** em branco.
    
    e. Clique em **OK**.

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. Em Olá **Hightail configuração** seção, clique em **configurar Hightail** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    >Antes de configurar Olá logon único no aplicativo Hightail, lista de permissões de seu domínio de email com Hightail da equipe para que todos os usuários que estão usando esse domínio de Olá pode use funcionalidade de logon único.


9. tooget SSO configurado para o seu aplicativo, você precisa em toosign tooyour Hightail locatário como um administrador.
   
    a. No menu de saudação na parte superior do hello, clique Olá **conta** guia e selecione **configurar SAML**.
 
    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    b. Selecione caixa de seleção de saudação do **Ativar autenticação SAML**.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    c. Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado de assinatura de Token SAML** caixa de texto.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    d. Em Olá **autoridade SAML (provedor de identidade)** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** copiada do portal do Azure.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    e. Se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP** selecione **"Provedor de identidade (IdP) iniciada pelo logon"**. Se você usar o **modo iniciado pelo SP**, selecione **"Logon iniciado pelo SP (Provedor de Serviços)"**.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    f. Copiar URL de consumidor SAML Olá para sua instância e cole-o em **URL de resposta** textbox em **Hightail domínio e URLs** seção no portal do Azure.
    
    g. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-hightail-test-user"></a>Criação de um usuário de teste do Hightail

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Hightail. 

Não há itens de ação para você nesta seção. Hightail dá suporte ao provisionamento de usuário just-in-time baseado em declarações personalizadas de hello. Se você tiver configurado as declarações personalizadas Olá conforme mostrado na seção de saudação  **[Configurando o AD do Azure Single Sign-On](#configuring-azure-ad-single-sign-on)**  acima, um usuário é criado automaticamente no aplicativo hello ainda não existir. 

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [a equipe de suporte Hightail](mailto:support@hightail.com). 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHightail.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHightail, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Hightail**.

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco Hightail Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Hightail aplicativo.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

