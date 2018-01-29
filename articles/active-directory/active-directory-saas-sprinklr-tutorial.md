---
title: "Tutorial: Integração do Azure Active Directory ao Sprinklr | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 13eea1b7889c6382f1f4a6fb5c9bc02578c52711
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Tutorial: Integração do Active Directory do Azure com o Sprinklr

Neste tutorial, você aprenderá a integrar o Sprinklr ao Azure AD (Azure Active Directory).

A integração do Sprinklr ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Sprinklr
- Você pode permitir que seus usuários façam logon automaticamente no Sprinklr (logon único) com as contas do Azure AD deles
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Sprinklr, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Sprinklr

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o Sprinklr da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sprinklr-from-the-gallery"></a>Adicionar o Sprinklr da galeria
Para configurar a integração do Sprinklr ao Azure AD, você precisará adicionar o Sprinklr da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Sprinklr da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **Sprinklr**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. No painel de resultados, selecione **Sprinklr** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Sprinklr, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Sprinklr é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Sprinklr.

No Sprinklr, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Sprinklr, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criação de um usuário de teste do Sprinklr](#creating-a-sprinklr-test-user)** – para ter um equivalente de Brenda Fernandes no Sprinklr que esteja vinculado à representação do usuário no Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Sprinklr.

**Para configurar o logon único do Azure AD com o Sprinklr, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Sprinklr**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. Na seção **URLs e Domínio do Sprinklr**, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sprinklr.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Logon e o Identificador reais. Contate a [equipe de suporte do cliente Sprinklr](https://www.sprinklr.com/contact-us/) para obter esses valores. 
 
4. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do Sprinklr**, clique em **Configurar Sprinklr** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do Sprinklr como um administrador.

8. Vá para **Administração \> Configurações**.
   
    ![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")

9. Vá para **Gerenciar Parceiro \> Logon Único** no painel à esquerda.
   
    ![Gerenciar Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gerenciar Parceiro")

10. Clique em **+Adicionar Logons Únicos**.
   
    ![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Logons Únicos")

11. Na página **Logon Único** , realize as seguintes etapas:
   
    ![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Logons Únicos")

    a. Na caixa de texto **Nome**, digite um nome para a sua configuração (por exemplo: *WAADSSOTest*).

    b. Selecione **Habilitado**.

    c. Selecione **Usar novo Certificado de SSO**.
             
    e. Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado do Provedor de Identidade**.

    f. Cole a **ID de Entidade do SAML** copiada no portal do Azure para a caixa de texto **ID da Entidade**.

    g. Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.

    h. Na caixa de texto **URL de Logoff do Provedor de Identidade**, cole o valor da **URL de Saída** que você copiou do Portal do Azure.
     
    i. Para **Tipo de ID de Usuário do SAML**, selecione **A declaração contém o nome de usuário de sprinklr.com do Usuário**.

    j. Para **Local da ID de Usuário do SAML**, selecione **A ID de Usuário está contida no elemento Identificador de Nome da instrução Subject**.

    k. Clique em **Salvar**.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sprinklr-test-user"></a>Criar um usuário de teste do Sprinklr

1. Faça logon em seu site de empresa do Sprinklr como um administrador.

2. Vá para **Administração \> Configurações**.
   
    ![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")

3. Vá para **Gerenciar Cliente \> Usuários** no painel à esquerda.
   
    ![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configurações")

4. Clique em **Adicionar Usuário**.
   
    ![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configurações")

5. No diálogo **Editar usuário** , realize as seguintes etapas:
   
    ![Editar usuário](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Editar usuário") 

    a. Nas caixas de texto **Email**, **Nome** e **Sobrenome**, digite as informações de uma conta de usuário do Azure AD que você deseja provisionar.

    b. Selecione **Senha Desabilitada**.

    c. Selecione **Idioma**.

    d. Selecione **Tipo de Usuário**.

    e. Clique em **Atualizar**.
   
     >[!IMPORTANT]
     >**Senha Desabilitada** deve ser marcada para permitir que um usuário faça logon por meio de um Provedor de identidade. 
     
6. Vá para **Função**e realize as seguintes etapas:
   
    ![Funções de Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Funções de Parceiro")

    a. Na lista **Global**, selecione **ALL\_Permissions**.  

    b. Clique em **Atualizar**.

>[!NOTE]
>Você pode usar qualquer outra ferramenta de criação da conta de usuário do Sprinklr ou APIs fornecidas pelo Sprinklr para provisionar contas de usuário do AD do Azure. 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Sprinklr.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Sprinklr, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Sprinklr**.

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando clicar no bloco do Sprinklr no Painel de Acesso, você deverá ser automaticamente conectado ao seu aplicativo Sprinklr. Para obter mais informações sobre o Painel de Acesso, consulte [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

