---
title: "Tutorial: integração do Azure Active Directory com o Treinamento de Reconhecimento de Segurança do KnowBe4 | Microsoft Docs"
description: "Aprenda como configurar o logon único entre o Azure Active Directory e o Treinamento de Reconhecimento de Segurança do KnowBe4."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/31/2017
ms.author: jeedes
ms.openlocfilehash: 8153c0824de2cda61fecf1da822c1ffa70d8f0d0
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a>Tutorial: integração do Azure Active Directory com o Treinamento de Reconhecimento de Segurança do KnowBe4

Neste tutorial, você aprenderá a integrar o Treinamento de Reconhecimento de Segurança do KnowBe4 ao Azure AD (Azure Active Directory).

A integração do Treinamento de Reconhecimento de Segurança do KnowBe4 ao Azure AD proporciona os seguintes benefícios:

- No Azure AD, você pode controlar quem tem acesso ao Treinamento de Reconhecimento de Segurança do KnowBe4.
- Você pode permitir que seus usuários façam logon automaticamente no Treinamento de Reconhecimento de Segurança do KnowBe4 (Logon Único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Treinamento de Reconhecimento de Segurança do KnowBe4, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada de logon único do Treinamento de Reconhecimento de Segurança do KnowBe4

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Como adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a>Como adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria
Para configurar a integração do Treinamento de Reconhecimento de Segurança do KnowBe4 ao Azure AD, você precisará adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 da galeria à sua lista de aplicativos de SaaS gerenciados.

**Para adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **Treinamento de Reconhecimento de Segurança do KnowBe4**, selecione **Treinamento de Reconhecimento de Segurança do KnowBe4** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Treinamento de Reconhecimento de Segurança do KnowBe4 na lista de resultados](./media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Treinamento de Reconhecimento de Segurança do KnowBe4 com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Treinamento de Reconhecimento de Segurança do KnowBe4 é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Treinamento de Reconhecimento de Segurança do KnowBe4.

No Treinamento de Reconhecimento de Segurança do KnowBe4, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Treinamento de Reconhecimento de Segurança do KnowBe4, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Treinamento de Reconhecimento de Segurança do KnowBe4](#create-a-knowbe4-security-awareness-training-test-user)** – para ter um equivalente de Brenda Fernandes no Treinamento de Reconhecimento de Segurança do KnowBe4 vinculado à representação do usuário no Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Treinamento de Reconhecimento de Segurança do KnowBe4.

**Para configurar o logon único do Azure AD com o Treinamento de Reconhecimento de Segurança do KnowBe4, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **Treinamento de Reconhecimento de Segurança do KnowBe4**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_samlbase.png)

3. Na seção **URLs e Domínio do Treinamento de Reconhecimento de Segurança do KnowBe4**, execute as seguintes etapas:

    ![Domínio de Treinamento de Reconhecimento de Segurança do KnowBe4 e informações de logon único das URLs](./media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`

    > [!NOTE] 
    > O valor da URL de logon não é real. Atualize esse valor com a URL de Logon real. Entre em contato com a [equipe de suporte do Cliente de Treinamento de Reconhecimento de Segurança do KnowBe4](mailto:support@KnowBe4.com) para obter esse valor. 

    b. Na caixa de texto **Identificador**, digite o valor da cadeia de caracteres: `KnowBe4`

    > [!NOTE]
    >Diferencia maiúsculas de minúsculas

4. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-knowbe4-tutorial/tutorial_general_400.png)

6. Na seção **Configuração do Treinamento de Reconhecimento de Segurança do KnowBe4**, clique em **Configurar Treinamento de Reconhecimento de Segurança do KnowBe4** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configuração do Treinamento de Reconhecimento de Segurança do KnowBe4](./media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_configure.png) 

7. Para configurar o logon único no lado do **Treinamento de Reconhecimento de Segurança do KnowBe4**, é necessário enviar o **Certificado (Bruto)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Cliente do Treinamento de Reconhecimento de Segurança do KnowBe4](mailto:support@KnowBe4.com).

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-knowbe4-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-knowbe4-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-knowbe4-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-knowbe4-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-knowbe4-security-awareness-training-test-user"></a>Criar um usuário de teste do Treinamento de Reconhecimento de Segurança do KnowBe4

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Treinamento de Reconhecimento de Segurança do KnowBe4. O Treinamento de Reconhecimento de Segurança do KnowBe4 dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Um novo usuário será criado durante uma tentativa de acesso ao Treinamento de Reconhecimento de Segurança do KnowBe4, caso ele ainda não exista. 

>[!NOTE]
>Se precisar criar um usuário manualmente, entre em contato com a equipe de suporte do [Treinamento de Reconhecimento de Segurança do KnowBe4](mailto:support@KnowBe4.com).

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, ao conceder acesso ao Treinamento de Reconhecimento de Segurança do KnowBe4.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, selecione **Treinamento de Reconhecimento de Segurança do KnowBe4**.

    ![Link Treinamento de Reconhecimento de Segurança do KnowBe4 na lista Aplicativos](./media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.
  
Ao clicar no bloco Treinamento de Reconhecimento de Segurança do KnowBe4 no Painel de Acesso, você deverá fazer logon automaticamente no seu aplicativo Treinamento de Reconhecimento de Segurança do KnowBe4. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_203.png

