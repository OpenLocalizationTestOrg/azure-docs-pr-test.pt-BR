---
title: "Tutorial: Integração do Azure Active Directory ao Boomi | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 40d034ff-7394-4713-923d-1f8f2ed8bf36
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/03/2018
ms.author: jeedes
ms.openlocfilehash: 6d1af05f40d6e57b2f6128261828791be7e516c7
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Tutorial: Integração do Active Directory do Azure ao Boomi

Neste tutorial, você aprenderá a integrar o Boomi ao Azure AD (Azure Active Directory).

A integração do Boomi ao Azure AD oferece os seguintes benefícios:

- No Azure AD você pode controlar quem tem acesso ao Boomi.
- Você pode permitir que seus usuários façam logon automaticamente no Boomi (Logon único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Boomi, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Boomi

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar Boomi da galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-boomi-from-the-gallery"></a>Adicionar Boomi da galeria
Para configurar a integração do Boomi ao Azure AD, você precisa adicionar o Boomi por meio da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Boomi da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **Boomi**, selecione **Boomi** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Boomi na lista de resultados](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Boomi, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Boomi é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Boomi.

No Boomi, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Boomi, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar de um usuário de teste do Boomi](#create-a-boomi-test-user)** – para ter um equivalente de Brenda Fernandes no Boomi que esteja vinculado à representação de usuário no Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Boomi.

**Para configurar o logon único do Azure AD com o Boomi, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Boomi**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. Na seção **URLs e Domínio do Boomi**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Boomi](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. Na caixa de texto **Identificador**, digite uma URL: `https://platform.boomi.com/`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://platform.boomi.com/sso/<boomi-tenant>/saml`

    > [!NOTE] 
    > O valor de URL de Resposta não é real. Atualize o valor com a URL de Resposta real. Para obter o valor, entre em contato com a [equipe de suporte do Boomi](https://boomi.com/company/contact/).
 
4. O aplicativo Boomi espera que as declarações SAML estejam em um formato específico. Configure as seguintes declarações para o aplicativo. Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo. A captura de tela a seguir mostra um exemplo disso.
    
    ![Configurar o logon único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, para cada linha mostrada na tabela a seguir, execute as seguintes etapas:

    | Nome do atributo | Valor do atributo |
    | -------------- | --------------- |
    | FEDERATION_ID | user.mail |
    
    a. Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.
    
    ![Configurar o logon único](./media/active-directory-saas-boomi-tutorial/tutorial_officespace_04.png)
    
    ![Configurar o logon único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.
    
    c. Na lista **Valor**, digite o valor do atributo mostrado para essa linha.
    
    d. Clique em **OK**.

6. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![O link de download do Certificado](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png) 

7. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

8. Na seção **Configuração do Boomi**, clique em **Configurar o Boomi** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configuração do Boomi](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

9. Em outra janela do navegador da Web, faça logon em seu site de empresa Boomi como um administrador. 

10. Navegue até **Nome da Empresa** e vá para **Configurar**.

11. Clique na guia **Opções de SSO** e execute etapas a seguir.

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Marque a caixa de seleção **Habilitar Logon Único do SAML**.

    b. Clique em **Importar** para carregar o certificado baixado do Azure AD no **Certificado do Provedor de Identidade**.
    
    c. Na caixa de texto **URL de Logon do Provedor de Identidade**, insira o valor da **URL de Serviço de Logon Único SAML** da janela de configuração de aplicativo do Azure AD.

    d. Para **Local do ID de Federação**, selecione o botão de opção **A Id de Federação está contida no elemento Atributo FEDERATION_ID**. 

    e. Clique no botão **Salvar** .

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
  
### <a name="create-a-boomi-test-user"></a>Criar um usuário de teste do Boomi

Para permitir que os usuários do Azure AD façam logon no Boomi, eles deverão ser provisionados no Boomi. No caso do Boomi, o provisionamento é uma tarefa manual.

### <a name="to-provision-a-user-account-perform-the-following-steps"></a>Para provisionar uma conta de usuário, execute as seguintes etapas:

1. Faça logon em seu site de empresa Boomi como um administrador.

2. Depois de fazer logon, navegue até **Gerenciamento de Usuário** e vá até **Usuários**.

    ![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuários")

3. Clique no ícone **+** e o diálogo **Adicionar/Manter Funções de Usuário** será aberto.

    ![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuários")

    ![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuários")

    a. Na caixa de texto **Endereço de email do usuário**, digite o email do usuário, como BrittaSimon@contoso.com.
    
    b. Na caixa de texto **Nome**, digite o Nome do usuário como Brenda.

    c. Na caixa de texto **Sobrenome**, digite o Sobrenome do usuário como Fernandes.
    
    d. Insira a **ID de Federação** do usuário. Cada usuário deve ter uma ID de Federação que o identifique exclusivamente na conta.
    
    e. Atribua a função **Usuário Padrão** ao usuário. Não atribua a função Administrador, pois isso daria acesso normal ao Atmosphere, bem como acesso de logon único.
    
    f. Clique em **OK**.
    
    > [!NOTE]
    > O usuário não receberá um email de notificação de boas-vindas contendo uma senha que pode ser usada para fazer logon na conta do AtomSphere, pois sua senha é gerenciada por meio do provedor de identidade. É possível usar qualquer outra ferramenta de criação da conta de usuário do Boomi ou as APIs fornecidas pelo Boomi para provisionar as contas de usuário do AAD.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Boomi.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Boomi, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, escolha **Boomi**.

    ![Link do Boomi na lista de Aplicativos](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Boomi no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Boomi.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

