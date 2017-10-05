---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Workplace by Facebook."
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
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="26512-103">Tutorial: Integração do Azure Active Directory com o Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="26512-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="26512-104">Neste tutorial, você aprenderá a integrar o Workplace by Facebook ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="26512-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26512-105">A integração do Workplace by Facebook ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="26512-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26512-106">No Azure AD, você pode controlar quem tem acesso ao Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="26512-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="26512-107">Você pode habilitar o logon automático de seus usuários no Workplace by Facebook (Logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26512-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26512-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="26512-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26512-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26512-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26512-110">Prerequisites</span></span>

<span data-ttu-id="26512-111">Para configurar a integração do Azure AD com o Workplace by Facebook, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="26512-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="26512-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26512-113">Uma assinatura do Workplace by Facebook habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="26512-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26512-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="26512-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26512-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="26512-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26512-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="26512-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26512-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26512-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26512-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="26512-118">Scenario description</span></span>
<span data-ttu-id="26512-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="26512-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26512-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="26512-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26512-121">Adicionar o Workplace by Facebook da Galeria</span><span class="sxs-lookup"><span data-stu-id="26512-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="26512-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="26512-123">Adicionar o Workplace by Facebook da Galeria</span><span class="sxs-lookup"><span data-stu-id="26512-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="26512-124">Para configurar a integração do Workplace by Facebook ao Azure AD, você precisa adicionar o Workplace by Facebook da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="26512-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26512-125">**Para adicionar o Workplace by Facebook da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26512-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26512-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26512-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26512-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="26512-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26512-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="26512-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="26512-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26512-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="26512-133">Na caixa de pesquisa, digite **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="26512-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="26512-135">No painel de resultados, selecione **Workplace by Facebook** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26512-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26512-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26512-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Workplace by Facebook, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="26512-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="26512-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Workplace by Facebook é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26512-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="26512-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="26512-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="26512-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="26512-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="26512-142">Para configurar e testar o logon único do Azure AD com o Workplace by Facebook, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="26512-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26512-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="26512-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26512-144">**[Configurando a frequência de reautenticação](#configuring-reauthentication-frequency)** – para configurar o Workplace para solicitar uma verificação SAML.</span><span class="sxs-lookup"><span data-stu-id="26512-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="26512-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26512-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="26512-146">**[Criação de um usuário de teste do Workplace by Facebook](#creating-a-workplace-by-facebook-test-user)** – para ter um equivalente de Brenda Fernandes no Workplace by Facebook que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26512-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="26512-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="26512-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="26512-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="26512-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26512-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26512-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26512-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="26512-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="26512-151">**Para configurar o logon único do Azure AD com o Workplace by Facebook, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26512-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="26512-152">No Portal do Azure, na página de integração de aplicativos do **Workplace by Facebook**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="26512-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="26512-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="26512-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="26512-156">Na seção **Domínio e URLs do Workplace by Facebook**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26512-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="26512-158">a.</span><span class="sxs-lookup"><span data-stu-id="26512-158">a.</span></span> <span data-ttu-id="26512-159">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="26512-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="26512-160">b.</span><span class="sxs-lookup"><span data-stu-id="26512-160">b.</span></span> <span data-ttu-id="26512-161">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="26512-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26512-162">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="26512-162">These values are not the real.</span></span> <span data-ttu-id="26512-163">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="26512-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="26512-164">Contate a [equipe de suporte ao Cliente do Workplace by Facebook](https://workplace.fb.com/faq/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="26512-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="26512-165">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="26512-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="26512-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="26512-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26512-169">Na seção **Configuração do Workplace by Facebook**, clique em **Configurar o Workplace by Facebook** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="26512-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="26512-170">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="26512-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="26512-172">Em outra janela do navegador da Web, faça logon em seu site de empresa do Workplace by Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="26512-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="26512-173">Como parte do processo de autenticação SAML, o Workplace poderá utilizar cadeias de consulta de até 2,5 quilobytes para passar parâmetros para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26512-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="26512-174">No **Painel da Empresa**, acesse a guia **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="26512-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="26512-175">Em **Autenticação SAML**, selecione **Somente SSO** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="26512-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="26512-176">Insira os valores copiados na seção **Configuração do Workplace by Facebook** do Portal do Azure nos campos correspondentes:</span><span class="sxs-lookup"><span data-stu-id="26512-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="26512-177">Na caixa de texto **URL de SAML**, cole o valor da **URL do Serviço de Logon Único** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26512-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="26512-178">Na caixa de texto **URL do Emissor SAML**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26512-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="26512-179">Em **Redirecionamento de Logoff SAML** (Opcional), cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26512-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="26512-180">Abra o **Certificado codificado em Base64** no bloco de notas baixado do Portal do Azure, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado SAML**.</span><span class="sxs-lookup"><span data-stu-id="26512-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="26512-181">Talvez seja necessário inserir uma URL do Público-Alvo, uma URL do Destinatário e uma URL do ACS (Serviço do Consumidor de Declaração) listadas na seção **Configuração do SAML**.</span><span class="sxs-lookup"><span data-stu-id="26512-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="26512-182">Role até o final da seção e clique no botão **Testar SSO**.</span><span class="sxs-lookup"><span data-stu-id="26512-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="26512-183">Isso resultará na exibição de uma janela pop-up com a página de logon do Azure AD apresentada.</span><span class="sxs-lookup"><span data-stu-id="26512-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="26512-184">Insira suas credenciais como de costume para se autenticar.</span><span class="sxs-lookup"><span data-stu-id="26512-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="26512-185">**Solução de problemas:** verifique se o endereço de email retornado do Azure AD é o mesmo da conta do Workplace com a qual você está conectado.</span><span class="sxs-lookup"><span data-stu-id="26512-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="26512-186">Depois que o teste for concluído com êxito, role até a parte inferior da página e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="26512-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="26512-187">Agora, todos os usuários que usam o Workplace verão a página de logon do Azure AD para autenticação.</span><span class="sxs-lookup"><span data-stu-id="26512-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="26512-188">**Redirecionamento de Logoff SAML (opcional)** -</span><span class="sxs-lookup"><span data-stu-id="26512-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="26512-189">Você pode optar por configurar uma URL de Logoff SAML, que pode ser usada para apontar para a página de logoff do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26512-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="26512-190">Quando essa configuração for habilitada e configurada, o usuário não será mais direcionado para a página de logoff do Workplace.</span><span class="sxs-lookup"><span data-stu-id="26512-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="26512-191">Em vez disso, o usuário será redirecionado para a URL que foi adicionada à configuração Redirecionamento de Logoff SAML.</span><span class="sxs-lookup"><span data-stu-id="26512-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="26512-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="26512-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26512-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="26512-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26512-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26512-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="26512-195">Configurando a frequência de reautenticação</span><span class="sxs-lookup"><span data-stu-id="26512-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="26512-196">É possível configurar o Workplace para solicitar uma verificação SAML todos os dias, a cada três dias, toda semana, a cada duas semanas, todos os meses ou nunca.</span><span class="sxs-lookup"><span data-stu-id="26512-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="26512-197">O valor mínimo para a verificação SAML em aplicativos móveis é definido como uma semana.</span><span class="sxs-lookup"><span data-stu-id="26512-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="26512-198">Você também pode forçar uma redefinição SAML para todos os usuários usando o botão Exigir autenticação SAML para todos os usuários agora.</span><span class="sxs-lookup"><span data-stu-id="26512-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26512-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="26512-200">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26512-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="26512-202">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26512-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26512-203">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26512-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26512-205">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="26512-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26512-207">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26512-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26512-209">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26512-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26512-211">a.</span><span class="sxs-lookup"><span data-stu-id="26512-211">a.</span></span> <span data-ttu-id="26512-212">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="26512-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26512-213">b.</span><span class="sxs-lookup"><span data-stu-id="26512-213">b.</span></span> <span data-ttu-id="26512-214">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26512-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26512-215">c.</span><span class="sxs-lookup"><span data-stu-id="26512-215">c.</span></span> <span data-ttu-id="26512-216">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="26512-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="26512-217">d.</span><span class="sxs-lookup"><span data-stu-id="26512-217">d.</span></span> <span data-ttu-id="26512-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="26512-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="26512-219">Criação de um usuário de teste do Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="26512-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="26512-220">Nesta seção, um usuário chamado Brenda Fernandes será criado no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="26512-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="26512-221">O Workplace by Facebook dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="26512-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="26512-222">Não há nenhuma ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="26512-222">There is no action for you in this section.</span></span> <span data-ttu-id="26512-223">Se um usuário ainda não existir no Workplace by Facebook, um novo será criado quando você tentar acessar o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="26512-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="26512-224">Se você precisar criar um usuário manualmente, contate a [equipe de suporte ao Cliente do Workplace by Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="26512-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="26512-225">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="26512-226">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="26512-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="26512-228">**Para atribuir Brenda Fernandes ao Workplace by Facebook, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26512-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="26512-229">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="26512-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="26512-231">Na lista de aplicativos, selecione **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="26512-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="26512-233">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="26512-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="26512-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="26512-235">Click **Add** button.</span></span> <span data-ttu-id="26512-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26512-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="26512-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="26512-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26512-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26512-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26512-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26512-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26512-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="26512-241">Testing single sign-on</span></span>

<span data-ttu-id="26512-242">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="26512-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="26512-243">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26512-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="26512-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="26512-244">Additional resources</span></span>

* [<span data-ttu-id="26512-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="26512-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26512-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26512-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="26512-247">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="26512-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



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

