---
title: "Tutorial: integração do Azure Active Directory com o Humanity | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Humanity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a>Tutorial: integração do Azure Active Directory com o Humanity

Neste tutorial, você aprenderá a integrar o Humanity ao Azure AD (Azure Active Directory).

A integração do Humanity ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Humanity
- Você pode permitir que seus usuários façam logon automaticamente no Humanity (logon único) com as contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Humanity, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do Humanity habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o Humanity da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-humanity-from-the-gallery"></a>Adicionar o Humanity da galeria
Para configurar a integração do Humanity ao Azure AD, você precisará adicionar o Humanity da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Humanity da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **Humanity**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. No painel de resultados, selecione **Humanity** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Humanity, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Humanity é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Humanity.

No Humanity, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Humanity, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criação de um usuário de teste do Humanity](#creating-a-humanity-test-user)** – para ter um equivalente de Brenda Fernandes no Humanity que esteja vinculado à representação do usuário no Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Humanity.

**Para configurar o logon único do Azure AD com o Humanity, realize as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Humanity**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. Na seção **Domínio e URLs do Humanity**, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://company.humanity.com/includes/saml/`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://company.humanity.com/app/`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte do Cliente Humanity](https://www.humanity.com/support/) para obter esses valores. 
 
4. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do Humanity**, clique em **Configurar Humanity** para abrir a janela **Configurar logon**. Copie a **URL do Serviço de Logon Único do SAML e a URL de Logoff** da **seção de Referência Rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do **Humanity** como um administrador.

8. No menu na parte superior, clique em **Administrador**.
   
    ![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")

9. Em **Integração**, clique em **Logon Único**.
   
    ![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Logon Único")

10. Na seção **Logon Único** , realize as seguintes etapas:
   
    ![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Logon Único")
   
    a. Selecione **SAML Habilitado**.

    b. Selecione **Permitir Logon de Senha**.

    c. Cole o valor da **URL do Serviço de Logon Único do SAML** na caixa de texto **URL do Emissor do SAML**.

    d. Cole o valor da **URL de Saída** na caixa de texto **URL de Logout Remota**.
   
    e. Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509** .

11. Clique em **Salvar Configurações**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-humanity-test-user"></a>Criar um usuário de teste do Humanity

Para permitir que os usuários do Azure AD façam logon no Humanity, eles deverão ser provisionados no Humanity. No caso do Humanity, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon em seu site de empresa do **Humanity** como administrador.

2. Clique em **Administrador**.
   
    ![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")

3. Clique em **Equipe**.
   
    ![Equipe](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Equipe")

4. Em **Ações**, clique em **Adicionar Funcionários**.
   
    ![Adicionar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Adicionar Funcionários")

5. Na seção **Adicionar Funcionários** , realize as seguintes etapas:
   
    ![Salvar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Salvar Funcionários")
   
    a. Nas caixas de texto correspondentes, digite o **Nome**, o **Sobrenome** e o **Email** de uma conta válida do AAD que você deseja provisionar.

    b. Clique em **Salvar Funcionários**.

>[!NOTE]
>É possível usar qualquer outra ferramenta de criação da conta de usuário do Humanity ou as APIs fornecidas pelo Humanity para provisionar as contas de usuário do AAD.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Humanity.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Humanity, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Humanity**.

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco Humanity no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Humanity.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

