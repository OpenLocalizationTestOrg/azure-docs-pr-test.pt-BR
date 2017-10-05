---
title: "Tutorial: integração do Azure Active Directory ao FreshGrade | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="2f139-103">Tutorial: Integração do Active Directory do Azure ao FreshGrade</span><span class="sxs-lookup"><span data-stu-id="2f139-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="2f139-104">Neste tutorial, você aprenderá a integrar o FreshGrade ao Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2f139-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f139-105">A integração do FreshGrade ao AD do Azure oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2f139-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f139-106">No Azure AD, é possível controlar quem tem acesso ao FreshGrade</span><span class="sxs-lookup"><span data-stu-id="2f139-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="2f139-107">É possível permitir que os usuários se conectem automaticamente ao FreshGrade (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f139-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f139-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f139-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f139-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f139-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f139-110">Prerequisites</span></span>

<span data-ttu-id="2f139-111">Para configurar a integração do AD do Azure ao FreshGrade, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2f139-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="2f139-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f139-113">Uma assinatura habilitada para logon único do FreshGrade</span><span class="sxs-lookup"><span data-stu-id="2f139-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f139-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2f139-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f139-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2f139-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f139-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2f139-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f139-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f139-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f139-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2f139-118">Scenario description</span></span>
<span data-ttu-id="2f139-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2f139-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f139-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2f139-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f139-121">Adicionar FreshGrade da galeria</span><span class="sxs-lookup"><span data-stu-id="2f139-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="2f139-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="2f139-123">Adicionar FreshGrade da galeria</span><span class="sxs-lookup"><span data-stu-id="2f139-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="2f139-124">Para configurar a integração do FreshGrade com o AD do Azure, você precisará adicionar o FreshGrade à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="2f139-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f139-125">**Para adicionar o FreshGrade por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2f139-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f139-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f139-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f139-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2f139-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f139-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f139-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2f139-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f139-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2f139-133">Na caixa de pesquisa, digite **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="2f139-133">In the search box, type **FreshGrade**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="2f139-135">No painel de resultados, selecione **FreshGrade** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f139-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f139-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f139-138">Nesta seção, você configurará e testará o logon único do AD do Azure com o FreshGrade, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2f139-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f139-139">Para que o logon único funcione, o AD do Azure precisa saber qual usuário do FreshGrade é equivalente a um usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f139-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="2f139-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado do FreshGradey.</span><span class="sxs-lookup"><span data-stu-id="2f139-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="2f139-141">No FreshGrade, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="2f139-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f139-142">Para configurar e testar o logon único do AD do Azure com o FreshGrade, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2f139-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f139-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2f139-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f139-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2f139-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f139-145">**[Criando um usuário de teste do FreshGrade](#creating-a-freshgrade-test-user)** – para ter um equivalente de Brenda Fernandes no FreshGrade que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f139-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f139-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f139-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f139-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2f139-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f139-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f139-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f139-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2f139-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="2f139-150">**Para configurar o logon único do AD do Azure com o FreshGrade, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2f139-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="2f139-151">No portal do Azure, na página de integração do aplicativo **FreshGrade**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2f139-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2f139-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2f139-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="2f139-155">Na seção **Domínio e URLs do FreshGrade**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2f139-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="2f139-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f139-157">a.</span></span> <span data-ttu-id="2f139-158">Na caixa de texto **URL de Logon**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="2f139-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="2f139-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f139-159">b.</span></span> <span data-ttu-id="2f139-160">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="2f139-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="2f139-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="2f139-161">These values are not real.</span></span> <span data-ttu-id="2f139-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="2f139-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2f139-163">Contate a [equipe de suporte ao Cliente do FreshGrade](mailTo:support@freshgrade.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="2f139-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="2f139-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2f139-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="2f139-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2f139-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f139-168">Na seção **Configuração do FreshGrade**, clique em **Configurar o FreshGrade** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="2f139-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f139-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="2f139-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="2f139-171">Para gerar a URL de **Metadados**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2f139-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="2f139-172">a.</span><span class="sxs-lookup"><span data-stu-id="2f139-172">a.</span></span> <span data-ttu-id="2f139-173">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="2f139-173">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="2f139-175">b.</span><span class="sxs-lookup"><span data-stu-id="2f139-175">b.</span></span> <span data-ttu-id="2f139-176">Clique em **Pontos de extremidade** para abrir a caixa de diálogo **Pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="2f139-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="2f139-178">c.</span><span class="sxs-lookup"><span data-stu-id="2f139-178">c.</span></span> <span data-ttu-id="2f139-179">Clique no botão copiar para copiar a URL **DOCUMENTO DE METADADOS DE FEDERAÇÃO** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="2f139-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="2f139-181">d.</span><span class="sxs-lookup"><span data-stu-id="2f139-181">d.</span></span> <span data-ttu-id="2f139-182">Agora, acesse a página de propriedades do **FreshGrade** e copie a **ID do Aplicativo** usando o botão **Copiar** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="2f139-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="2f139-184">e.</span><span class="sxs-lookup"><span data-stu-id="2f139-184">e.</span></span> <span data-ttu-id="2f139-185">Gere a **URL de Metadados** usando o padrão a seguir: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="2f139-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="2f139-186">Para configurar o logon único no lado do **FreshGrade**, é necessário enviar a **URL de Metadados** e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="2f139-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="2f139-187">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="2f139-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2f139-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="2f139-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f139-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2f139-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f139-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f139-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f139-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f139-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2f139-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2f139-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2f139-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f139-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f139-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f139-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2f139-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f139-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f139-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f139-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2f139-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f139-203">a.</span><span class="sxs-lookup"><span data-stu-id="2f139-203">a.</span></span> <span data-ttu-id="2f139-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2f139-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f139-205">b.</span><span class="sxs-lookup"><span data-stu-id="2f139-205">b.</span></span> <span data-ttu-id="2f139-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2f139-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f139-207">c.</span><span class="sxs-lookup"><span data-stu-id="2f139-207">c.</span></span> <span data-ttu-id="2f139-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2f139-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f139-209">d.</span><span class="sxs-lookup"><span data-stu-id="2f139-209">d.</span></span> <span data-ttu-id="2f139-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2f139-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="2f139-211">Criação de um usuário de teste FreshGrade</span><span class="sxs-lookup"><span data-stu-id="2f139-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="2f139-212">Nesta seção, você criará uma usuária chamado Brenda Fernandes no FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2f139-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="2f139-213">Trabalhe com a [equipe de suporte do FreshGrade](mailTo:support@freshgrade.com) para adicionar os usuários à plataforma FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2f139-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f139-214">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f139-215">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2f139-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2f139-217">**Para atribuir Brenda Fernandes ao FreshGrade, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2f139-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="2f139-218">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f139-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2f139-220">Na lista de aplicativos, escolha **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="2f139-220">In the applications list, select **FreshGrade**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="2f139-222">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2f139-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2f139-224">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2f139-224">Click **Add** button.</span></span> <span data-ttu-id="2f139-225">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f139-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2f139-227">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2f139-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f139-228">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f139-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f139-229">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f139-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f139-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2f139-230">Testing single sign-on</span></span>

<span data-ttu-id="2f139-231">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2f139-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f139-232">Ao clicar no bloco do FreshGrade no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2f139-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="2f139-233">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f139-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f139-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2f139-234">Additional resources</span></span>

* [<span data-ttu-id="2f139-235">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2f139-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f139-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f139-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

