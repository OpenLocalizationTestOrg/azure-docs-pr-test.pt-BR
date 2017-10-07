---
title: "Tutorial: integração do Azure Active Directory com o software Cezanne HR | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o software de RH Cezanne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Tutorial: integração do Azure Active Directory com o software Cezanne HR

Neste tutorial, você aprenderá como toointegrate Cezanne HR software com o Azure Active Directory (AD do Azure).

Integração de software de RH Cezanne com o Azure AD fornece Olá benefícios a seguir. Você pode:

- Controlar no AD do Azure que tenha acesso tooCezanne software de RH.
- Habilite seus usuários de entrada tooautomatically software tooCezanne HR com logon único (SSO) com suas contas do AD do Azure.
- Gerenciar suas contas em um local central: Olá portal do Azure.

toolearn mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e SSO com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com HR Cezanne software, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do software Cezanne HR com SSO habilitado

> [!NOTE]
> tootest Olá etapas deste tutorial, é recomendável que você não use um ambiente de produção.

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste. 

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

* Adicionar software de RH Cezanne da Galeria de saudação
* Configurar e testar o SSO do Azure AD

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Adicionar software Cezanne HR da Galeria de saudação
tooconfigure a integração de saudação do software Cezanne HR no AD do Azure, adicione o software de RH Cezanne da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

tooadd Cezanne HR software da Galeria hello, Olá a seguir:

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão. 

    ![botão de "Active Directory do Azure" Hello][1]

2. Selecione **Aplicativos empresariais** > **Todos os aplicativos**.

    ![Olá link de "Todos os aplicativos"][2]
    
3. tooadd um novo aplicativo, na parte superior de saudação do hello **todos os aplicativos** caixa de diálogo, selecione **novo aplicativo**.

    ![Olá "Novo application" botão][3]

4. Na caixa de pesquisa hello, digite **Cezanne HR Software**.

    ![caixa de pesquisa Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Na lista de resultados de saudação, selecione **Cezanne HR Software** e, em seguida, selecione Olá **adicionar** botão aplicativo hello de tooadd.

    ![lista de resultados de saudação](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configura e testa o SSO do Azure AD com o software Cezanne HR, com base em uma usuária de teste chamada “Brenda Fernandes”.

Para SSO toowork, AD do Azure precisa de usuário do AD do Azure tooknow Olá Cezanne HR software contraparte toohello. Em outras palavras, você deve estabelecer uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá no hello HR Cezanne software.

relação de link tooestablish hello, atribuir Olá software HR Cezanne **nome de usuário** valor como Olá AD do Azure **Username** valor.

tooconfigure e teste SSO de AD do Azure usando o software de RH Cezanne, Olá completa blocos de construção a seguir.

### <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Nesta seção, você pode habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO no seu aplicativo HR Cezanne fazendo Olá seguinte:

1. Em Olá portal do Azure, Olá **Cezanne HR Software** página de integração de aplicativos, selecione **o logon único**.

    ![Olá "Single sign-on" comando][4]

2. tooenable SSO, em Olá **o logon único** caixa de diálogo, selecione Olá **modo** como **baseado no SAML logon**.
 
    ![caixa de "Modo de" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. Em **Cezanne HR Software domínio e URLs**, Olá a seguir:

    ![Olá seção "Cezanne HR Software e URLs de domínio"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. Em Olá **URL de logon** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. Em Olá **URL de resposta** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Olá valores anteriores não são reais. Atualizá-las com a URL de resposta real hello e URL de entrada hello. valores tooobtain Olá Olá contato [Cezanne HR equipe de suporte de cliente de software](mailto:info@cezannehr.com).

4. Em **o certificado de autenticação SAML**, selecione **certificado (Base64)**e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Olá seção de "Certificado de autenticação SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Selecione **Salvar**.

    ![botão de "Salvar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. Em **a configuração de Software de RH Cezanne**, selecione **configurar Software de RH Cezanne** tooopen Olá **configurar o logon** janela. Saudação de cópia **ID da entidade SAML** e **serviço de logon único SAML** URL da saudação **referência rápida** seção.

    ![Olá seção "Configuração de Software de RH Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no locatário do software de RH Cezanne tooyour como um administrador.

8. No painel esquerdo do hello, selecione **configuração do sistema**. Selecione **Configurações de Segurança** > **Configuração de Logon Único**.

    ![link de "Única configuração de logon" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. Em Olá **permitem que os usuários toolog usando Olá serviços Single Sign-On (SSO) a seguir** painel, selecione Olá **SAML 2.0** caixa de seleção e selecione Olá **configuração avançada de** opção.

    ![Opções de logon único em serviços](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Selecione **Adicionar Novo**.

    ![botão "Adicionar novo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. Em **provedores de identidade SAML 2.0**, Olá a seguir:

    ![Olá seção "Provedores de identidade do SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. Em Olá **nome de exibição** , digite o nome de saudação do seu provedor de identidade.

    b. Em Olá **identificador da entidade** caixa, cole Olá **ID da entidade SAML** que você copiou da saudação portal do Azure. 

    c. Em Olá **SAML associação** caixa de listagem, selecione **POST**.

    d. Em Olá **ponto de extremidade de serviço de Token de segurança** caixa, cole Olá **serviço de logon único SAML** URL que você copiou da saudação portal do Azure. 
    
    e. Em Olá **nome do atributo de ID de usuário** , digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. Olá tooupload baixado o certificado do AD do Azure, selecione Olá **carregar** botão.
    
    g. Selecione **OK**. 

12. Selecione **Salvar**.

    ![botão de "Salvar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Como configurar o aplicativo hello, você pode ler uma versão concisa do hello precedem instruções em Olá [portal do Azure](https://portal.azure.com). Depois de adicionar o aplicativo hello da saudação **do Active Directory** > **aplicativos empresariais** seção, selecione Olá **o logon único** guia. Então Olá acesso incorporado documentação da saudação **configuração** seção. 

toolearn mais sobre o recurso de documentação do embedded hello, consulte [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Nesta seção, você cria o usuário de teste Britta Simon em Olá portal do Azure.

![usuário de teste Olá Britta Simon][100]

toocreate um usuário de teste no AD do Azure, Olá a seguir:

1. Em Olá **portal do Azure**, no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão.

    ![botão de "Active Directory do Azure" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. lista de saudação do toodisplay de usuários, selecionados **usuários e grupos** > **todos os usuários**.
    
    ![Olá link de "Todos os usuários"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Olá **todos os usuários** caixa de diálogo é aberta.

3. Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.
 
    ![botão de "Adicionar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo caixa, Olá a seguir:
 
    ![caixa de diálogo de "Usuário" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa, digite o usuário Britta Simon **endereço de email**.

    c. Selecione Olá **Mostrar senha** caixa de seleção e valor de saudação Observação que foi gerado em Olá **senha** caixa.

    d. Selecione **Criar**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Criar um usuário de teste do software Cezanne HR

toosign de usuários tooenable AD do Azure no software tooCezanne HR, eles devem ser provisionados no software de RH Cezanne. No caso de saudação de RH Cezanne software, o provisionamento é uma tarefa manual.

Provisione uma conta de usuário fazendo Olá seguinte:

1.  Entre no tooyour Cezanne HR site da empresa de software como um administrador.

2.  No painel esquerdo do hello, selecione **configuração do sistema** > **gerenciar usuários** > **adicionar novo usuário**.

    ![link de "Adicionar novo usuário" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "novo usuário")

3.  Em **detalhes da pessoa**, Olá a seguir:

    ![Olá pessoa seção "Detalhes"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "novo usuário")
    
    a. Defina **Internal User (Usuário Interno)** como **OFF (DESATIVADO)**.
    
    b. Em Olá **nome** caixa, tipo hello nome do usuário, por exemplo, **Britta**.  
 
    c. Em Olá **Sobrenome** caixa, tipo hello sobrenome do usuário, por exemplo, **Simon**.
    
    d. Em Olá **email** , digite o endereço de email do usuário hello, por exemplo, Brittasimon@contoso.com.

4.  Em **informações de conta**, Olá a seguir:

    ![Olá seção "Informações de conta"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "novo usuário")
    
    a. Em Olá **Username** , digite o endereço de email do usuário hello, por exemplo, Brittasimon@contoso.com.
    
    b. Em Olá **senha** , digite a senha do usuário hello.
    
    c. Em Olá **função de segurança** selecione **HR Professional**.
    
    d. Selecione **OK**.

5. Em Olá **o logon único** guia Olá **SAML 2.0 identificadores** seção, selecione **adicionar novo**.

    ![botão "Adicionar novo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "usuário")

6. Em Olá **provedor de identidade** caixa de listagem, selecione seu provedor de identidade. Em Olá **identificador de usuário** , digite o endereço de email Olá para conta de teste usuário Britta Simon.

    ![Olá caixas "Provedor de identidade" e "Identificador de usuário"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "usuário")
    
7. Selecione **Salvar**.

    ![botão de "Salvar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "usuário")

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você permitir que o usuário de teste Britta Simon toouse SSO do Azure, concedendo acesso tooCezanne HR software.

![Testar o acesso do usuário][200] 

1. No portal do Azure de Olá, abrir modo de exibição de aplicativos hello e vá toohello exibição de diretório. Selecione **Aplicativos empresariais** > **Todos os aplicativos**.

    ![Olá link de "Todos os aplicativos"][201] 

2. Na lista de aplicativos hello, selecione **Cezanne HR Software**.

    ![lista de "Aplicativos" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. No menu Olá Olá esquerda, selecione **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Selecione **Adicionar**. Em seguida, em Olá **Adicionar atribuição** caixa de diálogo, selecione **usuários e grupos**.

    ![Link “Usuários e Grupos”][203]

5. Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**.

6. Em Olá **usuários e grupos** caixa de diálogo, selecione **selecione**.

7. Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.
    
### <a name="test-sso"></a>Testar o SSO

Nesta seção, você pode testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.

Quando você seleciona o bloco de software de RH Cezanne Olá no painel de acesso de saudação, logon automaticamente tooyour HR Cezanne aplicativo de software.

## <a name="next-steps"></a>Próximas etapas

* [Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é acesso a aplicativos e SSO com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

