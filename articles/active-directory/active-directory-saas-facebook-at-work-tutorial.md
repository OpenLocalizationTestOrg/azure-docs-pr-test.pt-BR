---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o local de trabalho pelo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Tutorial: Integração do Azure Active Directory com o Workplace by Facebook

Neste tutorial, você aprenderá como toointegrate no local de trabalho pelo Facebook com o Azure Active Directory (AD do Azure).

Integração do local de trabalho pelo Facebook com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooWorkplace pelo Facebook.
- Você pode permitir que os usuários tooautomatically obter conectado tooWorkplace pelo Facebook (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central: Olá portal do Azure.

Para obter mais detalhes sobre a integração de aplicativos de SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Workplace by Facebook habilitada para SSO (logon único)

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicione espaço de trabalho pelo Facebook da Galeria de saudação.
2. Configurar e testar logon único do Azure AD.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Adicione o local de trabalho pelo Facebook da Galeria de saudação
tooconfigure Olá a integração da área de trabalho pelo Facebook AD do Azure, adicione no local de trabalho pelo Facebook na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

1. Em Olá [portal do Azure](https://portal.azure.com), no hello painel esquerdo, selecione **Active Directory do Azure**. 

    ![botão de Active Directory do Azure Olá][1]

2. Procurar muito**aplicativos empresariais** > **todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd Olá novo aplicativo, selecione **novo aplicativo** na parte superior de Olá Olá da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **no local de trabalho pelo Facebook**e selecione **no local de trabalho pelo Facebook** dos resultados. Em seguida, selecione **adicionar**, aplicativo de hello tooadd.

    ![Local de trabalho pelo Facebook na lista de resultados de saudação](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o SSO do Azure AD com o Workplace by Facebook, com base em um usuário de teste chamado “Brenda Fernandes”.

Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá na área de trabalho pelo Facebook é tooa usuário no AD do Azure. Em outras palavras, uma relação entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho pelo Facebook de vinculado deve ser estabelecida.

Estabelecer essa relação, atribuindo o valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na área de trabalho pelo Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO na área de trabalho pelo aplicativo do Facebook.

1. Em Olá portal do Azure, Olá **no local de trabalho pelo Facebook** página de integração de aplicativos, selecione **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable SSO.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Em Olá **no local de trabalho pelo domínio do Facebook e URLs** seção, Olá a seguir:

    a. Em Olá **URL de logon** caixa de texto, digite uma URL que usa o saudação padrão a seguir:`https://<company subdomain>.facebook.com`

    b. Em Olá **identificador** caixa de texto, digite uma URL que usa o saudação padrão a seguir:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Esses valores são apenas um exemplo. Atualize esses valores com URL de logon real hello e o identificador. Olá contato [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, selecione **certificado (Base64)**e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Selecione **Salvar**.

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. Em Olá **no local de trabalho pela configuração do Facebook** seção, selecione **configurar o local de trabalho pelo Facebook** tooopen Olá **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **referência rápida** seção.

    ![Configuração do Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. Em uma janela de navegador web diferente, entre tooyour no local de trabalho por site de empresa do Facebook como um administrador.
  
   > [!NOTE] 
   > Como parte da saudação o processo de autenticação SAML, o local de trabalho pode usar cadeias de caracteres de consulta de backup too2.5 quilobytes de tamanho em ordem toopass parâmetros tooAzure AD.

8. Em Olá **empresa painel**, vá toohello **autenticação** guia.

9. Em **autenticação SAML**, selecione **SSO apenas** da lista suspensa de saudação.

10. Insira valores hello copiados da saudação **no local de trabalho pela configuração do Facebook** seção Olá portal do Azure nos campos correspondentes hello:

    *   No **URL SAML** caixa de texto valor Olá colar **o URL de serviço de logon único**, que você copiou de saudação portal do Azure.
    *   No **URL do emissor SAML** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou de saudação portal do Azure.
    *   Em **redirecionamento de Logout de SAML (opcional)**, cole o valor de saudação do **URL de logout**, que você copiou de saudação portal do Azure.
    *   Abra o **certificado codificado na base 64** no bloco de notas, baixado do hello portal do Azure. Copie o conteúdo de saudação para sua área de transferência e, em seguida, cole-o toothe **certificado SAML** caixa de texto.

11. Talvez seja necessário público de saudação tooenter URL destinatário URL e o ACS (serviço do consumidor de declaração) URL, listado em Olá **configuração SAML** seção.

12. Role toohello inferior da seção hello e selecione **teste SSO**. Uma janela pop-up será exibida, com a página de entrada hello AD do Azure. tooauthenticate, insira suas credenciais como normal. Certifique-se de endereço de email Olá retornado pelo AD do Azure é Olá mesmo Olá você efetuou logon com conta da empresa.

13. Se o teste de saudação foi concluído com êxito, role toohello inferior da página hello e selecione **salvar**.

14. Agora, todas as pessoas que usam o Workplace verão a página de entrada do Azure AD para autenticação.

Você pode escolher tooconfigure uma URL, que pode ser usado toopoint na página de logout de saudação do AD do Azure de logout do SAML. Quando essa configuração é habilitada e configurada, Olá usuário não é mais direcionado toohello página de saída de local de trabalho. Em vez disso, o usuário de saudação é URL redirecionada toohello que foi adicionado na configuração de redirecionamento de saída do SAML hello.


> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello. Depois de adicionar a este aplicativo de saudação **do Active Directory** > **aplicativos empresariais** seção, basta selecionar Olá **Single Sign-On** guia e saudação de acesso inserido documentação por meio de saudação **configuração** seção na parte inferior da saudação. Você pode ler mais sobre recurso de documentação embedded Olá no hello [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Configurar a frequência de reautenticação

Você pode configurar o local de trabalho tooprompt uma verificação de SAML diariamente, três dias, uma semana, duas semanas, um mês, ou nunca.

> [!NOTE] 
>Olá valor mínimo para a seleção SAML Olá em aplicativos móveis é definido tooone semana.

Você também pode forçar uma redefinição de SAML para todos os usuários. toodo hello, use **exigem autenticação SAML para todos os usuários agora** botão.


### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

1. Em Olá **portal do Azure**, no hello painel esquerdo, selecione **Active Directory do Azure**.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e selecione **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo caixa, Olá a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar Senha** e tome nota.

    d. Selecione **Criar**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Criar um usuário de teste do Workplace by Facebook

Nesta seção, um usuário chamado Brenda Fernandes será criado no Workplace by Facebook. O Workplace by Facebook dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.

Não há nenhuma ação para você nesta seção. Se um usuário não existe no local de trabalho pelo Facebook, um novo será criado quando você tenta tooaccess no local de trabalho pelo Facebook.

>[!Note]
>Se você precisar toocreate um usuário manualmente, entre em contato com o hello [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse SSO do Azure, concedendo acesso tooWorkplace pelo Facebook.

![Atribuir usuário][200] 

1. Hello Azure exibir aplicativos de portal, abra hello. Acesse o modo de exibição de diretório toohello, vá muito**aplicativos empresariais**e, em seguida, selecione **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **no local de trabalho pelo Facebook**.

    ![Olá no local de trabalho por um link do Facebook na lista de aplicativos Olá](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. No menu Olá Olá esquerda, selecione **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Selecione **Adicionar**. Em seguida, no hello **Adicionar atribuição** painel, selecione **usuários e grupos**.

    ![Painel de atribuição adicionar Olá][203]

5. Em Olá **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Em Olá **usuários e grupos** caixa de diálogo, selecione **selecione**.

7. Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.
    
### <a name="test-single-sign-on"></a>Testar logon único

Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.
Para obter mais informações, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Próximas etapas

* Consulte Olá [lista de tutoriais sobre como toointegrate aplicativos SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md).
* Leia [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).
* Saiba mais sobre como muito[configurar provisionamento de usuário](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

