---
title: "Tutorial: Integração do Azure Active Directory com o Veracode | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Tutorial: Integração do Active Directory do Azure com o Veracode

Neste tutorial, você aprenderá como toointegrate Veracode com o Azure Active Directory (AD do Azure).

Integrando o Veracode com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooVeracode.
- Você pode habilitar seu usuários tooautomatically get conectado tooVeracode (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Veracode, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Veracode habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Veracode da Galeria de saudação
2. Configurar e testar logon único do Azure AD

## <a name="add-veracode-from-hello-gallery"></a>Adicionar Veracode da Galeria de saudação
integração de saudação tooconfigure de Veracode no AD do Azure, você precisa tooadd Veracode da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Veracode da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Veracode**, selecione **Veracode** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Veracode na lista de resultados de saudação](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Veracode, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Veracode é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Veracode precisa toobe estabelecida.

Veracode, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Veracode, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Veracode](#create-a-veracode-test-user)**  -toohave um equivalente do Britta Simon em Veracode é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Veracode.

**tooconfigure AD do Azure-logon único com o Veracode, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Veracode** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. Em Olá **Veracode domínio e URLs** seção, o usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure. 

    ![Configurar Logon Único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooVeracode com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

    Seu aplicativo de Veracode espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens saml** configuração. Olá captura de tela a seguir mostra um exemplo.
    
    ![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Atributos")

6. mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:

    | Nome do atributo | Valor do atributo |
    |--- |--- |
    | nome |User.givenname |
    | sobrenome |User.surname |
    | email |User.mail |
    
    a. Para cada linha de dados na tabela de saudação acima, clique em **Adicionar atributo de usuário**.
    
    ![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Atributos")
    
    ![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Atributos")
    
    b. Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. Em Olá **o valor do atributo** texto, o valor do atributo select Olá mostrado para aquela linha.
    
    d. Clique em **OK**.

7. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. Em Olá **Veracode configuração** seção, clique em **configurar Veracode** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**

    ![Configuração do Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Veracode como administrador.

10. No menu de saudação na parte superior de saudação, clique em **configurações**e, em seguida, clique em **Admin**.
   
    ![Administração](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administração")

11. Clique em Olá **SAML** guia.

12. Em Olá **configurações do SAML organização** , execute Olá etapas a seguir:
   
    ![Administração](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administração")
   
    a.  Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.
    
    b. tooupload seu certificado baixado do portal do Azure, clique **Escolher arquivo**.
   
    c. Selecione **Habilitar Autorregistro**.

13. Em Olá **configurações do registro de autoatendimento** seção, executar Olá etapas a seguir e, em seguida, clique em **salvar**:
   
    ![Administração](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administração")
   
    a. Para **Ativação de Novo Usuário**, selecione **Sem Ativação Necessária**.
   
    b. Para **Atualizações de Dados do Usuário**, selecione **Dados do Usuário de Preferência do Veracode**.
   
    c. Para **detalhes de atributos de SAML**, selecione Olá seguinte:
      * **Funções de usuário**
      * **Administrador de políticas**
      * **Revisor**
      * **Orientações de Segurança**
      * **Executivo**
      * **Emissor**
      * **Criador**
      * **Todos os Tipos de Verificação**
      * **Associações de Equipe**
      * **Equipe Padrão**

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-veracode-test-user"></a>Criar um usuário de teste do Veracode
Em ordem tooenable AD do Azure usuários toolog em Veracode, eles devem ser provisionados no Veracode. No caso de saudação de Veracode, o provisionamento é uma tarefa automatizada. Não há nenhum item de ação para você. Os usuários são criados automaticamente se necessário durante a saudação primeiro único tentativa de logon.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros Veracode usuário conta ou APIs fornecidas pelo Veracode tooprovision contas de usuário do AD do Azure.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooVeracode.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooVeracode, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Veracode**.

    ![link de Veracode Olá na lista de aplicativos Olá](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Veracode Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Veracode aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

