---
title: "Tutorial: Integração do Azure Active Directory com o Soonr Workplace | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Soonr no local de trabalho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Tutorial: Integração do Active Directory do Azure com o Soonr Workplace

Olá objetivo deste tutorial é tooshow você como toointegrate Soonr no local de trabalho com o Azure Active Directory (AD do Azure).  
Integrando Soonr no local de trabalho com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSoonr no local de trabalho
- Você pode habilitar seu usuários tooautomatically get conectado tooSoonr no local de trabalho (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Soonr no local de trabalho, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Soonr Workplace com logon único habilitado


> [!NOTE] 
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.  
cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Soonr no local de trabalho na Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Adicionando Soonr no local de trabalho na Galeria de saudação
integração de saudação tooconfigure do local de trabalho Soonr no AD do Azure, você precisa tooadd Soonr no local de trabalho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Soonr no local de trabalho na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 

    ![Active Directory][1]

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.

    ![Aplicativos][2]

4. Clique em **adicionar** final Olá Olá página.

    ![Aplicativos][3]

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
 
    ![Aplicativos][4]

6. Na caixa de pesquisa hello, digite **Soonr trabalho**.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. No painel de resultados de saudação, selecione **Soonr trabalho**e, em seguida, clique em **concluir** aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com Soonr de espaço de trabalho com base em um usuário de teste chamado "Britta Simon".

Para toowork de logon único, o AD do Azure precisa tooknow é que usuário de contraparte Olá no usuário do local de trabalho Soonr tooan no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho Soonr precisa toobe estabelecida.  

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na área de trabalho Soonr.

tooconfigure e teste de logon único do AD do Azure com Soonr de espaço de trabalho, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do local de trabalho Soonr](#creating-a-soonr-workplace-test-user)**  -toohave um equivalente do Britta Simon na área de trabalho Soonr que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único em seu aplicativo de área de trabalho Soonr.


**tooconfigure AD do Azure-logon único com o local de trabalho Soonr execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em hello **Soonr trabalho** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.

    ![Configurar Logon Único][6] 

2. Em Olá **como você gostaria toosign usuários no local de trabalho do tooSoonr** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:.

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Clique em **Avançar**.

    > [!NOTE] 
    > Observe que isso não é um valor real hello. Você tem tooupdate esse valor com hello real URL de logon. Entre em contato com tooget de equipe de suporte local de trabalho Soonr esse valor.

4. Em Olá **configurar logon único no local de trabalho Soonr** , clique em **baixar metadados** e, em seguida, salve o arquivo de saudação em seu computador:

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget SSO configurado para o seu aplicativo, entre em contato com sua equipe de suporte local de trabalho Soonr e fornecê-los com os seguintes hello: 

    • Olá baixado **metadados** arquivo

    • Olá **URL do emissor**

    • Olá **URL SSO SAML**

    • Olá **URL do serviço de logon único**

    >[!NOTE]
    >Este aplicativo é substituído por <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask trabalho</a> e você pode consultar <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">isso</a> tutorial para configurar o aplicativo hello com o Azure AD.
   
6. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.

    ![Logon Único do AD do Azure][10]

7. Em Olá **único logon confirmação** , clique em **concluir**.  
  
    ![Logon Único do AD do Azure][11]



### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.  

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Em Tipo de Usuário, selecione Novo usuário na organização.

    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.

    c. Clique em **Avançar**.

6.  Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. Em Olá **nome** caixa de texto, tipo **Britta**.  

    b. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.

    c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.

    d. Em Olá **função** lista, selecione **usuário**.

    e. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Anote o valor Olá Olá **nova senha**.

    b. Clique em **Concluído**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Criar um usuário de teste do Soonr Workplace

Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon na área de trabalho Soonr. Trabalhe com toocreate de equipe de suporte local de trabalho Soonr um usuário na plataforma de saudação. Você pode gerar um tíquete de suporte de saudação com Soonr de <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">aqui</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooSoonr seu acesso no local de trabalho.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSoonr no local de trabalho, execute Olá etapas a seguir:**

1. No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Soonr trabalho**.

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. No menu de saudação na parte superior de saudação, clique em **usuários**.

    ![Atribuir usuário][203] 

1. Na lista de usuários hello, selecione **Britta Simon**.

2. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.

    ![Atribuir usuário][205]



### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.  
Quando você clica em Olá Soonr no local de trabalho lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de área de trabalho Soonr.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
