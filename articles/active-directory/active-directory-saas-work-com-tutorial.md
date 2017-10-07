---
title: "Tutorial: Integração do Azure Active Directory com o Work.com | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Tutorial: Integração do Active Directory do Azure com o Work.com

Neste tutorial, você aprenderá como toointegrate Work.com com o Azure Active Directory (AD do Azure).

Integrando o Work.com com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooWork.com
- Você pode habilitar seus usuários tooautomatically get conectado tooWork.com (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Work.com, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Work.com habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Work.com da Galeria de saudação
2. Configurar e testar logon único do Azure AD

## <a name="add-workcom-from-hello-gallery"></a>Adicionar Work.com da Galeria de saudação
integração de saudação tooconfigure da Work.com no AD do Azure, você precisa tooadd Work.com na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Work.com da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Work.com**, selecione **Work.com** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Adicionar da galeria](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o Work.com, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na Work.com é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na Work.com precisa toobe estabelecida.

Na Work.com, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Work.com, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Work.com](#create-a-workcom-test-user)**  -toohave um equivalente do Britta Simon na Work.com que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo da Work.com.

>[!NOTE]
>tooconfigure logon único, você precisa ainda toosetup um nome de domínio personalizado do Work.com. Você precisa toodefine pelo menos um domínio nome, teste seu nome de domínio e implantá-lo tooyour toda a organização.

**tooconfigure AD do Azure-logon único com o Work.com, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Work.com** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Logon único baseado em SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. Em Olá **Work.com domínio e URLs** , execute o seguinte hello:

    ![Seção Domínio e URLs do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Entre em contato com [equipe de suporte do cliente Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget esse valor. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. Em Olá **Work.com configuração** seção, clique em **configurar Work.com** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Seção Configuração do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Faça logon no tooyour locatário do Work.com como administrador.

8. Vá muito**instalação**.
   
    ![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")

9. No painel de navegação à esquerda do hello, no hello **administrar** seção, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá  **Meu domínio** página. 
   
    ![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Meu Domínio")

10. tooverify seu domínio foi configurado corretamente, certifique-se de que ela está em "**etapa 4 implantado tooUsers**" e examine seu "**minhas configurações de domínio**".
   
    ![Domínio implantado tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser domínio implantado")

11. Faça logon no tooyour locatário do Work.com.

12. Vá muito**instalação**.
    
    ![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")

13. Expanda Olá **controles de segurança** menu e clique **configurações de logon único**.
    
    ![Configurações de Logon Único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configurações de Logon Único")

14. Em Olá **configurações de logon único** caixa de diálogo de página, execute Olá etapas a seguir:
    
    ![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")
    
    a. Selecione **SAML Habilitado**.
    
    b. Clique em **Novo**.

15. Em Olá **configurações de logon único SAML** , execute Olá etapas a seguir:
    
    ![Configurações de Logon Único do SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configurações de Logon Único do SAML")
    
    a. Em Olá **nome** caixa de texto, digite um nome para a sua configuração.  
       
    > [!NOTE]
    > Fornecer um valor para **nome** preencher automaticamente Olá **nome da API** caixa de texto.
    
    b. Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.
    
    c. certificado do tooupload Olá baixado do portal do Azure, clique em **procurar**.
    
    d. Em Olá **Id da entidade** caixa de texto, tipo `https://salesforce-work.com`.
    
    e. Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.
    
    f. Como **local da identidade do SAML**, selecione **identidade está no elemento Nameidentifier Olá Olá declaração assunto**.
    
    g. Em **URL de logon do provedor de identidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.

    h. Em **URL de Logout do provedor de identidade** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.
    
    i. Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.
    
    j. Clique em **Salvar**.

16. No portal clássico do Work.com, no painel de navegação esquerdo hello, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá **meu domínio**página. 
    
    ![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Meu Domínio")

17. Em Olá **meu domínio** página Olá **identidade visual da página de logon** seção, clique em **editar**.
    
    ![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic767826.png "Identidade Visual da Página de Logon")

14. Em Olá **identidade visual da página de logon** página Olá **serviço de autenticação** seção, o nome de saudação do seu **configurações de SSO do SAML** é exibido. Selecione-o e, em seguida, clique em **Salvar**.
    
    ![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic784366.png "Identidade Visual da Página de Logon")

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Adicionar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-workcom-test-user"></a>Criar um usuário de teste do Work.com
Para o Active Directory do Azure usuários toobe capaz de toosign no, eles devem ser provisionados tooWork.com. No caso de saudação do Work.com, o provisionamento é uma tarefa manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisionamento de usuário, execute Olá etapas a seguir:
1. Faça logon no tooyour site da empresa Work.com como administrador.

2. Vá muito**instalação**.
   
    ![Configuração](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuração")
3. Vá muito**gerenciar usuários \> usuários**.
   
    ![Gerenciar Usuários](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gerenciar Usuários")

4. Clique em **Novo Usuário**.
   
    ![Todos os Usuários](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos os Usuários")

5. Olá seção editar usuários, executar Olá seguindo as etapas, em atributos de um válida do Azure relacionados de conta do AD desejados tooprovision para Olá caixas de texto:
   
    ![Editar Usuário](./media/active-directory-saas-work-com-tutorial/ic794118.png "Editar Usuário")
   
    a. Em Olá **nome** caixa de texto, Olá tipo **nome** do usuário Olá **Britta**.
    
    b. Em Olá **Sobrenome** caixa de texto, Olá tipo **Sobrenome** do usuário Olá **Simon**.
    
    c. Em Olá **Alias** caixa de texto, Olá tipo **nome** do usuário Olá **BrittaS**.
    
    d. Em Olá **Email** caixa de texto, Olá tipo **endereço de email** do usuário  **Brittasimon@contoso.com** .
    
    e. Em Olá **nome de usuário** caixa de texto, digite um nome de usuário do usuário como  **Brittasimon@contoso.com** .
    
    f. Em Olá **apelido** caixa de texto, digite um **apelido** do usuário **Simon**.
    
    g. Selecione **Função**, **Licença de Usuário** e **Perfil**.
    
    h. Clique em **Salvar**.  
      
    > [!NOTE]
    > proprietário de conta do AD do Azure Olá receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWork.com.

![Atribuir usuário][200] 

**tooassign Britta Simon tooWork.com, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Work.com**.

    ![Work.com na lista do aplicativo](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Work.com Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo da Work.com.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

