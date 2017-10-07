---
title: "Tutorial: integração do Azure Active Directory com o Cisco Spark | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Spark Cisco."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>Tutorial: Integração do Azure Active Directory ao Cisco Spark

Neste tutorial, você aprenderá como toointegrate Cisco despertar com o Azure Active Directory (AD do Azure).

Integrando Cisco Spark com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooCisco Spark
- Você pode habilitar seu usuários tooautomatically get conectado tooCisco Spark (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Cisco Spark, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Cisco Spark

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Cisco Spark da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-cisco-spark-from-hello-gallery"></a>Adicionando Cisco Spark da Galeria de saudação
integração de saudação tooconfigure do Cisco Spark no Azure AD, é necessário tooadd Cisco Spark na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Cisco Spark da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Spark Cisco**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. No painel de resultados de saudação, selecione **Cisco Spark**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Cisco Spark com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Spark Cisco é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Spark Cisco precisa toobe estabelecida.

No Spark Cisco, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Cisco Spark, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave um equivalente do Britta Simon no Spark Cisco que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Cisco Spark.

**tooconfigure AD do Azure-logon único com o Cisco Spark, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Cisco Spark** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. Em Olá **Cisco Spark domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL como:`https://web.ciscospark.com/#/signin`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello identificador real. Entre em contato com [equipe de suporte do Cisco Spark cliente](https://support.ciscospark.com/) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. Aplicativo do Cisco Spark espera atributos específicos de toocontain Olá de asserções SAML. Configure Olá seguintes atributos para este aplicativo. Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos. Olá captura de tela a seguir mostra um exemplo.
    
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:
    
    | Nome do atributo  | Valor do atributo |
    | --------------- | -------------------- |    
    |   uid    | user.userprincipalname |   

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **OK**.

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. Entrar muito[Cisco nuvem colaboração gerenciamento](https://admin.ciscospark.com/) com suas credenciais de administrador completo.

9. Selecione **configurações** e em Olá **autenticação** seção, clique em **modificar**.
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. Escolha **Integrar um provedor de identidade de terceiros. (Avançado)**  e toohello vá próxima tela.

11. Em Olá **importar metadados de Idp** página, ou arraste e solte o arquivo de metadados de saudação do AD do Azure para a página de saudação ou usar toolocate de opção de navegador de arquivo hello e carregar o arquivo de metadados de saudação do AD do Azure. Em seguida, escolha **Exigir certificado assinado por uma autoridade de certificação em Metadados (mais seguro)** e clique em **Avançar**. 
    
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. Escolha **Testar Conexão SSO** e, quando uma nova guia do navegador for aberta, autentique-se com o Azure AD conectando-se.

13. Retornar toohello **Cisco nuvem colaboração gerenciamento** guia do navegador. Se o teste de saudação foi bem-sucedido, selecione **esse teste foi bem-sucedido. Habilitar Logon Único** e clique em **Avançar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-cisco-spark-test-user"></a>Criando um usuário de teste do Cisco Spark

Nesta seção, você criará um usuário chamado Brenda Fernandes no Cisco Spark. Nesta seção, você criará um usuário chamado Brenda Fernandes no Cisco Spark.

1. Vá toohello [Cisco nuvem colaboração gerenciamento](https://admin.ciscospark.com/) com suas credenciais de administrador completo.

2. Clique em **Usuários** e em **Gerenciar Usuários**.
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. Em Olá **usuário gerenciar** janela, selecione **adicionar manualmente ou modificar a usuários** e clique em **próximo**.

4. Escolha **Nomes e Endereço de email**. Em seguida, preencha o texto de saudação da seguinte maneira:
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. Em Olá **nome** caixa de texto, tipo **Britta**. 
    
    b. Em Olá **Sobrenome** caixa de texto, tipo **Simon**.
    
    c. Em Olá **endereço de Email** caixa de texto, tipo  **britta.simon@contoso.com** .

5. Clique em hello mais entrar tooadd Britta Simon. Em seguida, clique em **Avançar**.

6. Em Olá **adicionar serviços para os usuários** janela, clique em **salvar** e **concluir**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCisco Spark.

![Atribuir usuário][200] 

**tooassign Britta Simon tooCisco Spark, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Spark Cisco**.

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco Cisco Spark Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Cisco Spark.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

