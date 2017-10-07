---
title: "Tutorial: integração do Azure Active Directory com o Zscaler ZSCloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>Tutorial: integração do Azure Active Directory com o Zscaler ZSCloud

Neste tutorial, você aprenderá como toointegrate Zscaler ZSCloud com o Azure Active Directory (AD do Azure).

Integrando o Zscaler ZSCloud com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooZscaler ZSCloud
- Você pode habilitar seu usuários tooautomatically get conectado tooZscaler ZSCloud (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Zscaler ZSCloud, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Zscaler ZSCloud

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Zscaler ZSCloud da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>Adicionando Zscaler ZSCloud da Galeria de saudação
integração de saudação tooconfigure do Zscaler ZSCloud no AD do Azure, você precisa tooadd Zscaler ZSCloud na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Zscaler ZSCloud da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Zscaler ZSCloud**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. No painel de resultados de saudação, selecione **Zscaler ZSCloud**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Zscaler ZSCloud, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zscaler ZSCloud é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zscaler ZSCloud precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Zscaler ZSCloud.

tooconfigure e teste de logon único do AD do Azure com o Zscaler ZSCloud, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Definir configurações de proxy](#configuring-proxy-settings)**  -configurações de proxy de saudação tooconfigure no Internet Explorer
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave um equivalente do Britta Simon no Zscaler ZSCloud é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Zscaler ZSCloud.

**tooconfigure AD do Azure-logon único com o Zscaler ZSCloud, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Zscaler ZSCloud** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. Em Olá **Zscaler ZSCloud domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seu usuários em toosign tooyour aplicativo ZScaler ZSCloud.
    
    > [!NOTE] 
    > Você tem tooupdate esse valor com hello URL de logon real. Entre em contato com [equipe de suporte do Zscaler ZSCloud cliente](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. Em Olá **Zscaler ZSCloud configuração** seção, clique em **configurar Zscaler ZSCloud** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. Em uma janela do navegador web diferente, faça logon no tooyour site da empresa ZScaler ZSCloud como um administrador.

8. No menu de saudação na parte superior de saudação, clique em **administração**.
   
    ![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administração")

9. Em **Gerenciar Administradores e Funções**, clique em **Gerenciar Usuários e Autenticação**.   
            
    ![Gerenciar usuários e autenticação](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Gerenciar usuários e autenticação")

10. Em Olá **escolher opções de autenticação para sua organização** , execute Olá etapas a seguir:   
                
    ![Autenticação](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticação")
   
    a. Selecione **Autenticar usando o Logon Único do SAML**.

    b. Clique em **Configurar Parâmetros de Logon Único do SAML**.

11. Em Olá **configurar parâmetros único do SAML logon** página de diálogo Executar Olá etapas a seguir e, em seguida, clique em **feito**

    ![Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Logon Único")
    
    a. Saudação de colar **Single Sign-On URL do serviço SAML** valor em Olá **URL de usuários de toowhich do Portal SAML Olá são enviados para autenticação** caixa de texto.
    
    b. Em Olá **atributo que contém o nome de logon** caixa de texto, tipo **NameID**.
    
    c. tooupload seu certificado baixado, clique em **Zscaler pem**.
    
    d. Selecione **Habilitar Provisionamento Automático do SAML**.

12. Em Olá **configurar autenticação de usuário** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administração")
    
    a. Clique em **Salvar**.

    b. Clique em **Ativar Agora**.

## <a name="configuring-proxy-settings"></a>Definindo as configurações de proxy
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>configurações de proxy de saudação tooconfigure no Internet Explorer

1. Inicie o **Internet Explorer**.

2. Selecione **opções da Internet** de saudação **ferramentas** menu para abrir Olá **opções da Internet** caixa de diálogo.   
    
     ![Opções da Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opções da Internet")

3. Clique em Olá **conexões** guia.   
  
     ![Conexões](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Conexões")

4. Clique em **configurações da LAN** tooopen Olá **configurações da LAN** caixa de diálogo.

5. Olá seção do servidor Proxy, execute Olá etapas a seguir:   
   
    ![Servidor proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Servidor proxy")

    a. Selecione **Usar um servidor proxy para LAN**.

    b. Na caixa de texto de endereço hello, digite **gateway.zscalerone.net**.

    c. Na caixa de texto de porta hello, digite **80**.

    d. Selecione **Ignorar servidor proxy para endereços locais**.

    e. Clique em **Okey** tooclose Olá **configurações de rede Local (LAN)** caixa de diálogo.

6. Clique em **Okey** tooclose Olá **opções da Internet** caixa de diálogo.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.

### <a name="creating-a-zscaler-zscloud-test-user"></a>Criar um usuário de teste do Zscaler ZSCloud

toolog de usuários do AD do Azure de tooenable tooZScaler ZSCloud, elas devem ser provisionado tooZScaler ZSCloud.  
No caso de saudação do ZScaler ZSCloud, o provisionamento é uma tarefa manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisionamento de usuário, execute Olá etapas a seguir:

1. Faça logon no tooyour **Zscaler** locatário.

2. Clique em **Administração**.   
   
    ![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administração")

3. Clique em **Gerenciamento de Usuários**.   
        
     ![Adicionar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Adicionar")

4. Em Olá **usuários** , clique em **adicionar**.
      
    ![Adicionar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Adicionar")

5. Na seção Adicionar usuário do hello, execute Olá etapas a seguir:
        
    ![Adicionar Usuário](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Adicionar Usuário")
   
    a. Saudação de tipo **UserID**, **nome de exibição do usuário**, **senha**, **Confirmar senha**e, em seguida, selecione **grupos**e hello **departamento** de uma conta válida do AAD você deseja tooprovision.

    b. Clique em **Salvar**.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros ZScaler ZSCloud usuário conta ou APIs fornecidas pelo ZScaler ZSCloud tooprovision contas de usuário do AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZscaler ZSCloud.

![Atribuir usuário][200] 

**tooassign tooZscaler Britta Simon ZSCloud, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Zscaler ZSCloud**.

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.

Quando você clica em Olá Zscaler ZSCloud lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo Zscaler ZSCloud.

Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

