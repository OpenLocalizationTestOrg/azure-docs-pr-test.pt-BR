---
title: "Tutorial: Integração do Azure Active Directory ao Asana | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>Tutorial: Integração do Azure Active Directory ao Asana

Neste tutorial, você aprenderá como toointegrate Asana com o Azure Active Directory (AD do Azure).

Integrando Asana com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAsana
- Você pode habilitar seu usuários tooautomatically get conectado tooAsana (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Asana, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Asana

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Asana da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-asana-from-hello-gallery"></a>Adicionando Asana da Galeria de saudação
integração de saudação tooconfigure de Asana no AD do Azure, você precisa tooadd Asana da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Asana da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Asana**, selecione **Asana** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Asana, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Asana é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Asana precisa toobe estabelecida.

Asana, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Asana, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Asana](#create-an-asana-test-user)**  -toohave um equivalente do Britta Simon em Asana é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Asana.

**tooconfigure AD do Azure-logon único com Asana, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Asana** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. Em Olá **Asana domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite a URL:`https://app.asana.com/`

    b. Em Olá **identificador** caixa de texto, o valor de tipo:`https://app.asana.com/`
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. Em Olá **Asana configuração** seção, clique em **configurar Asana** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. Em uma janela de navegador diferente, logon tooyour Asana aplicativo. tooconfigure SSO no Asana, configurações de espaço de trabalho do access Olá clicando no nome do espaço de trabalho Olá no canto superior direito de saudação da tela hello. Em seguida, clique em **\<nome do espaço de trabalho\>Configurações**. 
   
    ![configurações de sso do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. Em Olá **as configurações da organização** janela, clique em **administração**. Em seguida, clique em **membros devem efetuar logon por meio de SAML** tooenable configuração de SSO de saudação. Olá execute Olá etapas a seguir:
   
    ![Definições de Configurar Organização de Logon Único](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. Em Olá **URL da página de entrada** caixa de texto, colar Olá **Single Sign-On URL do serviço SAML**.

     b. Clique com botão direito certificado Olá baixado do portal do Azure e abrir o arquivo de certificado hello usando o bloco de notas ou seu editor de texto preferido. Saudação de copiar conteúdo entre hello começar e Olá final certificado título e colá-lo em hello **certificado x. 509** caixa de texto.

9. Clique em **Salvar**. Vá muito[Asana guia para configurar SSO](https://asana.com/guide/help/premium/authentication#gl-saml) se precisar de assistência adicional.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![botão Adicionar de saudação](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-an-asana-test-user"></a>Criar um usuário de teste do Asana

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Asana.

1. Em **Asana**, vá toohello **equipes** seção no painel esquerdo da saudação. Clique em hello mais entrar botão. 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Digite o email Olá britta.simon@contoso.com Olá caixa de texto e, em seguida, selecione **convidar**.

3. Clique em **Enviar Convite**. novo usuário de saudação receberá um email em sua conta de email. Ela será necessário toocreate e validar a conta de saudação.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAsana.

![Atribuir função de usuário Olá][200]

**tooassign Britta Simon tooAsana, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Asana**.

    ![link de Asana Olá na lista de aplicativos Olá](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

objetivo Olá desta seção é tootest seu AD do Azure-logon único.

Acesse a página de logon tooAsana. No texto de endereço de Email hello, inserir o endereço de email Olá britta.simon@contoso.com. Deixe Olá caixa de texto de senha em branco e, em seguida, clique em **logon**. Você será redirecionado tooAzure AD página de logon. Preencha suas credenciais do Azure AD. Agora, você está conectado ao Asana.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
