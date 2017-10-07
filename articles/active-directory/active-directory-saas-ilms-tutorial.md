---
title: "Tutorial: Integração do Azure Active Directory ao iLMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Tutorial: Integração do Azure Active Directory ao iLMS

Neste tutorial, você aprenderá como iLMS toointegrate com o Azure Active Directory (AD do Azure).

Integrando iLMS com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooiLMS
- Você pode habilitar seus usuários tooautomatically get conectado tooiLMS (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com iLMS, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do iLMS habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando iLMS da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-ilms-from-hello-gallery"></a>Adicionando iLMS da Galeria de saudação
integração de saudação tooconfigure de iLMS no AD do Azure, você precisa iLMS tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**iLMS tooadd da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **iLMS**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. No painel de resultados de saudação, selecione **iLMS**, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o iLMS, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em iLMS é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em iLMS precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em iLMS.

tooconfigure e teste de logon único do AD do Azure com iLMS, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste iLMS](#creating-an-ilms-test-user)**  -toohave um equivalente do Britta Simon em iLMS é a representação toohello vinculado do Azure AD de seus.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo iLMS.

**tooconfigure AD do Azure-logon único com iLMS, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **iLMS** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. Em Olá **iLMS domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. Em hello **identificador** textbox, colar Olá **identificador** valor copiar de **provedor** seção das configurações de SAML no portal de administração de iLMS.

    b. Em Olá **URL de resposta** caixa de texto, colar Olá **(URL) do ponto de extremidade** valor copiar de **provedor de serviços** seção das configurações de SAML no portal de administração iLMS ter seguinte Olá padrão`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >“123456” é um valor de exemplo de identificador.

4. Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    Em hello **URL de logon** textbox, colar Olá **(URL) do ponto de extremidade** valor copiar de **provedor** seção das configurações de SAML no portal de administração de iLMS como`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT provisionamento, o aplicativo de iLMS espera asserções SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos. Olá captura de tela a seguir mostra um exemplo.
    
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Criar **departamento, região** e **divisão** atributos e adicione o nome da saudação desses atributos em iLMS. Todos esses atributos mostrados acima são necessários.    

    > [!NOTE] 
    > Você tem tooenable **criar conta de usuário Un-recognized** na iLMS toomap esses atributos. Siga as instruções de saudação [aqui](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget uma ideia na configuração de atributos de saudação.

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**

7. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. Em uma janela do navegador web diferente, faça logon no tooyour **portal de administração de iLMS** como um administrador.

10. Clique em **SSO:SAML** em **configurações** guia Configurações do SAML tooopen e executar Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Expanda Olá **provedor** Olá seção e cópia **identificador** e **(URL) do ponto de extremidade** valor.

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. Na seção **Provedor de Identidade**, clique em **Importar Metadados**.
    
    c. Selecione Olá **metadados** arquivo baixado do Portal do Azure de **o certificado de autenticação SAML** seção.

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Se você quiser tooenable JIT Provisionando toocreate iLMS contas para cancelar-reconhecer os usuários, execute as etapas a seguir:
        
       - Marque a opção **Criar Conta de Usuário Não Reconhecido**.
       
       ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Mapear atributos de saudação no AD do Azure com atributos de saudação em iLMS. Na coluna de atributo hello, especifique valor padrão do hello atributos nome ou hello.

    e. Vá muito**regras de negócio** guia e executar Olá etapas a seguir: 
        
       ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/5.png)

       - Verificar **criar regiões de Un-recognized, divisões e departamentos** toocreate regiões, divisões e departamentos que já não existem no tempo de saudação do logon único.
        
       - Verificar **atualização perfil de usuário durante entrar** toospecify se o perfil do usuário Olá é atualizado com cada logon único. 
        
       - Se hello **"Atualização em branco valores para não campos no perfil de usuário obrigatório"** opção estiver marcada, os campos de perfil opcional que estão em branco após a entrada será também fazem com que Olá iLMS perfil de usuário toocontain de valores em branco para esses campos.
        
       - Verificar **Enviar Email de notificação de erro** e insira o email de saudação do usuário Olá onde você deseja que o email de notificação de erro tooreceive hello.

11. Clique em **salvar** botão Configurações de saudação toosave.

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-ilms-test-user"></a>Criando um usuário de teste do iLMS

Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello. JIT funcionará, se você clicou Olá **criar conta de usuário Un-recognized** caixa de seleção durante a configuração de SAML no portal de administração de iLMS.

Se você precisar toocreate um usuário manualmente, em seguida, siga etapas a seguir:

1. Faça logon no site da empresa iLMS tooyour como um administrador.

2. Clique em **"Registrar usuário"** em **usuários** guia tooopen **registrar usuário** página. 
   
   ![Adicionar Funcionário](./media/active-directory-saas-ilms-tutorial/3.png)

3. Em Olá **"Registrar usuário"** página, execute Olá etapas a seguir.

    ![Adicionar Funcionário](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. Em Olá **nome** caixa de texto, tipo hello nome Britta.
   
    b. Em Olá **Sobrenome** caixa de texto, Olá tipo sobrenome Simon.

    c. Em Olá **ID de Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.

    d. Em Olá **região** suspenso, o valor Olá selecione região.

    e. Em Olá **divisão** suspenso, o valor Olá selecione divisão.

    f. Em Olá **departamento** suspenso, o valor Olá selecione departamento.

    g. Clique em **Salvar**.

    > [!NOTE] 
    > Você pode enviar toouser de email de registro selecionando **enviar email de registro** caixa de seleção.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooiLMS seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooiLMS, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **iLMS**.

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá iLMS bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour iLMS aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

