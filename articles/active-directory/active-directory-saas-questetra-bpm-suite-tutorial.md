---
title: "Tutorial: Integração do Azure Active Directory com o Questetra BPM Suite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Tutorial: Integração do Active Directory do Azure com o Questetra BPM Suite
Olá objetivo deste tutorial é tooshow você como toointegrate Questetra BPM Suite com o Azure Active Directory (AD do Azure).  
Pacote de BPM Questetra integrando o AD do Azure fornece Olá benefícios a seguir: 

* Você pode controlar no AD do Azure que tenha acesso tooQuestetra BPM Suite 
* Você pode habilitar seu usuários tooautomatically get conectado tooQuestetra BPM Suite (logon único) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com Questetra BPM Suite, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Uma assinatura habilitada para logon único do [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/)

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
> 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.  
cenário de saudação descrito neste tutorial consiste em três principais blocos de construção:

1. Adicionar pacote de BPM Questetra da Galeria de saudação 
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Adicionar pacote de BPM Questetra da Galeria de saudação
integração de saudação tooconfigure do pacote de BPM Questetra no AD do Azure, você precisa tooadd Questetra BPM Suite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Questetra BPM Suite da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1]

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2]

4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4]

6. Na caixa de pesquisa hello, digite **Questetra BPM Suite**.
   
    ![Aplicativos][5]

7. No painel de resultados de saudação, selecione **Questetra BPM Suite**e, em seguida, clique em **concluir** aplicativo hello de tooadd.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com o pacote de BPM Questetra com base em um usuário de teste chamado "Britta Simon".

Para toowork de logon único, o AD do Azure precisa tooknow é que usuário de contraparte saudação do usuário do pacote de BPM Questetra tooan no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no pacote de BPM Questetra precisa toobe estabelecida.  
Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no pacote de BPM Questetra.

tooconfigure e teste de logon único do AD do Azure com Questetra BPM Suite, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do pacote de BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  -toohave um equivalente do Britta Simon no pacote de BPM Questetra que é a representação toohello vinculado do Azure AD de seus.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do AD do Azure
Olá objetivo desta seção é tooenable AD do Azure-logon único no hello portal clássico do Azure e tooconfigure logon único no aplicativo Questetra BPM Suite.

**tooconfigure logon único do AD do Azure com o pacote de BPM Questetra, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **Questetra BPM Suite** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.
   
    ![Configurar Logon Único][8]

2. Em Olá **como você gostaria usuários toosign em tooQuestetra BPM Suite** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Logon Único do AD do Azure][9]

3. Em outra janela do navegador da Web, faça logon em seu site de empresa **Questetra BPM Suite** como administrador.

4. No menu de saudação na parte superior de saudação, clique em **configurações do sistema**. 
   
    ![Logon Único do AD do Azure][10]

5. Olá tooopen **SingleSignOnSAML** , clique em **SSO (SAML)**. 
   
    ![Logon Único do AD do Azure][11]

6. Em Olá portal clássico do Azure, em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Definir configurações de aplicativo][13]
   
    a. Você **Questetra BPM Suite** Olá seção SP informações do site de empresa, Olá cópia **URL do ACS**e, em seguida, cole-Olá **URL de logon** caixa de texto.
   
    b. Você **Questetra BPM Suite** Olá seção SP informações do site de empresa, Olá cópia **ID da entidade**e, em seguida, cole-Olá **URL do emissor** caixa de texto.
   
    c. Você **Questetra BPM Suite** Olá seção SP informações do site de empresa, Olá cópia **URL do ACS**e, em seguida, cole-Olá **URL de resposta** caixa de texto.
   
    d. Clique em **Avançar**.

7. Em Olá **configurar logon único no pacote de BPM Questetra** , clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação localmente no seu computador.
   
    ![Configurar Logon Único][14]

8. Você **Questetra BPM Suite** site da empresa, execute Olá etapas a seguir: 
   
    ![Configurar Logon Único][15]
   
    a. Selecione **Habilitar Logon Único**.
   
    b. No hello portal clássico do Azure, copie Olá **URL do emissor** valor e, em seguida, cole-o em Olá **ID da entidade** caixa de texto.
   
    c. No hello portal clássico do Azure, copie Olá **o URL de serviço de logon único** valor e, em seguida, cole-o em Olá **URL da página de entrada** caixa de texto.
   
    d. No hello portal clássico do Azure, copie Olá **URL do serviço de logon único** valor e, em seguida, cole-o em Olá **URL da página de logout** caixa de texto.
   
    e. Em Olá **formato NameID** caixa de texto, tipo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: emailAddress**.

    f. Crie um arquivo codificado em base 64 usando o certificado baixado. 

    >[!TIP] 
    >Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).

    g. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-Olá **certificado de validação** caixa de texto. 

    h. Clique em **Salvar**.

1. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**. 
   
    ![O que é o Azure AD Connect][17]

2. Em Olá **único logon confirmação** , clique em **concluir**.  
   
    ![O que é o Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criar um usuário de teste do AD do Azure][100] 

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criar um usuário de teste do AD do Azure][101] 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**. 
   
    ![Criar um usuário de teste do AD do Azure][102] 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criar um usuário de teste do AD do Azure][103]
   
    a. Em **Tipo de Usuário**, selecione **Novo usuário na organização**.
   
    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
   
    c. Clique em Avançar.

6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Criar um usuário de teste do AD do Azure][104] 
   
    a. Em Olá **nome** caixa de texto, tipo **Britta**. 
   
    b. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.
   
    c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
   
    d. Em Olá **função** lista, selecione **usuário**.
   
    e. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criar um usuário de teste do AD do Azure][105]  

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criar um usuário de teste do AD do Azure][106]   
   
    a. Anote o valor Olá Olá **nova senha**.
   
    b. Clique em **Concluído**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Criar um usuário de teste do Questetra BPM Suite
Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no pacote de BPM Questetra.

**toocreate um usuário chamado Britta Simon no pacote de BPM Questetra, execute Olá etapas a seguir:**

1. Site de empresa de Questetra BPM Suite tooyour logon como administrador.
2. Vá muito**configurações do sistema > lista de usuários > novo usuário**. 
3. Na caixa de diálogo de novo usuário hello, execute Olá etapas a seguir: 
   
    ![Criar um usuário de teste][300] 
   
    a. Em Olá **nome** caixa de texto, digite o nome de usuário de Britta no AD do Azure.
   
    b. Em Olá **Email** caixa de texto, digite o nome de usuário de Britta no AD do Azure.
   
    c. Em Olá **senha** caixa de texto, digite uma senha.

4. Clique em **Adicionar novo usuário**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooQuestetra seu acesso BPM Suite.

![O que é o Azure AD Connect][200]

**tooassign Britta Simon tooQuestetra BPM Suite, execute Olá etapas a seguir:**

1. No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.
   
    ![O que é o Azure AD Connect][201]
2. Na lista de aplicativos hello, selecione **Questetra BPM Suite**.
   
    ![O que é o Azure AD Connect][205]
3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![O que é o Azure AD Connect][202]
4. Na lista de usuários hello, selecione **Britta Simon**.
   
    ![O que é o Azure AD Connect][203]
5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![O que é o Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>Teste do logon único
Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.  
Quando você clica em bloco Questetra BPM Suite Olá Olá painel de acesso, você deve obter um aplicativo do pacote de BPM Questetra tooyour automaticamente conectado em.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
