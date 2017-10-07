---
title: "Tutorial: Integração do Azure Active Directory com o Qlik Sense Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Qlik sentido Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Tutorial: integração do Azure Active Directory ao Qlik Sense Enterprise

Neste tutorial, você aprenderá como toointegrate Qlik sentido Enterprise com o Azure Active Directory (AD do Azure).

Integrando Qlik sentido Enterprise com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooQlik sentido Enterprise.
- Você pode habilitar seu usuários tooautomatically get conectado tooQlik sentido Enterprise (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Qlik sentido Enterprise, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Qlik Sense Enterprise habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Qlik sentido Enterprise na Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Adicionando Qlik sentido Enterprise na Galeria de saudação
integração de saudação tooconfigure do Qlik sentido corporativo no AD do Azure, você precisa tooadd Qlik sentido Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Qlik sentido Enterprise na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Qlik sentido Enterprise**, selecione **Qlik sentido Enterprise** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Qlik sentido Enterprise na lista de resultados de saudação](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Qlik Sense Enterprise, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Qlik sentido empresa é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação Qlik sentido empresa precisa toobe estabelecida.

Qlik sentido Enterprise, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Qlik sentido Enterprise, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Qlik sentido Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave um equivalente de Britta Simon Qlik sentido empresa que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Qlik sentido Enterprise.

**tooconfigure logon único do AD do Azure com Qlik sentido Enterprise, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Qlik sentido Enterprise** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. Em Olá **URLs e domínio da empresa sentido Qlik** , execute Olá etapas a seguir:

    ![Informações de logon único em Domínio e URLs do Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Observe Olá barra no final da saudação desse URI à direita. Ela é necessária.
    
    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador que estão descritas mais adiante neste tutorial ou entre em contato com [a equipe de suporte Qlik sentido Enterprise Client](https://www.qlik.com/us/services/support) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Prepare o arquivo de XML de metadados de federação de saudação para que você pode carregar servidor tooQlik sentido.
   
    > [!NOTE]
    > Antes de carregar Olá IdP metadados toohello server Qlik sentido, o arquivo hello precisa toobe editado tooremove informações tooensure funcionamento entre o AD do Azure e o servidor Qlik sentido.
    
    ![QlikSense][qs24]
   
    a. Abra o arquivo de FederationMetaData.xml de saudação, que você baixou do portal do Azure em um editor de texto.
   
    b. Procure o valor de saudação **RoleDescriptor**.  Há quatro entradas (dois pares de marcas de elemento de abertura e fechamento).
   
    c. Exclua marcas de RoleDescriptor hello e todas as informações do arquivo hello.
   
    d. Salve o arquivo hello e mantê-lo nas proximidades para uso neste documento.

7. Navegue toohello Qlik sentido Qlik Management Console (QMC) como um usuário que pode criar configurações de proxy virtual.

8. No hello QMC, clique em Olá **Virtual Proxies** item de menu.
   
    ![QlikSense][qs6] 

9. Na parte inferior de saudação da tela hello, clique em Olá **criar novo** botão.
   
    ![QlikSense][qs7]

10. tela de edição de proxy Hello Virtual é exibida.  Em Olá lado direito da tela hello é um menu para tornar visível a opções de configuração.
   
    ![QlikSense][qs9]

11. Com a opção de menu de identificação Olá marcada, digite as informações de identificação de saudação hello Azure virtual configuração de proxy.
    
    ![QlikSense][qs8]  
    
    a. Olá **descrição** campo é um nome amigável para a configuração de proxy virtual hello.  Insira um valor para uma descrição.
    
    b. Olá **prefixo** campo identifica Olá o ponto de extremidade de proxy virtual para conectar-se tooQlik sentido com Azure AD Single Sign-On.  Insira um nome de prefixo exclusivo para esse proxy virtual.
    
    c. **Tempo limite de inatividade de sessão (minutos)** é o tempo limite de saudação para conexões através desse proxy virtual.
    
    d. Olá **nome de cabeçalho do cookie de sessão** é armazenar de nome de cookie Olá Olá identificador de sessão para Olá sessão Qlik sentido um usuário recebe após a autenticação bem-sucedida.  Esse nome deve ser exclusivo.

12. Clique em toomake de opção de menu de autenticação Olá visível.  tela de autenticação Hello aparece.
    
    ![QlikSense][qs10]
    
    a. Olá **modo de acesso anônimo** suspensa determina se os usuários anônimos podem acessar Qlik sentido por meio do proxy virtual hello.  opção de padrão de saudação não é nenhum usuário anônimo.
    
    b. Olá **método de autenticação** suspensa determina o esquema Olá Olá autenticação proxy virtual usará.  Selecione SAML na lista suspensa de saudação.  Mais opções são exibidas como resultado.
    
    c. Em Olá **campo URI de host SAML**, os usuários de nome de host de entrada hello insiram tooaccess Qlik sentido através desse proxy virtual SAML.  Olá hostname é o uri de saudação de saudação server Qlik sentido.
    
    d. Em Olá **ID da entidade SAML**, digite Olá mesmo valor inserido para o campo URI de host Olá SAML.
    
    e. Olá **metadados IdP SAML** arquivo hello editado anteriormente no hello **editar metadados de federação de configuração do AD do Azure** seção.  **Antes de carregar os metadados de IdP hello, arquivo hello precisa toobe editado** tooremove informações tooensure funcionamento entre o AD do Azure e o servidor Qlik sentido.  **Consulte toohello instruções acima se o arquivo hello tem ainda toobe editado.**  Se Olá arquivo foi editado clique no botão hello e tooupload de arquivo de metadados editado selecione Olá-configuração de proxy virtual toohello.
    
    f. Insira a referência de esquema ou nome de atributo Olá para atributo SAML de Olá representando Olá **UserID** AD do Azure envia toohello server Qlik sentido.  Informações de referência de esquema estão disponíveis na configuração de postagem de telas Olá aplicativo do Azure.  atributo de nome de saudação toouse, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Insira o valor de saudação para Olá **diretório de usuário** que será anexado toousers quando ele autenticar o servidor de sentido tooQlik por meio do AD do Azure.  Valores embutidos em código devem estar entre **colchetes []**.  toouse um atributo enviado em Olá asserção SAML do AD do Azure, insira o nome de saudação do atributo Olá nessa caixa de texto **sem** colchetes.
    
    h. Olá **algoritmo de assinatura de SAML** conjuntos Olá Olá virtual configuração de proxy de assinatura de certificado do serviço provedor (deste servidor Qlik sentido maiusculas).  Se o servidor de Qlik sentido usar um certificado confiável gerado usando o Microsoft Enhanced RSA e AES Cryptographic Provider, alterar algoritmo de assinatura de SAML Olá muito**SHA-256**.
    
    i. Olá seção de mapeamento de atributo SAML permite atributos adicionais, como grupos toobe enviado tooQlik sentido para uso em regras de segurança.

13. Clique em Olá **BALANCEAMENTO de carga** toomake da opção de menu-lo visível.  Olá balanceamento de carga de tela é exibida.
    
    ![QlikSense][qs11]

14. Clique em Olá **adicionar novo nó de servidor** botão, o nó do mecanismo de select ou nós Qlik sentido serão enviar fins de balanceamento de carga de toofor de sessões e clique Olá **adicionar** botão.
    
    ![QlikSense][qs12]

15. Clique em toomake de opção de menu Avançado Olá visível. tela de Hello avançadas é exibida.
    
    ![QlikSense][qs13]
    
    lista de permissões de Host Olá identifica os nomes de host são aceitas durante a conexão toohello server Qlik sentido.  **Insira o nome do host Olá os usuários especificarão ao se conectar a servidor de sentido tooQlik.** Olá hostname é hello mesmo valor como Olá SAML uri de host sem Olá https://.

16. Clique em Olá **aplicar** botão.
    
    ![QlikSense][qs14]

17. Clique em mensagem de aviso de saudação tooaccept Okey afirmando proxies proxy virtual toohello vinculado será reiniciado.
    
    ![QlikSense][qs15]

18. Olá direita da tela hello, menu de itens associados Olá aparece.  Clique em Olá **Proxies** opção de menu.
    
    ![QlikSense][qs16]

19. Olá proxy tela é exibida.  Clique em Olá **Link** botão no hello inferior toolink um proxy do proxy toohello virtual.
    
    ![QlikSense][qs17]

20. Nó de proxy Olá Select que oferecem suporte a esta conexão de proxy virtual e clique Olá **Link** botão.  Depois de vincular, proxy hello será listado na proxies associados.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. Depois de cinco segundos de tooten, Olá mensagem QMC atualização serão exibida.  Clique em Olá **QMC atualização** botão.
    
    ![QlikSense][qs20]

22. Quando Olá QMC for atualizado, clique em Olá **Virtual proxies** item de menu. nova entrada de proxy virtual SAML Hello está listada na tabela de saudação na tela hello.  Clique na entrada de proxy virtual hello.
    
    ![QlikSense][qs51]

23. Na parte inferior de saudação da tela hello, botão de metadados de SP baixar hello serão ativados.  Clique em Olá **SP baixar metadados** arquivo tooa do botão toosave Olá metadados.
    
    ![QlikSense][qs52]

24. Arquivo de metadados de sp Olá aberto.  Observar Olá **entityID** entrada e hello **AssertionConsumerService** entrada.  Esses valores são equivalente toohello **identificador** e hello **URL de logon** na configuração de aplicativo de saudação do AD do Azure. Cole esses valores hello **URLs e domínio da empresa sentido Qlik** seção na configuração de aplicativo hello AD do Azure se eles não são correspondentes, em seguida, você deve substituí-las no Assistente de configuração de aplicativo do Azure AD hello.
    
    ![QlikSense][qs53]

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

   ![botão de Active Directory do Azure Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

   ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

   ![botão Adicionar de saudação](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

   ![caixa de diálogo de usuário Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. Em Olá **nome** , digite **BrittaSimon**.

   b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

   c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

   d. Clique em **Criar**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Criar um usuário de teste do Qlik Sense Enterprise

Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Qlik Sense Enterprise. Trabalhar com [a equipe de suporte Qlik sentido Enterprise Client](https://www.qlik.com/us/services/support) para adicionar usuários de saudação na plataforma do hello Qlik sentido Enterprise. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooQlik sentido Enterprise.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooQlik sentido Enterprise, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Qlik sentido Enterprise**.

    ![link de Qlik sentido Enterprise Olá na lista de aplicativos Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Qlik sentido Enterprise Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Qlik sentido Enterprise. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

