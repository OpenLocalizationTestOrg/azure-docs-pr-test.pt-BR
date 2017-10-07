---
title: "Tutorial: integração do Azure Active Directory com o ServiceChannel | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a>Tutorial: integração do Azure Active Directory com o ServiceChannel

Neste tutorial, você aprenderá como toointegrate ServiceChannel com o Azure Active Directory (AD do Azure).

Integrando ServiceChannel com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooServiceChannel
- Você pode habilitar seu usuários tooautomatically get conectado tooServiceChannel (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com ServiceChannel, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do ServiceChannel habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ServiceChannel da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-servicechannel-from-hello-gallery"></a>Adicionando ServiceChannel da Galeria de saudação
integração de saudação tooconfigure de ServiceChannel no AD do Azure, você precisa tooadd ServiceChannel da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ServiceChannel da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **ServiceChannel**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. No painel de resultados de saudação, selecione **ServiceChannel**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o ServiceChannel, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em ServiceChannel é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ServiceChannel precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em ServiceChannel.

tooconfigure e teste de logon único do AD do Azure com ServiceChannel, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo ServiceChannel.

**tooconfigure AD do Azure-logon único com ServiceChannel, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **ServiceChannel** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. Em Olá **ServiceChannel domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    a. Em Olá **identificador** texto, o valor do tipo hello como:`http://adfs.<domain>.com/adfs/service/trust`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<customer domain>.servicechannel.com/saml/acs`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação. Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação. Entre em contato com [ServiceChannel a equipe de suporte](https://servicechannel.zendesk.com/hc/en-us) tooget esses valores.

4. Seu aplicativo de ServiceChannel espera asserções SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML. Olá captura de tela a seguir mostra um exemplo. **Identificador de nome (identificador de usuário)** é Olá somente declaração obrigatória e o valor de padrão de saudação é **User** mas ServiceChannel espera este toobe mapeada com **user.mail**. Se você estiver planejando tooenable apenas no provisionamento do usuário, você deve adicionar Olá seguintes declarações conforme mostrado abaixo. **Função** declaração precisa toobe mapeado muito**user.assignedroles** que contém a função de saudação do usuário hello.  

    Você pode consultar o guia do ServiceChannel [aqui](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) para obter diretrizes sobre declarações.
    
    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > Clique em [aqui](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow como tooconfigure **função** no AD do Azure

5. Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação.

    | Nome do atributo | Valor do atributo |
    | --- | --- |    
    | Função| user.assignedroles |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**
    
6. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. Clique em **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. Em Olá **ServiceChannel configuração** seção, clique em **configurar ServiceChannel** tooopen **configurar o logon** janela. Observação Olá **SAML Enitity ID** de saudação **referência rápida** seção.

9. tooconfigure logon único no **ServiceChannel** lado, você precisa toosend Olá baixado **certificado (Base64)** e **ID da entidade SAML** muito[ A equipe de suporte ServiceChannel](https://servicechannel.zendesk.com/hc/en-us). Eles serão configurados isso no hello toohave de ordem conexão SSO do SAML definido corretamente em ambos os lados.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 

### <a name="creating-a-servicechannel-test-user"></a>Criar um usuário de teste do ServiceChannel

Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente. Para um provisionamento de usuário completo, entre em contato com [a equipe de suporte do ServiceChannel](https://servicechannel.zendesk.com/hc/en-us)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooServiceChannel seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooServiceChannel, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ServiceChannel**.

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco ServiceChannel Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ServiceChannel aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png