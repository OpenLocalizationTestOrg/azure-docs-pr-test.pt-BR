---
title: "Como configurar o logon único federado para um aplicativo inexistente na galeria | Microsoft Docs"
description: "Como configurar o logon único federado para um aplicativo inexistente na galeria personalizado que você deseja integrar com o Azure AD"
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
ms.openlocfilehash: da7bc05c6452cde4d0236806f249559f178dd4e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="16de6-103">Como configurar o logon único federado para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="16de6-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="16de6-104">Para configurar um aplicativo inexistente na galeria, é necessário ter o Azure AD Premium e o aplicativo com suporte SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="16de6-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="16de6-105">Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="16de6-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="16de6-106">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="16de6-106">Overview of steps required</span></span>
<span data-ttu-id="16de6-107">Abaixo está uma visão geral de alto nível das etapas necessárias para configurar logon único federado para um aplicativo inexistente na galeria (por exemplo, personalizado).</span><span class="sxs-lookup"><span data-stu-id="16de6-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="16de6-108">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="16de6-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="16de6-109">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="16de6-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="16de6-110">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="16de6-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="16de6-111">Configurar os valores de metadados do Azure AD no aplicativo (URL de Logon, Emissor, URL de Logoff e certificado)</span><span class="sxs-lookup"><span data-stu-id="16de6-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="16de6-112">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="16de6-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="16de6-113">Configurar logon único para aplicativos não existentes na galeria</span><span class="sxs-lookup"><span data-stu-id="16de6-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="16de6-114">Para configurar o logon único para um aplicativo que não está na galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="16de6-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="16de6-115">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="16de6-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="16de6-116">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="16de6-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16de6-117">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16de6-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16de6-118">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16de6-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16de6-119">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="16de6-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="16de6-120">clique em **Aplicativo inexistente na galeria** na seção **Adicionar seu próprio aplicativo**</span><span class="sxs-lookup"><span data-stu-id="16de6-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="16de6-121">Digite o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="16de6-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="16de6-122">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="16de6-123">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="16de6-124">Selecione **Logon com base em SAML** na lista suspensa **Modo**.</span><span class="sxs-lookup"><span data-stu-id="16de6-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="16de6-125">Insira os valores necessários em **Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="16de6-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="16de6-126">É possível obter esses valores do fornecedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="16de6-127">Para configurar o aplicativo como SSO iniciado por IdP, insira a URL de Resposta e o Identificador.</span><span class="sxs-lookup"><span data-stu-id="16de6-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="16de6-128">**Opcional:** Para configurar o aplicativo como SSO iniciado por SP, a URL de Logon é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="16de6-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="16de6-129">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="16de6-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="16de6-130">**Opcional:** clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="16de6-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="16de6-131">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="16de6-131">To add an attribute:</span></span>

   1. <span data-ttu-id="16de6-132">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="16de6-132">click **Add attribute**.</span></span> <span data-ttu-id="16de6-133">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="16de6-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="16de6-134">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="16de6-134">Click **Save.**</span></span> <span data-ttu-id="16de6-135">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="16de6-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="16de6-136">clique em **Configurar &lt;nome do aplicativo&gt;**  para acessar a documentação sobre como configurar o logon único no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="16de6-137">Além disso, você tem URLs do Azure AD e o certificado necessários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. [<span data-ttu-id="16de6-138">Atribuir usuários ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-138">Assign users to the application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="16de6-139">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="16de6-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="16de6-140">Para selecionar o Identificador de Usuário ou adicionar os atributos de usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="16de6-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="16de6-141">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="16de6-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="16de6-142">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="16de6-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16de6-143">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16de6-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16de6-144">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16de6-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16de6-145">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="16de6-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="16de6-146">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="16de6-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="16de6-147">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="16de6-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="16de6-148">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="16de6-149">Na seção **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="16de6-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="16de6-150">A opção selecionada precisa corresponder ao valor esperado no aplicativo para autenticar o usuário.</span><span class="sxs-lookup"><span data-stu-id="16de6-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="16de6-151">[!OBSERVAÇÃO} O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="16de6-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="16de6-152">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="16de6-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="16de6-153">Para adicionar atributos de usuário, clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="16de6-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="16de6-154">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="16de6-154">To add an attribute:</span></span>

   1. <span data-ttu-id="16de6-155">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="16de6-155">click **Add attribute**.</span></span> <span data-ttu-id="16de6-156">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="16de6-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="16de6-157">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="16de6-157">Click **Save.**</span></span> <span data-ttu-id="16de6-158">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="16de6-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="16de6-159">Baixar o certificado ou metadados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="16de6-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="16de6-160">Para baixar o certificado ou metadados do aplicativo Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="16de6-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="16de6-161">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="16de6-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="16de6-162">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="16de6-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16de6-163">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16de6-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16de6-164">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16de6-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16de6-165">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="16de6-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="16de6-166">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="16de6-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="16de6-167">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="16de6-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="16de6-168">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="16de6-169">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="16de6-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="16de6-170">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="16de6-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="16de6-171">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="16de6-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="16de6-172">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="16de6-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="16de6-173">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="16de6-173">Assign users to the application</span></span>

<span data-ttu-id="16de6-174">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="16de6-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="16de6-175">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="16de6-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="16de6-176">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="16de6-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16de6-177">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16de6-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16de6-178">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16de6-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16de6-179">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="16de6-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="16de6-180">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="16de6-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="16de6-181">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="16de6-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="16de6-182">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="16de6-183">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="16de6-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="16de6-184">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="16de6-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="16de6-185">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="16de6-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="16de6-186">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="16de6-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="16de6-187">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="16de6-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="16de6-188">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="16de6-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="16de6-189">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16de6-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="16de6-190">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="16de6-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="16de6-191">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="16de6-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="16de6-192">Após um breve período, os usuários que você selecionou poderão iniciar esses aplicativos usando os métodos descritos na seção de descrição da solução.</span><span class="sxs-lookup"><span data-stu-id="16de6-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="16de6-193">Personalizando as declarações SAML enviadas para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="16de6-193">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="16de6-194">Para saber como personalizar as declarações de atributo SAML enviadas para seu aplicativo, consulte [Mapeamento de declarações no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="16de6-194">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16de6-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16de6-195">Next steps</span></span>
[<span data-ttu-id="16de6-196">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="16de6-196">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
