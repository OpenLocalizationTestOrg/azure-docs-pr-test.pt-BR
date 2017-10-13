---
title: "Tutorial: Integração do Azure Active Directory com o Adobe Sign | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Adobe Sign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Tutorial: Integração do Azure Active Directory ao Adobe Sign

Neste tutorial, você aprende a integrar o Adobe Sign ao Azure AD (Azure Active Directory).

A integração do Adobe Sign ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Adobe Sign
- É possível permitir que os usuários se conectem automaticamente ao Adobe Sign (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Adobe Sign, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Adobe Sign

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Adobe Sign por meio da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-adobe-sign-from-the-gallery"></a>Adicionando o Adobe Sign por meio da galeria
Para configurar a integração do Adobe Sign ao Azure AD, você precisa adicionar o Adobe Sign à lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Adobe Sign por meio da galeria, realize as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **Adobe Sign**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. No painel de resultados, selecione **Adobe Sign** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Adobe Sign, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Adobe Sign é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Adobe Sign.

No Adobe Sign, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Adobe Sign, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criando um usuário de teste do Adobe Sign](#creating-an-adobe-sign-test-user)** – para ter um equivalente de Brenda Fernandes no Adobe Sign que esteja vinculado à representação de usuário do Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Adobe Sign.

**Para configurar o logon único do Azure AD com o Adobe Sign, realize as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo do **Adobe Sign**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. Na seção **Domínio e URLs do Adobe Sign**, realize as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.echosign.com/`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.echosign.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte ao Cliente do Adobe Sign](https://helpx.adobe.com/in/contact/support.html) para obter esses valores. 
 
4. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![Configurar o logon único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do Adobe Sign**, clique em **Configurar o Adobe Sign** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. Em outra janela do navegador da Web, faça logon em seu site de empresa do Adobe Sign como administrador.

8. No menu na parte superior, clique em **Conta** e, depois, no painel de navegação do lado esquerdo, clique em **Configurações do SAML**, em **Configurações da Conta**.
   
   ![Conta](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Conta")

9. Na seção Configuração do SAML, execute as seguintes etapas:
   
   ![Configurações do SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Configurações do SAML")
   
   a. Para **Modo do SAML**, selecione **SAML Obrigatório**.
   
   b. Selecione **Permitir que os Administradores da Conta do EchoSign façam logon usando suas Credenciais do EchoSign**.
   
   c. Para **Criação de Usuário**, selecione **Adicionar automaticamente os usuários autenticados por meio do SAML**.

10. Siga em frente executando as seguintes etapas:

       ![Configurações do SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Configurações do SAML")

    a. Cole a **ID da Entidade SAML** copiada no portal do Azure para a caixa de texto **ID da Entidade do IdP**.
    
    b. Cole a **URL do Serviço de Logon Único SAML** copiada no portal do Azure para a caixa de texto **URL de Logon do IdP**.
   
    c. Cole a **URL de Saída** copiada no portal do Azure para a caixa de texto **URL de Logoff do IdP**.

    d. Abra o arquivo de **Certificado (Base64)** baixado no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado do IdP**

    e. Clique em **Salvar Alterações**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Criando um usuário de teste do Adobe Sign

Para permitir que os usuários do Azure AD façam logon no Adobe Sign, eles devem ser provisionados no Adobe Sign. No caso do Adobe Sign, o provisionamento é uma tarefa manual.

>[!NOTE]
>É possível usar qualquer outra ferramenta de criação da conta de usuário do Adobe Sign ou as APIs fornecidas pelo Adobe Sign para provisionar contas de usuário do AAD. 

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon em seu site de empresa do **Adobe Sign** como administrador.

2. No menu na parte superior, clique em **Conta** e, depois, no painel de navegação do lado esquerdo, clique em **Usuários e Grupos** e, em seguida, em **Criar um novo usuário**.
   
   ![Conta](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Conta")
   
3. Na seção **Criar Novo Usuário** , realize as seguintes etapas:
   
   ![Criar usuário](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Criar usuário")
   
   a. Digite o **Endereço de Email**, **Nome** e **Sobrenome** de uma conta válida do AAD que deseja provisionar nas caixas de texto relacionadas.
   
   b. Clique em **Criar Usuário**.

>[!NOTE]
>O titular da conta do Azure Active Directory recebe um email que inclui um link para confirmar a conta antes que ela se torne ativa. 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Adobe Sign.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Adobe Sign, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Adobe Sign**.

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Quando você clicar no bloco Adobe Sign no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Adobe Sign.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

