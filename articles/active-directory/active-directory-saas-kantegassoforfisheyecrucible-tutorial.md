---
title: "Tutorial: Integração do Azure Active Directory ao SSO do Kantega para o FishEye/Crucible | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kantega SSO para FishEye/Crucible."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a>Tutorial: Integração do Azure Active Directory ao SSO do Kantega para o FishEye/Crucible

Neste tutorial, você aprenderá como toointegrate Kantega SSO para FishEye/Crucible com o Azure Active Directory (AD do Azure).

Integrando Kantega SSO para FishEye/Crucible com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha tooKantega acesso SSO para FishEye/Crucible
- Você pode habilitar seu usuários tooautomatically get conectado tooKantega SSO para FishEye/Crucible (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Kantega SSO para FishEye/Crucible, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SSO do Kantega para o FishEye/Crucible

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Kantega SSO para FishEye/Crucible da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a>Adicionando Kantega SSO para FishEye/Crucible da Galeria de saudação
integração de saudação tooconfigure do Kantega SSO para FishEye/Crucible no AD do Azure, você precisa tooadd Kantega SSO para FishEye/Crucible da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Kantega SSO para FishEye/Crucible da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Kantega SSO para FishEye/Crucible**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. No painel de resultados de saudação, selecione **Kantega SSO para FishEye/Crucible**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o SSO do Kantega para o FishEye/Crucible, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Kantega SSO para FishEye/Crucible é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Kantega SSO para FishEye/Crucible precisa toobe estabelecida.

Kantega SSO para FishEye/Crucible, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e testar logon único do AD do Azure com o SSO Kantega FishEye/Crucible, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um Kantega SSO para o usuário de teste FishEye/Crucible](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave um equivalente do Britta Simon em Kantega SSO para FishEye/Crucible que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Kantega SSO para aplicativos FishEye/Crucible.

**tooconfigure logon único do AD do Azure com Kantega SSO para FishEye/Crucible, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Kantega SSO para FishEye/Crucible** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. Em **IDP** iniciada modo em Olá **Kantega SSO para o domínio de FishEye/Crucible e URLs** seção executar Olá etapa a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. Em **SP** modo iniciado, verifique **Mostrar configurações de URL avançadas** e executar Olá etapa a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Esses valores são recebidos durante a configuração de saudação do plug-in FishEye/Crucible explicada posteriormente no tutorial de saudação.

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. Em uma janela de navegador web diferente, faça logon em tooyour FishEye/Crucible no servidor local como um administrador.

8. Passe o mouse sobre engrenagem e clique em Olá **complementos**.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. Na seção Configurações do Sistema, clique em **Localizar novos complementos**. 

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. Pesquisa **Kantega SSO para Crucible** e clique em **instalar** tooinstall botão Olá novo plug-in SAML.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. Inicia a instalação do plug-in de saudação. 

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. Após a conclusão da instalação de saudação. Clique em **fechar**

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. Clique em **Gerenciar**.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. Clique em **configurar** tooconfigure Olá novo plug-in.  

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. Em Olá **SAML** seção. Selecione **do Azure Active Directory (AD do Azure)** de saudação **Adicionar provedor de identidade** lista suspensa.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. Selecione o nível de assinatura como **Básico**.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. Em Olá **propriedades do aplicativo** seção, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    a. Saudação de cópia **URI da ID do aplicativo** valor e usá-lo como **identificador, o URL de resposta e a URL de logon** em Olá **Kantega SSO para o domínio de FishEye/Crucible e URLs** seção no portal do Azure.

    b. Clique em **Avançar**.

18. Em Olá **importar metadados** seção, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    a. Selecione **Arquivo de metadados no meu computador** e carregue um arquivo de metadados baixado no portal do Azure.

    b. Clique em **Avançar**.

19. Em Olá **nome e SSO local** seção, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    a. Adicionar o nome do provedor de identidade de saudação em **nome do provedor de identidade** caixa de texto (por exemplo, o AD do Azure).

    b. Clique em **Avançar**.

20. Verifique se o certificado de autenticação de saudação e clique em **próximo**.    

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. Em Olá **contas de usuário de olho de peixe** seção, execute as seguintes etapas:

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    a. Selecione **criar usuários no diretório interno do FishEye se necessário** e insira nome apropriado saudação do grupo de saudação para usuários (pode ser não vários. de grupos separados por vírgula).

    b. Clique em **Avançar**.

22. Clique em **Concluir**.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. Em Olá **conhecido domínios do AD do Azure** seção, execute as seguintes etapas:   

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    a. Selecione **conhecido domínios** do painel esquerdo de saudação da página de saudação.

    b. Digite o nome de domínio em Olá **conhecido domínios** caixa de texto.

    c. Clique em **Salvar**.  

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a>Criando um usuário de teste do SSO do Kantega para o FishEye/Crucible

tooenable AD do Azure usuários toolog em tooFishEye/Crucible, eles devem ser provisionados no FishEye/Crucible. No SSO do Kantega para o FishEye/Crucible, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon tooyour Crucible no servidor local como um administrador.

2. Passe o mouse sobre engrenagem e clique em Olá **usuários**.

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. Na seção da guia **Usuários**, clique em **Adicionar usuário**.

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. Em Olá **adicionar novo usuário** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    a. Em Olá **Username** caixa de texto, como o email de saudação do tipo de usuário Brittasimon@contoso.com.
    
    b. Em Olá **nome de exibição** caixa de texto, nome de exibição do tipo de usuário hello como Britta Simon.
    
    c. Em Olá **endereço de Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.

    d. Em Olá **senha** caixa de texto, digite a senha de saudação do usuário.  

    e. Em Olá **Confirmar senha** caixa de texto, redigite a senha de saudação do usuário.

    f. Clique em **Adicionar**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKantega SSO para FishEye/Crucible.

![Atribuir usuário][200] 

**tooassign Britta Simon tooKantega SSO para FishEye/Crucible, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Kantega SSO para FishEye/Crucible**.

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em hello Kantega SSO para bloco FishEye/Crucible Olá painel de acesso, você deve obter automaticamente assinado em tooyour Kantega SSO para o aplicativo FishEye/Crucible.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

