---
title: "Tutorial: integração do Azure Active Directory com o ServiceChannel | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="2873e-103">Tutorial: integração do Azure Active Directory com o ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="2873e-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="2873e-104">Neste tutorial, você aprenderá a integrar o ServiceChannel ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2873e-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2873e-105">A integração do ServiceChannel ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2873e-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2873e-106">No Azure AD, é possível controlar quem tem acesso ao ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="2873e-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="2873e-107">Você pode permitir que os usuários façam logon automaticamente no ServiceChannel (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2873e-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2873e-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2873e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2873e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2873e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2873e-110">Prerequisites</span></span>

<span data-ttu-id="2873e-111">Para configurar a integração do Azure AD ao ServiceChannel, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2873e-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="2873e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2873e-113">Uma assinatura do ServiceChannel habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="2873e-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2873e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2873e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2873e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2873e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2873e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2873e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2873e-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2873e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2873e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2873e-118">Scenario description</span></span>
<span data-ttu-id="2873e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2873e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2873e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2873e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2873e-121">Adicionar o ServiceChannel da galeria</span><span class="sxs-lookup"><span data-stu-id="2873e-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="2873e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="2873e-123">Adicionar o ServiceChannel da galeria</span><span class="sxs-lookup"><span data-stu-id="2873e-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="2873e-124">Para configurar a integração do ServiceChannel ao Azure AD, você precisará adicionar o ServiceChannel à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="2873e-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2873e-125">**Para adicionar o ServiceChannel da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2873e-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2873e-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2873e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2873e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2873e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2873e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2873e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2873e-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2873e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2873e-133">Na caixa de pesquisa, digite **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="2873e-133">In the search box, type **ServiceChannel**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="2873e-135">No painel de resultados, selecione **ServiceChannel** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2873e-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2873e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2873e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ServiceChannel, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="2873e-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2873e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ServiceChannel é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2873e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="2873e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="2873e-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="2873e-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como sendo o valor de **Nome de Usuário** no ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="2873e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="2873e-142">Para configurar e testar o logon único do Azure AD com o ServiceChannel, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2873e-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2873e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2873e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2873e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2873e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2873e-145">**[Criação de um usuário de teste do ServiceChannel](#creating-a-servicechannel-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2873e-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2873e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2873e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2873e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2873e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2873e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2873e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2873e-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e o configura em seu aplicativo ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="2873e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="2873e-150">**Para configurar o logon único do Azure AD com o ServiceChannel, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2873e-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="2873e-151">No Portal de Gerenciamento do Azure, na página de integração do aplicativo **ServiceChannel**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2873e-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2873e-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2873e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="2873e-155">Na seção **URLs e Domínio do ServiceChannel**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2873e-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="2873e-157">a.</span><span class="sxs-lookup"><span data-stu-id="2873e-157">a.</span></span> <span data-ttu-id="2873e-158">Na caixa de texto **Identificador**, digite o valor como `http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="2873e-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="2873e-159">b.</span><span class="sxs-lookup"><span data-stu-id="2873e-159">b.</span></span> <span data-ttu-id="2873e-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="2873e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2873e-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="2873e-161">Please note that these are not the real values.</span></span> <span data-ttu-id="2873e-162">Você precisa atualizar esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="2873e-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2873e-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="2873e-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="2873e-164">Entre em contato com a [equipe de suporte do ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="2873e-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="2873e-165">Seu aplicativo ServiceChannel espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="2873e-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="2873e-166">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="2873e-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="2873e-167">**NameIdentifier (identificador de usuário)** é única declaração obrigatória e o valor padrão é **user.userprincipalname**, mas o ServiceChannel espera que isso seja mapeada com **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="2873e-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="2873e-168">Se você planeja habilitar o provisionamento do usuário Just-In-Time, você deve adicionar as declarações a seguir conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2873e-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="2873e-169">A declaração **Função** precisa ser mapeada para **user.assignedroles**, que contém a função do usuário.</span><span class="sxs-lookup"><span data-stu-id="2873e-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="2873e-170">Você pode consultar o guia do ServiceChannel [aqui](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) para obter diretrizes sobre declarações.</span><span class="sxs-lookup"><span data-stu-id="2873e-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="2873e-172">Clique [aqui](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) para saber como configurar a **Função** no Azure AD</span><span class="sxs-lookup"><span data-stu-id="2873e-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="2873e-173">Na seção **Atributos de Usuário**, clique em **Exibir e editar todos os outros atributos de usuário** e defina os atributos.</span><span class="sxs-lookup"><span data-stu-id="2873e-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="2873e-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="2873e-174">Attribute Name</span></span> | <span data-ttu-id="2873e-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="2873e-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="2873e-176">Função</span><span class="sxs-lookup"><span data-stu-id="2873e-176">Role</span></span>| <span data-ttu-id="2873e-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="2873e-177">user.assignedroles</span></span> |

    <span data-ttu-id="2873e-178">a.</span><span class="sxs-lookup"><span data-stu-id="2873e-178">a.</span></span> <span data-ttu-id="2873e-179">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="2873e-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="2873e-182">b.</span><span class="sxs-lookup"><span data-stu-id="2873e-182">b.</span></span> <span data-ttu-id="2873e-183">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="2873e-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="2873e-184">c.</span><span class="sxs-lookup"><span data-stu-id="2873e-184">c.</span></span> <span data-ttu-id="2873e-185">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="2873e-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="2873e-186">d.</span><span class="sxs-lookup"><span data-stu-id="2873e-186">d.</span></span> <span data-ttu-id="2873e-187">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="2873e-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="2873e-188">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2873e-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="2873e-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2873e-190">Click **Save**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2873e-192">Na seção **Configuração do ServiceChannel**, clique em **Configurar o ServiceChannel** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="2873e-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2873e-193">Copie a **ID da Entidade SAML** da seção **Referência Rápida**.</span><span class="sxs-lookup"><span data-stu-id="2873e-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="2873e-194">Para configurar o logon único no lado de **ServiceChannel**, você precisa enviar o **certificado (Base64)** baixado e a **ID da entidade SAML** para [equipe de suporte do ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="2873e-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="2873e-195">Isso será configurado para que a conexão de SSO do SAML seja definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="2873e-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2873e-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="2873e-197">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2873e-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2873e-199">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2873e-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2873e-200">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2873e-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2873e-202">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2873e-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2873e-204">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2873e-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2873e-206">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2873e-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2873e-208">a.</span><span class="sxs-lookup"><span data-stu-id="2873e-208">a.</span></span> <span data-ttu-id="2873e-209">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2873e-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2873e-210">b.</span><span class="sxs-lookup"><span data-stu-id="2873e-210">b.</span></span> <span data-ttu-id="2873e-211">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2873e-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2873e-212">c.</span><span class="sxs-lookup"><span data-stu-id="2873e-212">c.</span></span> <span data-ttu-id="2873e-213">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2873e-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2873e-214">d.</span><span class="sxs-lookup"><span data-stu-id="2873e-214">d.</span></span> <span data-ttu-id="2873e-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2873e-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="2873e-216">Criar um usuário de teste do ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="2873e-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="2873e-217">O aplicativo dá suporte ao provisionamento de usuário just-in-time e, após a autenticação, os usuários serão automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2873e-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="2873e-218">Para um provisionamento de usuário completo, entre em contato com [a equipe de suporte do ServiceChannel](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="2873e-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2873e-219">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2873e-220">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="2873e-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2873e-222">**Para atribuir Brenda Fernandes ao ServiceChannel, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2873e-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="2873e-223">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2873e-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2873e-225">Na lista de aplicativos, selecione **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="2873e-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="2873e-227">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2873e-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2873e-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2873e-229">Click **Add** button.</span></span> <span data-ttu-id="2873e-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2873e-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2873e-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2873e-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2873e-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2873e-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2873e-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2873e-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2873e-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2873e-235">Testing single sign-on</span></span>

<span data-ttu-id="2873e-236">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2873e-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2873e-237">Ao clicar no bloco do ServiceChannel no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="2873e-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2873e-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2873e-238">Additional resources</span></span>

* [<span data-ttu-id="2873e-239">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2873e-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2873e-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2873e-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png