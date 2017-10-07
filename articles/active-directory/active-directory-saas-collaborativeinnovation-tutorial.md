---
title: "Tutorial: Integração do Azure Active Directory com Inovação Colaborativa | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e inovação colaborativa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a>Tutorial: Integração do Azure Active Directory com Inovação Colaborativa

Neste tutorial, você aprenderá como toointegrate inovação colaboração com o Azure Active Directory (AD do Azure).

Integração de inovação de colaboração com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooCollaborative inovação
- Você pode habilitar seu usuários tooautomatically get conectado tooCollaborative inovação (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com inovações de colaboração, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Um logon único da Inovação Colaborativa em uma assinatura habilitada

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando inovação colaborativa da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-collaborative-innovation-from-hello-gallery"></a>Adicionando inovação colaborativa da Galeria de saudação
integração de saudação tooconfigure de inovação de colaboração no AD do Azure, você precisa tooadd inovação colaborativa de lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd inovação colaborativa da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **inovação colaborativa**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. No painel de resultados de saudação, selecione **inovação colaborativa**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com a Inovação Colaborativa com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na inovação colaborativa é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na inovação colaborativa precisa toobe estabelecida.

Em colaboração inovação, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com inovações de colaboração, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste inovação colaborativa](#creating-a-collaborative-innovation-test-user)**  -toohave um equivalente do Britta Simon na inovação colaborativa que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo inovação colaborativa.

**tooconfigure AD do Azure-logon único com inovações de colaboração, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **inovação colaborativa** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. Em Olá **domínio de inovação de colaboração e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.foundry.<companyname>.com/`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.foundry.<companyname>.com`
    
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente de colaboração inovação](https://www.unilever.com/contact/) tooget esses valores.  

4. Aplicativo de inovação de colaboração espera as asserções de SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo.
    
    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. Clique em **exibir e editar todos os outros atributos de usuário** caixa de seleção no hello **atributos de usuário** seção tooexpand atributos de saudação. Executar Olá seguindo as etapas em cada um dos atributos de saudação exibida-

    | Nome do atributo | Valor do atributo |
    | ---------------| --------------- |    
    | givenname | user.givenname |
    | sobrenome | user.surname |
    | emailaddress | user.userprincipalname |
    | name | user.userprincipalname |

    a. Clique em Olá Olá de tooopen atributo **Editar atributo** janela.

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    b. Excluir o valor da URL de saudação da saudação **Namespace**.
    
    c. Clique em **Okey** toosave configuração de saudação.

6. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. tooconfigure logon único no **inovação colaborativa** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte inovação colaborativa](https://www.unilever.com/contact/). Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-collaborative-innovation-test-user"></a>Como criar um usuário de teste da Inovação Colaborativa

tooenable AD do Azure usuários toolog em tooCollaborative inovação, eles devem ser provisionados no inovação colaborativa.  

No caso do aplicativo o provisionamento é automática como aplicativo hello dá suporte apenas durante o provisionamento do usuário. Portanto, há nenhuma necessidade tooperform todas as etapas aqui.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCollaborative inovação.

![Atribuir usuário][200] 

**tooassign Britta Simon tooCollaborative inovação, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **inovação colaborativa**.

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco inovação colaborativa Olá Olá painel de acesso, você deve obter a página de logon do aplicativo de inovação de colaboração.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

