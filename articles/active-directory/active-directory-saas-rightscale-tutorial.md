---
title: "Tutorial: Integração do Azure Active Directory ao Rightscale | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 62c95d798e851ddf6030714a052afb32b977b7e3
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Tutorial: Integração do Azure Active Directory ao Rightscale

Neste tutorial, você aprende a integrar o Rightscale ao Azure AD (Azure Active Directory).

A integração do Rightscale ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Rightscale
- É possível permitir que os usuários se conectem automaticamente ao Rightscale (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Rightscale, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Rightscale

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Rightscale por meio da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-rightscale-from-the-gallery"></a>Adicionando o Rightscale por meio da galeria
Para configurar a integração do Rightscale ao Azure AD, é necessário adicionar o Rightscale à lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Rightscale por meio da galeria, realize as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **Rightscale**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. No painel de resultados, selecione **Rightscale** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Rightscale, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Rightscale é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Rightscale.

No Rightscale, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Rightscale, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criando um usuário de teste do Rightscale](#creating-a-rightscale-test-user)** – para ter um equivalente de Brenda Fernandes no Rightscale que esteja vinculado à representação de usuário do Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Rightscale.

**Para configurar o logon único do Azure AD com o Rightscale, realize as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Rightscale**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. Na seção **Domínio e URLs do Rightscale**, se você desejar configurar o aplicativo no **modo iniciado pelo IDP**, não precisará realizar nenhuma etapa, pois o aplicativo já é pré-integrado ao Azure.

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. Na seção **Domínio e URLs do Rightscale**, se desejar configurar o aplicativo no **modo iniciado pelo SP**, realize as seguintes etapas:
    
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Clique em **Mostrar configurações de URL avançadas**.

    b. Na caixa de texto **URL de Logon**, digite a URL: `https://login.rightscale.com/`

5. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. Na seção **Configuração do Rightscale**, clique em **Configurar o Rightscale** para abrir a janela **Configurar logon**. Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. Para configurar o SSO para o aplicativo, você precisa entrar no locatário do RightScale como administrador.

    a. No menu na parte superior, clique na guia **Configurações** e selecione **Logon Único**.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Clique no botão "**novo**" para adicionar **Seus Provedores de Identidade do SAML**.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. Na caixa de texto do **Nome de Exibição**, insira o nome da sua empresa.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Selecione **Permitir o SSO iniciado pelo RightScale usando uma dica de descoberta** e insira seu **nome de domínio** na caixa de texto abaixo.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure no **Ponto de Extremidade do SSO do SAML** no RightScale.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Cole o valor da **ID da Entidade SAML** copiado do portal do Azure na **EntityID SAML** no RightScale.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Clique no botão **Navegador** para carregar o certificado baixado no portal do Azure.
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Clique em **Salvar**.
<CE>
> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-rightscale-test-user"></a>Criando um usuário de teste do Rightscale

Nesta seção, você criará um usuário chamado Brenda Fernandes no RightScale. Trabalhe com a [equipe de suporte ao Cliente do Rightscale](mailto:support@rightscale.com) para adicionar os usuários à plataforma RightScale.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Rightscale.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Rightscale, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Rightscale**.

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.  

Ao clicar no bloco do RightScale no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do RightScale.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

