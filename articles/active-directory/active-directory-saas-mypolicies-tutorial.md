---
title: "Tutorial: Integração do Azure Active Directory ao myPolicies | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: fcb403041cb3a8bd20ff7b34aa5cc4b7bf0c0a16
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a>Tutorial: Integração do Azure Active Directory ao myPolicies

Neste tutorial, você aprende a integrar o myPolicies ao Azure AD (Azure Active Directory).

A integração do myPolicies ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao myPolicies
- É possível permitir que os usuários se conectem automaticamente ao myPolicies (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao myPolicies, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do myPolicies

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o myPolicies por meio da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-mypolicies-from-the-gallery"></a>Adicionando o myPolicies por meio da galeria
Para configurar a integração do myPolicies ao Azure AD, é necessário adicionar o myPolicies à lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o myPolicies por meio da galeria, realize as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **myPolicies**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. No painel de resultados, selecione **myPolicies** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o myPolicies, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do myPolicies é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do myPolicies.

No myPolicies, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o myPolicies, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criando um usuário de teste do myPolicies](#creating-a-mypolicies-test-user)** – para ter um equivalente de Brenda Fernandes no myPolicies que esteja vinculado à representação de usuário do Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo myPolicies.

**Para configurar o logon único do Azure AD com o myPolicies, realize as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **myPolicies**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. Na seção **Domínio e URLs do myPolicies**, realize as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    a. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenantname>.mypolicies.com/`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador e a URL de Resposta reais. Contate a [equipe de suporte do myPolicies](mailto:support@mypolicies.com) para obter esses valores.

4. O aplicativo myPolicies espera que as declarações SAML estejam em um formato específico, o que exige a adição de mapeamentos de atributo personalizados para a configuração de atributos do token SAML. Configure as declarações a seguir para este aplicativo. Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo. A captura de tela a seguir mostra um exemplo disso. 

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. Clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** na seção **Atributos de Usuário** para expandir os atributos. Realize as seguintes etapas em cada um dos atributos exibidos:

    | Nome do atributo | Valor do atributo |
    | ------------------- | ---------- |
    | givenname | user.givenname |
    | sobrenome | user.surname |
    | emailaddress | user.mail |
    | name | user.userprincipalname |
    
    a. Clique no atributo para abrir a caixa de diálogo **Editar Atributo**.
    
    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    b. Exclua o valor da URL do **Namespace**.
    
    c. Clique em **OK** para salvar a configuração.
    
6. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![Configurar o logon único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. Na seção **Configuração do myPolicies**, clique em **Configurar o myPolicies** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. Para configurar o logon único no lado do **myPolicies**, é necessário enviar o **Certificado (Base64)** baixado e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do myPolicies](mailto:support@mypolicies.com). 

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-mypolicies-test-user"></a>Criando um usuário de teste do myPolicies

Nesta seção, você cria um usuário chamado Brenda Fernandes no myPolicies. Trabalhe com a [equipe de suporte do myPolicies](mailto:support@mypolicies.com) para adicionar os usuários à plataforma myPolicies. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao myPolicies.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao myPolicies, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **myPolicies**.

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco do myPolicies no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo myPolicies.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

