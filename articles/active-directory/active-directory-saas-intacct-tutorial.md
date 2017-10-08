---
title: "Tutorial: Integração do Azure Active Directory com o Intacct | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Tutorial: Integração do Active Directory do Azure com o Intacct

Neste tutorial, você aprenderá como toointegrate Intacct com o Azure Active Directory (AD do Azure).

Integrando o Intacct com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooIntacct
- Você pode habilitar seu usuários tooautomatically get conectado tooIntacct (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Intacct, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Intacct

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Intacct da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-intacct-from-hello-gallery"></a>Adicionando Intacct da Galeria de saudação
integração de saudação tooconfigure do Intacct no AD do Azure, você precisa tooadd Intacct da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Intacct da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Intacct**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. No painel de resultados de saudação, selecione **Intacct**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Intacct, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Intacct é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Intacct precisa toobe estabelecida.

No Intacct, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Intacct, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Intacct](#creating-an-intacct-test-user)**  -toohave um equivalente do Britta Simon no Intacct é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Intacct.

**tooconfigure AD do Azure-logon único com Intacct, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Intacct** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. Em Olá **Intacct domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de resposta real. Entre em contato com [equipe de suporte do Intacct](https://us.intacct.com/support) tooget esse valor.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. Em Olá **Intacct configuração** seção, clique em **configurar Intacct** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. Em uma janela de navegador web diferente, entre no site da empresa Intacct tooyour como um administrador.

8. Clique em Olá **empresa** guia e, em seguida, clique em **informações sobre a empresa**.

    ![Empresa](./media/active-directory-saas-intacct-tutorial/ic790037.png "Empresa")

9. Clique em Olá **segurança** guia e, em seguida, clique em **editar**.

    ![Segurança](./media/active-directory-saas-intacct-tutorial/ic790038.png "Segurança")

10. Em Olá **(SSO) do logon único** , execute Olá etapas a seguir:

    ![Logon único](./media/active-directory-saas-intacct-tutorial/ic790039.png "logon único")

    a. Selecione **Habilitar logon único**.

    b. Para **Tipo de provedor de identidade**, selecione **SAML 2.0**.

    c. Em **URL do emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.
   
    d. Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.

    e. Abra seu **base 64** codificado certificado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado** caixa.
   
    f. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-intacct-test-user"></a>Criação de um usuário de teste do Intacct

tooset os usuários do AD do Azure para que possam entrar em tooIntacct, eles devem ser provisionados no Intacct. Para o Intacct, o provisionamento é uma tarefa manual.

**contas de usuário tooprovision, execute Olá etapas a seguir:**

1. Entrar tooyour **Intacct** locatário.

2. Clique em Olá **empresa** guia e, em seguida, clique em **usuários**.

    ![Usuários](./media/active-directory-saas-intacct-tutorial/ic790041.png "Usuários")
3. Clique em Olá **adicionar** guia.

    ![Adicionar](./media/active-directory-saas-intacct-tutorial/ic790042.png "Adicionar")
4. Em Olá **informações do usuário** , execute Olá etapas a seguir:

    ![Informações do Usuário](./media/active-directory-saas-intacct-tutorial/ic790043.png "informações do Usuário")

    a. Digite hello **ID de usuário**, Olá **Sobrenome**, **nome**, Olá **endereço de Email**, Olá **título**, e hello **Phone** de uma conta do AD do Azure que você deseja tooprovision em Olá **informações do usuário** seção.

    b. Selecione Olá **privilégios de administrador** de uma conta do AD do Azure que você deseja tooprovision.
   
    c. Clique em **Salvar**. proprietário de conta do AD do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.

>[!NOTE]
>contas de usuário do AD do Azure tooprovision, você pode usar outras ferramentas de criação de conta de usuário do Intacct ou APIs fornecidas pela Intacct.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIntacct.

![Atribuir usuário][200] 

**tooassign Britta Simon tooIntacct, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Intacct**.

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Intacct Olá Olá painel de acesso, você deve ser conectado automaticamente tooyour Intacct aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

