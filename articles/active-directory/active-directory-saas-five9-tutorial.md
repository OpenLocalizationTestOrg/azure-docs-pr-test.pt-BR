---
title: "Tutorial: Integração do Azure Active Directory ao Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Five9 Plus Adapter (CTI, Contact Center Agents)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: d75163ea5eb3fa811e07861f06e6c4d5c758b898
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="19aa8-103">Tutorial: Integração do Azure Active Directory ao Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="19aa8-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="19aa8-104">Neste tutorial, você aprende a integrar o Five9 Plus Adapter (CTI, Contact Center Agents) ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="19aa8-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19aa8-105">A integração do Five9 Plus Adapter (CTI, Contact Center Agents) ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="19aa8-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="19aa8-106">No Azure AD, é possível controlar quem tem acesso ao Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="19aa8-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="19aa8-107">É possível permitir que os usuários se conectem automaticamente ao Five9 Plus Adapter (CTI, Contact Center Agents) (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="19aa8-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19aa8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="19aa8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19aa8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19aa8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="19aa8-110">Prerequisites</span></span>

<span data-ttu-id="19aa8-111">Para configurar a integração do Azure AD ao Five9 Plus Adapter (CTI, Contact Center Agents), você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="19aa8-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span></span>

- <span data-ttu-id="19aa8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19aa8-113">Uma assinatura habilitada para logon único do Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="19aa8-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19aa8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="19aa8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19aa8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="19aa8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19aa8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="19aa8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19aa8-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19aa8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19aa8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="19aa8-118">Scenario description</span></span>
<span data-ttu-id="19aa8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="19aa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19aa8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="19aa8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19aa8-121">Adicionando o Five9 Plus Adapter (CTI, Contact Center Agents) por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="19aa8-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
2. <span data-ttu-id="19aa8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a><span data-ttu-id="19aa8-123">Adicionando o Five9 Plus Adapter (CTI, Contact Center Agents) por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="19aa8-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
<span data-ttu-id="19aa8-124">Para configurar a integração do Five9 Plus Adapter (CTI, Contact Center Agents) ao Azure AD, é necessário adicionar o Five9 Plus Adapter (CTI, Contact Center Agents) à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="19aa8-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="19aa8-125">**Para adicionar o Five9 Plus Adapter (CTI, Contact Center Agents) por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19aa8-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="19aa8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19aa8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="19aa8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="19aa8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="19aa8-133">Na caixa de pesquisa, digite **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="19aa8-135">No painel de resultados, selecione **Five9 Plus Adapter (CTI, Contact Center Agents)** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19aa8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19aa8-138">Nesta seção, você configura e testa o logon único do Azure AD com o Five9 Plus Adapter (CTI, Contact Center Agents), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="19aa8-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19aa8-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Five9 Plus Adapter (CTI, Contact Center Agents) é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19aa8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span></span> <span data-ttu-id="19aa8-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="19aa8-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span></span>

<span data-ttu-id="19aa8-141">No Five9 Plus Adapter (CTI, Contact Center Agents), atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="19aa8-142">Para configurar e testar o logon único do Azure AD com o Five9 Plus Adapter (CTI, Contact Center Agents), você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="19aa8-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="19aa8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="19aa8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="19aa8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="19aa8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19aa8-145">**[Criando um usuário de teste do Five9 Plus Adapter (CTI, Contact Center Agents)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** – para ter um equivalente de Brenda Fernandes no Five9 Plus Adapter (CTI, Contact Center Agents) que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19aa8-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="19aa8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="19aa8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19aa8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="19aa8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19aa8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="19aa8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19aa8-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="19aa8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="19aa8-150">**Para configurar o logon único do Azure AD com o Five9 Plus Adapter (CTI, Contact Center Agents), realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19aa8-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="19aa8-151">No portal do Azure, na página de integração do aplicativo **Five9 Plus Adapter (CTI, Contact Center Agents)**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="19aa8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="19aa8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="19aa8-155">Na seção **Domínio e URLs do Five9 Plus Adapter (CTI, Contact Center Agents)**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="19aa8-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="19aa8-157">a.</span><span class="sxs-lookup"><span data-stu-id="19aa8-157">a.</span></span> <span data-ttu-id="19aa8-158">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="19aa8-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span>

    |    <span data-ttu-id="19aa8-159">Ambiente</span><span class="sxs-lookup"><span data-stu-id="19aa8-159">Environment</span></span>      |       <span data-ttu-id="19aa8-160">URL</span><span class="sxs-lookup"><span data-stu-id="19aa8-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="19aa8-161">Para o “Five9 Plus Adapter for Microsoft Dynamics CRM”</span><span class="sxs-lookup"><span data-stu-id="19aa8-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="19aa8-162">Para o “Five9 Plus Adapter for Zendesk”</span><span class="sxs-lookup"><span data-stu-id="19aa8-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="19aa8-163">Para o “Five9 Plus Adapter for Agent Desktop Toolkit”</span><span class="sxs-lookup"><span data-stu-id="19aa8-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="19aa8-164">b.</span><span class="sxs-lookup"><span data-stu-id="19aa8-164">b.</span></span> <span data-ttu-id="19aa8-165">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="19aa8-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    |      <span data-ttu-id="19aa8-166">Ambiente</span><span class="sxs-lookup"><span data-stu-id="19aa8-166">Environment</span></span>     |      <span data-ttu-id="19aa8-167">URL</span><span class="sxs-lookup"><span data-stu-id="19aa8-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="19aa8-168">Para o “Five9 Plus Adapter for Microsoft Dynamics CRM”</span><span class="sxs-lookup"><span data-stu-id="19aa8-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="19aa8-169">Para o “Five9 Plus Adapter for Zendesk”</span><span class="sxs-lookup"><span data-stu-id="19aa8-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="19aa8-170">Para o “Five9 Plus Adapter for Agent Desktop Toolkit”</span><span class="sxs-lookup"><span data-stu-id="19aa8-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="19aa8-171">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="19aa8-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="19aa8-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="19aa8-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19aa8-175">Na seção **Configuração do Five9 Plus Adapter (CTI, Contact Center Agents)**, clique em **Configurar o Five9 Plus Adapter (CTI, Contact Center Agents)** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="19aa8-176">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="19aa8-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="19aa8-178">Para configurar o logon único no lado do **Five9 Plus Adapter (CTI, Contact Center Agents)**, é necessário enviar o **Certificado (Base64) baixado, a URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** para a [equipe de suporte do Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="19aa8-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="19aa8-179">Além disso, para configurar o SSO adicional, siga as etapas abaixo de acordo com o adaptador:</span><span class="sxs-lookup"><span data-stu-id="19aa8-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span></span>

    <span data-ttu-id="19aa8-180">a.</span><span class="sxs-lookup"><span data-stu-id="19aa8-180">a.</span></span> <span data-ttu-id="19aa8-181">Guia do Administrador do “Five9 Plus Adapter for Agent Desktop Toolkit”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="19aa8-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="19aa8-182">b.</span><span class="sxs-lookup"><span data-stu-id="19aa8-182">b.</span></span> <span data-ttu-id="19aa8-183">Guia do Administrador do “Five9 Plus Adapter for Microsoft Dynamics CRM”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="19aa8-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="19aa8-184">c.</span><span class="sxs-lookup"><span data-stu-id="19aa8-184">c.</span></span> <span data-ttu-id="19aa8-185">Guia do Administrador do “Five9 Plus Adapter for Zendesk”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="19aa8-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="19aa8-186">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="19aa8-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="19aa8-187">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="19aa8-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="19aa8-188">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19aa8-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19aa8-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="19aa8-190">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="19aa8-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="19aa8-192">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19aa8-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="19aa8-193">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19aa8-195">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="19aa8-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19aa8-197">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19aa8-199">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="19aa8-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19aa8-201">a.</span><span class="sxs-lookup"><span data-stu-id="19aa8-201">a.</span></span> <span data-ttu-id="19aa8-202">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19aa8-203">b.</span><span class="sxs-lookup"><span data-stu-id="19aa8-203">b.</span></span> <span data-ttu-id="19aa8-204">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="19aa8-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19aa8-205">c.</span><span class="sxs-lookup"><span data-stu-id="19aa8-205">c.</span></span> <span data-ttu-id="19aa8-206">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="19aa8-207">d.</span><span class="sxs-lookup"><span data-stu-id="19aa8-207">d.</span></span> <span data-ttu-id="19aa8-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="19aa8-209">Criando um usuário de teste do Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="19aa8-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="19aa8-210">Nesta seção, você cria um usuário chamado Brenda Fernandes no Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="19aa8-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="19aa8-211">Trabalhe com a [equipe de suporte do Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact) para adicionar os usuários à plataforma Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="19aa8-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="19aa8-212">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="19aa8-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="19aa8-213">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="19aa8-214">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="19aa8-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="19aa8-216">**Para atribuir Brenda Fernandes ao Five9 Plus Adapter (CTI, Contact Center Agents), realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19aa8-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="19aa8-217">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="19aa8-219">Na lista de aplicativos, selecione **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="19aa8-221">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="19aa8-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="19aa8-223">Click **Add** button.</span></span> <span data-ttu-id="19aa8-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="19aa8-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="19aa8-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="19aa8-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19aa8-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19aa8-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19aa8-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="19aa8-229">Testing single sign-on</span></span>

<span data-ttu-id="19aa8-230">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="19aa8-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="19aa8-231">Quando você clicar no bloco do Five9 Plus Adapter (CTI, Contact Center Agents) no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="19aa8-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="19aa8-232">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19aa8-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19aa8-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="19aa8-233">Additional resources</span></span>

* [<span data-ttu-id="19aa8-234">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="19aa8-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19aa8-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19aa8-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

