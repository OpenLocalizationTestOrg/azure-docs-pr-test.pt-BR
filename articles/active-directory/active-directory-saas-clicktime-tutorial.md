---
title: "Tutorial: integração do Azure Active Directory com o ClickTime | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Tutorial: integração do Active Directory do Azure ao ClickTime

Neste tutorial, você aprenderá como toointegrate ClickTime com o Azure Active Directory (AD do Azure).

Integrando o ClickTime com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooClickTime
- Você pode habilitar seu usuários tooautomatically get conectado tooClickTime (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o ClickTime, é necessário Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do ClickTime habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ClickTime da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-clicktime-from-hello-gallery"></a>Adicionando ClickTime da Galeria de saudação
integração de saudação tooconfigure do ClickTime no AD do Azure, você precisa tooadd ClickTime da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ClickTime da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **ClickTime**, selecione **ClickTime** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![ClickTime na lista de resultados de saudação](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o ClickTime, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ClickTime é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ClickTime precisa toobe estabelecida.

No ClickTime, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o ClickTime, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do ClickTime](#create-a-clicktime-test-user)**  -toohave um equivalente do Britta Simon no ClickTime é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ClickTime.

**tooconfigure AD do Azure-logon único com o ClickTime, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **ClickTime** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. Em Olá **ClickTime domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL como:`https://app.clicktime.com/sp/`
    
    b. Em Olá **URL de resposta** caixa de texto, digite uma URL usando Olá seguintes padrões: 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. Em Olá **ClickTime configuração** seção, clique em **configurar ClickTime** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do ClickTime como administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em **preferências**e, em seguida, clique em **as configurações de segurança**.

9. Em Olá **preferências de logon único** configuração, execute Olá etapas a seguir:
   
    ![Configurações de segurança](./media/active-directory-saas-clicktime-tutorial/tic777280.png "as configurações de segurança")
   
    a.  Selecione **Permitir** a entrada usando o SSO (Logon Único) com **Azure AD**.
   
    b. Em Olá **ponto de extremidade de provedor de identidade** caixa de texto, colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
    c.  Olá abrir **certificado codificado na base 64** baixado do portal do Azure em **o bloco de notas**, copie o conteúdo de saudação e, em seguida, cole-o em hello **certificado x. 509** caixa de texto.
   
    d.  Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-clicktime-test-user"></a>Criar um usuário de teste do ClickTime

Em ordem tooenable AD do Azure usuários toolog no ClickTime, eles devem ser provisionados no ClickTime.  
No caso de saudação do ClickTime, o provisionamento é uma tarefa manual.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros ClickTime usuário conta ou APIs fornecidas pelo ClickTime tooprovision contas de usuário do AD do Azure.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**
1. Faça logon no tooyour **ClickTime** locatário.
2. Na barra de ferramentas de saudação na parte superior do hello, clique em **empresa**e, em seguida, clique em **pessoas**.
   
    ![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Pessoas")
3. Clique em **Adicionar Pessoa**.
   
    ![Adicionar pessoa](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Adicionar pessoa")
4. Olá seção nova pessoa, execute Olá etapas a seguir:
   
    ![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Pessoas")
   
    a.  Em Olá **nome completo** caixa de texto, digite nome completo de usuário como **Britta Simon**. 
  
    b.  Em Olá **endereço de email** caixa de texto, como o email de saudação do tipo de usuário  **brittasimon@contoso.com** .
       
    > [!NOTE]
    > Se desejar, você pode definir propriedades adicionais do novo objeto de pessoa hello.
   
    c.  Clique em **Salvar**.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooClickTime.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooClickTime, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ClickTime**.

    ![Link de ClickTimne na lista de aplicativos de saudação](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco ClickTime Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ClickTime aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

