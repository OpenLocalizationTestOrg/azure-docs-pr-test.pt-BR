---
title: "Tutorial: Integração do Azure Active Directory ao Boomi | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Tutorial: Integração do Active Directory do Azure ao Boomi

Neste tutorial, você aprenderá como toointegrate Boomi com o Azure Active Directory (AD do Azure).

Integrando o Boomi com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBoomi
- Você pode habilitar seu usuários tooautomatically get conectado tooBoomi (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Boomi, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Boomi

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Boomi da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-boomi-from-hello-gallery"></a>Adicionando Boomi da Galeria de saudação
integração de saudação tooconfigure do Boomi no AD do Azure, você precisa tooadd Boomi da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Boomi da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Boomi**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. No painel de resultados de saudação, selecione **Boomi**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Boomi, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Boomi é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Boomi precisa toobe estabelecida.

No Boomi, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Boomi, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Boomi](#creating-a-boomi-test-user)**  -toohave um equivalente do Britta Simon no Boomi é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Boomi.

**tooconfigure AD do Azure-logon único com Boomi, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Boomi** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. Em Olá **Boomi domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://platform.boomi.com/sso/<accountname>/saml`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [equipe de suporte do Boomi](https://boomi.com/company/contact/) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Aplicativo do Boomi espera asserções SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo.
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, para cada linha mostrada na tabela abaixo, a saudação execute Olá etapas a seguir:

    | Nome do atributo | Valor do atributo |
    | -------------- | --------------- |
    | FEDERATION_ID | user.mail |
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **OK**.

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. Em Olá **Boomi configuração** seção, clique em **configurar Boomi** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. Em outra janela do navegador da Web, faça logon em seu site de empresa Boomi como um administrador. 

9. Navegue muito**nome da empresa** e vá muito**configurar**.

10. Clique em Olá **opções SSO** guia e executar etapas a seguir.

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Marque a caixa de seleção **Habilitar Logon Único do SAML**.

    b. Clique em **importação** Olá tooupload baixado certificado do AD do Azure muito**certificado do provedor de identidade**.
    
    c. Em Olá **URL de logon do provedor de identidade** caixa de texto, coloque o valor de saudação do **Single Sign-On URL do serviço SAML** da janela de configuração de aplicativo do AD do Azure.

    d. Para **Local do ID de Federação**, selecione o botão de opção **A Id de Federação está contida no elemento Atributo FEDERATION_ID**. 

    e. Clique no botão **Salvar** .

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-boomi-test-user"></a>Criar um usuário de teste do Boomi

Em ordem tooenable AD do Azure usuários toolog em tooBoomi, eles devem ser provisionados no Boomi. No caso de saudação do Boomi, o provisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de usuário, execute Olá etapas a seguir:

1. Faça logon no tooyour site da empresa Boomi como um administrador.

2. Após o logon, navegue muito**gerenciamento de usuários** e vá muito**usuários**.

    ![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuários")

3. Clique em  **+**  ícone e hello **adicionar/manter as funções de usuário** caixa de diálogo é aberta.

    ![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuários")

    ![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuários")

    a. Em Olá **endereço de email do usuário** caixa de texto, como o email de saudação do tipo de usuário BrittaSimon@contoso.com.
    
    b. Em Olá **nome** caixa de texto, tipo hello primeiro nome do usuário, como Britta.

    c. Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome do usuário como Simon.
    
    d. Insira saudação do usuário **ID da federação**. Cada usuário deve ter uma ID de federação que identifica exclusivamente o usuário Olá na conta de saudação.
    
    e. Atribuir Olá **usuário padrão** usuário de toohello de função. Não atribua a função de administrador de saudação porque que poderia dar a ele acesso atmosfera normal, bem como acesso de logon único.
    
    f. Clique em **OK**.
    
    > [!NOTE]
    > usuário de saudação não receberá um email de notificação de boas-vindas contendo uma senha que pode ser usado toolog em toohello AtomSphere conta porque sua senha é gerenciada por meio do provedor de identidade hello. Você pode usar qualquer ferramenta de criação outros Boomi usuário conta ou APIs fornecidas pelo Boomi tooprovision contas de usuário do AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBoomi.

![Atribuir usuário][200] 

**tooassign Britta Simon tooBoomi, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Boomi**.

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Boomi Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Boomi aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

