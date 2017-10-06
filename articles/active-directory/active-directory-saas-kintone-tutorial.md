---
title: "Tutorial: Integração do Azure Active Directory com o Kintone | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a>Tutorial: integração do Azure Active Directory com o Kintone

Neste tutorial, você aprenderá como toointegrate Kintone com o Azure Active Directory (AD do Azure).

Integrando o Kintone com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooKintone
- Você pode habilitar seu usuários tooautomatically get conectado tooKintone (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Kintone, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Kintone com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Kintone da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-kintone-from-hello-gallery"></a>Adicionando Kintone da Galeria de saudação
integração de saudação tooconfigure do Kintone no AD do Azure, você precisa tooadd Kintone da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Kintone da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Kintone**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. No painel de resultados de saudação, selecione **Kintone**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Kintone, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Kintone é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Kintone precisa toobe estabelecida.

No Kintone, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Kintone, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Kintone](#creating-a-kintone-test-user)**  -toohave um equivalente do Britta Simon no Kintone é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kintone.

**tooconfigure AD do Azure-logon único com o Kintone, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Kintone** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. Em Olá **Kintone domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.kintone.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente Kintone](https://www.kintone.com/contact/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. Em Olá **Kintone configuração** seção, clique em **configurar Kintone** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. Em outra janela do navegador da Web, faça logon no site da sua empresa do **Kintone** como administrador.

8. Clique em **Configurações**.
   
    ![Configurações](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configurações")

9. Clique em **Usuários e administração do sistema**.
   
    ![Administração do Sistema e de Usuários](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administração do Sistema e de Usuários")

10. Em **Administração do Sistema \> Segurança**, clique em **Logon**.
   
    ![Logon](./media/active-directory-saas-kintone-tutorial/ic785881.png "Logon")

11. Selecione **Habilitar a autenticação do SAML**.
   
    ![Autenticação SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticação SAML")

12. Olá seção autenticação SAML, execute Olá etapas a seguir:
    
    ![Autenticação SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticação SAML")
    
    a. Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
    b. Em Olá **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.
    
    c. Clique em **procurar** tooupload seu certificado baixado.
    
    d. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-kintone-test-user"></a>Criação de um usuário de teste do Kintone

tooenable AD do Azure usuários toolog em tooKintone, eles devem ser provisionados no Kintone.  
No caso de saudação do Kintone, o provisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de usuário, execute Olá etapas a seguir:

1. Faça logon no tooyour **Kintone** site da empresa como um administrador.

2. Clique em **Configuração**.
   
    ![Configurações](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configurações")

3. Clique em **Usuários e administração do sistema**.
   
    ![Administração do Sistema e de Usuários](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administração do Sistema e de Usuários")

4. Em **Administração de Usuários**, clique em **Departamentos e Usuários**.
   
    ![Departamento e Usuários](./media/active-directory-saas-kintone-tutorial/ic785888.png "Departamento e Usuários")

5. Clique em **Novo Usuário**.
   
    ![Novos Usuários](./media/active-directory-saas-kintone-tutorial/ic785889.png "novos Usuários")

6. Em Olá **novo usuário** , execute Olá etapas a seguir:
   
    ![Novos Usuários](./media/active-directory-saas-kintone-tutorial/ic785890.png "novos Usuários")
   
    a. Digite um **exibir nome**, **nome de logon**, **nova senha**, **Confirmar senha**, **endereço de email**, e outros detalhes de uma conta válida do AAD que você deseja tooprovision em Olá relacionados caixas de texto.
 
    b. Clique em **Salvar**.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros Kintone usuário conta ou APIs fornecidas pela Kintone tooprovision contas de usuário do AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKintone.

![Atribuir usuário][200] 

**tooassign Britta Simon tooKintone, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Kintone**.

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco Kintone Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Kintone aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

