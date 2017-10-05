---
title: "Como configurar o logon único federado para um aplicativo na Galeria do Azure AD | Microsoft Docs"
description: "Como configurar o logon único federado para um aplicativo na Galeria do Azure AD existente e usar tutoriais para começar rapidamente"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="048ea-103">Como configurar o logon único federado para um aplicativo na Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048ea-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="048ea-104">Todos os aplicativos na galeria do Azure AD habilitados com o recurso de logon único Corporativo possuem um tutorial passo a passo disponível.</span><span class="sxs-lookup"><span data-stu-id="048ea-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="048ea-105">É possível acessar a [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhada.</span><span class="sxs-lookup"><span data-stu-id="048ea-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="048ea-106">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="048ea-106">Overview of steps required</span></span>
<span data-ttu-id="048ea-107">Para configurar um aplicativo da galeria do Azure AD, será necessário:</span><span class="sxs-lookup"><span data-stu-id="048ea-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="048ea-108">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048ea-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="048ea-109">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="048ea-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="048ea-110">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="048ea-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="048ea-111">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="048ea-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="048ea-112">Configurar os valores de metadados do Azure AD no aplicativo (URL de Logon, Emissor, URL de Logoff e certificado)</span><span class="sxs-lookup"><span data-stu-id="048ea-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="048ea-113">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="048ea-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="048ea-114">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048ea-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="048ea-115">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="048ea-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="048ea-116">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="048ea-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="048ea-117">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="048ea-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="048ea-118">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="048ea-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="048ea-119">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="048ea-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="048ea-120">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="048ea-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="048ea-121">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="048ea-122">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="048ea-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="048ea-123">Antes de adicionar o aplicativo, é possível alterar seu nome pela caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="048ea-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="048ea-124">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="048ea-125">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="048ea-126">Configurar o logon único para um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048ea-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="048ea-127">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="048ea-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="048ea-128">Abra o [**Porta do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="048ea-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="048ea-129">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** no botão do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="048ea-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="048ea-130">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="048ea-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="048ea-131">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="048ea-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="048ea-132">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="048ea-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="048ea-133">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="048ea-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="048ea-134">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="048ea-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="048ea-135">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="048ea-136">Selecione **Logon com base em SAML** da lista suspensa **Modo**.</span><span class="sxs-lookup"><span data-stu-id="048ea-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="048ea-137">Insira os valores necessários em **Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="048ea-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="048ea-138">É possível obter esses valores do fornecedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="048ea-139">Para configurar o aplicativo como SSO iniciado por SP, a URL de Logon é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="048ea-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="048ea-140">Para alguns aplicativos, o Identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="048ea-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="048ea-141">Para configurar o aplicativo como SSO iniciado por IdP, a URL de Resposta é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="048ea-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="048ea-142">Para alguns aplicativos, o Identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="048ea-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="048ea-143">**Opcional:** clique **Mostrar configurações avançadas de URL** se quiser ver os valores não obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="048ea-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="048ea-144">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="048ea-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="048ea-145">**Opcional:** clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="048ea-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="048ea-146">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="048ea-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="048ea-147">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="048ea-147">click **Add attribute**.</span></span> <span data-ttu-id="048ea-148">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="048ea-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="048ea-149">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="048ea-149">Click **Save.**</span></span> <span data-ttu-id="048ea-150">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="048ea-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="048ea-151">clique em **Configurar &lt;nome do aplicativo&gt;**  para acessar a documentação sobre como configurar o logon único no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="048ea-152">Além disso, você tem URLs de metadados e o certificado necessários para configurar o SSO com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="048ea-153">Clique em **Salvar** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="048ea-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="048ea-154">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="048ea-155">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="048ea-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="048ea-156">Para selecionar o Identificador de Usuário ou adicionar os atributos de usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="048ea-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="048ea-157">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="048ea-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="048ea-158">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="048ea-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="048ea-159">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="048ea-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="048ea-160">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="048ea-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="048ea-161">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="048ea-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="048ea-162">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="048ea-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="048ea-163">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="048ea-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="048ea-164">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="048ea-165">Na seção **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="048ea-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="048ea-166">A opção selecionada precisa corresponder ao valor esperado no aplicativo para autenticar o usuário.</span><span class="sxs-lookup"><span data-stu-id="048ea-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="048ea-167">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="048ea-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="048ea-168">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="048ea-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="048ea-169">Para adicionar atributos de usuário, clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="048ea-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="048ea-170">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="048ea-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="048ea-171">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="048ea-171">click **Add attribute**.</span></span> <span data-ttu-id="048ea-172">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="048ea-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="048ea-173">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="048ea-173">Click **Save**.</span></span> <span data-ttu-id="048ea-174">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="048ea-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="048ea-175">Baixar o certificado ou metadados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048ea-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="048ea-176">Para baixar o certificado ou metadados do aplicativo Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="048ea-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="048ea-177">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="048ea-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="048ea-178">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="048ea-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="048ea-179">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="048ea-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="048ea-180">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="048ea-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="048ea-181">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="048ea-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="048ea-182">Se você não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="048ea-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="048ea-183">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="048ea-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="048ea-184">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="048ea-185">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="048ea-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="048ea-186">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="048ea-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="048ea-187">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="048ea-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="048ea-188">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="048ea-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="048ea-189">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="048ea-189">Assign users to the application</span></span>

<span data-ttu-id="048ea-190">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="048ea-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="048ea-191">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="048ea-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="048ea-192">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="048ea-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="048ea-193">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="048ea-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="048ea-194">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="048ea-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="048ea-195">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="048ea-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="048ea-196">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="048ea-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="048ea-197">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="048ea-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="048ea-198">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="048ea-199">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="048ea-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="048ea-200">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="048ea-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="048ea-201">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="048ea-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="048ea-202">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="048ea-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="048ea-203">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="048ea-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="048ea-204">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="048ea-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="048ea-205">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="048ea-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="048ea-206">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="048ea-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="048ea-207">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="048ea-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="048ea-208">Após um breve período, os usuários que você selecionou poderão iniciar esses aplicativos usando os métodos descritos na seção de descrição da solução.</span><span class="sxs-lookup"><span data-stu-id="048ea-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="048ea-209">Personalizando as declarações SAML enviadas para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="048ea-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="048ea-210">Para saber como personalizar as declarações de atributo SAML enviadas para seu aplicativo, consulte [Mapeamento de declarações no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="048ea-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="048ea-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="048ea-211">Next steps</span></span>
[<span data-ttu-id="048ea-212">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="048ea-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



