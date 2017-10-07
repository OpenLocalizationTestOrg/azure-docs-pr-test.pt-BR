---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o local de trabalho pelo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Tutorial: Integração do Azure Active Directory com o Workplace by Facebook

Neste tutorial, você aprenderá como toointegrate no local de trabalho pelo Facebook com o Azure Active Directory (AD do Azure).

Integração do local de trabalho pelo Facebook com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooWorkplace pelo Facebook
- Você pode habilitar seu usuários tooautomatically get conectado tooWorkplace pelo Facebook (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Workplace by Facebook habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando local de trabalho pelo Facebook da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Adicionando local de trabalho pelo Facebook da Galeria de saudação
integração de saudação tooconfigure do local de trabalho pelo Facebook no AD do Azure, você precisa tooadd no local de trabalho pelo Facebook na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd no local de trabalho pelo Facebook da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **no local de trabalho pelo Facebook**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. No painel de resultados de saudação, selecione **no local de trabalho pelo Facebook**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Workplace by Facebook, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na área de trabalho pelo Facebook é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho pelo Facebook precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na área de trabalho pelo Facebook.

tooconfigure e teste de logon único do AD do Azure com o espaço de trabalho pelo Facebook, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Configurar a frequência de reautenticação](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt de local de trabalho para uma verificação SAML.
3. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
4. **[Criar um local de trabalho por usuário de teste do Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave um equivalente do Britta Simon na área de trabalho pelo Facebook é vinculado toohello AD do Azure representação do usuário.
5. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
6. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único na área de trabalho pelo aplicativo do Facebook.

**tooconfigure AD do Azure-logon único com espaço de trabalho pelo Facebook, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **no local de trabalho pelo Facebook** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Em Olá **no local de trabalho pelo domínio do Facebook e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.facebook.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Esses valores não são Olá real. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. Em Olá **no local de trabalho pela configuração do Facebook** seção, clique em **configurar o local de trabalho pelo Facebook** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. Em uma janela de navegador web diferente, tooyour de logon local de trabalho por site de empresa do Facebook como um administrador.
  
   > [!NOTE] 
   > Como parte da saudação o processo de autenticação SAML, local de trabalho pode usar cadeias de caracteres de consulta de backup too2.5 KB de tamanho em ordem toopass parâmetros tooAzure AD.

8. Em Olá **empresa painel**, vá toohello **autenticação** guia.

9. Em **autenticação SAML**, selecione **SSO apenas** da lista suspensa de saudação.

10. Valores de entrada hello copiados do **no local de trabalho pela configuração do Facebook** seção Olá portal do Azure nos campos correspondentes hello:

    *   Em **URL SAML** caixa de texto valor Olá colar **o URL de serviço de logon único**, que você copiou do portal do Azure.
    *   Em **caixa de texto URL do emissor SAML**, cole o valor de saudação do **ID da entidade SAML**, que você copiou do portal do Azure.
    *   Em **redirecionamento de Logout do SAML** (opcional), cole o valor de saudação do **URL de logout**, que você copiou do portal do Azure.
    *   Abra o **certificado codificado na base 64** no bloco de notas baixado do portal do Azure, copie o conteúdo de saudação para sua área de transferência e, em seguida, cole-o toothe **certificado SAML** caixa de texto.

11. Olá tooenter URL público, URL do destinatário, talvez seja necessário e a URL do ACS (serviço do consumidor de declaração) listados em Olá **configuração SAML** seção.

12. Role toohello inferior da seção hello e clique em Olá **teste SSO** botão. Isso resultará na exibição de uma janela pop-up com a página de logon do Azure AD apresentada. Insira suas credenciais no como tooauthenticate normal. 

    **Solução de problemas:** endereço de email de saudação Certifique-se de que está sendo retornado pelo AD do Azure é Olá mesmo Olá você efetuou logon com conta da empresa.

13. Depois que o teste de saudação for concluído com êxito, role toohello inferior da página hello e clique Olá **salvar** botão.

14. Agora, todos os usuários que usam o Workplace verão a página de logon do Azure AD para autenticação.

15. **Redirecionamento de Logoff SAML (opcional)** - 

    Você pode escolher toooptionally configurar uma Url de Logout do SAML, que pode ser usado toopoint na página de logout do AD do Azure. Quando essa configuração é habilitada e configurada, o usuário Olá não será direcionado toohello página de logout de área de trabalho. Em vez disso, o usuário de Olá será redirecionado toohello url que foi adicionado na configuração de redirecionamento de Logout do SAML de saudação.


> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Configurando a frequência de reautenticação

Você pode configurar tooprompt no local de trabalho para uma verificação SAML diariamente, três dias, semanas, duas semanas, meses ou nunca.

> [!NOTE] 
>Olá valor mínimo para a seleção SAML Olá em aplicativos móveis é definido tooone semana.

Você também pode forçar um redefinição para todos os usuários usando o botão de saudação SAML: exigir autenticação SAML para todos os usuários agora.


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Criação de um usuário de teste do Workplace by Facebook

Nesta seção, um usuário chamado Brenda Fernandes será criado no Workplace by Facebook. O Workplace by Facebook dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.

Não há nenhuma ação para você nesta seção. Se um usuário não existe no local de trabalho pelo Facebook, um novo será criado quando você tenta tooaccess no local de trabalho pelo Facebook.

>[!Note]
>Se você precisar toocreate um usuário manualmente, entre em contato com [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkplace pelo Facebook.

![Atribuir usuário][200] 

**tooassign Britta Simon tooWorkplace pelo Facebook, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **no local de trabalho pelo Facebook**.

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

