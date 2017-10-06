---
title: "Tutorial: integração do Azure Active Directory ao SAP Business Object Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a nuvem de objeto do SAP Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Tutorial: integração do Azure Active Directory ao SAP Business Object Cloud

Neste tutorial, você aprenderá como toointegrate SAP Business objeto nuvem com o Azure Active Directory (AD do Azure).

Você obtém Olá benefícios a seguir ao integrar a nuvem de objeto do SAP Business com o Azure AD:

- No AD do Azure, você pode controlar quem tem acesso tooSAP nuvem de objeto de negócios.
- Você pode entrar automaticamente no tooSAP seus usuários comerciais objeto nuvem usando o logon único e uma conta de usuário do AD do Azure.
- Você pode gerenciar suas contas em um local central, Olá portal do Azure.

toolearn mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooset a integração do AD do Azure com o SAP Business objeto nuvem, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Um SAP Business Object Cloud, com logon único habilitado

> [!NOTE]
> Se você testar etapas Olá neste tutorial, é recomendável que você não testá-las em um ambiente de produção.

Recomendações para testar etapas Olá neste tutorial:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. 

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicione a nuvem de objeto do SAP Business da Galeria de saudação.
2. Configurar e testar o logon único do Azure AD.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Adicionar a nuvem de objeto do SAP Business da Galeria de saudação
tooset a integração de saudação do SAP Business objeto nuvem com o AD do Azure, na Galeria de hello, adicionar lista de tooyour de nuvem de objeto do SAP Business de aplicativos SaaS gerenciados.

Nuvem de objeto do SAP Business da Galeria de saudação do tooadd:

1. Em Olá [portal do Azure](https://portal.azure.com), no hello menu à esquerda, selecione **Active Directory do Azure**. 

    ![botão de Active Directory do Azure Olá][1]

2. Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.

    ![página de aplicativos de empresa Olá][2]
    
3. tooadd um novo aplicativo, selecione **novo aplicativo**.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **SAP Business objeto nuvem**.

    ![caixa de pesquisa Olá](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. No painel de resultados de saudação, selecione **SAP Business objeto nuvem**e, em seguida, selecione **adicionar**.

    ![Nuvem de objeto do SAP Business na lista de resultados de saudação](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configurar e testar o logon único do Azure AD

Nesta seção, você vai configurar e testar o logon único do Azure AD com o SAP Business Object Cloud, com base em uma usuária de teste chamada *Brenda Fernandes*.

Para toowork de logon único, o AD do Azure precisa usuário correspondente do tooknow Olá AD do Azure na nuvem de objeto do SAP Business. Uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na nuvem de objeto do SAP Business deve ser estabelecida.

Olá tooestablish referente à relação, na nuvem de objeto do SAP Business, **Username**, atribuir valor Olá Olá **nome de usuário** no AD do Azure.

tooconfigure e teste de logon único do AD do Azure com a nuvem de objeto do SAP Business, Olá concluir tarefas a seguir:

1. [Configurar o logon único do Azure AD](#set-up-azure-ad-single-sign-on). Configura um usuário toouse esse recurso.
2. [Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user). Testes do AD do Azure-logon único com o usuário Olá Britta Simon.
3. [Criar um usuário de teste do SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user). Cria um equivalente de Britta Simon na nuvem de objeto do SAP Business que é vinculado toohello representação do AD do Azure do usuário hello.
4. [Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user). Define o Britta Simon toouse logon único do AD do Azure.
5. [Testar o logon único](#test-single-sign-on). Verifica que se a configuração de saudação funciona.

### <a name="set-up-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você ativar único do AD do Azure logon no portal do Azure de saudação. Em seguida, configura o logon único no seu aplicativo SAP Business Object Cloud.

tooset o AD do Azure-logon único com o SAP Business objeto nuvem:

1. Em Olá portal do Azure, Olá **SAP Business objeto nuvem** página de integração de aplicativos, selecione **o logon único**.

    ![Selecionar Logon Único][4]

2. Em Olá **o logon único** página, para **modo**, selecione **baseado no SAML logon**.
 
    ![Selecionar Logon com base em SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. Em **URLs e domínio de nuvem de objeto do SAP Business**completa Olá seguintes etapas:

    1. Em Olá **URL de logon** caixa, digite uma URL que tenha o saudação padrão a seguir: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. Em Olá **identificador** caixa, digite uma URL que tenha o saudação padrão a seguir:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URLs da página Domínio e URLs do SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > valores Hello essas URLs são apenas para demonstração. Atualizar valores de saudação com hello real URL de logon URL e o identificador. tooget Olá URL de logon, Olá contato [equipe de suporte do SAP Business objeto nuvem Client](https://www.sap.com/product/analytics/cloud-analytics.support.html). Você pode obter a URL de identificador Olá baixando metadados da nuvem de objeto do SAP Business de saudação do console de administração de saudação. Isso é explicado posteriormente no tutorial de saudação. 

4. Em **Certificado de Autenticação SAML**, selecione **XML de Metadados**. Em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Selecionar XML de Metadados](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Selecione **Salvar**.

    ![Selecionar Salvar](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. Em uma janela de navegador web diferente, entre no site da empresa tooyour SAP Business objeto nuvem como um administrador.

7. Selecione **Menu** > **Sistema** > **Administração**.
    
    ![Selecionar Menu, Sistema e Administração](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. Em Olá **segurança** guia, selecione Olá **editar** ícone (caneta).
    
    ![Na guia de segurança hello, selecione o ícone de edição de saudação](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. Para **Método de Autenticação**, selecione **SSO (Logon Único) do SAML**.

    ![Selecione logon único SAML para o método de autenticação Olá](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload Olá provedor metadados de serviço (etapa 1), selecione **baixar**. No arquivo de metadados de hello, localizar e copiar Olá **entityID** valor. Em hello Azure portal em **URLs e domínio de nuvem de objeto do SAP Business**, cole o valor de saudação em Olá **identificador** caixa.

    ![Copie e cole o valor de ID de saudação](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload Olá provedor metadados de serviço (etapa 2) no arquivo hello baixado do hello portal do Azure, em **metadados do provedor de identidade carregar**, selecione **carregar**.  

    ![Em Fazer upload dos metadados do Provedor de Identidade, selecionar Fazer Upload](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. Em Olá **usuário atributo** lista, o atributo de usuário selecione hello (etapa 3) que você deseja toouse para sua implementação. Esse atributo de usuário mapeia toohello provedor de identidade. tooenter um atributo personalizado na página do usuário hello, use Olá **mapeamento personalizado de SAML** opção. Ou, você pode selecionar o **Email** ou **ID de usuário** como atributo de saudação do usuário. Em nosso exemplo, selecionamos **Email** porque Mapeamos Olá declaração do identificador de usuário com hello **userprincipalname** atributo Olá **atributos de usuário** seção Olá Portal do Azure. Isso fornece um email exclusivo do usuário, que é enviado toohello aplicativo SAP Business objeto nuvem em cada resposta SAML bem-sucedida.

    ![Selecionar Atributo de Usuário](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. conta de saudação tooverify com o provedor de identidade de saudação (etapa 4), em Olá **credencial de logon (Email)** , digite o endereço de email do usuário hello. Em seguida, selecione **Verificar Conta**. sistema de saudação adiciona a conta de usuário de toohello de credenciais de logon.

    ![Inserir email e selecionar Verificar Conta](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Selecione Olá **salvar** ícone.

    ![Ícone Salvar](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Você pode ler uma versão concisa essas instruções Olá [portal do Azure](https://portal.azure.com), enquanto você estiver configurando seu aplicativo! Depois de adicionar o aplicativo hello selecionando **do Active Directory** > **aplicativos empresariais**, selecione Olá **Single Sign-On** guia. Você pode acessar a documentação Olá inserido em Olá **configuração** seção final Olá Olá página. Para saber mais, confira a [documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Nesta seção, você deve criar um usuário de teste chamado Britta Simon no hello portal do Azure.

toocreate um usuário de teste no AD do Azure:

1. No hello portal do Azure, no menu da esquerda hello, selecione **Active Directory do Azure**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. lista de saudação do toodisplay de usuários, selecionados **usuários e grupos**e, em seguida, selecione **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo, Olá concluir as etapas a seguir:
 
    1. Em Olá **nome** , digite **BrittaSimon**.

    2. Em Olá **nome de usuário** , digite o endereço de email de saudação do usuário Olá Britta Simon.

    3. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    4. Selecione **Criar**.

        ![caixa de diálogo de usuário Olá](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Criar um usuário do AD do Azure][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Criar um usuário de teste do SAP Business Object Cloud

Os usuários do AD do Azure devem ser provisionados no SAP Business objeto nuvem antes que ele possa entrar tooSAP nuvem de objeto de negócios. No SAP Business Object Cloud, o provisionamento é uma tarefa manual.

tooprovision uma conta de usuário:

1. Entre no tooyour site da empresa de nuvem de objeto do SAP Business como um administrador.

2. Selecione **Menu** > **Segurança** > **Usuários**.

    ![Adicionar Funcionário](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. Em Olá **usuários** , tooadd novos detalhes do usuário, selecione  **+** . 

    ![Página Adicionar Usuários](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Em seguida, conclua Olá etapas a seguir:

    1. Em Olá **ID de usuário** , digite a ID de usuário de saudação do usuário hello, como **Britta**.

    2. Em Olá **nome** , digite Olá primeiro nome do usuário hello, como **Britta**.

    3. Em Olá **Sobrenome** , digite o sobrenome de saudação do usuário hello, como **Simon**.

    4. Em Olá **nome de exibição** , digite o nome completo de saudação do usuário hello, como **Britta Simon**.

    5. Em Olá **email** , digite o endereço de email de saudação do usuário hello, como  **brittasimon@contoso.com** .

    6. Em Olá **selecionar funções** página, selecione a função apropriada Olá para usuário hello e, em seguida, selecione **Okey**.

      ![Escolher função](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Selecione Olá **salvar** ícone.  


### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você permitir que Olá usuário Britta Simon toouse AD do Azure-logon único, concedendo Olá usuário conta acesso tooSAP nuvem de objeto de negócios.

tooassign Britta Simon tooSAP nuvem de objeto de negócios:

1. No portal do Azure de Olá, abrir modo de exibição de aplicativos hello e vá toohello exibição de diretório. Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SAP Business objeto nuvem**.

    ![Configurar Logon Único](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. No menu à esquerda do hello, selecione **usuários e grupos**.

    ![Selecionar Usuários e grupos][202] 

4. Selecione **Adicionar**. Em seguida, na Olá **Adicionar atribuição** página, selecione **usuários e grupos**.

    ![página de adicionar atribuição Olá][203]

5. Em Olá **usuários e grupos** página, na lista de saudação de usuários, selecionados **Britta Simon**.

6. Em Olá **usuários e grupos** página, selecione **selecione**.

7. Em Olá **Adicionar atribuição** página, selecione **atribuir**.

![Atribuir função de usuário Olá][200] 
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você seleciona o bloco de nuvem de objeto do SAP Business Olá no painel de acesso hello, você deve ser conectado automaticamente tooyour aplicativo em nuvem de objeto do SAP Business.

Para obter mais informações sobre o painel de acesso hello, consulte [painel de acesso Introdução toohello](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

