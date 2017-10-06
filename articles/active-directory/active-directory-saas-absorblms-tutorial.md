---
title: "Tutorial: Integração do Azure Active Directory ao Absorb LMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e absorver LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Tutorial: Integração do Azure Active Directory ao Absorb LMS

Neste tutorial, você aprenderá como toointegrate Absorb LMS com o Azure Active Directory (AD do Azure).

Integrando absorver LMS com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAbsorb LMS
- Você pode habilitar seu usuários tooautomatically get conectado tooAbsorb LMS (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte. [O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com absorver LMS, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Absorb LMS com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando absorver LMS da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-absorb-lms-from-hello-gallery"></a>Adicionando absorver LMS da Galeria de saudação
tooconfigure Olá integração de absorver LMS tooAzure AD, é necessário tooadd Absorb LMS na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Absorb LMS da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **absorver LMS**, selecione **absorver LMS** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Absorver LMS na lista de resultados de saudação](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Absorb LMS, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LMS absorver é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em absorver LMS precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em absorver LMS.

tooconfigure e teste de logon único do AD do Azure com absorver LMS, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de absorver LMS](#create-an-absorb-lms-test-user)**  -toohave um equivalente do Britta Simon no LMS absorver que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de absorver LMS.

**tooconfigure AD do Azure-logon único com LMS absorver, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **absorver LMS** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Em Olá **absorver LMS domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Esses valores não são Olá real. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [equipe de suporte de absorver LMS cliente](https://www.absorblms.com/support) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Em Olá **absorver LMS configuração** seção, clique em **configurar LMS absorver** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. Em uma janela de navegador web diferente, faça logon no site da empresa absorver LMS tooyour como um administrador.

9. Clique em Olá **ícone conta** na interface de administração de saudação. 

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Clique em **Configurações do Portal**.

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Clique em Olá **usuários** guia.

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Execute Olá etapas tooaccess Olá logon único nos campos de configuração a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Selecione Olá apropriado **modo**.

    b. Abra Olá certificado que você baixou do hello portal do Azure no bloco de notas, remova Olá **---iniciar certificado---** e **---concluir certificado---** marca e cole Olá restantes conteúdo Olá **chave** caixa de texto.
    
    c. Em Olá **propriedade Id**, selecione Olá atributo apropriado que você tenha configurado como Olá identificador de usuário no hello AD do Azure (por exemplo, se userprinciplename Olá for selecionado no AD do Azure, em seguida, o nome de usuário deve ser selecionado.)

    d. Em Olá **URL de logon**, cole Olá **"Single Sign-On URL do serviço SAML"** valor que você copiou de saudação **configurar o logon** janela de saudação portal do Azure.

    e. Em Olá **URL de Logout**, cole Olá **"URL de logout"** valor que você copiou de saudação **configurar o logon** janela de saudação portal do Azure.

13. Habilitar **"Permitir apenas logon SSO"**.

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Clique em **"Salvar".**

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.

### <a name="create-an-absorb-lms-test-user"></a>Criar um usuário de teste do Absorb LMS

tooenable AD do Azure usuários toolog em tooAbsorb LMS, eles devem ser provisionados no tooAbsorb LMS.  
Para o Absorb LMS, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon tooyour site da empresa de absorver LMS como um administrador.

2. Clique na guia **Usuários**.

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Clique em **usuários** em Olá **usuários** guia.

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Selecione **Usuário** da lista suspensa **Adicionar Novo**.

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Em Olá **adicionar usuário** página, execute Olá etapas a seguir:

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. Em Olá **nome** caixa de texto Nome do tipo hello primeiro como Britta.

    b. Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome como Simon.
    
    c. Em Olá **Username** caixa de texto, nome de usuário do tipo hello como Britta Simon.

    d. Em Olá **senha** caixa de texto, digite a senha de saudação do Britta Simon.

    e. Em Olá **Confirmar senha** caixa de texto, Olá tipo mesma senha.
    
    f. Torne-a **ATIVA**.   

6. Clique em **"Salvar".**
 
### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAbsorb LMS.

![Atribuir função de usuário Olá][200]

**tooassign Britta Simon tooAbsorb LMS, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **absorver LMS**.

    ![Olá absorver LMS link na lista de aplicativos Olá](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Clique em Olá absorver LMS lado a lado no hello painel de acesso, você obterá tooyour automaticamente conectado no aplicativo de absorver LMS. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

