---
title: "Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Autenticação de Identidade | Microsoft Docs"
description: "Saiba como tooconfigure único logon entre o Active Directory do Azure e SAP HANA autenticação de identidade de plataforma de nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Autenticação de Identidade

Neste tutorial, você aprenderá como toointegrate SAP HANA autenticação de identidade de plataforma nuvem com o Azure Active Directory (AD do Azure). Autenticação de identidade de plataforma de nuvem do SAP HANA é usada como um proxy IdP tooaccess aplicativos SAP usando o AD do Azure como Olá IdP principal.

Autenticação de identidade de plataforma de nuvem do SAP HANA integrando o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSAP aplicativo
- Você pode habilitar seu usuários tooautomatically get conectado tooSAP aplicativos-logon único (SSO) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com autenticação de identidade de plataforma de nuvem do SAP HANA, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura da **Autenticação de Identidade da SAP HANA Cloud Platform** habilitada para SSO


>[!NOTE] 
>Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
>

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando a autenticação de identidade de plataforma de nuvem do SAP HANA da Galeria de saudação
2. Configurar e testar o SSO do Azure AD

Antes de mergulhar nos detalhes técnicos Olá, é vital toounderstand conceitos de Olá que vai toolook no. saudação de Federação do Active Directory do Azure e de autenticação de identidade de plataforma de nuvem do SAP HANA permite tooimplement SSO entre aplicativos ou serviços protegidos pelo AAD (como um IdP) com aplicativos SAP e serviços protegidos pela identidade de plataforma de nuvem do SAP HANA Autenticação.

No momento, a autenticação de identidade de plataforma de nuvem do SAP HANA atua como um provedor de identidade de Proxy de tooSAP aplicativos. Por sua vez, Active Directory do Azure atua como Olá levam o provedor de identidade nessa configuração. 

Olá diagrama a seguir ilustra isso:    

![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Com essa configuração, seu locatário de Autenticação de Identidade da SAP HANA Cloud Platform será configurado como um aplicativo confiável no Azure Active Directory. 

Todos os aplicativos do SAP e serviços que você deseja tooprotect por meio dessa maneira são posteriormente configurados no console de gerenciamento de autenticação de identidade de plataforma de nuvem do SAP HANA Olá!

Isso significa que a autorização para conceder acesso tooSAP aplicativos e serviços necessidades tootake local autenticação de identidade de plataforma de nuvem do SAP HANA para essa configuração (como autorização tooconfiguring contrário no Azure Active Directory).

Configurando a autenticação de identidade de plataforma de nuvem do SAP HANA como um aplicativo por meio de saudação Marketplace do Azure Active Directory, você não precisa tootake respeito Configurando declarações individuais necessárias / asserções SAML e transformações necessárias tooproduce um token de autenticação válido para aplicativos SAP.

>[!NOTE] 
>Atualmente, o SSO da Web foi testado somente por ambas as partes. Fluxos necessários para a comunicação de aplicativo a API ou de API para API devem funcionar, mas ainda não foram testados. Eles serão testados como parte das atividades subsequentes.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Adicionar autenticação de identidade de plataforma de nuvem do SAP HANA da Galeria de saudação
integração de saudação tooconfigure de autenticação de identidade de plataforma de nuvem do SAP HANA no AD do Azure, você precisa tooadd autenticação de identidade de plataforma de nuvem do SAP HANA na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd autenticação de identidade de plataforma do SAP HANA nuvem da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá [ **portal de gerenciamento do Azure**](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **autenticação de identidade de plataforma de nuvem do SAP HANA**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. No painel de resultados de saudação, selecione **autenticação de identidade de plataforma de nuvem do SAP HANA**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configura e testa o SSO do Azure AD com a Autenticação de Identidade da SAP HANA Cloud Platform com base em um usuário de teste chamado “Brenda Fernandes”.

Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá na autenticação de identidade de plataforma de nuvem do SAP HANA é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na autenticação de identidade de plataforma de nuvem do SAP HANA deve toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na autenticação de identidade de plataforma de nuvem do SAP HANA.

tooconfigure e teste do Azure AD SSO com a autenticação de identidade de plataforma de nuvem do SAP HANA, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de autenticação de identidade de plataforma de nuvem do SAP HANA](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave um equivalente do Britta Simon no SAP HANA plataforma de identidade de autenticação de nuvem que é a representação toohello vinculado do Azure AD de seus.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-sso"></a>Configurar o SSO do Azure AD

Nesta seção, habilitar o SSO de AD do Azure no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo de autenticação de identidade de plataforma de nuvem do SAP HANA.

Aplicativo de autenticação de identidade de plataforma de nuvem do SAP HANA espera asserções SAML de saudação em um formato específico. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo.

![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure SSO do AD do Azure com a autenticação do SAP HANA nuvem plataforma de identidade, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **autenticação de identidade de plataforma de nuvem do SAP HANA** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único][5]

3. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, se seu aplicativo SAP espera um atributo, por exemplo "firstName". No diálogo de atributos de token de SAML hello, adicione atributo de "firstName" hello.
 1. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.
 
    ![Configurar Logon Único][6]

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. Em Olá **nome do atributo** caixa de texto Nome do tipo de atributo hello "firstName".
 3. De saudação **o valor do atributo** lista, o valor do atributo select hello "user.givenname".
 4. Clique em **OK**.

4. Em Olá **URLs e domínio de autenticação de identidade de plataforma do SAP HANA nuvem** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. Em Olá **URL de logon** caixa de texto, digite Olá sinal na URL para aplicativo de SAP hello.
 2. Em Olá **identificador** caixa de texto valor de tipo de saudação padrão a seguir:`<entity-id>.accounts.ondemand.com` 
    * Se você não souber esse valor, siga documentação de autenticação de identidade de plataforma de nuvem do SAP HANA Olá na [locatário SAML 2.0 configuração](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Em Olá **configuração de autenticação de identidade de plataforma do SAP HANA nuvem** seção, clique em **configurar autenticação identidade de plataforma de nuvem do SAP HANA** tooopen **configurar o logon** caixa de diálogo. Em seguida, clique em **SAML XML metadados** e salve o arquivo hello em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget SSO configurado para o seu aplicativo, vá tooSAP Console de administração do HANA nuvem plataforma de identidade de autenticação. Olá URL tem saudação padrão a seguir:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Em seguida, siga a documentação do hello na autenticação de identidade de plataforma de nuvem do SAP HANA muito[configurar o AD do Azure como provedor de identidade corporativa na autenticação de identidade de plataforma de nuvem do SAP HANA](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. No portal de gerenciamento do Azure hello, clique em **salvar** botão.
8. Continue Olá etapas a seguir somente se você quiser tooadd e habilitar o SSO para outro aplicativo SAP. Repita as etapas em Olá seção "Adicionando SAP HANA nuvem plataforma autenticação de identidade da Galeria hello" tooadd outra instância de autenticação de identidade de plataforma de nuvem do SAP HANA.
9. No portal de gerenciamento do Azure do hello, no hello **autenticação de identidade de plataforma de nuvem do SAP HANA** página de integração de aplicativos, clique em **logon vinculado**.

    ![Configurar o logon vinculado](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Em seguida, salve a configuração de saudação.

>[!NOTE] 
>novo aplicativo de saudação aproveitará a configuração de SSO Olá para aplicativo SAP anterior de saudação. Certifique-se de use Olá mesmo provedores de identidade corporativa no hello Console de administração do SAP HANA nuvem plataforma de identidade de autenticação.
>

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no novo portal de saudação chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.
  2. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.
  3. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.
  4. Clique em **Criar**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Criar um usuário de teste da Autenticação de Identidade da SAP HANA Cloud Platform

Você não precisa toocreate um usuário na autenticação de identidade de plataforma de nuvem do SAP HANA. Os usuários que estão no repositório do usuário de saudação do AD do Azure podem usar a funcionalidade de SSO de saudação.

Autenticação de identidade de plataforma de nuvem do SAP HANA dá suporte à opção de federação de identidade hello. Esta opção permite Olá aplicativo toocheck se usuários Olá autenticados pelo provedor de identidade corporativa Olá existirem em Olá repositório do SAP HANA nuvem plataforma identidade autenticação do usuário. 

Na configuração padrão de saudação, Olá opção de federação de identidade está desabilitado. Se a federação de identidade é habilitada, somente os usuários de saudação que são importados na autenticação de identidade de plataforma de nuvem do SAP HANA são tooaccess capaz de aplicativo de hello. 

Para obter mais informações sobre como tooenable ou desabilitar a federação de identidade com a autenticação do SAP HANA nuvem plataforma de identidade, consulte Habilitar a federação de identidade com a autenticação de identidade de plataforma do SAP HANA nuvem em [configurar federação de identidade com hello repositório do SAP HANA nuvem plataforma identidade de autenticação do usuário. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooSAP seu acesso autenticação de identidade de plataforma de nuvem HANA.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSAP autenticação de identidade de plataforma de nuvem HANA, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **autenticação de identidade de plataforma de nuvem do SAP HANA**.

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    

### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.

Quando você clica em um bloco de autenticação de identidade de plataforma de nuvem do SAP HANA Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de autenticação de identidade de plataforma de nuvem do SAP HANA.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png