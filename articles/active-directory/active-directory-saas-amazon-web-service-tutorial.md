---
title: "Tutorial: Integração do Azure Active Directory com o AWS (Amazon Web Services) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e serviços AWS (Amazon Web)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Tutorial: Integração do Azure Active Directory com o AWS (Amazon Web Services)

Neste tutorial, você aprenderá como toointegrate AWS Amazon Web Services () com o Azure Active Directory (AD do Azure).

Integrando serviços AWS (Amazon Web) com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAmazon AWS (Web Services)
- Você pode habilitar seu usuários tooautomatically get conectado tooAmazon AWS (Web Services) (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com serviços AWS (Amazon Web), você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do AWS (Amazon Web Services)

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando serviços AWS (Amazon Web) da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Adicionando serviços AWS (Amazon Web) da Galeria de saudação
tooconfigure Olá a integração de serviços AWS (Amazon Web) no AD do Azure, você precisa tooadd serviços AWS (Amazon Web) da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd serviços AWS (Amazon Web) da Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **serviços AWS (Amazon Web)**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. No painel de resultados de saudação, selecione **serviços AWS (Amazon Web)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você vai configurar e testar o logon único do Azure AD com o AWS (Amazon Web Services), com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá em serviços AWS (Amazon Web) é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em serviços AWS (Amazon Web) precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em serviços AWS (Amazon Web).

tooconfigure e teste de logon único do AD do Azure com serviços AWS (Amazon Web), você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave um equivalente de Britta Simon em serviços AWS (Amazon Web) que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de serviços AWS (Amazon Web).

**tooconfigure logon único do AD do Azure com serviços AWS (Amazon Web), execute Olá etapas a seguir:**

1. Em Olá Portal do Azure, em Olá **serviços AWS (Amazon Web)** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. Em Olá **serviços AWS (Amazon Web) URLs e domínio** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.
    
    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Olá aplicativo AWS Amazon Web Services () espera as asserções de SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo.

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:
    
    | Nome do atributo  | Valor do atributo | Namespace |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://aws.amazon.com/SAML/Attributes |
    | Função            | user.assignedroles |  https://aws.amazon.com/SAML/Attributes |
    
    >[!TIP]
    >É necessário tooconfigure Olá provisionamento de usuário em AD do Azure toofetch todas as funções de saudação do Console do AWS. Consulte Olá provisionamento etapas abaixo.

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha. Adicione o valor de Namespace de saudação conforme fornecido acima.
    
    d. Clique em **OK**.

7. Clique em **salvar** botão Configurações de saudação toosave no Azure.

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. Em uma janela de navegador diferente, site da empresa serviços AWS (Amazon Web) tooyour logon como administrador.

9. Clique em **página inicial do Console**.
   
    ![Configurar Logon Único][11]

10. Clique em **IAM** no serviço **Segurança, Identidade e Conformidade**.
   
    ![Configurar Logon Único][12]

11. Clique em **Provedores de identidade**, e, em seguida, clique em **Criar provedor**.
   
    ![Configurar Logon Único][13]

12. Em Olá **Configurar provedor** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Configurar Logon Único][14]
 
    a. Como **Tipo de provedor**, selecione **SAML**.

    b. Em Olá **nome do provedor** caixa de texto, digite um nome de provedor (por exemplo: *WAAD*).

    c. tooupload seu arquivo de metadados baixado, clique em **Escolher arquivo**.

    d. Clique em **Próxima etapa**.

13. Em Olá **verificar informações do provedor** página da caixa de diálogo, clique em **criar**. 
    
    ![Configurar Logon Único][15]

14. Clique em **Funções** e, em seguida, clique em **Criar Nova Função**. 
    
    ![Configurar Logon Único][16]

15. Em Olá **definir nome de função** caixa de diálogo, executar Olá etapas a seguir: 
    
    ![Configurar Logon Único][17] 

    a. Em Olá **nome da função** caixa de texto, digite um nome de função (por exemplo: *TestUser*). 

    b. Clique em **Próxima etapa**.

16. Em Olá **Selecionar tipo de função** caixa de diálogo, executar Olá etapas a seguir: 
    
    ![Configurar Logon Único][18] 

    a. Selecione **Função de acesso do provedor de identidade**. 

    b. Em Olá **Grant Web Single Sign-On (WebSSO) tooSAML provedores de acesso a** seção, clique em **selecione**.

17. Em Olá **estabelecer confiança** caixa de diálogo, executar Olá etapas a seguir:  
    
    ![Configurar Logon Único][19] 

    a. Como provedor SAML, selecione o provedor SAML de saudação você criou anteriormente (por exemplo: *WAAD*)
  
    b. Clique em **Próxima etapa**.

18. Em Olá **verificar função confiança** caixa de diálogo, clique em **próxima etapa**.
    
    ![Configurar Logon Único][32]

19. Em Olá **anexar política** caixa de diálogo, clique em **próxima etapa**.
    
    ![Configurar Logon Único][33]

20. Em Olá **revisão** caixa de diálogo, executar Olá etapas a seguir:
    
    ![Configurar Logon Único][34]
 
    a. Clique em **Criar função**.

    b. Criar funções necessárias e mapeá-los toohello provedor de identidade.

21. Configurar usuário Olá provisionamento toofetch todas as funções de saudação do AWS

    a. No logon do Console do AWS Olá com sua conta raiz

    b. No canto direito superior de saudação clique em seu nome e clique em Olá **minhas credenciais de segurança** opção. Isso abrirá uma tela como uma mensagem de aviso. Botão Olá **as credenciais de segurança** toopass botão Olá tela.
        
       ![Configurar Logon Único][36]

       ![Configurar Logon Único][37]

    c. Em Olá chaves de acesso clique Olá **criar nova chave de acesso** botão. Isso gera hello ID da chave de acesso e um valor de token.
    
       ![Configurar Logon Único][38]

    d. Copie esses dois valores e baixe-os também para não perdê-los.

    e. No hello Portal do Azure, na página de integração de aplicativos do hello serviços AWS (Amazon Web), clique em **provisionamento**.
        
       ![Configurar Logon Único][35]

    f. Definir o modo de provisionamento de saudação muito**automática**
        
       ![Configurar Logon Único][39]

    g. Agora em Olá **clientsecret** e **segredo do Token** colar valores correspondentes hello, que você copiou do Console do AWS.
    
    h. Você pode clicar em Olá **Conexão de teste** botão tootest conectividade de saudação. Depois que for bem-sucedida, em seguida, você pode iniciar Olá provisionamento conector.
       
       ![Configurar Logon Único][40]

    i. Habilitar Olá Status de provisionamento muito**em**. Isso inicia a busca de funções de saudação do aplicativo hello.

       ![Configurar Logon Único][41]

    > [!NOTE]
    > Serviço de provisionamento do AD do Azure é executado após algumas funções do tempo toosync saudação do AWS cada. Você deve ver todos os Olá provedor de identidade anexado funções AWS no AD do Azure e você pode usá-los durante a atribuição de saudação aplicativo toousers ou grupos.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Criação de um usuário de teste do Amazon Web Services

Em ordem tooenable AD do Azure usuários toolog em tooAmazon AWS (Web Services), eles devem ser provisionados em serviços AWS (Amazon Web). No caso de saudação do Amazon Web Services AWS (), o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **serviços AWS (Amazon Web)** site da empresa como administrador.

2. Clique em Olá **página inicial do Console** ícone. 
   
    ![Configurar Logon Único][11]

3. Clique em Gerenciamento de identidades e acesso. 
   
    ![Configurar Logon Único][28]

4. No painel de Olá, clique em **usuários**e, em seguida, clique em **criar novos usuários**. 
   
    ![Configurar Logon Único][29]

5. Na caixa de diálogo de Create User hello, execute Olá etapas a seguir: 
   
    ![Configurar Logon Único][30]   
    
    a. Em Olá **Insira nomes de usuário** caixas de texto, digite o nome de usuário de Brita Simon (userprincipalname) no AD do Azure.

    b. Clicar em **Criar.**
        
### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooAmazon seu acesso AWS (Web Services).

![Atribuir usuário][200] 

**tooassign Britta Simon tooAmazon AWS (Web Services), execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **serviços AWS (Amazon Web)**.

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Em **Selecionar função** guia, a função apropriada Olá Selecione usuário hello. Todas essas funções são mostradas com o nome da função hello e o nome do provedor de identidade. Dessa forma, que você pode identificar facilmente as funções de saudação do AWS.

8. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá serviços AWS (Amazon Web) lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de serviços AWS (Amazon Web). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
