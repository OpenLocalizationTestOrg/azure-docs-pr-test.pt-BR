---
title: "Tutorial: Integração do Azure Active Directory com o Work.com | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7aa04faab5da9ee7dae977be3a8c040c3aed0b9c
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Tutorial: Integração do Active Directory do Azure com o Work.com

Neste tutorial, você aprenderá a integrar o Work.com ao Azure AD (Azure Active Directory).

A integração do Work.com ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Work.com
- Você pode permitir que os usuários façam logon automaticamente no Work.com (logon único) com as respectivas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Work.com, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do Work.com habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o Work.com da galeria
2. Configurar e testar logon único do Azure AD

## <a name="add-workcom-from-the-gallery"></a>Adicionar o Work.com da galeria
Para configurar a integração do Work.com ao Azure AD, você precisará adicionar o Work.com da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Work.com da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **Work.com**, selecione **Work.com** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Adicionar da galeria](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o Work.com, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Work.com é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Work.com.

No Work.com, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Work.com, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Work.com](#create-a-workcom-test-user)** – para ter um equivalente de Brenda Fernandes no Work.com vinculado à representação do usuário no Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Work.com.

>[!NOTE]
>Para configurar o logon único, você ainda precisa definir um nome de domínio personalizado Work.com. Você precisa definir pelo menos um nome de domínio, testá-lo e implantá-lo em toda a sua organização.

**Para configurar o logon único do Azure AD com o Work.com, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **Work.com**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Logon único baseado em SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. Na seção **Domínio e URLs do Work.com**, siga as etapas a seguir:

    ![Seção Domínio e URLs do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com a URL de Logon real. Contate a [equipe de suporte ao cliente do Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) para obter esse valor. 

4. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do Work.com**, clique em **Configurar o Work.com** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Seção Configuração do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Faça logon no seu locatário Work.com como administrador.

8. Vá para **Configuração**.
   
    ![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")

9. No painel de navegação à esquerda, na seção **Administrador**, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e clique em **Meu Domínio** para abrir a página **Meu Domínio**. 
   
    ![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Meu Domínio")

10. Para confirmar se o domínio foi configurado corretamente, verifique se ele está em “**Etapa 4 Implantado nos Usuários**” e examine “**Minhas Configurações de Domínio**”.
   
    ![Domínio Implantado no Usuário](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domínio Implantado no Usuário")

11. Faça logon no seu locatário Work.com.

12. Vá para **Configuração**.
    
    ![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")

13. Expanda o menu **Controles de Segurança** e clique em **Configurações de Logon Único**.
    
    ![Configurações de Logon Único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configurações de Logon Único")

14. Na página do diálogo **Configurações de Logon Único** , realize as seguintes etapas:
    
    ![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")
    
    a. Selecione **SAML Habilitado**.
    
    b. Clique em **Novo**.

15. Na seção de **Configurações de Logon Único do SAML** , realize as seguintes etapas:
    
    ![Configurações de Logon Único do SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configurações de Logon Único do SAML")
    
    a. Na caixa de texto **Nome** , digite um nome para a sua configuração.  
       
    > [!NOTE]
    > Fornecer um valor para **Nome** popula automaticamente a caixa de texto **Nome da API**.
    
    b. Na caixa de texto **Emissor**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.
    
    c. Para carregar o certificado baixado do Portal do Azure, clique em **Procurar**.
    
    d. Na caixa de texto **ID da Entidade**, digite `https://salesforce-work.com`.
    
    e. Para o **Tipo de Identidade SAML**, selecione **A declaração contém a ID de Federação do objeto de Usuário**.
    
    f. Para **Local de Identidade do SAML**, selecione **A identidade está contida no elemento NameIdentifier da instrução Subject**.
    
    g. Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.

    h. Na caixa de texto **URL de Logoff do Provedor de Identidade**, cole o valor da **URL de Saída** copiado do Portal do Azure.
    
    i. Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.
    
    j. Clique em **Salvar**.

16. No painel de navegação à esquerda, no portal clássico do Work.com, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e clique em **Meu Domínio** para abrir a página **Meu Domínio**. 
    
    ![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Meu Domínio")

17. Na página **Meu Domínio**, na seção **Identidade Visual da Página de Logon**, clique em **Editar**.
    
    ![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic767826.png "Identidade Visual da Página de Logon")

14. Na página **Identidade Visual da Página de Logon**, na seção **Serviço de Autenticação**, o nome das **Configurações de SSO do SAML** é exibido. Selecione-o e, em seguida, clique em **Salvar**.
    
    ![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic784366.png "Identidade Visual da Página de Logon")

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Adicionar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-workcom-test-user"></a>Criar um usuário de teste do Work.com
Para que os usuários do Active Directory do Azure possam entrar, eles devem ser provisionados para Work.com. No caso do Work.com, o provisionamento é uma tarefa manual.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>Para configurar o provisionamento de usuários, execute as seguintes etapas:
1. Faça logon no site da sua empresa do Work.com como um administrador.

2. Vá para **Configuração**.
   
    ![Configuração](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuração")
3. Vá para **Gerenciar Usuários \> Usuários**.
   
    ![Gerenciar Usuários](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gerenciar Usuários")

4. Clique em **Novo Usuário**.
   
    ![Todos os Usuários](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos os Usuários")

5. Na seção Editar Usuários, execute as etapas a seguir nos atributos de uma conta do Azure AD válida que você deseja provisionar nas caixas de texto relacionadas:
   
    ![Editar Usuário](./media/active-directory-saas-work-com-tutorial/ic794118.png "Editar Usuário")
   
    a. Na caixa de texto **Nome**, digite o **nome** do usuário, **Brenda**.
    
    b. Na caixa de texto **Sobrenome**, digite o **sobrenome** do usuário, **Fernandes**.
    
    c. Na caixa de texto **Alias**, digite o **nome** do usuário, **BrendaF**.
    
    d. Na caixa de texto **Email**, digite o **endereço de email** do usuário, **Brittasimon@contoso.com**.
    
    e. Na caixa de texto **Nome de Usuário**, digite um nome de usuário do usuário, assim como **Brittasimon@contoso.com**.
    
    f. Na caixa de texto **Apelido**, digite um **apelido** para o usuário, assim como **Fernandes**.
    
    g. Selecione **Função**, **Licença de Usuário** e **Perfil**.
    
    h. Clique em **Salvar**.  
      
    > [!NOTE]
    > O titular da conta do Azure AD receberá um email com um link de confirmação de conta para que ela se torne ativa.
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Work.com.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Work.com, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Work.com**.

    ![Work.com na lista do aplicativo](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Work.com no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Work.com.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

