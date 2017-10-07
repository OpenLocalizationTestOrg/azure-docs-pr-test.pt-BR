---
title: "Tutorial: Integração do Azure Active Directory ao Symantec WSS (Web Security Service) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Symantec Web segurança Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Tutorial: Integração do Azure Active Directory ao Symantec WSS (Web Security Service)

Neste tutorial, você aprenderá como toointegrate o Symantec Web segurança Service (WSS) a conta com sua conta do Azure Active Directory (AD do Azure) para que o WSS possa autenticar um usuário final provisionado no hello AD do Azure usando a autenticação do SAML e impor o usuário ou regras de política no nível do grupo.

Integrando o Symantec Web segurança Service (WSS) com o AD do Azure fornece Olá benefícios a seguir:

- Gerencie todos os usuários finais de saudação e os grupos usados por sua conta do WSS do seu portal do AD do Azure. 

- Permitir tooauthenticate de usuários finais Olá si no WSS usando suas credenciais do AD do Azure.

- Habilitar a imposição de saudação do usuário e grupo de regras de política no nível definidas em sua conta do WSS.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Symantec Web segurança Service (WSS), você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma conta do Symantec WSS (Web Security Service)

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar uma conta do WSS que está sendo usada para fins de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use sua conta do WSS que esteja sendo usada para fins de produção neste teste, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você irá configurar o AD do Azure tooenable único logon tooWSS usando credenciais do usuário final Olá definidas em sua conta do AD do Azure.
cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o aplicativo de serviço de segurança da Web da Symantec (WSS) hello da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Adicionando Symantec Web segurança Service (WSS) da Galeria de saudação
integração de saudação do tooconfigure da Symantec Web segurança Service (WSS) no AD do Azure, você precisa tooadd Symantec Web segurança Service (WSS) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Symantec Web segurança Service (WSS) da Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Symantec Web segurança Service (WSS)**, selecione **Symantec Web segurança Service (WSS)** no painel de resultados e clique em **adicionar** saudação do botão tooadd aplicativo.

    ![Symantec Web segurança Service (WSS) na lista de resultados de saudação](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Symantec WSS (Web Security Service), com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no Symantec Web segurança Service (WSS) é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Symantec Web segurança Service (WSS) precisa toobe estabelecida.

No Web segurança Service (WSS) de Symantec, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Symantec Web segurança Service (WSS), você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do serviço de segurança da Web da Symantec (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave um equivalente de Britta Simon na segurança de Web da Symantec Service (WSS) que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de serviço de segurança da Web da Symantec (WSS).

**tooconfigure logon único do AD do Azure com o Web segurança Service (WSS) de Symantec, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Symantec Web segurança Service (WSS)** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. Em Olá **Symantec Web segurança Service (WSS) domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. Em Olá **URL de resposta** caixa de texto, digite a URL de saudação:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Entre em contato com hello [equipe de suporte do cliente do serviço de segurança da Web da Symantec (WSS)](https://www.symantec.com/contact-us) se valores Olá Olá **identificador** e **URL de resposta** por algum motivo, não estão funcionando.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure logon único no hello lado Symantec Web segurança Service (WSS), consulte a documentação online do toohello WSS. Olá baixado **Metadata XML** arquivo precisará toobe importada no portal do WSS hello. Olá contato [equipe de suporte do serviço de segurança da Web da Symantec (WSS)](https://www.symantec.com/contact-us) se precisar de ajuda com a configuração de saudação no portal do WSS hello.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Criar um usuário de teste do Symantec WSS (Web Security Service)

Nesta seção, você cria um usuário chamado Brenda Fernandes no Symantec WSS (Web Security Service). Olá de nome correspondente de usuário final pode ser criado manualmente no portal do WSS hello, ou pode esperar que os usuários/grupos de saudação provisionados no portal WSS hello Azure AD toobe sincronizado toohello após alguns minutos (aproximadamente 15 minutos). Os usuários devem ser criados e ativados antes de usar o logon único. endereço IP público de saudação do computador do usuário final hello, que será usado toobrowse sites também precisará toobe provisionada no portal de serviço de segurança da Web da Symantec (WSS) hello.

> [!NOTE]
> Por favor, [clique aqui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget sua máquina do pública IPaddress.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSymantec segurança de Web Service (WSS).

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooSymantec Web segurança Service (WSS), execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Symantec Web segurança Service (WSS)**.

    ![Olá Symantec Web segurança Service (WSS) link na lista de aplicativos Olá](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você vai testar a funcionalidade de logon único Olá agora que você configurou seu toouse de conta do WSS AD do Azure para autenticação SAML.

Depois de ter configurado o tráfego de tooproxy do navegador da web tooWSS, quando você abre o navegador da web e tente toobrowse tooa site e em seguida, você será redirecionado página toohello logon do Azure. Insira as credenciais de saudação do usuário final do hello teste que foi configurado no hello (ou seja, BrittaSimon) do AD do Azure e associados a senha. Uma vez autenticados, você será capaz de toobrowse toohello site que você escolheu. Você deve criar uma regra de política em Olá WSS lado tooblock BrittaSimon de navegação tooa determinado site, em seguida, você deve ver Olá WSS bloco página quando você tenta toobrowse toothat site como usuário BrittaSimon.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

