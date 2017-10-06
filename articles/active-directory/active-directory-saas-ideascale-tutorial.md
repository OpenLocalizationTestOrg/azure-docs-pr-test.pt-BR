---
title: "Tutorial: Integração do Azure Active Directory ao IdeaScale | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Tutorial: integração do Active Directory do Azure ao IdeaScale

Neste tutorial, você aprenderá como toointegrate IdeaScale com o Azure Active Directory (AD do Azure).

Integrando o IdeaScale com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooIdeaScale
- Você pode habilitar seu usuários tooautomatically get conectado tooIdeaScale (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com IdeaScale, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do IdeaScale

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando IdeaScale da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-ideascale-from-hello-gallery"></a>Adicionando IdeaScale da Galeria de saudação
integração de saudação tooconfigure do IdeaScale no AD do Azure, você precisa tooadd IdeaScale da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd IdeaScale da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **IdeaScale**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. No painel de resultados de saudação, selecione **IdeaScale**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o IdeaScale com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no IdeaScale é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no IdeaScale precisa toobe estabelecida.

No IdeaScale, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com IdeaScale, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do IdeaScale](#creating-an-ideascale-test-user)**  -toohave um equivalente do Britta Simon no IdeaScale é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo IdeaScale.

**tooconfigure AD do Azure-logon único com IdeaScale, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **IdeaScale** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. Em Olá **IdeaScale domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.ideascale.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente do IdeaScale](http://support.ideascale.com/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. Em Olá **IdeaScale configuração** seção, clique em **configurar IdeaScale** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e a ID da entidade SAML** de saudação **seção de referência rápida**.

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa IdeaScale tooyour como um administrador.

8. Vá muito**configurações da comunidade**.
   
    ![Configurações da Comunidade](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configurações da Comunidade")

9. Vá muito**segurança \> configurações de logon único**.
   
    ![Configurações de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Configurações de Logon Único")

10. Para **Tipo de Logon Único**, selecione **SAML 2.0**.
   
    ![Tipo de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Tipo de Logon Único")

11. Em Olá **configurações de logon único** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurações de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Configurações de Logon Único")
   
    a. Em **ID da entidade IdP SAML** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.

    b. Copiar o conteúdo de saudação do seu arquivo de metadados baixado do portal do Azure e cole-o em Olá **metadados IdP SAML** caixa de texto.

    c. Em **URL de Logout do sucesso** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.

    d. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-ideascale-test-user"></a>Como criar um usuário de teste do IdeaScale

toolog de usuários tooenable AD do Azure no IdeaScale, eles devem ser provisionados no tooIdeaScale. No caso de saudação do IdeaScale, o provisionamento é uma tarefa manual.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **IdeaScale** site da empresa como administrador.

2. Vá muito**configurações da comunidade**.
   
    ![Configurações da Comunidade](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configurações da Comunidade")

3. Vá muito**configurações básicas \> gerenciamento membro**.

4. Clique em **Adicionar Membro**.
   
    ![Gerenciamento de Membros](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Gerenciamento de Membros")

5. Na seção Adicionar novo membro de hello, execute Olá etapas a seguir:
   
    ![Adicionar Novo Membro](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Adicionar Novo Membro")
   
    a. Em Olá **endereços de Email** caixa de texto, endereço de email de saudação do tipo de uma conta válida do AAD você deseja tooprovision.
   
    b. Clique em **Salvar Alterações**. 
   
    >[!NOTE]
    >proprietário de conta do Active Directory do Azure Olá obtém um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.
      
>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros IdeaScale usuário conta ou APIs fornecidas pelo IdeaScale tooprovision contas de usuário do AAD.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIdeaScale.

![Atribuir usuário][200] 

**tooassign Britta Simon tooIdeaScale, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **IdeaScale**.

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único


Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco IdeaScale Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour IdeaScale aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

