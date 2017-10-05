---
title: "Tutorial: Integração do Azure Active Directory com o OfficeSpace Software | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="65a55-103">Tutorial: Integração do Active Directory do Azure com o OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="65a55-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="65a55-104">Neste tutorial, você aprende a integrar o OfficeSpace Software ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="65a55-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65a55-105">A integração do OfficeSpace Software ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="65a55-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65a55-106">No Azure AD, é possível controlar quem tem acesso ao OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="65a55-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="65a55-107">Você pode permitir que os usuários sejam conectados automaticamente ao OfficeSpace Software (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65a55-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65a55-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a55-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="65a55-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65a55-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65a55-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="65a55-110">Prerequisites</span></span>

<span data-ttu-id="65a55-111">Para configurar a integração do Azure AD ao OfficeSpace Software, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="65a55-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="65a55-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65a55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65a55-113">Uma assinatura do OfficeSpace Software habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="65a55-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65a55-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="65a55-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65a55-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="65a55-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65a55-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="65a55-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65a55-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65a55-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65a55-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="65a55-118">Scenario description</span></span>
<span data-ttu-id="65a55-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="65a55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65a55-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="65a55-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65a55-121">Adicionando o OfficeSpace Software por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="65a55-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="65a55-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65a55-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="65a55-123">Adicionando o OfficeSpace Software por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="65a55-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="65a55-124">Para configurar a integração do OfficeSpace Software no Azure AD, é necessário adicionar o OfficeSpace Software por meio da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="65a55-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65a55-125">**Para adicionar o OfficeSpace Software por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65a55-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65a55-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65a55-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="65a55-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="65a55-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65a55-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="65a55-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="65a55-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65a55-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="65a55-133">Na caixa de pesquisa, digite **OfficeSpace Software**, selecione **OfficeSpace Software** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65a55-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![OfficeSpace Software na lista de resultados](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65a55-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="65a55-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="65a55-136">Nesta seção, você configura e testa o logon único do Azure AD com o OfficeSpace Software, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="65a55-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65a55-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do OfficeSpace Software é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65a55-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="65a55-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="65a55-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="65a55-139">No OfficeSpace Software, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="65a55-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65a55-140">Para configurar e testar o logon único do Azure AD com o OfficeSpace Software, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="65a55-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65a55-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="65a55-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65a55-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="65a55-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65a55-143">**[Criar um usuário de teste do OfficeSpace Software](#create-a-officespace-software-test-user)** – para ter um equivalente de Brenda Fernandes no OfficeSpace Software que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65a55-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65a55-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65a55-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65a55-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="65a55-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65a55-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="65a55-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65a55-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="65a55-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="65a55-148">**Para configurar o logon único do Azure AD com o OfficeSpace Software, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65a55-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="65a55-149">No Portal do Azure, na página de integração de aplicativos do **OfficeSpace Software**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="65a55-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="65a55-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="65a55-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="65a55-153">Na seção **URLs e Domínio do OfficeSpace Software**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65a55-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="65a55-155">a.</span><span class="sxs-lookup"><span data-stu-id="65a55-155">a.</span></span> <span data-ttu-id="65a55-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="65a55-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="65a55-157">b.</span><span class="sxs-lookup"><span data-stu-id="65a55-157">b.</span></span> <span data-ttu-id="65a55-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="65a55-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65a55-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="65a55-159">These values are not real.</span></span> <span data-ttu-id="65a55-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="65a55-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65a55-161">Contate a [equipe de suporte ao cliente do OfficeSpace Software](mailto:support@officespacesoftware.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="65a55-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="65a55-162">O aplicativo OfficeSpace Software espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="65a55-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="65a55-163">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65a55-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="65a55-164">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65a55-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="65a55-165">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="65a55-165">The following screenshot shows an example for this.</span></span>
    
    ![Configurar atributo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="65a55-167">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, selecione **user.mail** como **Identificador de Usuário** e, para cada linha mostrada na tabela a seguir, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65a55-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="65a55-168">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="65a55-168">Attribute Name</span></span> | <span data-ttu-id="65a55-169">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="65a55-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="65a55-170">email</span><span class="sxs-lookup"><span data-stu-id="65a55-170">email</span></span> | <span data-ttu-id="65a55-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="65a55-171">user.mail</span></span> |
    | <span data-ttu-id="65a55-172">name</span><span class="sxs-lookup"><span data-stu-id="65a55-172">name</span></span> | <span data-ttu-id="65a55-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="65a55-173">user.displayname</span></span> |
    | <span data-ttu-id="65a55-174">first_name</span><span class="sxs-lookup"><span data-stu-id="65a55-174">first_name</span></span> | <span data-ttu-id="65a55-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="65a55-175">user.givenname</span></span> |
    | <span data-ttu-id="65a55-176">last_name</span><span class="sxs-lookup"><span data-stu-id="65a55-176">last_name</span></span> | <span data-ttu-id="65a55-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="65a55-177">user.surname</span></span> |

    <span data-ttu-id="65a55-178">a.</span><span class="sxs-lookup"><span data-stu-id="65a55-178">a.</span></span> <span data-ttu-id="65a55-179">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="65a55-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="65a55-180">Configurar Adicionar</span><span class="sxs-lookup"><span data-stu-id="65a55-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configurar atributo](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="65a55-182">b.</span><span class="sxs-lookup"><span data-stu-id="65a55-182">b.</span></span> <span data-ttu-id="65a55-183">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="65a55-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="65a55-184">c.</span><span class="sxs-lookup"><span data-stu-id="65a55-184">c.</span></span> <span data-ttu-id="65a55-185">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="65a55-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="65a55-186">d.</span><span class="sxs-lookup"><span data-stu-id="65a55-186">d.</span></span> <span data-ttu-id="65a55-187">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="65a55-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="65a55-188">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="65a55-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="65a55-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="65a55-190">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="65a55-192">Na seção **Configuração do OfficeSpace Software**, clique em **Configurar o OfficeSpace Software** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="65a55-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65a55-193">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="65a55-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="65a55-195">Em outra janela do navegador da Web, faça logon no locatário do OfficeSpace Software como administrador.</span><span class="sxs-lookup"><span data-stu-id="65a55-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="65a55-196">Acesse **Configurações** e clique em **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="65a55-196">Go to **Settings** and click **Connectors**.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="65a55-198">Clique em **Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="65a55-198">Click **SAML Authentication**.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="65a55-200">Na seção **Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65a55-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="65a55-202">a.</span><span class="sxs-lookup"><span data-stu-id="65a55-202">a.</span></span> <span data-ttu-id="65a55-203">Na caixa de texto **URL do provedor de logoff**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a55-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65a55-204">b.</span><span class="sxs-lookup"><span data-stu-id="65a55-204">b.</span></span> <span data-ttu-id="65a55-205">Na caixa de texto **URL de destino de IdP do cliente**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a55-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65a55-206">c.</span><span class="sxs-lookup"><span data-stu-id="65a55-206">c.</span></span> <span data-ttu-id="65a55-207">Cole o valor da **Impressão digital** copiado do Portal do Azure na caixa de texto **Impressão digital de certificado de IdP do cliente**.</span><span class="sxs-lookup"><span data-stu-id="65a55-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="65a55-208">d.</span><span class="sxs-lookup"><span data-stu-id="65a55-208">d.</span></span> <span data-ttu-id="65a55-209">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="65a55-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="65a55-210">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="65a55-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65a55-211">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="65a55-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65a55-212">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65a55-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65a55-213">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="65a55-213">Create an Azure AD test user</span></span>

<span data-ttu-id="65a55-214">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="65a55-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="65a55-216">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65a55-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65a55-217">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65a55-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="65a55-219">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="65a55-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="65a55-221">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="65a55-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="65a55-223">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65a55-223">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="65a55-225">a.</span><span class="sxs-lookup"><span data-stu-id="65a55-225">a.</span></span> <span data-ttu-id="65a55-226">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="65a55-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65a55-227">b.</span><span class="sxs-lookup"><span data-stu-id="65a55-227">b.</span></span> <span data-ttu-id="65a55-228">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="65a55-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="65a55-229">c.</span><span class="sxs-lookup"><span data-stu-id="65a55-229">c.</span></span> <span data-ttu-id="65a55-230">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="65a55-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="65a55-231">d.</span><span class="sxs-lookup"><span data-stu-id="65a55-231">d.</span></span> <span data-ttu-id="65a55-232">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="65a55-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="65a55-233">Criar um usuário de teste do OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="65a55-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="65a55-234">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="65a55-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="65a55-235">O OfficeSpace Software dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="65a55-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="65a55-236">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="65a55-236">There is no action item for you in this section.</span></span> <span data-ttu-id="65a55-237">Um novo usuário será criado durante uma tentativa de acessar o OfficeSpace Software, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="65a55-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="65a55-238">Se precisar criar um usuário manualmente, será necessário contatar a [equipe de suporte do OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="65a55-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="65a55-239">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="65a55-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="65a55-240">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="65a55-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="65a55-242">**Para atribuir Brenda Fernandes ao OfficeSpace Software, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65a55-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="65a55-243">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="65a55-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="65a55-245">Na lista de aplicativos, selecione **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="65a55-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![O link do OfficeSpace Software na lista de Aplicativos](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="65a55-247">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="65a55-247">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="65a55-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="65a55-249">Click **Add** button.</span></span> <span data-ttu-id="65a55-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65a55-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="65a55-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="65a55-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65a55-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65a55-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65a55-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65a55-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65a55-255">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="65a55-255">Test single sign-on</span></span>

<span data-ttu-id="65a55-256">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="65a55-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65a55-257">Ao clicar no bloco OfficeSpace Software no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="65a55-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65a55-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="65a55-258">Additional resources</span></span>

* [<span data-ttu-id="65a55-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="65a55-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65a55-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65a55-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

