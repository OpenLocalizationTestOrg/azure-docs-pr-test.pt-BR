---
title: "Tutorial: Integração do Azure Active Directory com o MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e transferência MOVEit - integração do AD do Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Tutorial: Integração do Azure Active Directory com o MOVEit Transfer - Azure AD integration

Neste tutorial, você aprenderá como toointegrate MOVEit transferência - integração do AD do Azure com o Azure Active Directory (AD do Azure).

Integrar MOVEit transferência - integração do AD do Azure com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooMOVEit transferência - integração do AD do Azure.
- Você pode habilitar seu usuários tooautomatically get conectado tooMOVEit transferência - integração do AD do Azure (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com transferência MOVEit - integração do AD do Azure, você precisará Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do MOVEit Transfer - Azure AD integration habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando MOVEit transferência - integração do AD do Azure da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Adicionando MOVEit transferência - integração do AD do Azure da Galeria de saudação
integração de saudação tooconfigure de transferência MOVEit - integração do AD do Azure no AD do Azure, você precisa tooadd MOVEit transferência - integração do AD do Azure da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd MOVEit transferência - integração do AD do Azure da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **MOVEit transferência - integração do Azure AD**, selecione **MOVEit transferência - integração do Azure AD** no painel de resultados e clique em **adicionar** saudação do botão tooadd aplicativo.

    ![Transferência de MOVEit - integração do AD do Azure na lista de resultados de saudação](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o MOVEit Transfer - Azure AD integration, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá na transferência MOVEit - integração do AD do Azure é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na transferência MOVEit - integração do AD do Azure precisa toobe estabelecida.

Transferência MOVEit - integração do AD do Azure, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com transferência MOVEit - integração do AD do Azure, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar uma transferência MOVEit - usuário de teste de integração do AD do Azure](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave um equivalente do Britta Simon na transferência MOVEit - integração de AD do Azure que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em sua transferência MOVEit - aplicativo de integração do AD do Azure.

**tooconfigure AD do Azure-logon único com transferência MOVEit - integração do AD do Azure, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **MOVEit transferência - integração do Azure AD** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. Em Olá **MOVEit transferência - integração do Azure AD domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://contoso.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://contoso.com/<tenatid>`

    c. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Você pode consultar esses valores posteriormente em **URL de metadados do provedor de serviço** seção ou entre em contato com [MOVEit transferência - a equipe de suporte de cliente de integração do AD do Azure](https://community.ipswitch.com/s/support) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Logon tooyour MOVEit transferência locatário como um administrador.

7. No painel de navegação esquerdo hello, clique em **configurações**.

    ![Seção Configurações no lado do aplicativo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Clique no link **Logon Único** que está em **Políticas de Segurança -> Autenticação de Usuário**.

    ![Políticas de segurança no lado do aplicativo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Clique em documento de metadados de Olá Olá URL de metadados link toodownload.

    ![URL de metadados do provedor de serviço](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Verifique se **entityID** corresponde **identificador** em Olá **MOVEit transferência - integração do Azure AD domínio e URLs** seção.
    * Verifique se **AssertionConsumerService** corresponde a URL local **URL de resposta** em Olá **MOVEit transferência - integração do Azure AD domínio e URLs** seção.
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Clique em **Adicionar provedor de identidade** botão tooadd um novo provedor de identidade federada.

    ![Adicionar Provedor de Identidade](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Clique em **procurar...**  tooselect Olá arquivo de metadados que você baixou do portal do Azure, clique em **Adicionar provedor de identidade** Olá tooupload o arquivo baixado.

    ![Provedor de identidade SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Selecione "**Sim**" como **habilitado** em Olá **editar configurações de provedor de identidade federada...**  página e clique em **salvar**.

    ![Configurações de Provedor de Identidade Federado](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. Em Olá **Editar federado identidade do provedor de configurações do usuário** página, execute Olá ações a seguir:
    
    ![Edite Configurações de Provedor de Identidade Federado](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Selecione **SAML NameID** como **Nome de logon**.
    
    b. Selecione **outros** como **nome completo** e em Olá **nome do atributo** caixa de texto, coloque o valor de saudação: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Selecione **outros** como **Email** e em Olá **nome do atributo** caixa de texto, coloque o valor de saudação: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Selecione **Sim** para **Criação automática de conta no momento da conexão**.
    
    e. Clique no botão **Salvar** .

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Crie um usuário de teste do MOVEit Transfer - Azure AD integration

Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon na transferência MOVEit - integração do AD do Azure. O MOVEit Transfer - Azure AD integration dá suporte ao provisionamento just-in-time, que você habilitou. Não há itens de ação para você nesta seção. Um novo usuário é criado durante uma tentativa tooaccess MOVEit transferência - integração do AD do Azure se ele ainda não existir.

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [MOVEit transferência - a equipe de suporte de cliente de integração do AD do Azure](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMOVEit transferência - integração do AD do Azure.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooMOVEit transferência - integração do AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **MOVEit transferência - integração do Azure AD**.

    ![Olá MOVEit transferência - integração do AD do Azure link na lista de aplicativos Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em Olá MOVEit transferência - bloco de integração do AD do Azure em Olá painel de acesso, você deve obter automaticamente assinado em tooyour MOVEit transferência - aplicativo de integração do AD do Azure. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

