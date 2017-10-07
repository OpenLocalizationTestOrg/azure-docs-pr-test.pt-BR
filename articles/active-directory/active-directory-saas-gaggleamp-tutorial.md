---
title: "Tutorial: integração do Azure Active Directory com o GaggleAMP | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a>Tutorial: Integração do Active Directory do Azure com o GaggleAMP

Neste tutorial, você aprenderá como toointegrate GaggleAMP com o Azure Active Directory (AD do Azure).

Integrando GaggleAMP com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooGaggleAMP
- Você pode habilitar seu usuários tooautomatically get conectado tooGaggleAMP (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com GaggleAMP, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do GaggleAMP com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando GaggleAMP da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-gaggleamp-from-hello-gallery"></a>Adicionando GaggleAMP da Galeria de saudação
integração de saudação tooconfigure de GaggleAMP no AD do Azure, você precisa tooadd GaggleAMP da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd GaggleAMP da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **GaggleAMP**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. No painel de resultados de saudação, selecione **GaggleAMP**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o GaggleAMP com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em GaggleAMP é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em GaggleAMP precisa toobe estabelecida.

GaggleAMP, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com GaggleAMP, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave um equivalente do Britta Simon em GaggleAMP é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo GaggleAMP.

**tooconfigure AD do Azure-logon único com GaggleAMP, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **GaggleAMP** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. Em Olá **GaggleAMP domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.gaggleamp.com`

    > [!NOTE] 
    > Olá valor não é real. Valor de saudação de atualização com hello URL de logon real. Entre em contato com [equipe de suporte do cliente GaggleAMP](mailto:sales@gaggleamp.com) tooget valor de saudação. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. Em Olá **GaggleAMP configuração** seção, clique em **configurar GaggleAMP** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. Em outra instância do navegador, navegue toohello página SSO do SAML criada para você por Olá alguns equipe de suporte (por exemplo: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).

8. Em seu **SSO do SAML** página, execute Olá etapas a seguir:  
   
    ![Logon único do GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    a. Em Olá **emissor do provedor de identidade** caixa de texto valor Olá colar **URL do emissor** que você copiou do portal do Azure. 
 
    b. Em Olá **URL provedor de identidade Single Sign-On** caixa de texto valor Olá colar **o URL de serviço de logon único** que você copiou do portal do Azure. 

    c. Clique em **Salvar**      

    d. Enviar Olá **certificado (Base64)** certificado tooyour [a equipe de suporte GaggleAMP](mailto:sales@gaggleamp.com).

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-gaggleamp-test-user"></a>Criação de um usuário de teste do GaggleAMP

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no GaggleAMP. O GaggleAMP dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Um novo usuário é criado durante uma tentativa tooaccess GaggleAMP se ele ainda não existir. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooGaggleAMP.

![Atribuir usuário][200] 

**tooassign Britta Simon tooGaggleAMP, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **GaggleAMP**.

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco GaggleAMP Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour GaggleAMP aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

