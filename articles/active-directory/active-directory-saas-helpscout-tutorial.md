---
title: "Tutorial: Integração do Azure Active Directory com o Help Scout | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Scout ajuda."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Tutorial: integração do Azure Active Directory com o Help Scout

Neste tutorial, você aprenderá como toointegrate ajuda atendente com o Azure Active Directory (AD do Azure).

Você obtém Olá seguindo os benefícios da integração Scout ajudar com o Azure AD:

- No AD do Azure, você pode controlar quem tem acesso tooHelp Scout.
- Você pode entrar automaticamente no seu tooHelp usuários Scout usando logon único e uma conta de usuário do AD do Azure.
- Você pode gerenciar suas contas em um local central, Olá portal do Azure.

toolearn mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooset a integração do AD do Azure com Scout ajuda, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Help Scout, com o logon único ativado 

> [!NOTE]
> Se você testar etapas Olá neste tutorial, é recomendável que você não testá-las em um ambiente de produção.

Recomendações para testar etapas Olá neste tutorial:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. 

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicione Scout ajuda da Galeria de saudação.
2. Configurar e testar o logon único do Azure AD.

## <a name="add-help-scout-from-hello-gallery"></a>Adicionar Scout ajuda da Galeria de saudação
tooset a integração de saudação do Scout ajudar com o AD do Azure, na Galeria de hello, adicionar lista de tooyour de ajudar Scout de aplicativos SaaS gerenciados.

tooadd Scout ajuda da Galeria de saudação:

1. Em Olá [portal do Azure](https://portal.azure.com), no hello menu à esquerda, selecione **Active Directory do Azure**. 

    ![botão de Active Directory do Azure Olá][1]

2. Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.

    ![página de aplicativos de empresa Olá][2]
    
3. tooadd um novo aplicativo, selecione **novo aplicativo**.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Scout ajuda**. Nos resultados da pesquisa hello, selecione **ajuda Scout**e, em seguida, selecione **adicionar**.

    ![Ajuda Scout na lista de resultados de saudação](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configurar e testar o logon único do Azure AD

Nesta seção, você vai configurar e testar o logon único do Azure AD com o Help Scout, com base em uma usuária de teste chamada *Brenda Fernandes*.

Para toowork de logon único, o AD do Azure precisa tooknow Olá AD do Azure contraparte usuário Scout ajuda. Uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Scout ajuda deve ser estabelecida.

Olá tooestablish referente à relação, na Ajuda Scout, **Username**, atribuir valor Olá Olá **nome de usuário** no AD do Azure.

tooconfigure e teste de logon único do AD do Azure com Scout ajudar, Olá concluir tarefas a seguir:

1. [Configurar o logon único do Azure AD](#set-up-azure-ad-single-sign-on). Configura um usuário toouse esse recurso.
2. [Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user). Testes do AD do Azure-logon único com o usuário Olá Britta Simon.
3. [Criar um usuário de teste do Help Scout](#create-a-help-scout-test-user). Cria um equivalente de Britta Simon Scout ajuda que é vinculado toohello representação do AD do Azure do usuário hello.
4. [Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user). Define o Britta Simon toouse logon único do AD do Azure.
5. [Testar o logon único](#test-single-sign-on). Verifica que se a configuração de saudação funciona.

### <a name="set-up-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você deve configurar o AD do Azure-logon único no portal do Azure de saudação. Em seguida, define o logon único no aplicativo Help Scout.

tooset o AD do Azure-logon único com Scout ajuda:

1. Em Olá portal do Azure, Olá **ajuda Scout** página de integração de aplicativos, selecione **o logon único**.
 
    ![Link Configurar logon único][4]

2. Em Olá **o logon único** página, para **modo**, selecione **baseado no SAML logon**.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. Em **ajuda Scout domínio e URLs**, se você quiser tooset o aplicativo hello no modo iniciado pelo IDP, Olá concluir as etapas a seguir:

    1. Em Olá **identificador** caixa, digite uma URL que tenha o saudação padrão a seguir:`urn:auth0:helpscout:<instancename>`

    2. Em Olá **URL de resposta** caixa, digite uma URL que tenha o saudação padrão a seguir:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Informações de logon único de Domínio e URLs do Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Se você quiser tooset o aplicativo hello no modo iniciado pelo SP, selecione Olá **Mostrar configurações de URL avançadas** caixa de seleção e, em seguida, Olá a seguir:

    * Em Olá **URL de logon** , digite uma URL com hello formato a seguir:`https://secure.helpscout.net/members/login/`

    ![Informações de logon único de Domínio e URLs do Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > valores Hello essas URLs são apenas para demonstração. Atualize valores de saudação com URL de identificador real de saudação e a URL de resposta. entre em contato com tooget esses valores, [a equipe de suporte Scout ajuda](mailto:help@helpscout.com). 

5. Em **o certificado de autenticação SAML**, selecione **Metadata XML**e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Selecione **Salvar**.

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset backup único logon no lado de ajuda Scout hello, enviar Olá baixado metadados XML arquivo toohello [a equipe de suporte Scout ajuda](mailto:help@helpscout.com). a equipe de suporte de ajuda Scout Olá aplica essa configuração para que Olá SAML único logon conexão está definida corretamente nos dois lados.

> [!TIP]
> Você pode ler uma versão concisa essas instruções Olá [portal do Azure](https://portal.azure.com), enquanto você estiver configurando seu aplicativo! Depois de adicionar o aplicativo hello selecionando **do Active Directory** > **aplicativos empresariais**, selecione Olá **Single Sign-On** guia. Você pode acessar a documentação Olá inserido em Olá **configuração** seção final Olá Olá página. Para saber mais, confira a [documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Nesta seção, no hello portal do Azure, você deve criar um usuário de teste chamado Britta Simon.

![Criar um usuário de teste do Azure AD][100]

toocreate um usuário de teste no AD do Azure:

1. No hello portal do Azure, no menu da esquerda hello, selecione **Active Directory do Azure**.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. lista de saudação do toodisplay de usuários, selecionados **usuários e grupos**e, em seguida, selecione **todos os usuários**.

    ![Selecionar Usuários e grupos e depois Todos os usuários](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, na parte superior de saudação do hello **todos os usuários** página, selecione **adicionar**.

    ![botão Adicionar de saudação](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo, Olá concluir as etapas a seguir:

    1. Em Olá **nome** , digite **BrittaSimon**.

    2. Em Olá **nome de usuário** , digite o endereço de email de saudação do usuário Britta Simon.

    3. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    4. Selecione **Criar**.

        ![caixa de diálogo de usuário Olá](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Criar um usuário de teste do Help Scout

objeto Olá desta seção é toocreate um usuário chamado Britta Simon em Scout ajuda. O Help Scout dá suporte ao provisionamento JIT (Just-In-Time), que é ativado por padrão.

Nesta seção, não há nenhum toocomplete de ação ou tarefa. Se um usuário não existir no Scout ajudar, um novo é criado quando você tenta tooaccess Scout ajuda.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você permitir que usuário Olá Britta Simon toouse AD do Azure-logon único concedendo Olá usuário conta acesso tooHelp Scout.

![Atribuir função de usuário Olá][200] 

tooassign Britta Simon tooHelp Scout:

1. No portal do Azure de Olá, abrir modo de exibição de aplicativos hello e vá toohello exibição de diretório. Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Scout ajuda**.

    ![link de ajuda Scout Olá na lista de aplicativos Olá](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. No menu à esquerda do hello, selecione **usuários e grupos**.

    ![Olá usuários e grupos de link][202]

4. Selecione **Adicionar**. Em seguida, na Olá **Adicionar atribuição** página, selecione **usuários e grupos**.

    ![Painel de atribuição adicionar Olá][203]

5. Em Olá **usuários e grupos** página, na lista de saudação de usuários, selecionados **Britta Simon**.

6. Em Olá **usuários e grupos** página, selecione **selecione**.

7. Em Olá **Adicionar atribuição** página, selecione **atribuir**.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você seleciona lado a lado Olá Scout ajuda no painel de acesso hello, você deve ser conectado automaticamente tooyour aplicativo Scout ajuda.

Para obter mais informações sobre o painel de acesso, consulte [painel de acesso Introdução toohello](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

