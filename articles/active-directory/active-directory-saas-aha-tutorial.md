---
title: "Tutorial: Integração do Active Directory do Azure ao Aha! | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a>Tutorial: Integração do Active Directory do Azure ao Aha!

Neste tutorial, você aprenderá como toointegrate Aha! ao Azure AD (Azure Active Directory).

A integração do Aha! com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAha!
- Você pode habilitar seu usuários tooautomatically get conectado tooAha! (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Aha!, é necessário Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura da Aha! Uma assinatura habilitada para logon único do Aha!

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o Aha! da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-aha-from-hello-gallery"></a>Adicionando o Aha! da Galeria de saudação
integração de saudação do tooconfigure do Aha! no AD do Azure, você precisa tooadd Aha! na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Aha! na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Aha!**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. No painel de resultados de saudação, selecione **Aha!**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, configura e testa o logon único do Azure AD com o Aha!, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Aha! é o usuário tooa no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e hello relacionados ao usuário no Aha! precisa de toobe estabelecida.

No Aha!, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste do AD do Azure, logon único com o Aha!, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um Aha! usuário de teste](#creating-an-aha-test-user)**  -toohave um equivalente do Britta Simon no Aha! que é vinculado toohello representação do AD do Azure do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Aha! .

**tooconfigure logon único do AD do Azure com o Aha!, executar Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Aha!** clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. Em Olá **Aha! Domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.aha.io/session/new`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.aha.io`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Contate a [equipe de suporte ao Cliente do Equipe de suporte do cliente](https://www.aha.io/company/contact) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. Em uma janela de navegador web diferente, faça logon no tooyour Aha! como um administrador.

7. No menu de saudação na parte superior de saudação, clique em **configurações**.

    ![Configurações](./media/active-directory-saas-aha-tutorial/IC798950.png "Configurações")

8. Clique em **Conta**.
   
    ![Perfil](./media/active-directory-saas-aha-tutorial/IC798951.png "Perfil")

9. Clique em **Segurança e logon único**.
   
    ![Segurança e logon único](./media/active-directory-saas-aha-tutorial/IC798952.png "Segurança e logon único")

10. Na seção **Logon Único**, como **Provedor de Identidade**, selecione **SAML2.0**.
   
    ![Segurança e logon único](./media/active-directory-saas-aha-tutorial/IC798953.png "Segurança e logon único")

11. Em Olá **Single Sign-On** configuração de página, execute Olá etapas a seguir:
    
    ![Logon Único](./media/active-directory-saas-aha-tutorial/IC798954.png "Logon Único")
    
       a. Em Olá **nome** caixa de texto, digite um nome para a sua configuração.

       b. Para **Configurar usando**, selecione **Arquivo de Metadados**.
   
       c. tooupload seu arquivo de metadados baixado, clique em **procurar**.
   
       d. Clique em **Atualizar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-aha-test-user"></a>Criando um usuário de teste do Aha!

toolog de usuários tooenable AD do Azure no tooAha!, eles devem ser provisionados no Aha!.  

No caso de saudação do Aha!, o provisionamento é uma tarefa automatizada. Não há nenhum item de ação para você.

Os usuários são criados automaticamente se necessário durante a saudação primeiro único tentativa de logon.

>[!NOTE]
>É possível usar qualquer outra ferramenta de criação da conta de usuário do Aha! ou as APIs fornecidas pelo Aha! contas de usuário do AAD tooprovision.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAha!.

![Atribuir usuário][200] 

**tooassign tooAha Britta Simon!, executar Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Aha!**.

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

