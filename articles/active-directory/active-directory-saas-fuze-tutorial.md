---
title: "Tutorial: integração do Azure Active Directory com o Fuze | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: c7f7b095aac6202a7ec5248ee2bbb109615287a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a>Tutorial: integração do Azure Active Directory com o Fuze

Neste tutorial, você aprenderá a integrar o Fuze ao Azure AD (Azure Active Directory).

A integração do Fuze com o Azure AD oferece os seguintes benefícios:

- É possível controlar, no Azure AD, quem terá acesso ao Fuze
- É possível permitir que seus usuários façam logon automaticamente no Fuze (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Fuze, são necessários os seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do Fuze habilitada para logon único


> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.


Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Fuze da galeria
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-fuze-from-the-gallery"></a>Adicionando o Fuze da galeria
Para configurar a integração do Fuze com o Azure AD, é necessário adicionar o Fuze da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Fuze da galeria, siga as etapas abaixo:**

1. No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **Fuze**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. No painel de resultados, selecione **Fuze** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Fuze, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Fuze é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Fuze.

Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como sendo o valor de **nome de usuário** no Fuze.

Para configurar e testar o logon único do Azure AD com o Fuze, é necessário concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criando um usuário de teste do Fuze](#creating-a-fuze-test-user)** – para ter um equivalente de Brenda Fernandes no Fuze que esteja vinculado à representação dela no Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal de Gerenciamento do Azure e configurará o logon único em seu aplicativo Fuze.

**Para configurar o logon único do Azure AD com o Fuze, siga as etapas abaixo:**

1. No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **Fuze**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. Na seção **URLs e Domínio do Fuze**, siga as etapas abaixo:

    ![Configurar o logon único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    Na caixa de texto **URL de Logon**, digite a URL de logon como: `https://www.thinkingphones.com/jetspeed/portal/`

4.  Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. Na seção **Certificado de Autenticação SAML**, clique em **XML de metadados** e, em seguida, salve o arquivo xml em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. Para configurar o logon único no lado do **Fuze**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte Fuze](https://www.fuze.com/support). Isso será configurado para que a conexão de SSO do SAML seja definida corretamente em ambos os lados.


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**. 


### <a name="creating-a-fuze-test-user"></a>Criando um usuário de teste do Fuze

O aplicativo Fuze dá suporte ao provisionamento de usuário just-in-time completo. Dessa forma, os usuários serão criados automaticamente quando eles conectarem. Para outros esclarecimentos, contate o [suporte](https://www.fuze.com/support) Fuze.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Fuze.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Fuze, siga as etapas abaixo:**

1. No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Fuze**.

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    

### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco Fuze no Painel de Acesso, seu logon deverá ser feito automaticamente no aplicativo Fuze.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png