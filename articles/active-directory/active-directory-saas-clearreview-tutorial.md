---
title: "Tutorial: Integração do Azure Active Directory ao Clear Review | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Clear Review."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 8264159a-11a2-4a8c-8285-4efea0adac8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2017
ms.author: jeedes
ms.openlocfilehash: e999e375d11f5d2a4657b360cf774ae10c28b0e0
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clear-review"></a>Tutorial: integração do Azure Active Directory ao Clear Review

Neste tutorial, você aprenderá a integrar o Clear Review ao Azure Active Directory (Azure AD).

A integração do Clear Review ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao Clear Review.
- Você pode permitir que seus usuários façam logon automaticamente no Clear Review (logon único) com as contas do Azure AD deles.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Clear Review, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único no Clear Review

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando Clear Review da Galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-clear-review-from-the-gallery"></a>Adicionando Clear Review da Galeria
Para configurar a integração do Clear Review com o Azure AD, você precisará adicionar o Clear Review à sua lista de aplicativos SaaS gerenciados da galeria.

**Para adicionar o Clear Review por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **Clear Review**, selecione **Clear Review** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Clear Review na lista de resultados](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Clear Review, com base em uma usuária de teste chamada "Britta Simon".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Clear Review é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado em Clear Review.

No Clear Review, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Clear Review, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Clear Review](#create-a-clear-review-test-user)** – para ter um equivalente de Britta Simon no Clear Review vinculado à representação do usuário do Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Clear Review.

**Para configurar o logon único do Azure AD com o Clear Review, execute as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Clear Review**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_samlbase.png)

3. Na seção **Domínio e URLs do Clear Review**, realize as seguintes etapas se desejar configurar o aplicativo no modo **iniciado pelo IDP**:

    ![Informações de logon único em Domínio e URLs do Clear Review](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_url.png)

    a. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<customer name>.clearreview.com/sso/metadata`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<customer>.clearreview.com/sso/acs/`

4. Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:

    ![Informações de logon único em Domínio e URLs do Clear Review](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_url_sp.png)

    Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<customer name>.clearreview.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador e a URL de Resposta reais. Entre em contato com a [equipe de suporte do Clear Review](https://clearreview.com/contact/) para obter valores.

5. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_certificate.png)

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clearreview-tutorial/tutorial_general_400.png)

7. Na seção **Configuração do Clear Review**, clique em **Configurar o Clear Review** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configuração do Clear Review](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_configure.png) 

8. Para configurar o logon único no **Clear Review**, abra o portal **Clear Review** com credenciais de administrador.

9. Selecione **Admin** do painel de navegação esquerdo.

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app_admin1.png)

10. Na parte inferior da página, selecione **Mudar**.

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app_admin2.png)

11. Na página **Configurações de Logon Único**, realize as seguintes etapas

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app_admin3.png)

    a. Na caixa de texto **URL do Emissor**, cole o valor da **ID da Entidade SAML** copiada do portal do Azure.

    b. Na caixa de texto **Ponto de Extremidade SAML**, cole o valor da **URL do Serviço de Logon Único SAML** copiada do portal do Azure.    

    c. Na caixa de texto **Ponto de Extremidade SLO**, cole o valor da **URL do Serviço de Logon Único** copiada do portal do Azure. 

    d. Abra o certificado baixado no Bloco de Notas, copie o conteúdo e cole-o na caixa de texto **Certificado x.509**.   

12. Clique em **Salvar**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-clearreview-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-clearreview-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-clearreview-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-clearreview-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
  
### <a name="create-a-clear-review-test-user"></a>Criar um usuário de teste de Clear Review

Nesta seção, você criará um usuário chamado Britta Simon no Clear Review. Trabalhe com a [equipe de suporte do Clear Review](https://clearreview.com/contact/) para adicionar os usuários na plataforma do Clear Review.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Britta Simon use o logon único do Azure concedendo acesso ao Clear Review.

![Atribuir a função de usuário][200] 

**Para atribuir Britta Simon ao Clear Review, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Clear Review**.

    ![O link do Clear Review na lista de Aplicativos](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Clear Review no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Clear Review.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_203.png

