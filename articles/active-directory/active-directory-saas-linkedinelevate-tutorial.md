---
title: "Tutorial: integração do Azure Active Directory com o LinkedIn Elevate | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e elevar LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Tutorial: integração do Azure Active Directory com o LinkedIn Elevate

Neste tutorial, você aprenderá como toointegrate LinkedIn elevar com o Azure Active Directory (AD do Azure).

Integrando LinkedIn elevar AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLinkedIn elevar
- Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn elevar (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com elevar LinkedIn, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do LinkedIn Elevate habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando LinkedIn elevar da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>Adicionando LinkedIn elevar da Galeria de saudação
integração de saudação tooconfigure do LinkedIn elevar no AD do Azure, você precisa tooadd LinkedIn elevar na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd LinkedIn elevar da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **LinkedIn elevar**. No painel de resultados, clique em **LinkedIn elevar** aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Elevate, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LinkedIn elevar é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no LinkedIn elevar precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no LinkedIn elevar.

tooconfigure e teste de logon único do AD do Azure com elevar LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste LinkedIn elevar](#creating-a-linkedin-elevate-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo LinkedIn elevar.

**tooconfigure AD do Azure-logon único com elevar LinkedIn, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **LinkedIn elevar** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. Em uma janela de navegador web diferente, logon tooyour LinkedIn elevar locatário como um administrador.

4. Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**. Além disso, selecione **elevar - elevar AAD teste** na lista suspensa hello.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. No Portal do Azure, em **LinkedIn elevar domínio e URLs**, executar Olá etapas a seguir se você quiser tooconfigure SSO em **iniciado pelo IdP** modo

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn 

    b. Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn

7. Se você quiser tooconfigure SSO em **iniciado pelo SP**, clique em Mostrar avançado URL opção de configuração na seção de configuração de saudação e configurar Olá logon URL com saudação padrão a seguir:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. Seu aplicativo LinkedIn elevar espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML. Olá captura de tela a seguir mostra um exemplo. Olá valor padrão de **identificador de usuário** é **User** mas LinkedIn elevar espera este toobe mapeada com o endereço de email do usuário hello. Para que você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização. 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação. Você precisa tooadd outra declaração denominada **departamento** e o valor de saudação precisa toobe mapeado muito**User. Department**.

    | Nome do atributo | Valor do atributo |
    | --- | --- |    
    | department| user.department |

      ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. Clique na página de detalhes de atributo Adicionar atributo tooopen Olá Adicionar atributo de departamento Olá conforme mostrado abaixo-

      ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Clique em **Okey** toosave atributo de saudação.

      c. Alterar o nome de saudação do atributo Olá **emailaddress** muito**email**.


10. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. Clique em **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Vá muito**as configurações de administração do LinkedIn** seção. Carregar arquivo XML Olá que você acabou de baixar da saudação portal do Azure clicando em Olá opção de carregar o XML de arquivo.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Clique em **na** tooenable SSO. SSO status será alterado de **não conectado** muito**conectado**

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Criando um usuário de teste do LinkedIn Elevate

Aplicativo elevar vinculado oferece suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente. Na página de configurações de administrador Olá no comutador de portal Olá invertido LinkedIn elevar Olá **automaticamente atribuir licenças** tooactive tooenable apenas durante o provisionamento e isso também irá atribuir um usuário de toohello de licença.

   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooLinkedIn seu acesso elevar.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLinkedIn elevar, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **LinkedIn elevar**.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica Olá LinkedIn elevar lado a lado no painel de acesso de saudação, você deve obter a página de logon do Azure hello e após o logon bem-sucedido, você deve obter em seu aplicativo LinkedIn elevar.

## <a name="additional-resources"></a>Recursos adicionais

* [Tutorial: Configurar o LinkedIn Elevate para o provisionamento automático de usuário com o Azure Active Directory](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
