---
title: "Tutorial: Integração do Azure Active Directory ao vxMaintain | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Tutorial: Integração do Azure Active Directory ao vxMaintain

Neste tutorial, você aprenderá como vxMaintain toointegrate com o Azure Active Directory (AD do Azure).

Essa integração oferece vários benefícios importantes. Você pode:

- Controle no AD do Azure que tenha acesso toovxMaintain.
- Habilite seus usuários de entrada tooautomatically toovxMaintain com logon único (SSO) com suas contas do AD do Azure.
- Gerenciar suas contas em um local central: Olá portal do Azure.

toolearn mais sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com vxMaintain, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada pelo SSO do vxMaintain

> [!NOTE]
> Quando você testar etapas Olá neste tutorial, é recomendável que você não use um ambiente de produção.

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. 

cenário de saudação que este tutorial descreve consiste em dois elementos básicos:

* Adicionando vxMaintain da Galeria de saudação
* Configurar e testar o logon único do AD do Azure

## <a name="add-vxmaintain-from-hello-gallery"></a>Adicionar vxMaintain da Galeria de saudação
integração de saudação do tooconfigure do vxMaintain com o Azure AD, é necessário vxMaintain tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

vxMaintain tooadd da Galeria de Olá Olá a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com), no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão. 

    ![botão de Active Directory do Azure Olá][1]

2. Selecione **Aplicativos empresariais** > **Todos os aplicativos**.

    ![Painel de "Aplicativos corporativos" Hello][2]
    
3. tooadd um aplicativo, em Olá **todos os aplicativos** caixa de diálogo, selecione **novo aplicativo**.

    ![Olá "Novo application" botão][3]

4. Na caixa de pesquisa hello, digite **vxMaintain**.

    ![lista de suspensa Hello "Único modo de logon"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Na lista de resultados de saudação, selecione **vxMaintain**e, em seguida, selecione **adicionar**.

    ![link de vxMaintain Olá](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o SSO do Azure AD usando o vxMaintain, com base em um usuário de teste chamado “Brenda Fernandes”.

Para SSO toowork, AD do Azure precisa de usuário do AD do Azure do tooknow Olá vxMaintain contraparte toohello. Ou seja, você deve estabelecer uma relação de link entre usuários do AD do Azure hello e usuário vxMaintain correspondente de saudação.

relação de link tooestablish hello, atribuir Olá vxMaintain **nome de usuário** valor como Olá AD do Azure **Username** valor.

tooconfigure e teste SSO de AD do Azure usando vxMaintain, Olá completa blocos de construção a seguir.

### <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Nesta seção, você pode habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO em seu aplicativo vxMaintain fazendo Olá seguinte:

1. Em Olá portal do Azure, Olá **vxMaintain** página de integração de aplicativos, selecione **o logon único**.

    ![Olá "Single sign-on" comando][4]

2. tooenable SSO, em Olá **modo de logon único** lista suspensa, selecione **baseado no SAML logon**.
 
    ![Olá "baseado em SAML logon" comando](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. Em **vxMaintain domínio e URLs**, Olá a seguir:

    ![Olá vxMaintain seção URLs e de domínio](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. Em Olá **identificador** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://<company name>.verisae.com`

    b. Em Olá **URL de resposta** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Olá valores anteriores não são reais. Atualizá-los com o identificador real hello e URL de resposta. valores tooobtain Olá Olá contato [a equipe de suporte vxMaintain](http://www.verisae.com/contact-us).
 
4. Em **o certificado de autenticação SAML**, selecione **Metadata XML**e, em seguida, salve o computador de tooyour de arquivo de metadados de saudação.

    ![Olá seção de "Certificado de autenticação SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Selecione **Salvar**.

    ![botão de salvar Olá](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO, Olá envio baixado **Metadata XML** arquivo toohello [a equipe de suporte vxMaintain](http://www.verisae.com/contact-us).

> [!TIP]
> Como configurar o aplicativo hello, você pode ler uma versão concisa do hello precedem instruções em Olá [portal do Azure](https://portal.azure.com). Depois de adicionar o aplicativo hello da saudação **do Active Directory** > **aplicativos empresariais** seção, selecione Olá **Single Sign-On** guia e, em seguida, Olá de acesso incorporado a documentação de saudação **configuração** seção. 
>
>toolearn mais sobre o recurso de documentação do embedded hello, consulte [gerenciar logon único para aplicativos corporativos](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Nesta seção, você pode criar Britta Simon de usuário de teste no portal do Azure de saudação fazendo Olá seguinte:

![usuário de teste de saudação do AD do Azure][100]

1. Em Olá **portal do Azure**, no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão.

    ![botão de "Active Directory do Azure" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay uma lista de usuários, vá muito**usuários e grupos** > **todos os usuários**.
    
    ![Olá link de "Todos os usuários"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Olá **todos os usuários** caixa de diálogo é aberta. 

3. Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo caixa, Olá a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário de teste Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e valor de saudação Observação que foi gerado em Olá **senha** caixa.

    d. Selecione **Criar**.
 
### <a name="create-a-vxmaintain-test-user"></a>Criar um usuário de teste vxMaintain

Nesta seção, você cria a usuária de teste Brenda Fernandes no vxMaintain. os usuários de tooadd na plataforma de vxMaintain hello, trabalhar com o [a equipe de suporte vxMaintain](http://www.verisae.com/contact-us). Antes de usar o SSO, criar e ativar usuários hello.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você permitir que o usuário de teste Britta Simon toouse SSO do Azure, concedendo acesso toovxMaintain. toodo, portanto, Olá a seguir:

![Usuário de teste na lista de nomes de exibição de saudação][200] 

1. No portal do Azure de saudação **aplicativos** exibir, vá muito**diretório** exibição > **aplicativos empresariais** > **detodososaplicativos**.

    ![Olá link de "Todos os aplicativos"][201] 

2. Em Olá **aplicativos** lista, selecione **vxMaintain**.

    ![link de vxMaintain Olá](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. No painel esquerdo do hello, selecione **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Selecione **adicionar** e, em seguida, em Olá **Adicionar atribuição** painel, selecione **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][203]

5. Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**e, em seguida, selecione Olá **selecione** botão.

7. Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Testar o logon único do Azure AD

Nesta seção, você pode testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.

Olá selecionando **vxMaintain** bloco no painel de acesso de saudação deve entrar no aplicativo de vxMaintain tooyour automaticamente.

Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Próximas etapas

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

