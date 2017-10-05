---
title: "Tutorial: Integração do Azure Active Directory com o TeamSeer | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="4b350-103">Tutorial: Integração do Active Directory do Azure ao TeamSeer</span><span class="sxs-lookup"><span data-stu-id="4b350-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="4b350-104">Neste tutorial, você aprenderá a integrar o TeamSeer ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4b350-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b350-105">A integração do TeamSeer ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4b350-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b350-106">No Azure AD, é possível controlar quem tem acesso ao TeamSeer</span><span class="sxs-lookup"><span data-stu-id="4b350-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="4b350-107">Você pode permitir que seus usuários façam logon automaticamente no TeamSeer (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="4b350-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b350-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b350-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b350-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b350-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b350-110">Prerequisites</span></span>

<span data-ttu-id="4b350-111">Para configurar a integração do Azure AD ao TeamSeer, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4b350-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="4b350-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b350-113">Uma assinatura habilitada para logon único do TeamSeer</span><span class="sxs-lookup"><span data-stu-id="4b350-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b350-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b350-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b350-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4b350-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b350-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4b350-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b350-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b350-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b350-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4b350-118">Scenario description</span></span>
<span data-ttu-id="4b350-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b350-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b350-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4b350-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b350-121">Adicionar o TeamSeer da galeria</span><span class="sxs-lookup"><span data-stu-id="4b350-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="4b350-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="4b350-123">Adicionar o TeamSeer da galeria</span><span class="sxs-lookup"><span data-stu-id="4b350-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="4b350-124">Para configurar a integração do TeamSeer ao Azure AD, você precisará adicionar o TeamSeer por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4b350-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b350-125">**Para adicionar o TeamSeer da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b350-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b350-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b350-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b350-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4b350-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b350-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b350-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4b350-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b350-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4b350-133">Na caixa de pesquisa, digite **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="4b350-133">In the search box, type **TeamSeer**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="4b350-135">No painel de resultados, selecione **TeamSeer** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b350-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b350-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b350-138">Nesta seção, você configurará e testará o logon único do Azure AD com o TeamSeer, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4b350-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b350-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do TeamSeer é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b350-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="4b350-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="4b350-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="4b350-141">No TeamSeer, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4b350-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b350-142">Para configurar e testar o logon único do Azure AD com o TeamSeer, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4b350-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b350-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4b350-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b350-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b350-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b350-145">**[Criação de um usuário de teste do TeamSeer](#creating-a-teamseer-test-user)** – para ter um equivalente de Brenda Fernandes no TeamSeer que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b350-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b350-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b350-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b350-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4b350-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b350-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b350-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b350-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="4b350-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="4b350-150">**Para configurar o logon único do Azure AD com o TeamSeer, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b350-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="4b350-151">No portal do Azure, na página de integração de aplicativos do **TeamSeer**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4b350-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4b350-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4b350-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="4b350-155">Na seção **URLs e Domínio do TeamSeer**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b350-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="4b350-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="4b350-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b350-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="4b350-158">The value is not real.</span></span> <span data-ttu-id="4b350-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="4b350-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="4b350-160">Contate a [equipe de suporte ao cliente do TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="4b350-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="4b350-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="4b350-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="4b350-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4b350-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b350-165">Na seção **Configuração do TeamSeer**, clique em **Configurar o TeamSeer** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4b350-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b350-166">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4b350-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="4b350-168">Em outra janela do navegador da Web, faça logon em seu site de empresa TeamSeer como um administrador.</span><span class="sxs-lookup"><span data-stu-id="4b350-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="4b350-169">Vá para **Administrador de RH**.</span><span class="sxs-lookup"><span data-stu-id="4b350-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="4b350-170">![Administrador de RH](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Administrador de RH")</span><span class="sxs-lookup"><span data-stu-id="4b350-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="4b350-171">Clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="4b350-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="4b350-172">![Configuração](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="4b350-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="4b350-173">Clique em **Configurar detalhes do provedor de SAML**.</span><span class="sxs-lookup"><span data-stu-id="4b350-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="4b350-174">![Configurações do SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="4b350-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="4b350-175">Na seção de detalhes do provedor de SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b350-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="4b350-176">![Configurações do SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="4b350-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="4b350-177">a.</span><span class="sxs-lookup"><span data-stu-id="4b350-177">a.</span></span> <span data-ttu-id="4b350-178">Cole o valor da **URL do Serviço de Logon Único** na caixa de texto **URL**.</span><span class="sxs-lookup"><span data-stu-id="4b350-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="4b350-179">b.</span><span class="sxs-lookup"><span data-stu-id="4b350-179">b.</span></span> <span data-ttu-id="4b350-180">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado Público do IdP**.</span><span class="sxs-lookup"><span data-stu-id="4b350-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="4b350-181">Para concluir a configuração do provedor de SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b350-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="4b350-182">![Configurações do SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="4b350-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="4b350-183">a.</span><span class="sxs-lookup"><span data-stu-id="4b350-183">a.</span></span> <span data-ttu-id="4b350-184">Nos **Endereços de Email de Teste**, digite o endereço de email do usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="4b350-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="4b350-185">b.</span><span class="sxs-lookup"><span data-stu-id="4b350-185">b.</span></span> <span data-ttu-id="4b350-186">Na caixa de texto **Emissor** , digite a URL do Emissor do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="4b350-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="4b350-187">c.</span><span class="sxs-lookup"><span data-stu-id="4b350-187">c.</span></span> <span data-ttu-id="4b350-188">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4b350-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4b350-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4b350-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b350-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4b350-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b350-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b350-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b350-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b350-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b350-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4b350-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b350-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b350-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b350-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b350-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4b350-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b350-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b350-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b350-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b350-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b350-204">a.</span><span class="sxs-lookup"><span data-stu-id="4b350-204">a.</span></span> <span data-ttu-id="4b350-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4b350-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b350-206">b.</span><span class="sxs-lookup"><span data-stu-id="4b350-206">b.</span></span> <span data-ttu-id="4b350-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b350-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b350-208">c.</span><span class="sxs-lookup"><span data-stu-id="4b350-208">c.</span></span> <span data-ttu-id="4b350-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4b350-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b350-210">d.</span><span class="sxs-lookup"><span data-stu-id="4b350-210">d.</span></span> <span data-ttu-id="4b350-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4b350-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="4b350-212">Criar um usuário de teste do TeamSeer</span><span class="sxs-lookup"><span data-stu-id="4b350-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="4b350-213">Para permitir que os usuários do Azure AD façam logon no TeamSeer, eles deverão ser provisionados no ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="4b350-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="4b350-214">No caso do TeamSeer, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4b350-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="4b350-215">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b350-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4b350-216">Faça logon em seu site de empresa do **TeamSeer** como administrador.</span><span class="sxs-lookup"><span data-stu-id="4b350-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="4b350-217">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b350-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="4b350-218">![Administrador de RH](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Administrador de RH")</span><span class="sxs-lookup"><span data-stu-id="4b350-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="4b350-219">a.</span><span class="sxs-lookup"><span data-stu-id="4b350-219">a.</span></span> <span data-ttu-id="4b350-220">Vá para **Administrador de RH \> Usuários**.</span><span class="sxs-lookup"><span data-stu-id="4b350-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="4b350-221">b.</span><span class="sxs-lookup"><span data-stu-id="4b350-221">b.</span></span> <span data-ttu-id="4b350-222">Clique em **Executar o assistente de Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4b350-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="4b350-223">Na seção **Detalhes do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b350-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="4b350-224">![Detalhes do Usuário](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Detalhes do Usuário")</span><span class="sxs-lookup"><span data-stu-id="4b350-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="4b350-225">a.</span><span class="sxs-lookup"><span data-stu-id="4b350-225">a.</span></span> <span data-ttu-id="4b350-226">Digite o **Nome**, **Sobrenome** e **Nome de usuário (Endereço de email)** de uma conta válida do AAD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="4b350-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="4b350-227">b.</span><span class="sxs-lookup"><span data-stu-id="4b350-227">b.</span></span> <span data-ttu-id="4b350-228">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4b350-228">Click **Next**.</span></span>

4. <span data-ttu-id="4b350-229">Siga as instruções na tela para adicionar um novo usuário e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4b350-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="4b350-230">Você pode usar qualquer outra ferramenta de criação da conta de usuário do TeamSeer ou APIs fornecidas pelo TeamSeer para provisionar as contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b350-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b350-231">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b350-232">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="4b350-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4b350-234">**Para atribuir Brenda Fernandes ao TeamSeer, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b350-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="4b350-235">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b350-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4b350-237">Na lista de aplicativos, selecione **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="4b350-237">In the applications list, select **TeamSeer**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="4b350-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b350-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4b350-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4b350-241">Click **Add** button.</span></span> <span data-ttu-id="4b350-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b350-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4b350-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4b350-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b350-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b350-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b350-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b350-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b350-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4b350-247">Testing single sign-on</span></span>

<span data-ttu-id="4b350-248">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4b350-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="4b350-249">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b350-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b350-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4b350-250">Additional resources</span></span>

* [<span data-ttu-id="4b350-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4b350-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b350-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b350-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

