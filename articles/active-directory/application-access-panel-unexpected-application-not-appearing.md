---
title: "Um aplicativo atribuído não aparece no painel de acesso | Microsoft Docs"
description: "Solucionar problemas por que um aplicativo não aparece no Painel de Acesso"
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
ms.reviwer: japere
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="005c0-103">Um aplicativo atribuído não aparece no painel de acesso</span><span class="sxs-lookup"><span data-stu-id="005c0-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="005c0-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário com uma conta corporativa ou de estudante no Azure Active Directory (Azure AD) exibir e iniciar aplicativos baseados em nuvem para os quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="005c0-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="005c0-105">Esses aplicativos são configurados em nome do usuário no portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="005c0-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="005c0-106">O aplicativo deve ser configurado corretamente e atribuído ao usuário ou a um grupo no qual o usuário é membro para ver o aplicativo no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="005c0-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="005c0-107">Os tipos de aplicativos que um usuário pode ver se enquadram nas categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="005c0-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="005c0-108">Aplicativos do Office 365</span><span class="sxs-lookup"><span data-stu-id="005c0-108">Office 365 Applications</span></span>

-   <span data-ttu-id="005c0-109">Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação</span><span class="sxs-lookup"><span data-stu-id="005c0-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="005c0-110">Aplicativos de SSO baseadas em senhas</span><span class="sxs-lookup"><span data-stu-id="005c0-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="005c0-111">Aplicativos com soluções de SSO existentes</span><span class="sxs-lookup"><span data-stu-id="005c0-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="005c0-112">Questões gerais que primeiro devem ser verificadas</span><span class="sxs-lookup"><span data-stu-id="005c0-112">General issues to check first</span></span>

-   <span data-ttu-id="005c0-113">Se um aplicativo acabou de ser adicionado a um usuário, tente entrar e sair novamente no Painel de Acesso do usuário após alguns minutos para ver se o aplicativo foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="005c0-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="005c0-114">Se uma licença tiver acabado de ser removida de um usuário ou de um grupo de que o usuário faz parte, isso poderá levar um longo período, dependendo do tamanho e da complexidade do grupo.</span><span class="sxs-lookup"><span data-stu-id="005c0-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="005c0-115">Espere mais algum tempo antes de entrar no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="005c0-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="005c0-116">Problemas relacionados à configuração de aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-116">Problems related to application configuration</span></span>

<span data-ttu-id="005c0-117">Um aplicativo pode não aparecer no Painel de Acesso de um usuário porque não está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="005c0-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="005c0-118">Abaixo, são apresentadas algumas maneiras de solucionar problemas relacionados à configuração do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="005c0-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="005c0-119">Como configurar o logon único federado para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="005c0-120">Como configurar o logon único federado para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="005c0-121">Como configurar um aplicativo de logon único com senha para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="005c0-122">Como configurar um aplicativo de logon único com senha para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="005c0-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="005c0-123">Como configurar o logon único federado para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="005c0-124">Todos os aplicativos na galeria do Azure AD habilitados com a capacidade de Logon Único Corporativo têm um tutorial passo a passo disponível.</span><span class="sxs-lookup"><span data-stu-id="005c0-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="005c0-125">É possível acessar a [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhada.</span><span class="sxs-lookup"><span data-stu-id="005c0-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="005c0-126">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="005c0-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="005c0-127">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="005c0-128">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="005c0-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="005c0-129">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="005c0-130">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="005c0-131">Configurar os valores de metadados do Azure AD no aplicativo (URL de Logon, Emissor, URL de Logoff e certificado)</span><span class="sxs-lookup"><span data-stu-id="005c0-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="005c0-132">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="005c0-133">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-134">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="005c0-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="005c0-135">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-136">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-137">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-138">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="005c0-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="005c0-139">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="005c0-140">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="005c0-141">Antes de adicionar o aplicativo, é possível alterar seu nome pela caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="005c0-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="005c0-142">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="005c0-143">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="005c0-144">Configurar o logon único para um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="005c0-145">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-146">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-147">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-148">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-149">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-150">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="005c0-151">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-152">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="005c0-153">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-154">Selecione **Logon com base em SAML** da lista suspensa **Modo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="005c0-155">Insira os valores necessários em **Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="005c0-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="005c0-156">É possível obter esses valores do fornecedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="005c0-157">Para configurar o aplicativo como SSO iniciado por SP, a URL de Logon é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="005c0-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="005c0-158">Para alguns aplicativos, o Identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="005c0-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="005c0-159">Para configurar o aplicativo como SSO iniciado por IdP, a URL de Resposta é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="005c0-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="005c0-160">Para alguns aplicativos, o Identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="005c0-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="005c0-161">**Opcional:** clique **Mostrar configurações avançadas de URL** se quiser ver os valores não obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="005c0-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="005c0-162">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="005c0-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="005c0-163">**Opcional:** clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="005c0-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="005c0-164">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="005c0-164">To add an attribute:</span></span>

   1. <span data-ttu-id="005c0-165">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-165">click **Add attribute**.</span></span> <span data-ttu-id="005c0-166">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="005c0-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="005c0-167">clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="005c0-167">click **Save.**</span></span> <span data-ttu-id="005c0-168">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="005c0-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="005c0-169">clique em **Configurar &lt;nome do aplicativo&gt;**  para acessar a documentação sobre como configurar o logon único no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="005c0-170">Além disso, você tem URLs de metadados e o certificado necessários para configurar o SSO com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="005c0-171">clique em **Salvar** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="005c0-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="005c0-172">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="005c0-173">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="005c0-174">Para selecionar o Identificador de Usuário ou adicionar os atributos de usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-175">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-176">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-177">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-178">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-179">clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="005c0-180">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-181">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="005c0-182">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-183">Na seção **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="005c0-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="005c0-184">A opção selecionada precisa corresponder ao valor esperado no aplicativo para autenticar o usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="005c0-185">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="005c0-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="005c0-186">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="005c0-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="005c0-187">Para adicionar atributos de usuário, clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="005c0-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="005c0-188">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="005c0-188">To add an attribute:</span></span>

   1. <span data-ttu-id="005c0-189">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-189">click **Add attribute**.</span></span> <span data-ttu-id="005c0-190">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="005c0-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="005c0-191">clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="005c0-191">click **Save.**</span></span> <span data-ttu-id="005c0-192">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="005c0-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="005c0-193">Baixar o certificado ou metadados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="005c0-194">Para baixar o certificado ou metadados do aplicativo Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-195">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-196">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-197">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-198">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-199">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="005c0-200">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-201">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="005c0-202">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-203">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="005c0-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="005c0-204">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="005c0-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="005c0-205">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="005c0-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="005c0-206">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="005c0-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="005c0-207">Como configurar o logon único federado para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="005c0-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="005c0-208">Para configurar um aplicativo inexistente na galeria, é necessário ter o Azure AD Premium e o aplicativo com suporte SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="005c0-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="005c0-209">Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="005c0-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="005c0-210">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="005c0-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="005c0-211">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="005c0-212">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="005c0-213">Configurar os valores de metadados do Azure AD no aplicativo (URL de Logon, Emissor, URL de Logoff e certificado)</span><span class="sxs-lookup"><span data-stu-id="005c0-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="005c0-214">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="005c0-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="005c0-215">Para configurar o logon único para um aplicativo que não está na galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-216">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-217">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-218">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-219">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-220">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="005c0-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="005c0-221">clique em **Aplicativo inexistente na galeria** na seção **Adicionar seu próprio aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="005c0-222">Digite o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="005c0-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="005c0-223">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="005c0-224">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="005c0-225">Selecione **Logon com base em SAML** na lista suspensa **Modo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="005c0-226">Insira os valores necessários em **Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="005c0-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="005c0-227">É possível obter esses valores do fornecedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="005c0-228">Para configurar o aplicativo como SSO iniciado por IdP, insira a URL de Resposta e o Identificador.</span><span class="sxs-lookup"><span data-stu-id="005c0-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="005c0-229">**Opcional:** Para configurar o aplicativo como SSO iniciado por SP, a URL de Logon é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="005c0-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="005c0-230">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="005c0-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="005c0-231">**Opcional:** clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="005c0-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="005c0-232">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="005c0-232">To add an attribute:</span></span>

   1. <span data-ttu-id="005c0-233">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-233">click **Add attribute**.</span></span> <span data-ttu-id="005c0-234">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="005c0-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="005c0-235">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="005c0-235">Click **Save.**</span></span> <span data-ttu-id="005c0-236">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="005c0-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="005c0-237">clique em **Configurar &lt;nome do aplicativo&gt;**  para acessar a documentação sobre como configurar o logon único no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="005c0-238">Além disso, você tem URLs do Azure AD e o certificado necessários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="005c0-239">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="005c0-240">Para selecionar o Identificador de Usuário ou adicionar os atributos de usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-241">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-242">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-243">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-244">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-245">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="005c0-246">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-247">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="005c0-248">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-249">Na seção **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="005c0-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="005c0-250">A opção selecionada precisa corresponder ao valor esperado no aplicativo para autenticar o usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="005c0-251">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="005c0-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="005c0-252">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="005c0-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="005c0-253">Para adicionar atributos de usuário, clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="005c0-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="005c0-254">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="005c0-254">To add an attribute:</span></span>

   1. <span data-ttu-id="005c0-255">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="005c0-255">click **Add attribute**.</span></span> <span data-ttu-id="005c0-256">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="005c0-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="005c0-257">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="005c0-257">Click **Save.**</span></span> <span data-ttu-id="005c0-258">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="005c0-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="005c0-259">Baixar o certificado ou metadados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="005c0-260">Para baixar o certificado ou metadados do aplicativo Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-261">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-262">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-263">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-264">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-265">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="005c0-266">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-267">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="005c0-268">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-269">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="005c0-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="005c0-270">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="005c0-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="005c0-271">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="005c0-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="005c0-272">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="005c0-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="005c0-273">Como configurar o login único com senha para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="005c0-274">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="005c0-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="005c0-275">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="005c0-276">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="005c0-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="005c0-277">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="005c0-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="005c0-278">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-279">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="005c0-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="005c0-280">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-281">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-282">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-283">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="005c0-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="005c0-284">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="005c0-285">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="005c0-286">Antes de adicionar o aplicativo, é possível alterar seu nome pela caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="005c0-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="005c0-287">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="005c0-288">Após um breve período, você verá a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="005c0-289">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="005c0-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="005c0-290">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-291">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-292">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-293">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-294">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-295">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="005c0-296">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-297">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="005c0-298">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-299">Selecione o modo **Logon baseado em Senha.**</span><span class="sxs-lookup"><span data-stu-id="005c0-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="005c0-300">[Atribuir usuários ao aplicativo](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="005c0-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="005c0-301">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="005c0-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="005c0-302">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="005c0-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="005c0-303">Como configurar o logon único com senha para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="005c0-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="005c0-304">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="005c0-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="005c0-305">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="005c0-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="005c0-306">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="005c0-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="005c0-307">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="005c0-307">Add a non-gallery application</span></span>

<span data-ttu-id="005c0-308">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-309">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="005c0-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="005c0-310">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-311">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-312">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-313">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="005c0-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="005c0-314">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="005c0-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="005c0-315">Insira o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="005c0-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="005c0-316">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="005c0-316">Select **Add.**</span></span>

<span data-ttu-id="005c0-317">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="005c0-318">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="005c0-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="005c0-319">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-320">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="005c0-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="005c0-321">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-322">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-323">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-324">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="005c0-325">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-326">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="005c0-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="005c0-327">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-328">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="005c0-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="005c0-329">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="005c0-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="005c0-330">Trata-se da URL em que os usuários inserem o nome de usuário e senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="005c0-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="005c0-331">Verifique se os campos de entrada estão visíveis na URL.</span><span class="sxs-lookup"><span data-stu-id="005c0-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="005c0-332">[Atribuir usuários ao aplicativo](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="005c0-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="005c0-333">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="005c0-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="005c0-334">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="005c0-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="005c0-335">Problemas relacionados à atribuição de aplicativos para usuários</span><span class="sxs-lookup"><span data-stu-id="005c0-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="005c0-336">Um usuário pode não ver um aplicativo no seu Painel de Acesso porque o usuário não está atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="005c0-337">Abaixo, são apresentadas algumas maneiras de verificação:</span><span class="sxs-lookup"><span data-stu-id="005c0-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="005c0-338">Verificar se um usuário está atribuído ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="005c0-339">Como atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="005c0-340">Verificar se um usuário está atribuído a uma licença relacionada ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="005c0-341">Como atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="005c0-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="005c0-342">Verificar se um usuário está atribuído ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="005c0-343">Para verificar se um usuário está atribuído ao aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-344">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="005c0-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="005c0-345">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-346">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-347">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-348">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="005c0-349">**Pesquise** pelo nome do aplicativo em questão.</span><span class="sxs-lookup"><span data-stu-id="005c0-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="005c0-350">Clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="005c0-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="005c0-351">Verifique se o usuário está atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="005c0-352">Se não, siga as etapas em "Como atribuir um usuário diretamente a um aplicativo" para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="005c0-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="005c0-353">Como atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="005c0-354">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-355">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global**.</span><span class="sxs-lookup"><span data-stu-id="005c0-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="005c0-356">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-357">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-358">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-359">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="005c0-360">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-361">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="005c0-362">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-363">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="005c0-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="005c0-364">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="005c0-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="005c0-365">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="005c0-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="005c0-366">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="005c0-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="005c0-367">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="005c0-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="005c0-368">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="005c0-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="005c0-369">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="005c0-370">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="005c0-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="005c0-371">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="005c0-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="005c0-372">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="005c0-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="005c0-373">Verificar se um usuário está sob uma licença relacionada ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="005c0-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="005c0-374">Para verificar as licenças atribuídas de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-375">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="005c0-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="005c0-376">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-377">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-378">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="005c0-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="005c0-379">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="005c0-379">click **All users**.</span></span>

6.  <span data-ttu-id="005c0-380">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="005c0-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="005c0-381">Clique em **Licenças** para ver quais licenças estão atribuídas ao usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="005c0-382">Se o usuário for atribuído a uma licença do Office, isso permitirá que os aplicativos primários do Office apareçam no Painel de Acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="005c0-383">Como atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="005c0-383">How to assign a user a license</span></span> 

<span data-ttu-id="005c0-384">Para atribuir uma licença a um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-385">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="005c0-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="005c0-386">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-387">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-388">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="005c0-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="005c0-389">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="005c0-389">click **All users**.</span></span>

6.  <span data-ttu-id="005c0-390">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="005c0-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="005c0-391">clique em **Licenças** para ver quais licenças o usuário atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="005c0-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="005c0-392">clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="005c0-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="005c0-393">Selecione **um ou mais produtos** da lista de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="005c0-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="005c0-394">**Opcional** clique no item **opções de atribuição** para atribuir produtos granularmente.</span><span class="sxs-lookup"><span data-stu-id="005c0-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="005c0-395">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="005c0-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="005c0-396">Clique no botão **Atribuir** para atribuir essas licenças para esse usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="005c0-397">Problemas relacionados à atribuição de aplicativos para usuários</span><span class="sxs-lookup"><span data-stu-id="005c0-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="005c0-398">Um usuário pode estar vendo um aplicativo em seu Painel de Acesso por fazer parte de um grupo ao qual o aplicativo foi atribuído.</span><span class="sxs-lookup"><span data-stu-id="005c0-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="005c0-399">Abaixo, são descritas algumas formas de verificar:</span><span class="sxs-lookup"><span data-stu-id="005c0-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="005c0-400">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="005c0-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="005c0-401">Como atribuir um aplicativo diretamente a um grupo</span><span class="sxs-lookup"><span data-stu-id="005c0-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="005c0-402">Verificar se um usuário faz parte do grupo atribuído a uma licença</span><span class="sxs-lookup"><span data-stu-id="005c0-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="005c0-403">Como atribuir uma licença a um grupo</span><span class="sxs-lookup"><span data-stu-id="005c0-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="005c0-404">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="005c0-404">Check a user’s group memberships</span></span>

<span data-ttu-id="005c0-405">Para verificar as associações de um grupo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-406">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="005c0-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="005c0-407">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-408">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-409">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="005c0-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="005c0-410">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="005c0-410">click **All users**.</span></span>

6.  <span data-ttu-id="005c0-411">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="005c0-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="005c0-412">clique em **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="005c0-412">click **Groups**.</span></span>

8.  <span data-ttu-id="005c0-413">Verifique se o usuário faz parte de um Grupo atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="005c0-414">Se você quiser remover o usuário do grupo, **clique na linha** do grupo e selecione excluir.</span><span class="sxs-lookup"><span data-stu-id="005c0-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="005c0-415">Como atribuir um aplicativo diretamente a um grupo</span><span class="sxs-lookup"><span data-stu-id="005c0-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="005c0-416">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-417">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global**.</span><span class="sxs-lookup"><span data-stu-id="005c0-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="005c0-418">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-419">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-420">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="005c0-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="005c0-421">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="005c0-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="005c0-422">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="005c0-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="005c0-423">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="005c0-424">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="005c0-425">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="005c0-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="005c0-426">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="005c0-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="005c0-427">Digite o **nome completo do grupo** que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="005c0-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="005c0-428">Passe o mouse sobre o **grupo** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="005c0-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="005c0-429">Clique na caixa de seleção próxima ao logotipo ou ao perfil do grupo para adicionar o usuário na lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="005c0-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="005c0-430">**Opcional:** caso queira **adicionar mais de um grupo**, digite outro **nome de grupo completo** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse grupo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="005c0-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="005c0-431">Ao concluir a seleção dos grupos, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="005c0-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="005c0-432">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="005c0-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="005c0-433">Clique no botão **Atribuir** para atribuir o aplicativo aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="005c0-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="005c0-434">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="005c0-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="005c0-435">Verificar se um usuário faz parte do grupo atribuído a uma licença</span><span class="sxs-lookup"><span data-stu-id="005c0-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="005c0-436">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="005c0-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="005c0-437">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-438">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-439">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="005c0-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="005c0-440">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="005c0-440">click **All users**.</span></span>

6.  <span data-ttu-id="005c0-441">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="005c0-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="005c0-442">clique em **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="005c0-442">click **Groups**.</span></span>

8.  <span data-ttu-id="005c0-443">clique na linha de um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="005c0-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="005c0-444">Clique em **Licenças** para ver quais licenças o grupo atribuiu a ele.</span><span class="sxs-lookup"><span data-stu-id="005c0-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="005c0-445">Se o grupo for atribuído a uma licença do Office, isso poderá permitir que determinados aplicativos primários do Office apareçam no Painel de Acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="005c0-446">Como atribuir uma licença a um grupo</span><span class="sxs-lookup"><span data-stu-id="005c0-446">How to assign a license to a group</span></span>

<span data-ttu-id="005c0-447">Para atribuir uma licença a um grupo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="005c0-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="005c0-448">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="005c0-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="005c0-449">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="005c0-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="005c0-450">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005c0-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="005c0-451">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="005c0-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="005c0-452">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="005c0-452">click **All groups**.</span></span>

6.  <span data-ttu-id="005c0-453">**Pesquise** pelo grupo no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="005c0-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="005c0-454">clique em **Licenças** para ver quais licenças o grupo atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="005c0-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="005c0-455">clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="005c0-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="005c0-456">Selecione **um ou mais produtos** da lista de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="005c0-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="005c0-457">**Opcional** clique no item **opções de atribuição** para atribuir produtos granularmente.</span><span class="sxs-lookup"><span data-stu-id="005c0-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="005c0-458">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="005c0-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="005c0-459">Clique no botão **Atribuir** para atribuir essas licenças para esse grupo.</span><span class="sxs-lookup"><span data-stu-id="005c0-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="005c0-460">Isso pode levar algum tempo, dependendo do tamanho e da complexidade do grupo.</span><span class="sxs-lookup"><span data-stu-id="005c0-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="005c0-461">Para fazer isso mais rápido, considere atribuir temporariamente uma licença diretamente ao usuário.</span><span class="sxs-lookup"><span data-stu-id="005c0-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="005c0-462">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="005c0-462">Next steps</span></span>
[<span data-ttu-id="005c0-463">Adicionar novos usuários ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="005c0-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

