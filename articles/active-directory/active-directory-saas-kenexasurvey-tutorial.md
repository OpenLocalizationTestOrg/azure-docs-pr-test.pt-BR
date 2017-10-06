---
title: "Tutorial: Integração do Azure Active Directory com o IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o IBM Kenexa pesquisa Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Tutorial: Integração do Azure Active Directory com o IBM Kenexa Survey Enterprise

Neste tutorial, você aprenderá como toointegrate IBM Kenexa pesquisa Enterprise com o Azure Active Directory (AD do Azure).

Integração do IBM Kenexa pesquisa Enterprise com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooIBM Kenexa pesquisa Enterprise.
- Você pode habilitar seus usuários de entrada tooautomatically tooIBM Kenexa pesquisa Enterprise usando logon único (SSO) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central: Olá portal do Azure.

Se você quiser tooknow mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o IBM Kenexa pesquisa Enterprise, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para SSO do IBM Kenexa Survey Enterprise

> [!NOTE]
> Quando você testar etapas Olá neste tutorial, é recomendável que você não use um ambiente de produção.

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste. cenário de saudação descrito Olá tutorial consiste em duas principais blocos de construção:

* Adicionando IBM Kenexa pesquisa Enterprise na Galeria de saudação
* Configurar e testar o SSO do Azure AD

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Adicionar IBM Kenexa pesquisa Enterprise na Galeria de saudação
tooconfigure a integração de saudação do IBM Kenexa pesquisa Enterprise no AD do Azure, adicione IBM Kenexa pesquisa Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

tooadd IBM Kenexa pesquisa Enterprise na Galeria de hello, Olá a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com), no painel esquerdo de hello, clique Olá **Active Directory do Azure** botão. 

    ![botão de Active Directory do Azure Olá][1]

2. Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd um aplicativo, clique em Olá **novo aplicativo** botão.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **IBM Kenexa pesquisa Enterprise**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Na lista de resultados de saudação, selecione **IBM Kenexa pesquisa Enterprise**e, em seguida, clique em Olá **adicionar** botão aplicativo hello de tooadd.

    ![IBM Kenexa pesquisa Enterprise na lista de resultados de saudação](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configura e testa o SSO do Azure AD com o IBM Kenexa Survey Enterprise, com base em um usuário de teste chamado “Brenda Fernandes”.

Para SSO toowork, o AD do Azure precisa equivalente de usuário tooidentify Olá IBM Kenexa pesquisa corporativo no AD do Azure. Em outras palavras, o Azure AD precisa estabelecer uma relação de vínculo entre um usuário do Azure AD e um usuário relacionado do IBM Kenexa Survey Enterprise.

relação de link tooestablish hello, atribuir valor Olá Olá **nome de usuário** no IBM Kenexa pesquisa Enterprise como valor de saudação do hello **Username** no AD do Azure.

tooconfigure e teste do Azure AD SSO com o IBM Kenexa pesquisa Enterprise, blocos de construção de saudação concluída em duas seções de saudação.

### <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Nesta seção, habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO em seu aplicativo IBM Kenexa pesquisa Enterprise fazendo Olá seguinte:

1. Em Olá portal do Azure, Olá **IBM Kenexa pesquisa Enterprise** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único do IBM Kenexa Survey Enterprise][4]

2. Em Olá **o logon único** caixa de diálogo Olá **modo** selecione **baseado no SAML logon** tooenable SSO.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. Em Olá **URLs e domínio da empresa de pesquisa do IBM Kenexa** , execute Olá etapas a seguir:

    ![Informações de logon único em Domínio e URLs do IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. Em Olá **identificador** caixa de texto, digite uma URL com saudação padrão a seguir:`https://surveys.kenexa.com/<companycode>`

    b. Em Olá **URL de resposta** caixa de texto, digite uma URL com saudação padrão a seguir:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Olá valores anteriores não são reais. Atualizá-los com o identificador real hello e URL de resposta. tooobtain Olá valores reais, Olá contato [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).

4. Em **o certificado de autenticação SAML**, clique em **certificado (Base64)**e, em seguida, salve o computador de tooyour de arquivo de certificado hello.

    ![link de download de certificado (Base64) Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Olá aplicativo corporativo de pesquisa do IBM Kenexa espera asserções do tooreceive Olá Security asserções Markup Language (SAML) em um formato específico, o que exige que você tooadd atributo personalizado toohello configuração de mapeamentos de seus atributos de token SAML. Olá valor da declaração do identificador de usuário Olá em resposta Olá deve corresponder Olá ID de SSO é configurado no sistema de Kenexa hello. toomap Olá identificador de usuário apropriado na sua organização como protocolo de datagrama de Internet para SSO (IDP), trabalhará com hello [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw). 

    Por padrão, o AD do Azure define o identificador de usuário Olá como valor de nome principal (UPN) do usuário hello. Você pode alterar esse valor no hello **atributo** guia, conforme mostrado no hello captura de tela a seguir. integração de saudação funciona somente depois de concluir Olá mapeamento corretamente.
    
    ![caixa de diálogo atributos de usuário Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Clique em **Salvar**.

    ![Olá configurar logon único botão Salvar](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. Olá tooopen **configurar o logon** janela, em **IBM Kenexa pesquisa Enterprise Configuration**, clique em **configurar o IBM Kenexa pesquisa Enterprise**. 
 
    ![link de configurar o IBM Kenexa pesquisa Enterprise Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Saudação de cópia **URL de logout**, **ID da entidade SAML**, e **único logon URL do serviço SAML** valores de saudação **referência rápida** seção.

8. Em Olá **configurar o logon** janela, em **referência rápida**, Olá cópia **URL de logout**, **ID da entidade SAML**, e  **Único logon URL do serviço SAML** valores.

9. tooconfigure SSO em Olá **IBM Kenexa pesquisa Enterprise** lado, enviar Olá baixado **certificado (Base64)**, **URL de logout**, **ID da entidade SAML**, e **único logon URL do serviço SAML** valores toohello [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Você pode consultar a versão concisa tooa essas instruções Olá [portal do Azure](https://portal.azure.com) enquanto você estiver configurando o aplicativo hello. Depois de adicionar o aplicativo hello da saudação **do Active Directory** > **aplicativos empresariais** seção, basta clicar em Olá **o logon único** guia e, em seguida, acessar Olá inseridos documentação por meio de saudação **configuração** seção Olá final. toolearn mais sobre o recurso de documentação do embedded hello, consulte [AD do Azure inseridos documentação](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Nesta seção, você pode criar Britta Simon de usuário de teste no portal do Azure de saudação fazendo Olá seguinte:

![Criar um usuário de teste do Azure AD][100]

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Criar um usuário de teste do IBM Kenexa Survey Enterprise

Nesta seção, você criará uma usuária chamada Brenda Fernandes no IBM Kenexa Survey Enterprise. 

usuários toocreate Olá sistema IBM Kenexa pesquisa Enterprise e Olá mapa identificação do SSO para eles, você pode trabalhar com hello [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw). Este valor de ID de SSO também deve ser mapeado toohello valor de identificador de usuário do AD do Azure. Você pode alterar essa configuração padrão em Olá **atributo** guia.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você permitir que o usuário Britta Simon toouse SSO do Azure, concedendo acesso tooIBM Kenexa pesquisa Enterprise.

![Atribuir função de usuário Olá][200] 

usuário tooassign Britta Simon tooIBM Kenexa pesquisa Enterprise, Olá a seguir:

1. Olá portal do Azure, abra o hello **aplicativos** exibir, vá toohello **diretório** exibição, selecione **aplicativos empresariais**e, em seguida, clique em **todos os aplicativos**.

    ![Olá "aplicativos corporativos" e links de "Todos os aplicativos"][201] 

2. Em Olá **aplicativos** lista, selecione **IBM Kenexa pesquisa Enterprise**.

    ![link do IBM Kenexa pesquisa Enterprise Olá na lista de aplicativos Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. No painel esquerdo do hello, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique em Olá **adicionar** botão e, em seguida, em Olá **Adicionar atribuição** painel, selecione **usuários e grupos**.

    ![Painel de atribuição adicionar Olá][203]

5. Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**.

6. Em Olá **usuários e grupos** caixa de diálogo, clique em Olá **selecione** botão.

7. Em Olá **Adicionar atribuição** caixa de diálogo, clique em Olá **atribuir** botão.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você pode testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.

Quando você clica em Olá **IBM Kenexa pesquisa Enterprise** Olá de bloco no painel de acesso, você deve ser conectado automaticamente tooyour aplicativo IBM Kenexa pesquisa empresarial.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
