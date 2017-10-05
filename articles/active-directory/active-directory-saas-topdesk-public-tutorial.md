---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Público | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o TOPdesk – Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Tutorial: integração do Azure Active Directory com o TOPdesk – Public

Neste tutorial, você aprenderá a integrar o TOPdesk – Public ao Azure AD (Azure Active Directory).

A integração do TOPdesk – Public ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao TOPdesk – Public.
- Você pode permitir que os usuários façam logon automaticamente no TOPdesk – Public (logon único) com as respectivas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao TOPdesk – Public, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do TOPdesk – Public habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o TOPdesk – Public da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-topdesk---public-from-the-gallery"></a>Adicionar o TOPdesk – Public da galeria
Para configurar a integração do TOPdesk – Public ao Azure AD, é necessário adicionar o TOPdesk – Public da galeria à lista de aplicativos SaaS gerenciados.

**Para adicionar o TOPdesk – Public da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **TOPdesk – Public**, selecione **TOPdesk – Public** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![TOPdesk – Public na lista de resultados](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o TOPdesk – Public, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do TOPdesk – Public é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no TOPdesk – Public.

No TOPdesk – Public, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o TOPdesk – Public, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do TOPdesk – Public](#create-a-topdesk---public-test-user)** – para ter um equivalente de Brenda Fernandes no TOPdesk – Public vinculado à representação do usuário no Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo TOPdesk – Public.

**Para configurar o logon único do Azure AD com o TOPdesk – Public, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **TOPdesk – Public**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. Na seção **Domínio e URLs do TOPdesk – Public**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.topdesk.net`
    
    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.topdesk.net/tas/public/login/verify`

    c. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada. A URL de resposta é explicada posteriormente no tutorial. Contate a [equipe de suporte ao cliente do TOPdesk – Public](https://help.topdesk.com/saas/enterprise/user/) para obter esses valores.  

4. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. Na seção **Configuração do TOPdesk – Public**, clique em **Configurar o TOPdesk – Public** para abrir a janela **Configurar o logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configuração do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Faça logon em seu site de empresa do **TOPdesk - Public** como administrador.

8. No menu **TOPdesk**, clique em **Configurações**.
   
    ![Configurações](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configurações")

9. Clique em **Configurações de Logon**.
   
    ![Configurações de logon](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configurações de logon")

10. Expanda o menu **Configurações de Logon** e clique em **Geral**.
   
    ![Geral](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Geral")

11. Na seção **Público** da seção de configuração de **Logon do SAML**, realize as seguintes etapas:
   
    ![Configurações técnicas](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configurações técnicas")
   
    a. Clique em **Baixar** para baixar o arquivo de metadados públicos e salve-o localmente no computador.
   
    b. Abra o arquivo de metadados baixado e localize o nó **AssertionConsumerService**.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Copie o valor **AssertionConsumerService**, cole-o na caixa de texto **URL de resposta** na seção **Domínio e URLs do TOPdesk – Public**.      
   
12. Execute as seguintes etapas para criar um arquivo de certificado:
    
    ![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")
    
    a. Abra o arquivo de metadados baixado do Portal do Azure.
    
    b. Expanda o nó **RoleDescriptor** que contém um **xsi:type** de **fed:ApplicationServiceType**.
    
    c. Copie o valor do nó **X509Certificate** .
    
    d. Salve o valor copiado de **X509Certificate** localmente no computador em um arquivo.

13. Na seção **Público**, clique em **Adicionar**.
    
    ![Logon SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "logon SAML")

14. Na página do diálogo **Assistente de configuração do SAML** , realize as seguintes etapas:
    
    ![Assistente de configuração SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistente de configuração SAML")
    
    a. Para carregar o arquivo de metadados baixado do Portal do Azure, em **Metadados de Federação**, clique em **Procurar**.

    b. Para carregar o arquivo de certificado, em **Certificado (RSA)**, clique em **Procurar**.

    c. Para carregar o arquivo de logotipo que você recebeu da equipe de suporte do TOPdesk, em **Ícone do logotipo**, clique em **Procurar**.

    d. Na caixa de texto **Atributo de nome de usuário**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. Na caixa de texto **Nome de exibição** , digite um nome para a sua configuração.

    f. Clique em **Salvar**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-topdesk---public-test-user"></a>Criar um usuário de teste do TOPdesk – Public

Para permitir que os usuários do AD do Azure façam logon no TOPdesk - Público, eles deverão ser provisionados no TOPdesk - Público.  
No caso do TOPdesk - Público, o provisionamento é uma tarefa manual.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>Para configurar o provisionamento de usuários, execute as seguintes etapas:
1. Faça logon em seu site de empresa do **TOPdesk - Public** como administrador.

2. No menu na parte superior, clique em **TOPdesk \> Novo \> Arquivos de Suporte \> Pessoa**.
   
    ![Pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Pessoa")

3. Na caixa de diálogo Nova Pessoa, execute as seguintes etapas:
   
    ![Nova pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nova pessoa")
   
    a. Clique na guia Geral.

    b. Na caixa de texto **Sobrenome**, digite o sobrenome do usuário, tal como Fernandes
 
    c. Selecione um **Site** para a conta.
 
    d. Clique em **Salvar**.

> [!NOTE]
> É possível usar qualquer outra ferramenta de criação da conta de usuário do TOPdesk – Público ou APIs fornecidas pelo TOPdesk – Público para provisionar as contas de usuário do Azure AD.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao TOPdesk – Public.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao TOPdesk – Public, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **TOPdesk – Public**.

    ![O link do TOPdesk – Public na lista de Aplicativos](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco TOPdesk – Public no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo TOPdesk – Public.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

