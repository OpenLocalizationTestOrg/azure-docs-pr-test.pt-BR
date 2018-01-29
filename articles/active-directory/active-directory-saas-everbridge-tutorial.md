---
title: "Tutorial: Integração do Azure Active Directory ao EverBridge | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 493705359186dc9d27e01d0d5fae65829a8af834
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a>Tutorial: integração do Azure Active Directory ao Everbridge

Neste tutorial, você aprenderá a integrar o EverBridge ao Azure AD (Azure Active Directory).

A integração do EverBridge ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao EverBridge
- Você pode habilitar o logon automático de seus usuários no EverBridge (Logon Único) com as contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao EverBridge, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do EverBridge com logon único habilitado

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar EverBridge da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-everbridge-from-the-gallery"></a>Adicionar EverBridge da galeria
Para configurar a integração do EverBridge ao Azure AD, você precisará adicionar o EverBridge da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o EverBridge da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **EverBridge**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. No painel de resultados, selecione **EverBridge** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o EverBridge com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do EverBridge é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no EverBridge.

No EverBridge, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o EverBridge, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criar um usuário de teste do EverBridge](#creating-an-everbridge-test-user)** – para ter um equivalente de Brenda Fernandes no EverBridge que esteja vinculado à representação desse usuário no Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo EverBridge.

**Para configurar o logon único do Azure AD com o EverBridge, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **EverBridge**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. Na seção **URLs e Domínio do EverBridge**, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    a. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://sso.everbridge.net/<companyname>`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador e a URL de Resposta reais. Entre em contato com a [equipe de suporte do EverBridge](mailto:support@everbridge.com) para obter esses valores.
 
4. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![Configurar o logon único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do EverBridge**, clique em **Configurar o EverBridge** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. Para configurar o SSO para o aplicativo, você precisa entrar no locatário Everbridge como administrador.

7. No menu na parte superior, clique na guia **Configurações** e selecione **Logon Único** em **Segurança**.
   
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    a. Na caixa de texto **Nome**, digite o nome do Provedor do Identificador (por exemplo: o nome de sua empresa).
   
    b. Na caixa de texto **Nome da API** , digite o nome da API.
   
    c. Clique no botão **Escolher Arquivo** para carregar o arquivo de metadados que você baixou do portal do Azure.
   
    d. No Local de Identidade do SAML, selecione **A identidade está no elemento NameIdentifier da instrução Subject**.
   
    e. Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da URL do SSO do SAML do Azure AD.
   
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    f. Na Associação de Solicitação Iniciada pelo Provedor de Serviço, selecione **Redirecionamento HTTP**.

    g. Clique em **Salvar**

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-everbridge-test-user"></a>Criar um usuário de teste do EverBridge

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Everbridge. Trabalhe com a [equipe de suporte do EverBridge](mailto:support@everbridge.com) para adicionar os usuários na plataforma do Everbridge.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao EverBridge.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao EverBridge, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **EverBridge**.

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Everbridge no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo Everbridge.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

