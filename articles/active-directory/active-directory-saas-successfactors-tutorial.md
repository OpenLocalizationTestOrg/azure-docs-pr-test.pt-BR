---
title: "Tutorial: integração do Azure Active Directory ao SuccessFactors | Microsoft Docs"
description: "Saiba como toouse SuccessFactors com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Tutorial: Integração do Azure Active Directory com o SuccessFactors
Olá objetivo deste tutorial é tooshow você como toointegrate SuccessFactors com o Azure Active Directory (AD do Azure).

Integrando o SuccessFactors com o AD do Azure fornece Olá benefícios a seguir:

* Você pode controlar no AD do Azure que tenha acesso tooSuccessFactors
* Você pode habilitar seus usuários tooautomatically get conectado tooSuccessFactors (logon único) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com o SuccessFactors, você precisa Olá itens a seguir:

* Uma assinatura válida do Azure
* Um locatário no SuccessFactors

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
> 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando SuccessFactors da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-successfactors-from-hello-gallery"></a>Adicionando SuccessFactors da Galeria de saudação
integração de saudação tooconfigure do SuccessFactors no AD do Azure, você precisa tooadd SuccessFactors da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SuccessFactors da Galeria hello, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
    ![Configurando o logon único][1]
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Configurando o logon único][2]
4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Configurando o logon único][4]
6. Em Olá **caixa de pesquisa**, tipo **SuccessFactors**.
   
    ![Configurando o logon único][5]
7. No painel de resultados de saudação, selecione **SuccessFactors**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Configurando o logon único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com o SuccessFactors com base em um usuário de teste chamado "Britta Simon".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SuccessFactors tooan usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SuccessFactors precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no SuccessFactors.

tooconfigure e teste de logon único do AD do Azure com o SuccessFactors, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do SuccessFactors](#creating-a-successfactors-test-user)**  -toohave um equivalente do Britta Simon no SuccessFactors é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD
Nesta seção, habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único em seu aplicativo SuccessFactors.

**tooconfigure AD do Azure-logon único com o SuccessFactors, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **SuccessFactors** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
    ![Configurando o logon único][7]
2. Em Olá **como você gostaria usuários toosign em tooSuccessFactors** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurando o logon único][8]
3. Em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**.
   
    ![Configurando o logon único][9]
   
    a. Em Olá **URL de logon** caixa de texto, digite um URL usando uma saudação padrões a seguir: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando uma saudação padrões a seguir: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Clique em **Avançar**. 

    > [!NOTE]
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com a URL real Olá URL de logon e de resposta. entre em contato com tooget esses valores, [equipe de suporte do SuccessFactors](https://www.successfactors.com/en_us/support.html).

1. Em Olá **configurar logon único no SuccessFactors** , clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação localmente no seu computador.
   
    ![Configurando o logon único][10]

2. Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do **portal de administração do SuccessFactors** como administrador.

3. Visite **segurança do aplicativo** e nativo muito**logon único no recurso**. 

4. Inserir qualquer valor na Olá **redefinir Token** e clique em **salvar Token** tooenable SSO do SAML.
   
    ![Configurar o logon único no lado do aplicativo][11]

    > [!NOTE] 
    > Esse valor é usado apenas como Olá interruptor. Se nenhum valor for salvo, Olá SSO do SAML é ON. Se um valor em branco é salvo Olá SSO do SAML é OFF.

1. Captura de tela de toobelow nativos e executar Olá ações a seguir.
   
    ![Configurar o logon único no lado do aplicativo][12]
   
    a. Selecione Olá **SSO do SAML v2** botão de opção
   
    b. Defina Olá SAML declarar parte Name(e.g. SAml issuer + company name).
   
    c. Em Olá **emissor SAML** caixa de texto colocar o valor de saudação de **URL do emissor** do Assistente de configuração de aplicativo do AD do Azure.
   
    d. Selecione **Resposta(Gerada pelo Cliente/IdP/AP)** como **Exigir Assinatura Obrigatória**.
   
    e. Selecione **Habilitado** como **Habilitar Sinalizador SAML**.
   
    f. Selecione **Não** como **Assinatura da Solicitação de Logon (Gerado por SF/SP/RP)**.
   
    g. Selecione **Perfil de Navegador/Postagem** como **Perfil SAML**.
   
    h. Selecione **Não** como **Impor Período de Certificado Válido**.
   
    i. Copiar conteúdo Olá Olá baixado do arquivo de certificado e, em seguida, cole-Olá **SAML verificando certificado** caixa de texto.

    > [!NOTE] 
    > conteúdo do certificado Olá deve ter começar marcas de certificado do certificado e de fim.

1. Navegar tooSAML V2 e, em seguida, executar Olá etapas a seguir:
   
    ![Configurar o logon único no lado do aplicativo][13]
   
    a. Selecione **Sim** como **Logoff Global iniciado por SP de suporte**.
   
    b. Em Olá **URL do serviço Global Logout (destino LogoutRequest)** caixa de texto colocar o valor de saudação de **URL de Logout remoto** do Assistente de configuração de aplicativo do AD do Azure.
   
    c. Selecione **Não** como **Exigir que sp criptografe todos os elementos NameID**.
   
    d. Selecione **não especificado** como **Formato de NameID**.
   
    e. Selecione **Sim** como **Habilitar logon iniciado por sp (AuthnRequest)**.
   
    f. Em Olá **solicitação de envio como o emissor de toda a empresa** caixa de texto colocar o valor de saudação de **URL de logon remoto** do Assistente de configuração de aplicativo do AD do Azure.
2. Execute estas etapas se desejar que os nomes de usuário de logon de saudação toomake não diferencia maiusculas de minúsculas.
   
    a. Visite **configurações da empresa**(parte inferior Olá).
   
    b. marque a caixa de seleção ao lado de **Habilitar Nome de Usuário que Não Diferencia Maiúsculas de Minúsculas**.
   
    c.Clique em **Salvar**.
   
    ![Configurar Logon Único][29]

    > [!NOTE] 
    > Se você tentar tooenable isso, o sistema de saudação verifica se ele criará um nome de logon do SAML duplicado. Por exemplo, se o cliente Olá tem nomes de usuário Usuário1 e user1. Parar de diferenciar maiúsculas e minúsculas cria essas duplicatas. sistema de saudação dará a você uma mensagem de erro e não habilitará o recurso de saudação. Olá cliente precisará toochange um dos nomes de usuário Olá para ele, na verdade, está escrito diferentes. 

1. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
   
    ![Aplicativos][14]
2. Em Olá **único logon confirmação** , clique em **concluir**.
   
    ![Aplicativos][15]

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no portal clássico do hello chamado Britta Simon.

![Criar um usuário do AD do Azure][16]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criação de um usuário de teste do AD do Azure][17]
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criação de um usuário de teste do AD do Azure][18]
4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.
   
    ![Criação de um usuário de teste do AD do Azure][19]
5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure][20]
   
    a. Em Tipo de Usuário, selecione Novo usuário na organização.
   
    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Avançar**.
6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure][21]
   
    a. Em Olá **nome** caixa de texto, tipo **Britta**.  
   
    b. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.
   
    c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
   
    d. Em Olá **função** lista, selecione **usuário**.
   
    e. Clique em **Avançar**.
7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criação de um usuário de teste do AD do Azure][22]
8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure][23]
   
    a. Anote o valor Olá Olá **nova senha**.
   
    b. Clique em **Concluído**.  

### <a name="creating-a-successfactors-test-user"></a>Criação de um usuário de teste do SuccessFactors
Ordem tooenable AD do Azure usuários toolog no SuccessFactors, eles devem ser provisionados no SuccessFactors.  
No caso de saudação do SuccessFactors, o provisionamento é uma tarefa manual.

usuários tooget criados no SuccessFactors, você precisa Olá toocontact [equipe de suporte do SuccessFactors](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooSuccessFactors seu acesso.

![Atribuir usuário][24]

**tooassign Britta Simon tooSuccessFactors, execute Olá etapas a seguir:**

1. No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.
   
    ![Atribuir usuário][25]
2. Na lista de aplicativos hello, selecione **SuccessFactors**.
   
    ![Configurar Logon Único][26]
3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![Atribuir usuário][27]
4. Na lista de usuários hello, selecione **Britta Simon**.
5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![Atribuir usuário][28]

### <a name="testing-single-sign-on"></a>Teste do logon único
Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em Olá SuccessFactors bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo SuccessFactors.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
