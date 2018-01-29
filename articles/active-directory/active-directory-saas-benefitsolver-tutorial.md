---
title: "Tutorial: integração do Azure Active Directory ao Benefitsolver | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Benefitsolver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 333394c1-b5a7-489c-8f7b-d1a5b4e782ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2017
ms.author: jeedes
ms.openlocfilehash: d23f1c4d6613d525695ed222e0d84736b9007833
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Tutorial: Integração do Active Directory do Azure ao Benefitsolver

Neste tutorial, você aprenderá a integrar o Benefitsolver ao Azure AD (Azure Active Directory).

A integração do Benefitsolver ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao Benefitsolver.
- Você pode permitir que seus usuários façam logon automaticamente no Benefitsolver (logon único) com as respectivas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>pré-requisitos

Para configurar a integração do Azure AD ao Benefitsolver, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Benefitsolver

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Benefitsolver da galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-benefitsolver-from-the-gallery"></a>Adicionando o Benefitsolver da galeria
Para configurar a integração do Benefitsolver ao Azure AD, você precisará adicionar o Benefitsolver da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Benefitsolver da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **Benefitsolver**, selecione **Benefitsolver** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Benefitsolver na lista de resultados](./media/active-directory-saas-benefitsolver-tutorial/tutorial_benefitsolver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Benefitsolver, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Benefitsolver é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Benefitsolver.

No Benefitsolver, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Benefitsolver, você precisará executar as seguintes tarefas básicas:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Benefitsolver](#create-a-benefitsolver-test-user)** – para ter um equivalente de Brenda Fernandes no Benefitsolver que esteja vinculado à representação de usuário do Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Benefitsolver.

**Para configurar o logon único do Azure AD com o Benefitsolver, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração do aplicativo **Benefitsolver**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-benefitsolver-tutorial/tutorial_benefitsolver_samlbase.png)

3. Na seção **Domínio e URLs do Benefitsolver**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Benefitsolver](./media/active-directory-saas-benefitsolver-tutorial/tutorial_benefitsolver_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<companyname>.benefitsolver.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.benefitsolver.com/saml20`

    c. Na caixa de texto **URL de Resposta**, digite a URL: `https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml`

    > [!NOTE] 
    > Esses valores não são reais. Você precisa atualizar esses valores com a URL de Logon, o Identificador e a URL de Resposta reais. Entre em contato com a [equipe de suporte ao cliente do Benefitsolver](https://www.businessolver.com/contact) para obter esses valores.

4. Seu aplicativo Benefitsolver espera as declarações do SAML em um formato específico, o que exige a adição de mapeamentos de atributo personalizados de acordo com a sua configuração de **atributos do token SAML** .

    ![Seção de atributo do Benefitsolver](./media/active-directory-saas-benefitsolver-tutorial/tutorial_attribute.png)

5. Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:
    
    | Nome do atributo| Valor do atributo|
    |---------------|----------------|
    | ClientID | Você precisa obter esse valor com a [equipe de suporte do Benefitsolver](https://www.businessolver.com/contact).|
    | ClientKey | Você precisa obter esse valor com a [equipe de suporte do Benefitsolver](https://www.businessolver.com/contact).|
    | LogoutURL | Você precisa obter esse valor com a [equipe de suporte do Benefitsolver](https://www.businessolver.com/contact).|
    | EmployeeID | Você precisa obter esse valor com a [equipe de suporte do Benefitsolver](https://www.businessolver.com/contact).|

    a. Clique em Adicionar atributo para abrir o diálogo Adicionar Atributo.

    ![Seção de atributo do Benefitsolver](./media/active-directory-saas-benefitsolver-tutorial/tutorial_attribute_04.png)
    
    ![Seção de atributo do Benefitsolver](./media/active-directory-saas-benefitsolver-tutorial/tutorial_attribute_05.png)

    b. Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.
    
    c. Na lista **Valor**, digite o valor do atributo mostrado para essa linha.
    
    d. Clique em **OK**.

6. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/active-directory-saas-benefitsolver-tutorial/tutorial_benefitsolver_certificate.png) 

7. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_400.png)

8. Para configurar o logon único no **Benefitsolver**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Benefitsolver](https://www.businessolver.com/contact).

    > [!NOTE]
    > A equipe de suporte do Benefitsolver precisa fazer a configuração real do SSO. Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-benefitsolver-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-benefitsolver-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-benefitsolver-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-benefitsolver-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-benefitsolver-test-user"></a>Criar um usuário de teste do Benefitsolver

Para permitir que os usuários do AD do Azure façam logon no Benefitsolver, eles deverão ser provisionados no Benefitsolver. No caso do Benefitsolver, os dados de funcionários são preenchidos em seu aplicativo por meio de um arquivo de censo do sistema HRIS (geralmente à noite).

> [!NOTE]
> É possível usar qualquer outra ferramenta de criação da conta de usuário do Benefitsolver ou as APIs fornecidas pelo Benefitsolver para provisionar as contas de usuário do AAD.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Benefitsolver.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Benefitsolver, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, escolha **Benefitsolver**.

    ![O link do Benefitsolver na lista de Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/tutorial_benefitsolver_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco Benefitsolver no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Benefitsolver.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefitsolver-tutorial/tutorial_general_203.png

