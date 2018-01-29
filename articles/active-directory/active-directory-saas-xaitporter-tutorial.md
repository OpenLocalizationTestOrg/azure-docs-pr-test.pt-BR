---
title: "Tutorial: integração do Azure Active Directory ao XaitPorter | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory do Azure e o XaitPorter."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d33c7cb7-0550-425b-882a-619a713a71b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/28/2017
ms.author: jeedes
ms.openlocfilehash: 2012d990f7cdcb8c12da5f16db518b261b06a5b7
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xaitporter"></a>Tutorial: integração do Azure Active Directory ao XaitPorter

Neste tutorial, você aprenderá a integrar o XaitPorter ao Azure AD (Azure Active Directory).

A integração do XaitPorter ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao XaitPorter.
- Você pode permitir que os usuários façam logon automaticamente no XaitPorter (Logon Único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao XaitPorter, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do XaitPorter

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando XaitPorter da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-xaitporter-from-the-gallery"></a>Adicionando XaitPorter da galeria
Para configurar a integração do XaitPorter ao Azure AD, você precisará adicionar o XaitPorter da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o XaitPorter da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **XaitPorter**, selecione **XaitPorter** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![XaitPorter na lista de resultados](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o XaitPorter com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do XaitPorter é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no XaitPorter.

No XaitPorter, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o XaitPorter, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do XaitPorter](#create-a-xaitporter-test-user)** – para ter um equivalente de Brenda Fernandes no XaitPorter que esteja vinculado à representação de usuário do Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo XaitPorter.

**Para configurar o logon único do Azure AD com o XaitPorter, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **XaitPorter**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_samlbase.png)

3. Na seção **Domínio e URLs do XaitPorter**, realize as seguintes etapas:

    ![Informações de logon único em de URLs e Domínio do XaitPorter](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.xaitporter.com/saml/login`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.xaitporter.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte ao cliente do XaitPorter](https://www.xait.com/support/) para obter esses valores. 

4. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/tutorial_general_400.png)

5. Para gerar a URL de **Metadados**, execute as seguintes etapas:

    a. Clique em **Registros do aplicativo**.
    
    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_appregistrations.png)
   
    b. Clique em **Pontos de extremidade** para abrir a caixa de diálogo **Pontos de extremidade**.  
    
    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_endpointicon.png)

    c. Clique no botão copiar para copiar a URL **DOCUMENTO DE METADADOS DE FEDERAÇÃO** e cole-a no bloco de notas.
    
    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_endpoint.png)
     
    d. Agora acesse a página de propriedades do **XaitPorter** e copie a **ID do Aplicativo** usando o botão **Copiar** e cole-a no bloco de notas.
 
    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_appid.png)

    e. Gere a **URL de Metadados** usando o padrão a seguir: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

6. Forneça o **endereço IP** ou a **URL de metadados** para a [equipe de suporte SmartRecruiters](https://www.smartrecruiters.com/about-us/contact-us/), de modo que XaitPorter possa garantir que o endereço IP esteja acessível da sua instância XaitPorter configurando a lista de permissões em seu lado. 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do XaitPorter como um administrador.

8. Clique em **Admin**.

    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/user1.png)

9. Selecione **Gerenciar Logon Único** na lista suspensa **Configuração do Sistema**.

    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/user2.png)

10. Na seção **GERENCIAR LOGON ÚNICO**, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-xaitporter-tutorial/user3.png)

    a. Selecione **Habilitar Autenticação de Logon Único**.

    b. Na caixa de texto **Configurações do Provedor de Identidade**, cole a **URL de Metadados** copiada do Azure e clique em **Buscar**.

    c. Selecione **Habilitar Criação Automática de Usuários**.

    d. Clique em **OK**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-xaitporter-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-xaitporter-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-xaitporter-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-xaitporter-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-xaitporter-test-user"></a>Criar um usuário de teste do XaitPorter

Nesta seção, você criará um usuário chamado Brenda Fernandes no XaitPorter. Trabalhe com a [equipe de suporte ao cliente do XaitPorter](https://www.xait.com/support/) para adicionar usuários na plataforma do XaitPorter. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao XaitPorter.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao XaitPorter, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, escolha **XaitPorter**.

    ![O link do XaitPorter na lista de Aplicativos](./media/active-directory-saas-xaitporter-tutorial/tutorial_xaitporter_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do XaitPorter no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do XaitPorter.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xaitporter-tutorial/tutorial_general_203.png

