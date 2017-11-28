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
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="76e53-103">Tutorial: integração do Azure Active Directory ao SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="76e53-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="76e53-104">Neste tutorial, você aprenderá como toointegrate SAP Business objeto nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="76e53-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76e53-105">Você obtém Olá benefícios a seguir ao integrar a nuvem de objeto do SAP Business com o Azure AD:</span><span class="sxs-lookup"><span data-stu-id="76e53-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="76e53-106">No AD do Azure, você pode controlar quem tem acesso tooSAP nuvem de objeto de negócios.</span><span class="sxs-lookup"><span data-stu-id="76e53-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="76e53-107">Você pode entrar automaticamente no tooSAP seus usuários comerciais objeto nuvem usando o logon único e uma conta de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e53-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="76e53-108">Você pode gerenciar suas contas em um local central, Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e53-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="76e53-109">toolearn mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76e53-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76e53-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76e53-110">Prerequisites</span></span>

<span data-ttu-id="76e53-111">tooset a integração do AD do Azure com o SAP Business objeto nuvem, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="76e53-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="76e53-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="76e53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76e53-113">Um SAP Business Object Cloud, com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="76e53-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="76e53-114">Se você testar etapas Olá neste tutorial, é recomendável que você não testá-las em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="76e53-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="76e53-115">Recomendações para testar etapas Olá neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="76e53-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="76e53-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="76e53-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="76e53-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76e53-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76e53-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="76e53-118">Scenario description</span></span>
<span data-ttu-id="76e53-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="76e53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="76e53-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="76e53-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76e53-121">Adicione a nuvem de objeto do SAP Business da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="76e53-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="76e53-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76e53-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="76e53-123">Adicionar a nuvem de objeto do SAP Business da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="76e53-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="76e53-124">tooset a integração de saudação do SAP Business objeto nuvem com o AD do Azure, na Galeria de hello, adicionar lista de tooyour de nuvem de objeto do SAP Business de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="76e53-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76e53-125">Nuvem de objeto do SAP Business da Galeria de saudação do tooadd:</span><span class="sxs-lookup"><span data-stu-id="76e53-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="76e53-126">Em Olá [portal do Azure](https://portal.azure.com), no hello menu à esquerda, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="76e53-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="76e53-128">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="76e53-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![página de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="76e53-130">tooadd um novo aplicativo, selecione **novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="76e53-130">tooadd a new application, select **New application**.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="76e53-132">Na caixa de pesquisa hello, digite **SAP Business objeto nuvem**.</span><span class="sxs-lookup"><span data-stu-id="76e53-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![caixa de pesquisa Olá](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="76e53-134">No painel de resultados de saudação, selecione **SAP Business objeto nuvem**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![Nuvem de objeto do SAP Business na lista de resultados de saudação](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="76e53-136">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="76e53-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="76e53-137">Nesta seção, você vai configurar e testar o logon único do Azure AD com o SAP Business Object Cloud, com base em uma usuária de teste chamada *Brenda Fernandes*.</span><span class="sxs-lookup"><span data-stu-id="76e53-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="76e53-138">Para toowork de logon único, o AD do Azure precisa usuário correspondente do tooknow Olá AD do Azure na nuvem de objeto do SAP Business.</span><span class="sxs-lookup"><span data-stu-id="76e53-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="76e53-139">Uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na nuvem de objeto do SAP Business deve ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="76e53-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="76e53-140">Olá tooestablish referente à relação, na nuvem de objeto do SAP Business, **Username**, atribuir valor Olá Olá **nome de usuário** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e53-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="76e53-141">tooconfigure e teste de logon único do AD do Azure com a nuvem de objeto do SAP Business, Olá concluir tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="76e53-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="76e53-142">[Configurar o logon único do Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="76e53-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="76e53-143">Configura um usuário toouse esse recurso.</span><span class="sxs-lookup"><span data-stu-id="76e53-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="76e53-144">[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="76e53-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="76e53-145">Testes do AD do Azure-logon único com o usuário Olá Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76e53-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="76e53-146">[Criar um usuário de teste do SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="76e53-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="76e53-147">Cria um equivalente de Britta Simon na nuvem de objeto do SAP Business que é vinculado toohello representação do AD do Azure do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="76e53-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="76e53-148">[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="76e53-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="76e53-149">Define o Britta Simon toouse logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e53-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76e53-150">[Testar o logon único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="76e53-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="76e53-151">Verifica que se a configuração de saudação funciona.</span><span class="sxs-lookup"><span data-stu-id="76e53-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="76e53-152">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="76e53-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="76e53-153">Nesta seção, você ativar único do AD do Azure logon no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="76e53-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="76e53-154">Em seguida, configura o logon único no seu aplicativo SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="76e53-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="76e53-155">tooset o AD do Azure-logon único com o SAP Business objeto nuvem:</span><span class="sxs-lookup"><span data-stu-id="76e53-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="76e53-156">Em Olá portal do Azure, Olá **SAP Business objeto nuvem** página de integração de aplicativos, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="76e53-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Selecionar Logon Único][4]

2. <span data-ttu-id="76e53-158">Em Olá **o logon único** página, para **modo**, selecione **baseado no SAML logon**.</span><span class="sxs-lookup"><span data-stu-id="76e53-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Selecionar Logon com base em SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="76e53-160">Em **URLs e domínio de nuvem de objeto do SAP Business**completa Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="76e53-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="76e53-161">Em Olá **URL de logon** caixa, digite uma URL que tenha o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="76e53-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="76e53-162">Em Olá **identificador** caixa, digite uma URL que tenha o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="76e53-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URLs da página Domínio e URLs do SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="76e53-164">valores Hello essas URLs são apenas para demonstração.</span><span class="sxs-lookup"><span data-stu-id="76e53-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="76e53-165">Atualizar valores de saudação com hello real URL de logon URL e o identificador.</span><span class="sxs-lookup"><span data-stu-id="76e53-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="76e53-166">tooget Olá URL de logon, Olá contato [equipe de suporte do SAP Business objeto nuvem Client](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="76e53-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="76e53-167">Você pode obter a URL de identificador Olá baixando metadados da nuvem de objeto do SAP Business de saudação do console de administração de saudação.</span><span class="sxs-lookup"><span data-stu-id="76e53-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="76e53-168">Isso é explicado posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="76e53-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="76e53-169">Em **Certificado de Autenticação SAML**, selecione **XML de Metadados**.</span><span class="sxs-lookup"><span data-stu-id="76e53-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="76e53-170">Em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="76e53-170">Then, save hello metadata file on your computer.</span></span>

    ![Selecionar XML de Metadados](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="76e53-172">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-172">Select **Save**.</span></span>

    ![Selecionar Salvar](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76e53-174">Em uma janela de navegador web diferente, entre no site da empresa tooyour SAP Business objeto nuvem como um administrador.</span><span class="sxs-lookup"><span data-stu-id="76e53-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="76e53-175">Selecione **Menu** > **Sistema** > **Administração**.</span><span class="sxs-lookup"><span data-stu-id="76e53-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Selecionar Menu, Sistema e Administração](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="76e53-177">Em Olá **segurança** guia, selecione Olá **editar** ícone (caneta).</span><span class="sxs-lookup"><span data-stu-id="76e53-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Na guia de segurança hello, selecione o ícone de edição de saudação](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="76e53-179">Para **Método de Autenticação**, selecione **SSO (Logon Único) do SAML**.</span><span class="sxs-lookup"><span data-stu-id="76e53-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Selecione logon único SAML para o método de autenticação Olá](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="76e53-181">toodownload Olá provedor metadados de serviço (etapa 1), selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="76e53-182">No arquivo de metadados de hello, localizar e copiar Olá **entityID** valor.</span><span class="sxs-lookup"><span data-stu-id="76e53-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="76e53-183">Em hello Azure portal em **URLs e domínio de nuvem de objeto do SAP Business**, cole o valor de saudação em Olá **identificador** caixa.</span><span class="sxs-lookup"><span data-stu-id="76e53-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Copie e cole o valor de ID de saudação](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="76e53-185">tooupload Olá provedor metadados de serviço (etapa 2) no arquivo hello baixado do hello portal do Azure, em **metadados do provedor de identidade carregar**, selecione **carregar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Em Fazer upload dos metadados do Provedor de Identidade, selecionar Fazer Upload](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="76e53-187">Em Olá **usuário atributo** lista, o atributo de usuário selecione hello (etapa 3) que você deseja toouse para sua implementação.</span><span class="sxs-lookup"><span data-stu-id="76e53-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="76e53-188">Esse atributo de usuário mapeia toohello provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="76e53-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="76e53-189">tooenter um atributo personalizado na página do usuário hello, use Olá **mapeamento personalizado de SAML** opção.</span><span class="sxs-lookup"><span data-stu-id="76e53-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="76e53-190">Ou, você pode selecionar o **Email** ou **ID de usuário** como atributo de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="76e53-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="76e53-191">Em nosso exemplo, selecionamos **Email** porque Mapeamos Olá declaração do identificador de usuário com hello **userprincipalname** atributo Olá **atributos de usuário** seção Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e53-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="76e53-192">Isso fornece um email exclusivo do usuário, que é enviado toohello aplicativo SAP Business objeto nuvem em cada resposta SAML bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="76e53-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Selecionar Atributo de Usuário](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="76e53-194">conta de saudação tooverify com o provedor de identidade de saudação (etapa 4), em Olá **credencial de logon (Email)** , digite o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="76e53-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="76e53-195">Em seguida, selecione **Verificar Conta**.</span><span class="sxs-lookup"><span data-stu-id="76e53-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="76e53-196">sistema de saudação adiciona a conta de usuário de toohello de credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="76e53-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Inserir email e selecionar Verificar Conta](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="76e53-198">Selecione Olá **salvar** ícone.</span><span class="sxs-lookup"><span data-stu-id="76e53-198">Select hello **Save** icon.</span></span>

    ![Ícone Salvar](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="76e53-200">Você pode ler uma versão concisa essas instruções Olá [portal do Azure](https://portal.azure.com), enquanto você estiver configurando seu aplicativo!</span><span class="sxs-lookup"><span data-stu-id="76e53-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="76e53-201">Depois de adicionar o aplicativo hello selecionando **do Active Directory** > **aplicativos empresariais**, selecione Olá **Single Sign-On** guia. Você pode acessar a documentação Olá inserido em Olá **configuração** seção final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="76e53-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="76e53-202">Para saber mais, confira a [documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="76e53-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="76e53-203">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="76e53-203">Create an Azure AD test user</span></span>
<span data-ttu-id="76e53-204">Nesta seção, você deve criar um usuário de teste chamado Britta Simon no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e53-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="76e53-205">toocreate um usuário de teste no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="76e53-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="76e53-206">No hello portal do Azure, no menu da esquerda hello, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="76e53-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76e53-208">lista de saudação do toodisplay de usuários, selecionados **usuários e grupos**e, em seguida, selecione **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="76e53-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76e53-210">Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76e53-212">Em Olá **usuário** caixa de diálogo, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="76e53-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="76e53-213">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76e53-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="76e53-214">Em Olá **nome de usuário** , digite o endereço de email de saudação do usuário Olá Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76e53-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="76e53-215">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="76e53-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="76e53-216">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-216">Select **Create**.</span></span>

        ![caixa de diálogo de usuário Olá](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Criar um usuário do AD do Azure][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="76e53-219">Criar um usuário de teste do SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="76e53-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="76e53-220">Os usuários do AD do Azure devem ser provisionados no SAP Business objeto nuvem antes que ele possa entrar tooSAP nuvem de objeto de negócios.</span><span class="sxs-lookup"><span data-stu-id="76e53-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="76e53-221">No SAP Business Object Cloud, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="76e53-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="76e53-222">tooprovision uma conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="76e53-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="76e53-223">Entre no tooyour site da empresa de nuvem de objeto do SAP Business como um administrador.</span><span class="sxs-lookup"><span data-stu-id="76e53-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="76e53-224">Selecione **Menu** > **Segurança** > **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="76e53-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="76e53-226">Em Olá **usuários** , tooadd novos detalhes do usuário, selecione  **+** .</span><span class="sxs-lookup"><span data-stu-id="76e53-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Página Adicionar Usuários](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="76e53-228">Em seguida, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="76e53-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="76e53-229">Em Olá **ID de usuário** , digite a ID de usuário de saudação do usuário hello, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="76e53-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="76e53-230">Em Olá **nome** , digite Olá primeiro nome do usuário hello, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="76e53-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="76e53-231">Em Olá **Sobrenome** , digite o sobrenome de saudação do usuário hello, como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="76e53-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="76e53-232">Em Olá **nome de exibição** , digite o nome completo de saudação do usuário hello, como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="76e53-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="76e53-233">Em Olá **email** , digite o endereço de email de saudação do usuário hello, como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="76e53-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="76e53-234">Em Olá **selecionar funções** página, selecione a função apropriada Olá para usuário hello e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="76e53-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Escolher função](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="76e53-236">Selecione Olá **salvar** ícone.</span><span class="sxs-lookup"><span data-stu-id="76e53-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="76e53-237">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="76e53-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="76e53-238">Nesta seção, você permitir que Olá usuário Britta Simon toouse AD do Azure-logon único, concedendo Olá usuário conta acesso tooSAP nuvem de objeto de negócios.</span><span class="sxs-lookup"><span data-stu-id="76e53-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="76e53-239">tooassign Britta Simon tooSAP nuvem de objeto de negócios:</span><span class="sxs-lookup"><span data-stu-id="76e53-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="76e53-240">No portal do Azure de Olá, abrir modo de exibição de aplicativos hello e vá toohello exibição de diretório.</span><span class="sxs-lookup"><span data-stu-id="76e53-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="76e53-241">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="76e53-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="76e53-243">Na lista de aplicativos hello, selecione **SAP Business objeto nuvem**.</span><span class="sxs-lookup"><span data-stu-id="76e53-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="76e53-245">No menu à esquerda do hello, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="76e53-245">In hello left menu, select **Users and groups**.</span></span>

    ![Selecionar Usuários e grupos][202] 

4. <span data-ttu-id="76e53-247">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="76e53-247">Select **Add**.</span></span> <span data-ttu-id="76e53-248">Em seguida, na Olá **Adicionar atribuição** página, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="76e53-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![página de adicionar atribuição Olá][203]

5. <span data-ttu-id="76e53-250">Em Olá **usuários e grupos** página, na lista de saudação de usuários, selecionados **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="76e53-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="76e53-251">Em Olá **usuários e grupos** página, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="76e53-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="76e53-252">Em Olá **Adicionar atribuição** página, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="76e53-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Atribuir função de usuário Olá][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="76e53-254">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="76e53-254">Test single sign-on</span></span>

<span data-ttu-id="76e53-255">Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="76e53-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="76e53-256">Quando você seleciona o bloco de nuvem de objeto do SAP Business Olá no painel de acesso hello, você deve ser conectado automaticamente tooyour aplicativo em nuvem de objeto do SAP Business.</span><span class="sxs-lookup"><span data-stu-id="76e53-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="76e53-257">Para obter mais informações sobre o painel de acesso hello, consulte [painel de acesso Introdução toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76e53-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="76e53-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="76e53-258">Additional resources</span></span>

* [<span data-ttu-id="76e53-259">Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="76e53-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76e53-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="76e53-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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

