---
title: "Tutorial: integração do Azure Active Directory com o TINFOIL SECURITY | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Tutorial: integração do Azure Active Directory com o TINFOIL SECURITY

Neste tutorial, você aprenderá como toointegrate TINFOIL SECURITY com o Azure Active Directory (AD do Azure).

Integração do TINFOIL SECURITY com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTINFOIL segurança
- Você pode habilitar seu usuários tooautomatically get conectado tooTINFOIL segurança (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com TINFOIL SECURITY, é necessário Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do TINFOIL SECURITY habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar TINFOIL SECURITY da Galeria de saudação
2. Configurar e testar logon único do Azure AD

## <a name="add-tinfoil-security-from-hello-gallery"></a>Adicionar TINFOIL SECURITY da Galeria de saudação
integração de saudação tooconfigure do TINFOIL SECURITY no AD do Azure, você precisa tooadd TINFOIL SECURITY na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd TINFOIL SECURITY da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **TINFOIL SECURITY**, selecione **TINFOIL SECURITY** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![TINFOIL SECURITY da galeria](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o TINFOIL SECURITY com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no TINFOIL SECURITY é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TINFOIL SECURITY precisa toobe estabelecida.

TINFOIL SECURITY, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com TINFOIL SECURITY, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave um equivalente do Britta Simon no TINFOIL SECURITY que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do TINFOIL SECURITY.

**tooconfigure AD do Azure-logon único com TINFOIL SECURITY, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **TINFOIL SECURITY** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Logon baseado em SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. Em Olá **TINFOIL SECURITY domínio e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.

    ![Configurar Logon Único](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** valor.

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:
    
    ![Atributos](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Atributos")
    
    | Nome do atributo    |   Valor do atributo |
    | ------------------- | -------------------- |
    | accountid | UXXXXXXXXXXXXX |
    
    a. Clique em **adicionar atributo de usuário**.
    
    ![ADICIONAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Atributos")
    
    ![ADICIONAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Atributos")
    
    b. Em Olá **nome do atributo** caixa de texto, tipo **accountid**.
    
    c. Em Olá **o valor do atributo** caixa de texto, colar Olá conta valor da ID que você obterá mais tarde no tutorial de saudação.
    
    d. Clique em **OK**.    

6. Clique no botão **Salvar** .

    ![Botão Salvar](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. Em Olá **TINFOIL SECURITY Configuration** seção, clique em **configurar TINFOIL SECURITY** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. Em uma janela diferente do navegador da Web, faça logon no site da empresa TINFOIL SECURITY como administrador.

9. Na barra de ferramentas de saudação na parte superior do hello, clique em **minha conta**.
   
    ![Painel](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Painel")

10. Clique em **Segurança**.
   
    ![Segurança](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Segurança")

11. Em Olá **Single Sign-On** configuração de página, execute Olá etapas a seguir:
   
    ![Logon Único](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Logon Único")
   
    a. Selecione **Habilitar SAML**.
   
    b. Clique em **Configuração Manual**.
   
    c. Em **URL de postagem de SAML** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure
   
    d. Em **impressão digital do certificado SAML** caixa de texto valor Olá colar **impressão digital** que você copiou de **o certificado de autenticação SAML** seção.
  
    e. Cópia **seu ID de conta** valor e cole o valor de saudação em **o valor do atributo** textbox em **Adicionar atributo** seção no portal do Azure.
   
    f. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Usuários e grupos -> Todos os usuários ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Usuário](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Criar um usuário de teste do TINFOIL SECURITY

Em ordem tooenable AD do Azure usuários toolog no TINFOIL SECURITY, eles devem ser provisionados no TINFOIL SECURITY. No caso de saudação do TINFOIL SECURITY, o provisionamento é uma tarefa manual.

**tooget um usuário provisionado, execute Olá etapas a seguir:**

1. Se o usuário Olá faz parte de uma conta da empresa, será necessário muito[entre em contato com a equipe de suporte do TINFOIL SECURITY Olá](https://www.tinfoilsecurity.com/contact) tooget Olá conta de usuário.

2. Se Olá é um usuário regular do TINFOIL SECURITY SaaS, usuário Olá pode adicionar tooany um colaborador de sites saudação do usuário. Email desse aciona um toosend de processo especificado um convite toohello toocreate uma nova conta de usuário do TINFOIL SECURITY.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros TINFOIL SECURITY usuário conta ou APIs fornecidas pelo TINFOIL SECURITY tooprovision contas de usuário do AD do Azure.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTINFOIL segurança.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTINFOIL segurança, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **TINFOIL SECURITY**.

    ![selecione TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco TINFOIL SECURITY Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de TINFOIL SECURITY. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

