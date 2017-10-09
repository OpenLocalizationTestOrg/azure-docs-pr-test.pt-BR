---
title: "Tutorial: Integração do Azure Active Directory com o SilkRoad Life Suite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SilkRoad vida Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Tutorial: integração do Active Directory do Azure com o SilkRoad Life Suite
Olá objetivo deste tutorial é tooshow você como toointegrate SilkRoad vida Suite com o Azure Active Directory (AD do Azure). 

Integrando SilkRoad vida Suite AD do Azure fornece Olá benefícios a seguir: 

* Você pode controlar no AD do Azure que tenha acesso tooSilkRoad Suite de vida 
* Você pode habilitar seu usuários tooautomatically get conectado tooSilkRoad vida Suite-logon único (SSO) com suas contas do AD do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com SilkRoad vida Suite, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Uma assinatura do SilkRoad Life Suite habilitada para logon único

>[!NOTE]
>Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção. 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable você tootest SSO do AD do Azure em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando SilkRoad vida Suite da Galeria de saudação 
2. Configurar e testar o SSO do Azure AD

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Adicionar conjunto de vida de SilkRoad da Galeria de saudação
integração de Olá tooconfigure do conjunto de vida SilkRoad no AD do Azure, você precisa tooadd SilkRoad vida Suite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SilkRoad Suite de vida da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1]

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2]

4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4]

6. Na caixa de pesquisa hello, digite **SilkRoad vida Suite**.
   
    ![Aplicativos][5]

7. No painel de resultados de saudação, selecione **SilkRoad vida Suite**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Aplicativos][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Olá o objetivo desta seção é tooshow como tooconfigure e teste do Azure AD SSO com o pacote de vida SilkRoad com base em um usuário de teste chamado "Britta Simon".

Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá no usuário de tooan SilkRoad vida Suite no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no conjunto de vida SilkRoad precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no conjunto de vida SilkRoad.

tooconfigure e teste de logon único do AD do Azure com SilkRoad vida Suite, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de conjunto de vida SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave um equivalente do Britta Simon no conjunto de vida de SilkRoad toohello vinculado do Azure AD representação dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD
objetivo Olá desta seção é tooenable SSO do AD do Azure no portal clássico do Azure do hello e tooconfigure SSO em seu aplicativo SilkRoad vida Suite.

**tooconfigure logon único do AD do Azure com o pacote de vida SilkRoad, execute Olá etapas a seguir:**

1. Site de empresa de SilkRoad tooyour logon como administrador. 

  >[!NOTE] 
  > acesso de tooobtain toohello aplicativo SilkRoad vida Suite autenticação para configurar a federação com o Microsoft Azure AD, entre em contato com suporte SilkRoad ou seu representante de serviços SilkRoad.
  > 

2. Vá muito**provedor**e, em seguida, clique em **federação detalhes**. 
   
    ![Logon Único do AD do Azure][10] 

3. Clique em **baixar metadados de Federação**e, em seguida, salve o arquivo de metadados de saudação em seu computador.
   
    ![Logon Único do AD do Azure][11] 

4. Em Olá portal clássico do Azure, em Olá **SilkRoad vida Suite** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.
   
    ![Configurar Logon Único][6] 

5. Em Olá **como você gostaria usuários toosign em tooSilkRoad vida Suite** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Logon Único do AD do Azure][7] 

6. Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Logon Único do AD do Azure][8]   
 1. Em Olá **URL de logon** caixa de texto, digite a URL Olá usada pelo seu site de conjunto de vida SilkRoad tooyour toosign em usuários (por exemplo: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Abra Olá baixado **Silkroad** arquivo de metadados. 
 3. Localizar Olá **AssertionConsumerService** marca e, em seguida, Olá cópia **local** atributo.         
   
    ![Logon Único do AD do Azure][21] 
 4. Cole o valor de Olá Olá **URL de resposta** caixa de texto.  
 5. Clique em **Avançar**.

6. Em Olá **configurar logon único no conjunto de vida SilkRoad** página, execute Olá etapas a seguir:
   
    ![Logon Único do AD do Azure][9]  
 1. Clique em Download de certificado e, em seguida, salve o arquivo de saudação em seu computador.  
 2. Clique em **Avançar**.

7. No aplicativo **SilkRoad**, clique em **Fontes de Autenticação**.
   
    ![Logon Único do AD do Azure][12] 

8. Clique em **Adicionar Fonte de Autenticação**. 
   
    ![Logon Único do AD do Azure][13] 

9. Em Olá **adicionar fonte de autenticação** , execute Olá etapas a seguir: 
   
    ![Logon Único do AD do Azure][14]  
 1. Em **opção 2 - arquivo de metadados**, clique em **procurar** Olá tooupload baixou o arquivo de metadados.  
 2. Clique em **Criar Provedor de Identidade usando Dados de Arquivo**.

10. Em Olá **fontes de autenticação** seção, clique em **editar**. 
    
     ![Logon Único do AD do Azure][15] 

11. Em Olá **Editar autenticação fonte** caixa de diálogo, executar Olá etapas a seguir: 
    
     ![Logon Único do AD do Azure][16] 
 1. Para **Habilitado**, selecione **Sim**.   
 2. Em Olá **IdP descrição** caixa de texto, digite uma descrição para a sua configuração (por exemplo: *SSO do AD do Azure*).  
 3. Em Olá **nome IdP** caixa de texto, digite um nome de configuração específico tooyour (por exemplo: *Azure SP*).  
 4. Clique em **Salvar**.

12. Desabilite todas as outras fontes de autenticação. 
    
     ![Logon Único do AD do Azure][17]

13. Em Olá portal clássico do Azure, em Olá **único logon confirmação** , clique em **próximo**.  
    
     ![Logon Único do AD do Azure][18]

14. Em Olá **único logon confirmação** , clique em **concluir**.
    
     ![Logon Único do AD do Azure][19]

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**. 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. Em Tipo de Usuário, selecione Novo usuário na organização.  
 2. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**. 
 3. Clique em **Avançar**.

6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. Em Olá **nome** caixa de texto, tipo **Britta**.    
 2. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**. 
 3. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**. 
 4. Em Olá **função** lista, selecione **usuário**.
 5. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Anote o valor Olá Olá **nova senha**. 
 2. Clique em **Concluído**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Criar um usuário de teste do SilkRoad Life Suite
Olá objetivo desta seção é toocreate um usuário chamado Britta Simon SilkRoad vida conjunto. Britta deve ter uma ID de SSO (às vezes chamado tooas um *AuthParam*) que faz a correspondência de Britta **emailaddress** no AD do Azure.

**toocreate um usuário chamado Britta Simon no conjunto de vida SilkRoad, execute Olá etapas a seguir:**

- Peça para um usuário que tem como seu toocreate de equipe de suporte SilkRoad vida Suite **identificação do SSO** Olá atributo mesmo valor Olá **emailaddress** de Britta Simon no AD do Azure.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenable Britta Simon toouse Azure SSO concedendo tooSilkRoad seu acesso vida Suite.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSilkRoad vida Suite, execute Olá etapas a seguir:**

1. No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.
   
    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SilkRoad vida Suite**.
   
    ![Atribuir usuário][202] 

3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![Atribuir usuário][203] 

4. Na lista de usuários hello, selecione **Britta Simon**.

5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a>Testar logon único
Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.  

Quando você clica em bloco SilkRoad vida Suite Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de SilkRoad vida Suite.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





