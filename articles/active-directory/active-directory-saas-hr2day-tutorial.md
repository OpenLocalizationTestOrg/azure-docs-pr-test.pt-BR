---
title: "Tutorial: Integração do Azure Active Directory ao HR2day by Merces | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e HR2day por Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Tutorial: Integração do Active Directory do Azure ao HR2day by Merces

Neste tutorial, você aprenderá como toointegrate HR2day por Merces com o Azure Active Directory (AD do Azure).

Integrando HR2day por Merces com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHR2day por Merces.
- Você pode permitir que os usuários tooautomatically obter conectado tooHR2day por Merces com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central – Olá portal do Azure.

Para obter mais informações sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com HR2day por Merces, você precisa Olá itens a seguir:

- Uma assinatura do Azure AD.
- Uma assinatura do HR2day by Merces habilitada para logon único.

> [!NOTE]
> Não é recomendável usar uma saudação de tootest do ambiente de produção as etapas neste tutorial.

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção a menos que seja necessário.
- Obtenha uma [avaliação gratuita de um mês do Azure AD](https://azure.microsoft.com/pricing/free-trial/) se você ainda não o fez.  

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação que é descrito aqui consiste em duas principais blocos de construção:

1. Adicionando HR2day por Merces da Galeria de saudação.
2. Configurar e testar o logon único do Azure AD.

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Adicionar HR2day por Merces da Galeria de saudação
integração de saudação do tooconfigure do HR2day por Merces no AD do Azure, adicionar HR2day por Merces na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd HR2day por Merces da Galeria hello, Olá execute as etapas a seguir:**

1. Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, selecione Olá **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Vá muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd um novo aplicativo, selecione Olá **novo aplicativo** botão na parte superior de Olá Olá da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **HR2day por Merces**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. No painel de resultados de saudação, selecione **HR2day por Merces**e, em seguida, selecione Olá **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o HR2day by Merces, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário contraparte Olá HR2day por Merces tooa usuário no AD do Azure. Em outras palavras, você precisa tooestablish um link entre um usuário do AD do Azure e o usuário relacionado de saudação em HR2day por Merces.

HR2day por Merces, atribuir Olá **nome de usuário** no AD do Azure muito **Username** tooestablish relação de saudação.

tooconfigure e teste de logon único do AD do Azure com HR2day por Merces, você precisa Olá toocomplete blocos de construção a seguir:

1. [Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on): habilitar seu usuários toouse esse recurso.
2. [Criar um usuário de teste do Azure AD](#creating-an-azure-ad-test-user): para testar o logon único do Azure AD com Brenda Fernandes.
3. [Criar um HR2day pelo usuário de teste Merces](#creating-an-hr2day-by-merces-test-user): criar um equivalente de Britta Simon HR2day por Merces é vinculado toohello AD do Azure representação do usuário.
4. [Atribuir um usuário de teste de saudação do AD do Azure](#assigning-the-azure-ad-test-user): habilitar Britta Simon toouse logon único do AD do Azure.
5. [Testar o logon único](#testing-single-sign-on): verificar se a configuração de saudação funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu HR2day pelo aplicativo Merces.

**tooconfigure AD do Azure-logon único com HR2day por Merces, levar Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **HR2day por Merces** página de integração de aplicativos, selecione **o logon único**.

    ![Configurar o Logon Único][4]

2. tooenable logon único, em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon**.
 
    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. Em Olá **HR2day Merces domínio e URLs** seção, levar Olá etapas a seguir:

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. Em Olá **URL de logon** caixa, digite uma URL usando o saudação padrão a seguir: `https://<tenantname>.force.com/<instancename>`.

    b. Em Olá **identificador** caixa, digite uma URL usando o saudação padrão a seguir: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de logon real hello e o identificador. Olá contato [HR2day pela equipe de suporte de cliente Merces](mailto:servicedesk@merces.nl) tooget esses valores. 
 


4. Em Olá **o certificado de autenticação SAML** seção, selecione **Certificate(Base64)**e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. Esta seção descreve como tooenable usuários tooauthenticate tooHR2day por Merces com suas contas no AD do Azure. Eles fazem isso usando a federação com base no protocolo SAML de saudação.

    O HR2day pelo aplicativo Merces espera asserções SAML de saudação em um formato específico, o que exige que o token SAML tooadd atributo personalizado mapeamentos tooyour. Olá captura de tela a seguir mostra um exemplo disso. 

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Antes de configurar de asserção SAML hello, você deverá contatar Olá [HR2day pela equipe de suporte do cliente Merces](mailto:servicedesk@merces.nl) e solicitar o valor de saudação do atributo de identificador exclusivo de saudação para seu locatário. Você precisa de etapas de Olá de toocomplete esse valor na próxima seção, Olá. 

6. Em Olá **o logon único** caixa de diálogo Olá **atributos de usuário** seção, configure o atributo de token de SAML Olá conforme Olá a imagem a seguir. Depois, pegue Olá etapas a seguir.
    
      | Nome do atributo    |   Valor do atributo |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      a. Olá tooopen **Adicionar atributo** caixa de diálogo, selecione **Adicionar atributo**.

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurar o Logon Único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. Em Olá **nome** , digite **ATTR_LOGINCLAIM**.

    c. De saudação **valor** lista, selecione **JOIN ()**.

    d. De saudação **String1** lista, selecione **user.mail**.

    e. Para **String2**, digite Olá identificador exclusivo que é fornecido pela sua equipe HR2day.

    f. Em Olá **separador** , digite  **@** .
    
    g. Selecione **Ok**.

7. Selecione Olá **salvar** botão.

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. Em Olá **HR2day pela configuração Merces** seção, selecione **HR2day configurar por Merces** tooopen Olá **configurar o logon** janela. Saudação de cópia **URL de logout**, **ID da entidade SAML**, e **Single Sign-On URL do serviço SAML** de saudação **referência rápida** seção.

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure SSO para seu aplicativo, entre em contato com hello [HR2day pela equipe de suporte de cliente Merces](mailTo:servicedesk@merces.nl). Anexar Olá baixado **Certificate(Base64)** tooyour email de arquivo. Também fornecem Olá **URL de logout**, **ID da entidade SAML**, e **Single Sign-On URL do serviço SAML** para que eles podem ser configurados para integração com o SSO.

    > [!NOTE]
    >Mencione toohello Merces equipe que essa integração precisa Olá toobe ID de entidade com um padrão de saudação **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar este aplicativo de saudação **do Active Directory** > **aplicativos empresariais** seção, selecione Olá **Single Sign-On** guia. Então Olá acesso incorporado documentação por meio de saudação **configuração** seção na parte inferior da saudação. Você pode ler mais sobre recurso de documentação embedded Olá no hello [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, Olá execute as etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, selecione Olá **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, selecione **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, selecione **adicionar** na parte superior de Olá Olá da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo, Olá execute as etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha**e, em seguida, anote a senha de saudação.

    d. Selecione **Criar**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Criar um usuário de teste do HR2day by Merces

Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no HR2day por Merces. os usuários de saudação de tooadd na conta Olá HR2day, trabalhar com hello [HR2day pela equipe de suporte de cliente Merces](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Se você precisar toocreate um usuário manualmente, entre em contato com o hello [HR2day pela equipe de suporte de cliente Merces](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooHR2day seu acesso por Merces.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHR2day por Merces, Olá execute as etapas a seguir:**

1. Em hello Azure aplicativos de portal, abra Olá exibir, vá toohello exibição de diretório e, em seguida, ir muito**aplicativos empresariais**. Em seguida, selecione **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **HR2day por Merces**.

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. No menu Olá Olá esquerda, selecione **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Selecione Olá **adicionar** botão. Em seguida, no hello **Adicionar atribuição** caixa de diálogo, selecione **usuários e grupos**.

    ![Atribuir usuário][203]

5. Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**.

6. Clique em Olá **selecione** botão.

7. Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá, o objetivo desta seção é tootest Olá de seu AD do Azure única configuração de logon usando o painel de acesso.  

Quando você seleciona Olá HR2day pelo bloco Merces Olá painel de acesso, você obter conectado automaticamente tooyour HR2day pelo aplicativo Merces.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

