---
title: "Tutorial: integração do Azure Active Directory ao AnswerHub | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="92b13-103">Tutorial: Integração do Active Directory do Azure ao AnswerHub</span><span class="sxs-lookup"><span data-stu-id="92b13-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="92b13-104">Neste tutorial, você aprende a integrar o AnswerHub ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="92b13-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92b13-105">A integração do AnswerHub ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="92b13-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92b13-106">No Azure AD, é possível controlar quem tem acesso ao AnswerHub</span><span class="sxs-lookup"><span data-stu-id="92b13-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="92b13-107">É possível permitir que os usuários se conectem automaticamente ao AnswerHub (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b13-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92b13-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92b13-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92b13-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92b13-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92b13-110">Prerequisites</span></span>

<span data-ttu-id="92b13-111">Para configurar a integração do Azure AD ao AnswerHub, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="92b13-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="92b13-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92b13-113">Uma assinatura habilitada para logon único do AnswerHub</span><span class="sxs-lookup"><span data-stu-id="92b13-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92b13-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="92b13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92b13-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="92b13-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92b13-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="92b13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92b13-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92b13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92b13-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="92b13-118">Scenario description</span></span>
<span data-ttu-id="92b13-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="92b13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92b13-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="92b13-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92b13-121">Adicionando o AnswerHub por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="92b13-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="92b13-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="92b13-123">Adicionando o AnswerHub por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="92b13-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="92b13-124">Para configurar a integração do AnswerHub ao Azure AD, você precisa adicionar o AnswerHub à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="92b13-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92b13-125">**Para adicionar o AnswerHub por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="92b13-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92b13-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92b13-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92b13-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="92b13-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92b13-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="92b13-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="92b13-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92b13-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="92b13-133">Na caixa de pesquisa, digite **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="92b13-133">In the search box, type **AnswerHub**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="92b13-135">No painel de resultados, selecione **AnswerHub** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92b13-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92b13-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92b13-138">Nesta seção, você configura e testa o logon único do Azure AD com o AnswerHub, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="92b13-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92b13-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do AnswerHub é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b13-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="92b13-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="92b13-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="92b13-141">No AnswerHub, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="92b13-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92b13-142">Para configurar e testar o logon único do Azure AD com o AnswerHub, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="92b13-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92b13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="92b13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92b13-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="92b13-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92b13-145">**[Criando um usuário de teste do AnswerHub](#creating-an-answerhub-test-user)** – para ter um equivalente de Brenda Fernandes no AnswerHub que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b13-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92b13-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="92b13-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92b13-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="92b13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92b13-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b13-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92b13-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="92b13-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="92b13-150">**Para configurar o logon único do Azure AD com o AnswerHub, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="92b13-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="92b13-151">No portal do Azure, na página de integração do aplicativo do **AnswerHub**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="92b13-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="92b13-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="92b13-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="92b13-155">Na seção **Domínio e URLs do AnswerHub**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="92b13-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="92b13-157">a.</span><span class="sxs-lookup"><span data-stu-id="92b13-157">a.</span></span> <span data-ttu-id="92b13-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="92b13-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="92b13-159">b.</span><span class="sxs-lookup"><span data-stu-id="92b13-159">b.</span></span> <span data-ttu-id="92b13-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="92b13-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92b13-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="92b13-161">These values are not real.</span></span> <span data-ttu-id="92b13-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="92b13-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92b13-163">Contate a [equipe de suporte ao Cliente do AnswerHub](mailto:success@answerhub.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="92b13-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="92b13-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="92b13-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="92b13-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="92b13-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92b13-168">Na seção **Configuração do AnswerHub**, clique em **Configurar o AnswerHub** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="92b13-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="92b13-169">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="92b13-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="92b13-171">Em outra janela do navegador da Web, faça logon em seu site de empresa AnswerHub como um administrador.</span><span class="sxs-lookup"><span data-stu-id="92b13-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="92b13-172">Se você precisar de ajuda para configurar o AnswerHub, entre em contato com a [equipe de suporte do AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="92b13-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="92b13-173">Vá para **Administração**.</span><span class="sxs-lookup"><span data-stu-id="92b13-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="92b13-174">Clique na guia **Usuário e Grupo** .</span><span class="sxs-lookup"><span data-stu-id="92b13-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="92b13-175">No painel de navegação à esquerda, na seção **Configurações Sociais**, clique em **Configuração do SAML**.</span><span class="sxs-lookup"><span data-stu-id="92b13-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="92b13-176">Clique na guia **Config. de IDP** .</span><span class="sxs-lookup"><span data-stu-id="92b13-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="92b13-177">Na guia **Config. de IDP** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="92b13-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="92b13-178">![Instalação do SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Instalação do SAML")</span><span class="sxs-lookup"><span data-stu-id="92b13-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="92b13-179">a.</span><span class="sxs-lookup"><span data-stu-id="92b13-179">a.</span></span> <span data-ttu-id="92b13-180">Na caixa de texto **URL de Logon do IDP**, cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92b13-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="92b13-181">b.</span><span class="sxs-lookup"><span data-stu-id="92b13-181">b.</span></span> <span data-ttu-id="92b13-182">Na caixa de texto **URL de Logoff do IDP**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92b13-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="92b13-183">c.</span><span class="sxs-lookup"><span data-stu-id="92b13-183">c.</span></span> <span data-ttu-id="92b13-184">Na caixa de texto **Formato do Identificador de Nome do IDP**, insira o mesmo valor de Identificador de usuário selecionado no portal do Azure na seção **Atributos de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="92b13-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="92b13-185">d.</span><span class="sxs-lookup"><span data-stu-id="92b13-185">d.</span></span> <span data-ttu-id="92b13-186">Clique em **Chaves e Certificados**.</span><span class="sxs-lookup"><span data-stu-id="92b13-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="92b13-187">Na guia Chaves e Certificados, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="92b13-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="92b13-188">![Chaves e Certificados](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Chaves e Certificados")</span><span class="sxs-lookup"><span data-stu-id="92b13-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="92b13-189">a.</span><span class="sxs-lookup"><span data-stu-id="92b13-189">a.</span></span> <span data-ttu-id="92b13-190">Abra o certificado codificado em Base 64 baixado no portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Chave Pública do IDP (Formato x509)**.</span><span class="sxs-lookup"><span data-stu-id="92b13-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="92b13-191">b.</span><span class="sxs-lookup"><span data-stu-id="92b13-191">b.</span></span> <span data-ttu-id="92b13-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="92b13-192">Click **Save**.</span></span>

14. <span data-ttu-id="92b13-193">Na guia **Config. de IDP**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="92b13-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="92b13-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="92b13-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92b13-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="92b13-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92b13-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92b13-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92b13-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="92b13-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="92b13-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="92b13-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="92b13-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92b13-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92b13-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92b13-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="92b13-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92b13-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92b13-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92b13-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="92b13-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92b13-209">a.</span><span class="sxs-lookup"><span data-stu-id="92b13-209">a.</span></span> <span data-ttu-id="92b13-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="92b13-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92b13-211">b.</span><span class="sxs-lookup"><span data-stu-id="92b13-211">b.</span></span> <span data-ttu-id="92b13-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="92b13-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92b13-213">c.</span><span class="sxs-lookup"><span data-stu-id="92b13-213">c.</span></span> <span data-ttu-id="92b13-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="92b13-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92b13-215">d.</span><span class="sxs-lookup"><span data-stu-id="92b13-215">d.</span></span> <span data-ttu-id="92b13-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="92b13-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="92b13-217">Criando um usuário de teste do AnswerHub</span><span class="sxs-lookup"><span data-stu-id="92b13-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="92b13-218">Para permitir que os usuários do Azure AD façam logon no AnswerHub, eles devem ser provisionados no AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="92b13-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="92b13-219">No caso do AnswerHub, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="92b13-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="92b13-220">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="92b13-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="92b13-221">Faça logon em seu site de empresa do **AnswerHub** como administrador.</span><span class="sxs-lookup"><span data-stu-id="92b13-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="92b13-222">Vá para **Administração**.</span><span class="sxs-lookup"><span data-stu-id="92b13-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="92b13-223">Clique na guia **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="92b13-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="92b13-224">No painel de navegação à esquerda, na seção **Gerenciar Usuários**, clique em **Criar ou importar usuários**.</span><span class="sxs-lookup"><span data-stu-id="92b13-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="92b13-225">![Usuários e Grupos](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Usuários e Grupos")</span><span class="sxs-lookup"><span data-stu-id="92b13-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="92b13-226">Digite **Endereço de email**, **Nome de usuário** e **Senha** de uma conta válida do Active Directory do Azure que você deseja provisionar nas caixas de texto relacionadas e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="92b13-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="92b13-227">É possível usar qualquer outra ferramenta de criação da conta de usuário do AnswerHub ou as APIs fornecidas pelo AnswerHub para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="92b13-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92b13-228">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92b13-229">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="92b13-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="92b13-231">**Para atribuir Brenda Fernandes ao AnswerHub, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="92b13-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="92b13-232">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="92b13-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="92b13-234">Na lista de aplicativos, selecione **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="92b13-234">In the applications list, select **AnswerHub**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="92b13-236">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="92b13-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="92b13-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="92b13-238">Click **Add** button.</span></span> <span data-ttu-id="92b13-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92b13-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="92b13-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="92b13-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92b13-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92b13-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92b13-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92b13-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92b13-244">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="92b13-244">Testing single sign-on</span></span>

<span data-ttu-id="92b13-245">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="92b13-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92b13-246">Quando você clicar no bloco AnswerHub no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="92b13-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="92b13-247">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92b13-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92b13-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="92b13-248">Additional resources</span></span>

* [<span data-ttu-id="92b13-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="92b13-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92b13-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92b13-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

