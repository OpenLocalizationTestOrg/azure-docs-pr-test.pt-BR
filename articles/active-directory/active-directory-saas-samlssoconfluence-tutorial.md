---
title: "Tutorial: Integração do Azure Active Directory com o SSO do SAML para Confluence da Resolution GmbH | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e SSO do SAML para Confluence da Resolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Tutorial: Integração do Azure Active Directory com o SSO do SAML para Confluence da Resolution GmbH

Neste tutorial, você aprenderá a integrar o SSO do SAML para Confluence da Resolution GmbH com o Azure AD (Azure Active Directory).

A integração de SSO do SAML para Confluence da Resolution GmbH com o Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao SSO do SAML para Confluence da Resolution GmbH
- Você pode habilitar os usuários a entrarem automaticamente no SSO do SAML para Confluence da Resolution GmbH (logon único) com as próprias contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o SSO de SAML para Confluence da Resolution GmbH, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SSO do SAML para Confluence da Resolution GmbH

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o SSO do SAML para Confluence da Resolution GmbH da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a>Adicionando o SSO do SAML para Confluence da Resolution GmbH da galeria

Para configurar a integração do SSO do SAML para Confluence da Resolution GmbH no Azure AD, adicione o SSO do SAML para Confluence da Resolution GmbH da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar SSO do SAML para Confluence da Resolution GmbH da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![Aplicativos][3]

4. Na caixa de pesquisa, digite **SSO do SAML para Confluence da Resolution GmbH**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. No painel resultados, selecione **SSO do SAML para Confluence da Resolution GmbH** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure

Nesta seção, você configura e testa o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH com base em um usuário de teste chamado "Brenda Fernandes".

Para o logon único funcionar, o Azure AD precisa saber que o usuário da contraparte no SSO do SAML para Confluence da Resolution GmbH é para um usuário no Azure AD. Em outras palavras, uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SSO do SAML para Confluence da Resolution GmbH precisa ser estabelecida.

No SSO do SAML para Confluence da Resolution GmbH, atribua o valor de **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH, conclua os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criar um usuário de teste de SSO do SAML para Confluence da Resolution GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  – para ter um equivalente de Brenda Fernandes no SSO do SAML para Confluence da Resolution GmbH vinculado à representação do usuário do Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo SSO do SAML para Confluence da Resolution GmbH.

**Para configurar o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativo **SSO do SAML para Confluence da Resolution GmbH**, clique em **Logon único**.

    ![Configurar Logon Único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. Na seção **Domínio e URLs do SSO do SAML para Confluence da Resolution GmbH**, se quiser configurar o aplicativo no modo iniciado **IDP**:

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`

4. Marque **Mostrar configurações de URL avançadas**. Se quiser configurar o aplicativo no modo iniciado em **SP**:

    ![Configurar o logon único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada. Entre em contato com a [equipe de suporte ao Cliente do SSO do SAML para Confluence da Resolution GmbH](https://www.resolution.de/go/support) para obter esses valores. 

5. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![Configurar o logon único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. Em uma janela diferente do navegador da Web, faça logon no **portal do administrador do SSO do SAML para Confluence da Resolution GmbH** como administrador.

8. Passe o cursor do mouse sobre a engrenagem e clique em **Complementos**.
    
    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Você é redirecionado à página de Acesso de Administrador. Insira a Senha e clique no botão **Confirmar**.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. Na guia **ATLASSIAN MARKETPLACE**, clique em **Localizar novos complementos**. 

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Pesquise **SSO (Logon Único) do SAML para Confluence** e clique no botão **Instalar** para instalar o novo plug-in do SAML.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. A instalação do plug-in será iniciada. Clique em **fechar**

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Clique em **Gerenciar**.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Clique em **Configurar** para configurar o novo plug-in.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Este novo plug-in também pode ser encontrado na guia **USUÁRIOS E SEGURANÇA**.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. Em **Configuração de Plug-in de Logon Único do SAML**, clique no botão **Adicionar Provedor de Identidade adicional** para definir as configurações do Provedor de Identidade.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. Execute as seguintes etapas nesta página:

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    a. Adicionar **Nome** do Provedor de Identidade (por exemplo, Azure AD).
    
    b. Adicionar **Descrição** do Provedor de Identidade (por exemplo, Azure AD).

    c. Clique em **XML** e selecione o arquivo **Metadados** que você baixou do portal do Azure.

    d. Clique no botão **Carregar**.

    e. Ele lê os metadados IdP e preenche os campos conforme destacado na captura de tela. 
18. Clique no botão **Salvar Configurações** para salvar as configurações.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Criando um usuário de teste do SSO do SAML para Confluence da Resolution GmbH

Para habilitar usuários do Azure AD a fazerem logon no SSO do SAML para Confluence da Resolution GmbH, eles devem ser provisionados no SSO do SAML para Confluence da Resolution GmbH.  
No SSO do SAML para Confluence da Resolution GmbH, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon no site da empresa do SAML SSO para Confluence da Resolution GmbH como administrador.

2. Passe o cursor do mouse sobre a engrenagem e clique em **Gerenciamento de usuário**.

    ![Adicionar Funcionário](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. Na seção usuários, clique na guia **Adicionar usuários**. Na página do diálogo **“Adicionar um usuário”**, realize as seguintes etapas:

    ![Adicionar Funcionário](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. Na caixa de texto **Nome de usuário**, digite o email do usuário, como Brenda Fernandes.

    b. Na caixa de texto **Nome completo**, digite o nome completo do usuário, como Brenda Fernandes.

    c. Na caixa de texto **Email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.

    d. Na caixa de texto **Senha**, digite a senha de Brenda Fernandes.

    e. Clique em **Confirmar Senha** e redigite a senha.
    
    f. Clique no botão **Adicionar**.    

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, habilite Brenda Fernandes a usar o logon único do Azure concedendo acesso ao SSO do SAML para Confluence da Resolution GmbH.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao SSO do SAML para Confluence da Resolution GmbH, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **SSO do SAML para Confluence da Resolution GmbH**.

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco SSO do SAML para Confluence da Resolution GmbH no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo SSO do SAML para Confluence da Resolution GmbH.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

