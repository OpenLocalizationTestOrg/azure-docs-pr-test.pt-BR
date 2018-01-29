---
title: "Tutorial: Integração do Azure Active Directory ao Apptio | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Apptio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: b23eba91-7698-47e7-ae75-0ceafd739965
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/6/2017
ms.author: jeedes
ms.openlocfilehash: 2948b3df7e2258b6d842f9d9d5f632e531929676
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-apptio"></a>Tutorial: Integração do Azure Active Directory ao Apptio

Neste tutorial, você aprende a integrar o Apptio ao Azure AD (Azure Active Directory).

A integração do Apptio ao Azure AD oferece os seguintes benefícios:

- No Azure AD, você pode controlar quem tem acesso ao Apptio.
- Você pode permitir que os usuários se conectem automaticamente ao Apptio (Logon Único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Apptio, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Apptio

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Apptio por meio da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-apptio-from-the-gallery"></a>Adicionando o Apptio por meio da galeria
Para configurar a integração do Apptio ao Azure AD, você precisa adicionar o Apptio à lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Apptio por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **Apptio**, selecione **Apptio** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Apptio na lista de resultados](./media/active-directory-saas-apptio-tutorial/tutorial_apptio_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Apptio, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Apptio é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Apptio.

No Apptio, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Apptio, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Apptio](#create-an-apptio-test-user)** – para ter um equivalente de Brenda Fernandes no Apptio que está vinculado à representação de usuário do Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Apptio.

**Para configurar o logon único do Azure AD com o Apptio, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Apptio**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-apptio-tutorial/tutorial_apptio_samlbase.png)

3. Na seção **Domínio e URLs do Apptio**, execute as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo IDP:

    ![Informações de logon único em Domínio e URLs do Apptio](./media/active-directory-saas-apptio-tutorial/tutorial_apptio_url.png)

    Na caixa de texto **Identificador**, digite o valor: `urn:federation:apptio`

4. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/active-directory-saas-apptio-tutorial/tutorial_apptio_certificate.png) 

5. O aplicativo Apptio Software espera que as declarações SAML estejam em um formato específico. Configure as seguintes declarações para o aplicativo. Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo. Observe que o **Identificador de Usuário** é mapeado com **user.mail**. Há outros três atributos – **fullname, mail e role**, que precisam ser configurados. A captura de tela a seguir mostra um exemplo disso.

    ![Configurar Logon Único](./media/active-directory-saas-apptio-tutorial/tutorial_apptio_attributes.png)       
    
    > [!NOTE]
    > Clique [aqui](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) para saber como configurar a **Função** no Azure AD
    
6. Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:

    | Nome do atributo | Valor do atributo |
    | -------------- | -------------------- |    
    | fullname       | user.displayname |
    | mail           | user.mail |
    | função           | user.assignedrole |
    
    a. Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.

    ![Configurar o logon único](./media/active-directory-saas-apptio-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-apptio-tutorial/tutorial_attribute_05.png)

    b. Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.

    c. Na lista **Valor**, digite o valor do atributo mostrado para essa linha.
    
    d. Clique em **OK**.

8. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-apptio-tutorial/tutorial_general_400.png)
    
9. Para configurar o logon único no lado do **Apptio**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Apptio](https://www.apptio.com/about/contact). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-apptio-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-apptio-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-apptio-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-apptio-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-an-apptio-test-user"></a>Criar um usuário de teste do Apptio

Nesta seção, você cria um usuário chamado Brenda Fernandes no Apptio. Trabalhe com a [equipe de suporte do Apptio](https://www.apptio.com/about/contact) para adicionar os usuários à plataforma Apptio. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Apptio.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Apptio, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Apptio**.

    ![O link do Apptio na lista de Aplicativos](./media/active-directory-saas-apptio-tutorial/tutorial_apptio_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Apptio no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Apptio.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-apptio-tutorial/tutorial_general_203.png

