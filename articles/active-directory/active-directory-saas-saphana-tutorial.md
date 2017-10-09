---
title: "Tutorial: integração do Azure Active Directory com o SAP HANA | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Tutorial: integração do Azure Active Directory com o SAP HANA

Neste tutorial, você aprenderá como toointegrate SAP HANA com o Azure Active Directory (AD do Azure).

Integração do SAP HANA com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSAP HANA
- Você pode habilitar seu usuários tooautomatically get conectado tooSAP HANA (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o SAP HANA, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do SAP HANA habilitada para logon único
- Uma instância do HANA em execução, seja em qualquer IaaS público, local, em VMs do Azure ou em grandes instâncias SAP no Azure
- Olá XSA administração da Web Interface, bem como HANA Studio instalado na instância do HANA hello.

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção do SAP HANA. Teste a integração de saudação primeiro em desenvolvimento ou ambiente de aplicativo hello e, em seguida, ambiente de produção de hello do uso de preparo.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando SAP HANA da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sap-hana-from-hello-gallery"></a>Adicionando SAP HANA da Galeria de saudação
integração de saudação tooconfigure do SAP HANA no AD do Azure, você precisa tooadd SAP HANA na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SAP HANA na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **SAP HANA**, selecione **SAP HANA** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd. 

    ![Olá novo aplicativo](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o SAP HANA, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SAP HANA é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SAP HANA deve toobe estabelecida.

SAP HANA, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o SAP HANA, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do SAP HANA](#creating-a-sap-hana-test-user)**  -toohave um equivalente do Britta Simon no SAP HANA é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SAP HANA.

**tooconfigure AD do Azure-logon único com o SAP HANA, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **SAP HANA** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. Em Olá **URLs e SAP HANA domínio** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. Em Olá **identificador** caixa de texto, tipo:`HA100` 

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [equipe de suporte do cliente do SAP HANA](https://cloudplatform.sap.com/contact.html) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Se o certificado não está ativo, em seguida, ativá-lo clicando Olá caixa de seleção "Criar novo certificado active" na saudação do AD do Azure. 

5. Aplicativos do SAP HANA espera as asserções de SAML de saudação em um formato específico. Olá captura de tela a seguir mostra um exemplo. Aqui nós mapeou hello **identificador de usuário** com **ExtractMailPrefix()** função de **user.mail**. Isso retorna o valor de prefixo de saudação de email do usuário de saudação que é Olá ID exclusivo do usuário. Isto é enviado toohello aplicativo SAP HANA em cada resposta bem-sucedida.

    ![Configurar Logon Único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo:

    a. Em Olá **identificador de usuário** lista suspensa, selecione **ExtractMailPrefix**.
    
    b. Em Olá **Mail** lista suspensa, selecione **user.mail**.

7. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure logon único no **SAP HANA** lado, o logon tooyour **HANA XSA Web Console** navegando toohello respectivo HTTPS-ponto de extremidade.

    > [!Note]
    > Na configuração padrão de saudação, Olá URL redireciona Olá solicitação tooa tela de logon, que exige credenciais de saudação de um autenticado SAP HANA banco de dados toocomplete saudação do processo de logon. usuário Olá que fizer logon deve ter tarefas de administração do hello privilégios necessários tooperform SAML.

9. Olá XSA a Interface da Web, navegar muito**provedor de identidade SAML** e clique Olá **"+"** -botão na parte inferior de saudação do painel de adicionar informações de provedor de identidade do hello tela toodisplay hello e executar Olá etapas a seguir:

    ![Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. Em Olá **adicionar informações do provedor de identidade** painel, colar conteúdo Olá Olá Metadata XML, que você baixou do portal do Azure em Olá **metadados** caixa de texto.

    ![Configurações para Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Se o conteúdo de saudação do documento XML de saudação for válido, Olá análise processo extrai Olá informações necessárias tooinsert Olá **assunto, ID de entidade e emissor** campos Olá geral dados área da tela e Olá campos URL Olá Área de tela de destino, por exemplo,  **URL Base e a URL de logon único (*)**.

    ![Configurações para Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. Na caixa de nome de saudação da saudação geral dados área da tela, insira um nome para o novo provedor de identidade SAML SSO hello.

    > [!Note]
    > nome de saudação do hello IDP SAML é obrigatório e deve ser exclusiva. ele aparece na lista de saudação do IDPs SAML disponível que é exibida, se selecionar o SAML como método de autenticação de saudação do SAP HANA XS aplicativos toouse, por exemplo, na área de tela de autenticação Olá Olá XS artefato da ferramenta de administração.

10. Salve os detalhes de saudação do novo provedor de identidade SAML hello. Escolha **salvar** toosave Olá detalhes do provedor de identidade SAML hello e adicionar Olá nova lista de IDP SAML toohello de IDPs de SAML conhecidos.

    ![botão salvar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. No Studio HANA em Propriedades do sistema de saudação do hello **configuração** guia, apenas as configurações de filtro **saml** e ajuste Olá **assertion_timeout** de **10 segundos** muito**120 s**.

    ![configuração assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sap-hana-test-user"></a>Criação de um usuário de teste SAP HANA

tooenable AD do Azure usuários toolog em tooSAP HANA, eles devem ser provisionados no SAP HANA.
O SAP HANA dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Se você precisar toocreate um usuário manualmente, execute Olá etapas a seguir:

>[!Note]
>Você pode alterar autenticação externa de saudação usada pelo usuário hello.
Os usuários externos são autenticados usando um sistema externo, por exemplo, um sistema Kerberos. Para obter informações detalhadas sobre identidades externas, contate seu [administrador de domínio](https://cloudplatform.sap.com/contact.html).

1. Olá abrir [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como um administrador e habilitar hello usuário de banco de dados para o SSO do SAML.

    ![criar usuário](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Escala Olá invisível da caixa de seleção toohello à esquerda do **SAML** e siga o link de configurar hello.

3. Clique em **adicionar** tooadd Olá IDP SAML e clique em **Okey** selecionando Olá SAML IDP apropriado.

4. Adicionar Olá **identidade externa** (ex. BrendaFernandes aqui) ou escolha **"Qualquer"** e clique em **OK**.

    >[!Note]
    >Se "Qualquer" caixa de seleção não estiver marcada, o nome de usuário de saudação em HANA precisa tooexactly nome de saudação de correspondência de usuário Olá Olá UPN antes de sufixo de domínio de saudação (ou seja, BrittaSimon@contoso.com seria BrittaSimon em HANA).

5. Para fins de teste, atribuir todos **"XS"** usuário de toohello de funções.

    ![atribuição de funções](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Você deve conceder apenas as permissões apropriadas para seus casos de uso.

6. Salve Olá de usuário.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAP HANA.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooSAP HANA, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SAP HANA**.

    ![Atribuir usuário](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco SAP HANA Olá Olá painel de acesso, você deve obter aplicativos do SAP HANA automaticamente assinado em tooyour.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

