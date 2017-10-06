---
title: "Tutorial: Integração do Azure Active Directory ao ArcGIS Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Tutorial: Integração do Azure Active Directory ao ArcGIS Online

Neste tutorial, você aprenderá como toointegrate ArcGIS Online com o Azure Active Directory (AD do Azure).

Integrando ArcGIS Online com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooArcGIS Online
- Você pode habilitar seus usuários tooautomatically get conectado tooArcGIS on-line (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o ArcGIS Online, você precisará Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do ArcGIS Online

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ArcGIS Online da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-arcgis-online-from-hello-gallery"></a>Adicionando ArcGIS Online da Galeria de saudação
integração de saudação tooconfigure do ArcGIS Online no AD do Azure, você precisa tooadd ArcGIS Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ArcGIS Online da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do hello diálogo tooadd.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **ArcGIS Online**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. No painel de resultados de saudação, selecione **ArcGIS Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o ArcGIS Online, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ArcGIS Online é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ArcGIS Online precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no ArcGIS Online.

tooconfigure e teste de logon único do AD do Azure com o ArcGIS Online, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste ArcGIS Online](#creating-an-arcgis-online-test-user)**  -toohave um equivalente do Britta Simon no ArcGIS Online que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo ArcGIS Online.

**tooconfigure AD do Azure-logon único do ArcGIS Online, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **ArcGIS Online** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. Em Olá **URLs e domínio Online ArcGIS** , execute Olá etapa a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Esse valor não é hello real. Atualize esse valor com hello URL de logon real. Entre em contato com [equipe de suporte do cliente Online ArcGIS](http://support.esri.com/) tooget esse valor. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. Em outra janela do navegador da Web, faça logon em seu site de empresa ArcGIS como um administrador.

7. Clique em **EDITAR CONFIGURAÇÕES**.

    ![Editar Configurações](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Editar Configurações")

8. Clique em **Segurança**.

    ![Segurança](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Segurança")

9. Em **Logons Corporativos**, clique em **DEFINIR PROVEDOR DE IDENTIDADE**.

    ![Logons Corporativos](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Logons Corporativos")

10. Em Olá **definir provedor de identidade** configuração de página, execute Olá etapas a seguir:
   
    ![Definir Provedor de Identidade](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Definir Provedor de Identidade")
   
    a. Em Olá **nome** caixa de texto, digite o nome da sua organização.

    b. Para **metadados para Olá provedor de identidade da empresa serão fornecidos usando**, selecione **um arquivo**.

    c. tooupload seu arquivo de metadados baixado, clique em **Escolher arquivo**.

    d. Clique em **DEFINIR PROVEDOR DE IDENTIDADE**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-arcgis-online-test-user"></a>Criando um usuário de teste do ArcGIS Online

Ordem tooenable AD do Azure usuários toolog no ArcGIS Online, eles devem ser provisionados no ArcGIS Online.  
No caso de saudação do ArcGIS Online, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **ArcGIS** locatário.

2. Clique em **CONVIDAR MEMBROS**.
   
    ![Convidar Membros](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Convidar Membros")

3. Selecione **Adicionar membros automaticamente sem enviar um email** e, depois, clique em **AVANÇAR**.
   
    ![Adicionar Membros Automaticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Adicionar Membros Automaticamente")

4. Em Olá **membros** caixa de diálogo de página, execute Olá etapas a seguir:
   
     ![Adicionar e examinar](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Adicionar e examinar")
    
     a. Digite hello **Email**, **nome**, e **Sobrenome** de uma conta válida do AAD você deseja tooprovision.
  
     b. Clique em **ADICIONAR E EXAMINAR**.
5. Examinar os dados de saudação você digitou e, em seguida, clique em **adicionar MEMBROS**.
   
    ![Adicionar membro](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Adicionar membro")
        
    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooArcGIS on-line.

![Atribuir usuário][200] 

**tooassign Britta Simon tooArcGIS Online, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ArcGIS Online**.

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco ArcGIS Online Olá Olá painel de acesso, você deve obter aplicativo ArcGIS Online automaticamente assinado em tooyour.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

