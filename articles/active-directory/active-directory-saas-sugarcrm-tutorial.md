---
title: "Tutorial: integração do Azure Active Directory ao Sugar CRM | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a>Tutorial: integração do Azure Active Directory ao Sugar CRM

Neste tutorial, você aprenderá como toointegrate Sugar CRM com o Azure Active Directory (AD do Azure).

Integrando o Sugar CRM com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSugar CRM
- Você pode habilitar seu usuários tooautomatically get conectado tooSugar CRM (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Sugar CRM, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Sugar CRM habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Sugar CRM da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sugar-crm-from-hello-gallery"></a>Adicionando Sugar CRM da Galeria de saudação
integração de saudação tooconfigure do Sugar CRM no AD do Azure, você precisa tooadd Sugar CRM na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Sugar CRM da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Sugar CRM**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. No painel de resultados de saudação, selecione **Sugar CRM**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Sugar CRM, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Sugar CRM é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação do Sugar CRM precisa toobe estabelecida.

No Sugar CRM, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Sugar CRM, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave um equivalente do Britta Simon no Sugar CRM é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Sugar CRM.

**tooconfigure AD do Azure-logon único com o Sugar CRM, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Sugar CRM** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. Em Olá **Sugar CRM domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > Olá valor não é real. Valor de saudação de atualização com hello URL de logon real. Entre em contato com [equipe de suporte do Sugar CRM cliente](https://support.sugarcrm.com/) tooget valor de saudação. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. Em Olá **Sugar CRM configuração** seção, clique em **configurar Sugar CRM** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Sugar CRM como um administrador.

8. Vá muito**Admin**.
   
    ![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")

9. Em Olá **administração** seção, clique em **gerenciamento de senha**.
   
    ![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administração")

10. Selecione **Habilitar Autenticação SAML**.
   
    ![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administração")

11. Em Olá **autenticação SAML** , execute Olá etapas a seguir:
   
    ![Autenticação SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Autenticação SAML")  
 
    a. Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.
  
    b. Em Olá **URL de SLO** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.
  
    c. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado x. 509** caixa de texto.
  
    d. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sugar-crm-test-user"></a>Criar um usuário de teste do Sugar CRM

Ordem tooenable AD do Azure usuários toolog em tooSugar CRM, elas devem ser provisionado tooSugar CRM.

No caso de saudação do Sugar CRM, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Sugar CRM** site da empresa como administrador.

2. Vá muito**Admin**.
   
    ![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")

3. Em Olá **administração** seção, clique em **gerenciamento de usuário**.
   
    ![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administração")

4. Vá muito**usuários \> criar novo usuário**.
   
    ![Criar Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Criar Novo Usuário")

5. Em Olá **perfil de usuário** guia, execute Olá etapas a seguir:
   
    ![Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Novo Usuário")

    a. Saudação de tipo **nome de usuário**, **Sobrenome**, e **endereço de email** de um usuário válido do Active Directory do Azure em Olá relacionados caixas de texto.
  
6. Para **Status**, selecione **Ativo**.

7. Na guia de senha hello, execute Olá etapas a seguir:
   
    ![Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Novo Usuário")

    a. Digite a senha em Olá Olá relacionadas a caixa de texto.

    b. Clique em **Salvar**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Sugar CRM usuário conta ou APIs fornecidas pelo Sugar CRM tooprovision contas de usuário do AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSugar CRM.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSugar CRM, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Sugar CRM**.

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco Sugar CRM Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Sugar CRM.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

