---
title: "Tutorial: integração do Azure Active Directory com o LinkedIn Learning | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e aprendizado LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Tutorial: integração do Azure Active Directory com o LinkedIn Learning

Neste tutorial, você aprenderá como toointegrate LinkedIn aprendizado com o Azure Active Directory (AD do Azure).

Integração de aprendizado do LinkedIn com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLinkedIn de aprendizado
- Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn aprendizado (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o aprendizado LinkedIn, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do LinkedIn Learning habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando LinkedIn aprendizado da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-linkedin-learning-from-hello-gallery"></a>Adicionando LinkedIn aprendizado da Galeria de saudação
integração de saudação tooconfigure do LinkedIn aprendizado no AD do Azure, você precisa tooadd LinkedIn aprendizado da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd LinkedIn aprendizado da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **LinkedIn aprendizado**. No painel de resultados, clique em **LinkedIn aprendizado** aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Learning, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no aprendizado LinkedIn é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no aprendizado LinkedIn precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no aprendizado LinkedIn.

tooconfigure e teste de logon único do AD do Azure com o aprendizado LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de aprendizado LinkedIn](#creating-a-linkedin-learning-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de aprendizado do LinkedIn.

**tooconfigure AD do Azure-logon único com o aprendizado LinkedIn, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **LinkedIn aprendizado** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. Em uma janela de navegador web diferente, locatário de aprendizado LinkedIn tooyour logon como administrador.

4. Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**. Além disso, selecione **aprendizado - padrão** na lista suspensa hello.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. No portal do Azure, em **LinkedIn aprendizado de domínio e URLs**, executar Olá etapas a seguir se você quiser tooconfigure SSO em **iniciado pelo IdP** modo

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    a. Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn 

    b. Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn

7. Se você quiser tooconfigure SSO em **iniciado pelo SP**, clique em Mostrar avançado URL opção de configuração na seção de configuração hello e configurar a URL de entrada hello com saudação padrão a seguir:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. Seu aplicativo de aprendizado LinkedIn espera asserções SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML. Olá captura de tela a seguir mostra um exemplo. Olá valor padrão de **identificador de usuário** é **User** mas LinkedIn aprendizado espera este toobe mapeada com o endereço de email do usuário hello. Para que você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização. 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação. usuário Olá precisa tooadd quatro declarações denominadas **email**, **departamento**, **firstname**, e **lastname** e valor de saudação é toobe mapeada com **user.mail**, **User. Department**, **user.givenname**, e **user.surname** respectivamente

    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | nome| user.givenname |
    | sobrenome| user.surname |
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    a. Clique em **Adicionar atributo** caixa de diálogo do atributo tooopen hello.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**

10. Executar Olá seguindo as etapas na Olá **nome** atributo -

    a. Clique em saudação do hello atributo tooopen **Editar atributo** janela.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Excluir o valor da URL de saudação da saudação **namespace**.
    
    c. Clique em **Okey** toosave configuração de saudação.

11. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. Clique em **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Vá muito**as configurações de administração do LinkedIn** seção. Carregar arquivo XML Olá baixado do hello portal do Azure clicando em opção de arquivo hello carregar XML.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Clique em **na** tooenable SSO. Status SSO é alterado de **não conectado** muito**conectado**

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 

### <a name="creating-a-linkedin-learning-test-user"></a>Criando um usuário de teste do LinkedIn Learning

Com suporte do aplicativo Linked Learning. Apenas durante o provisionamento do usuário e após a autenticação de usuários são criados automaticamente no aplicativo hello. Na página de configurações de administrador Olá no comutador de portal Olá invertido LinkedIn aprendizado Olá **automaticamente atribuir licenças** tooactive tooenable apenas durante o provisionamento e isso também irá atribuir um usuário de toohello de licença.
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você deve habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLinkedIn de aprendizado.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLinkedIn aprendizado, executar Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **LinkedIn aprendizado**.

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em um bloco de aprendizado LinkedIn Olá Olá painel de acesso, você deve obter a página de logon do Azure hello e após o logon bem-sucedido, você deve obter em seu aplicativo de aprendizado do LinkedIn.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png