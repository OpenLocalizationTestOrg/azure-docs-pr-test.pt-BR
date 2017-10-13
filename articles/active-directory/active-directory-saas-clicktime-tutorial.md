---
title: "Tutorial: integração do Azure Active Directory com o ClickTime | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Tutorial: integração do Active Directory do Azure ao ClickTime

Neste tutorial, você aprenderá a integrar o ClickTime ao Azure AD (Azure Active Directory).

A integração do ClickTime ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao ClickTime
- É possível permitir que seus usuários façam logon automaticamente no ClickTime (logon único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o ClickTime, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura do ClickTime habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando ClickTime da galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-clicktime-from-the-gallery"></a>Adicionando ClickTime da galeria
Para configurar a integração do ClickTime com o Azure AD, você precisará adicionar o ClickTime à sua lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o ClickTime por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **ClickTime**, selecione **ClickTime** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![ClickTime na lista de resultados](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o ClickTime, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do ClickTime é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ClickTime.

No ClickTime, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o ClickTime, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do ClickTime](#create-a-clicktime-test-user)** – para ter um equivalente de Brenda Fernandes no ClickTime que esteja vinculado à representação do usuário no Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo ClickTime.

**Para configurar o logon único do Azure AD com o ClickTime, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração do aplicativo **ClickTime**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. Na seção **Domínio e URLs do ClickTime**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    a. Na caixa de texto **Identificador**, digite uma URL como: `https://app.clicktime.com/sp/`
    
    b. Na caixa de texto **URL de Resposta** , digite uma URL nos seguintes padrões: 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![O link de download do Certificado](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do ClickTime**, clique em **Configurar o ClickTime** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configuração do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do ClickTime como administrador.

8. Na barra de ferramentas na parte superior, clique em **Preferências** e em **Configurações de Segurança**.

9. Na seção de configuração de **Preferências de Logon Único** , realize as seguintes etapas:
   
    ![Configurações de segurança](./media/active-directory-saas-clicktime-tutorial/tic777280.png "as configurações de segurança")
   
    a.  Selecione **Permitir** a entrada usando o SSO (Logon Único) com **Azure AD**.
   
    b. Na caixa de texto **Ponto de Extremidade de Provedor de Identidade**, cole a **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.
   
    c.  Abra o **certificado codificado em Base 64** baixado no Portal do Azure no **Bloco de notas**, copie o conteúdo e cole-o na caixa de texto **Certificado X.509**.
   
    d.  Clique em **Salvar**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.
 
    ![O botão Adicionar](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-clicktime-test-user"></a>Criar um usuário de teste do ClickTime

Para permitir que os usuários do Azure AD façam logon no ClickTime, eles devem ser provisionados no ClickTime.  
No caso do ClickTime, o provisionamento é uma tarefa manual.

> [!NOTE]
> É possível usar qualquer outra ferramenta de criação da conta de usuário do ClickTime ou as APIs fornecidas pelo ClickTime para provisionar as contas de usuário do Azure AD.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**
1. Faça logon em seu locatário do **ClickTime** .
2. Na barra de ferramentas na parte superior, clique na **Empresa** e em **Pessoas**.
   
    ![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Pessoas")
3. Clique em **Adicionar Pessoa**.
   
    ![Adicionar pessoa](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Adicionar pessoa")
4. Na seção Nova Pessoa, execute as etapas a seguir:
   
    ![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Pessoas")
   
    a.  Na caixa de texto **nome completo**, digite o nome completo do usuário, por exemplo, **Brenda Fernandes**. 
  
    b.  Na caixa de texto **endereço de email**, digite o endereço de email do usuário, por exemplo, **brittasimon@contoso.com**.
       
    > [!NOTE]
    > Se quiser, defina propriedades adicionais do novo objeto pessoa.
   
    c.  Clique em **Salvar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao ClickTime.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao ClickTime, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **ClickTime**.

    ![O link do ClickTimne na lista de Aplicativos](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do ClickTime no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo do ClickTime.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

