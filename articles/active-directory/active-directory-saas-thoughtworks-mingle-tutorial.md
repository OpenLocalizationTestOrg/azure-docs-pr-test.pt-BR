---
title: "Tutorial: Integração do Azure Active Directory com o Thoughtworks Mingle | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Tutorial: Integração do Active Directory do Azure com o Thoughtworks Mingle

Neste tutorial, você aprenderá como toointegrate Thoughtworks Mingle com o Azure Active Directory (AD do Azure).

Integrar Thoughtworks Mingle com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooThoughtworks Mingle
- Você pode habilitar seus usuários tooautomatically get conectado tooThoughtworks Mingle (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Thoughtworks Mingle, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Thoughtworks Mingle habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Thoughtworks Mingle da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Adicionando Thoughtworks Mingle da Galeria de saudação
integração de saudação tooconfigure do Thoughtworks Mingle no AD do Azure, você precisa tooadd Thoughtworks Mingle na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Thoughtworks Mingle da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Thoughtworks Mingle**, selecione **Thoughtworks Mingle** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![ThoughtWorks Mingle na lista de resultados de saudação](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o Thoughtworks Mingle, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Thoughtworks Mingle é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Thoughtworks Mingle precisa toobe estabelecida.

Thoughtworks Mingle, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Thoughtworks Mingle, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave um equivalente do Britta Simon no Thoughtworks Mingle que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Thoughtworks Mingle.

**tooconfigure AD do Azure-logon único com Thoughtworks Mingle, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Thoughtworks Mingle** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. Em Olá **Thoughtworks Mingle domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > Olá valor não é real. Valor de saudação de atualização com hello URL de logon real. Entre em contato com [a equipe de suporte Thoughtworks Mingle cliente](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget valor de saudação. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. Faça logon no tooyour **Thoughtworks Mingle** site da empresa como administrador.

7. Clique em Olá **Admin** guia e, em seguida, clique em **Config SSO**.
   
    ![Guia Administrador](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuração de SSO")

8. Em Olá **Config SSO** , execute Olá etapas a seguir:
   
    ![Configuração de SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuração de SSO")
    
    a. arquivo de metadados de saudação tooupload, clique em **Escolher arquivo**. 

    b. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Criar um usuário de teste do Thoughtworks Mingle

Para o AD do Azure usuários toobe capaz de toosign no, eles devem ser provisionado toohello aplicativo Thoughtworks Mingle usando seus nomes de usuário do Active Directory do Azure. No caso de saudação do Thoughtworks Mingle, o provisionamento é uma tarefa manual.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour site da empresa Thoughtworks Mingle como administrador.

2. Clique em **Perfil**.
   
    ![Seu primeiro projeto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Seu primeiro projeto")

3. Clique em Olá **Admin** guia e, em seguida, clique em **usuários**.
   
    ![Usuários](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Usuários")

4. Clique em **Novo Usuário**.
   
    ![Novo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Novo Usuário")

5. Em Olá **novo usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Caixa de diálogo Novo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Novo Usuário")  
 
    a. Saudação de tipo **nome de usuário**, **nome de exibição**, **escolher senha**, **Confirmar senha** de uma válida do Azure você deseja tooprovision de conta do AD em Olá relacionados caixas de texto. 

    b. Para **Tipo de usuário**, selecione **Usuário completo**.

    c. Clique em **Criar este Perfil**.

>[!NOTE]
>Você pode usar outras Thoughtworks Mingle usuário conta ferramentas de criação ou APIs fornecidas pelo Thoughtworks Mingle tooprovision contas de usuário do AAD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooThoughtworks Mingle.

![Atribuir função de usuário Olá][200] 

**tooassign tooThoughtworks Britta Simon Mingle, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Thoughtworks Mingle**.

    ![link de Thoughtworks Mingle Olá na lista de aplicativos Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em Olá Thoughtworks Mingle lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Thoughtworks Mingle aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

