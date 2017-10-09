---
title: "Tutorial: Integração do Azure Active Directory ao SumoLogic | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a>Tutorial: Integração do Azure Active Directory ao SumoLogic

Neste tutorial, você aprenderá como toointegrate SumoLogic com o Azure Active Directory (AD do Azure).

Integrando o SumoLogic com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSumoLogic
- Você pode habilitar seu usuários tooautomatically get conectado tooSumoLogic (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com SumoLogic, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SumoLogic

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando SumoLogic da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sumologic-from-hello-gallery"></a>Adicionando SumoLogic da Galeria de saudação
integração de saudação tooconfigure do SumoLogic no AD do Azure, você precisa tooadd SumoLogic da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SumoLogic da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **SumoLogic**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. No painel de resultados de saudação, selecione **SumoLogic**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o SumoLogic, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na SumoLogic é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na SumoLogic precisa toobe estabelecida.

Na SumoLogic, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do Azure AD com SumoLogic, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do SumoLogic](#creating-a-sumologic-test-user)**  -toohave um equivalente do Britta Simon na SumoLogic que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SumoLogic.

**tooconfigure AD do Azure-logon único com o SumoLogic, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **SumoLogic** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. Em Olá **SumoLogic domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.SumoLogic.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente SumoLogic](https://www.sumologic.com/contact-us/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. Em Olá **SumoLogic configuração** seção, clique em **configurar SumoLogic** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour SumoLogic como um administrador.

8. Vá muito**gerenciar \> segurança**.
   
    ![Gerenciar](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gerenciar")

9. Clique em **SAML**.
   
    ![Configurações de segurança global](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Configurações de segurança global")

10. De saudação **selecionar uma configuração ou criar um novo** , selecione **AD do Azure**e, em seguida, clique em **configurar**.
   
    ![Configurar o SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurar o SAML 2.0")

11. Em Olá **configurar SAML 2.0** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar o SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurar o SAML 2.0")
   
    a. Em Olá **nome da configuração** caixa de texto, tipo **AD do Azure**. 

    b. Selecione **Modo de Depuração**.

    c. Em hello **emissor** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure. 

    d. Em Olá **URL de solicitação de autenticação nos quais** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.

    e. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado x. 509** caixa de texto.

    f. Para **Atributo de Email**, selecione **Usar entidade do SAML**.  

    g. Selecione **Configuração de Logon iniciada pelo SP**.

    h. Em Olá **caminho de logon** caixa de texto, tipo **Azure** e clique em **salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sumologic-test-user"></a>Criar um usuário de teste do SumoLogic

Ordem tooenable AD do Azure usuários toolog em tooSumoLogic, elas devem ser provisionado tooSumoLogic.  

* No caso de saudação do SumoLogic, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **SumoLogic** locatário.

2. Vá muito**gerenciar \> usuários**.
   
    ![Usuários](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Usuários")

3. Clique em **Adicionar**.
   
    ![Usuários](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Usuários")

4. Em Olá **novo usuário** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Novo Usuário](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Novo Usuário") 
 
    a. Informações da conta de saudação do AD do Azure que você deseja tooprovision em Olá relacionadas à saudação do tipo **nome**, **Sobrenome**, e **Email** caixas de texto.
  
    b. Selecione uma função.
  
    c. Para **Status**, selecione **Ativo**.
  
    d. Clique em **Salvar**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros SumoLogic usuário conta ou APIs fornecidas pela SumoLogic tooprovision contas de usuário do AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSumoLogic.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSumoLogic, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SumoLogic**.

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco SumoLogic Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour SumoLogic aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

