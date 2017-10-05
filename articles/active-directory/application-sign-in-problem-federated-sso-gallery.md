---
title: "Problemas ao entrar em um aplicativo na galeria configurado para logon único federado | Microsoft Docs"
description: "Diretrizes para os erros específicos ao entrar em um aplicativo configurado para o logon único federado baseado em SAML com Azure AD"
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
ms.openlocfilehash: 0fc5a8eb3d033d60bf6082d61bf1698924ab91c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="e8600-103">Problemas ao entrar em um aplicativo na galeria configurado para logon único federado</span><span class="sxs-lookup"><span data-stu-id="e8600-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="e8600-104">Para solucionar o problema é necessário verificar a configuração do aplicativo no Azure AD, conforme a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8600-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="e8600-105">Você seguiu todas as etapas de configuração do aplicativo na galeria do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="e8600-106">O Identificador e a URL de Resposta configurados no AAD correspondem aos valores esperados no aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8600-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="e8600-107">Você atribuiu os usuários para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8600-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="e8600-108">Aplicativo não encontrado no diretório</span><span class="sxs-lookup"><span data-stu-id="e8600-108">Application not found in directory</span></span>

<span data-ttu-id="e8600-109">*Erro AADSTS70001: aplicativo com o identificador ‘https://contoso.com’ não encontrado no diretório*.</span><span class="sxs-lookup"><span data-stu-id="e8600-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="e8600-110">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="e8600-110">**Possible cause**</span></span>

<span data-ttu-id="e8600-111">O atributo que o Emissor envia do aplicativo para o Azure AD na solicitação SAML não corresponde ao valor do Identificador configurado no aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="e8600-112">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="e8600-112">**Resolution**</span></span>

<span data-ttu-id="e8600-113">Certifique-se de que o atributo Emissor na solicitação SAML corresponde ao valor do Identificador configurado no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e8600-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="e8600-114">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="e8600-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8600-115">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="e8600-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8600-116">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8600-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8600-117">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8600-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8600-118">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e8600-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e8600-119">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="e8600-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e8600-120">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="e8600-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="e8600-121">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e8600-122">Acesse a seção **Domínio e URLs**.</span><span class="sxs-lookup"><span data-stu-id="e8600-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="e8600-123">Verifique se o valor na caixa de texto Identificador corresponde ao valor para o valor do identificador exibido no erro.</span><span class="sxs-lookup"><span data-stu-id="e8600-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="e8600-124">Após atualizar o valor do Identificador no Azure AD e correspondê-lo com o valor enviado pelo aplicativo na solicitação SAML, deverá ser possível entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="e8600-125">O endereço de resposta não corresponde aos endereços de resposta configurados para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-125">The reply address does not match the reply addresses configured for the application.</span></span>

<span data-ttu-id="e8600-126">*Erro AADSTS50011: O endereço de resposta 'https://contoso.com' não corresponde aos endereços de resposta configurados para o aplicativo*</span><span class="sxs-lookup"><span data-stu-id="e8600-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span>

<span data-ttu-id="e8600-127">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="e8600-127">**Possible cause**</span></span>

<span data-ttu-id="e8600-128">O valor de AssertionConsumerServiceURL na solicitação SAML não corresponde ao valor da URL de resposta ou ao padrão configurado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="e8600-129">O valor de AssertionConsumerServiceURL na solicitação SAML é a URL que você vê no erro.</span><span class="sxs-lookup"><span data-stu-id="e8600-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span>

<span data-ttu-id="e8600-130">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="e8600-130">**Resolution**</span></span>

<span data-ttu-id="e8600-131">Verifique se o valor de AssertionConsumerServiceURL na solicitação SAML corresponde ao valor da URL de resposta configurado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="e8600-132">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="e8600-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8600-133">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="e8600-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8600-134">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8600-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8600-135">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8600-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8600-136">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e8600-136">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e8600-137">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="e8600-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e8600-138">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="e8600-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="e8600-139">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e8600-140">Acesse a seção **Domínio e URLs**.</span><span class="sxs-lookup"><span data-stu-id="e8600-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="e8600-141">Verifique ou atualize o valor na caixa de texto URL de Resposta para corresponder ao valor AssertionConsumerServiceURL na solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="e8600-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>  
    * <span data-ttu-id="e8600-142">Se você não vir a caixa de texto URL de Resposta, selecione a caixa de seleção **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="e8600-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="e8600-143">Após atualizar o valor da URL de Resposta no Azure AD e correspondê-lo com o valor enviado pelo aplicativo na solicitação SAML, deverá ser possível entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="e8600-144">Usuário não atribuído a uma função</span><span class="sxs-lookup"><span data-stu-id="e8600-144">User not assigned a role</span></span>

<span data-ttu-id="e8600-145">*Erro AADSTS50105: o usuário conectado 'brian@contoso.com' não está atribuído a uma função para o aplicativo*.</span><span class="sxs-lookup"><span data-stu-id="e8600-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="e8600-146">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="e8600-146">**Possible cause**</span></span>

<span data-ttu-id="e8600-147">O usuário não teve acesso concedido para o aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="e8600-148">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="e8600-148">**Resolution**</span></span>

<span data-ttu-id="e8600-149">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e8600-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="e8600-150">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="e8600-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e8600-151">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="e8600-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8600-152">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8600-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8600-153">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8600-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8600-154">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e8600-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e8600-155">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="e8600-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e8600-156">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="e8600-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="e8600-157">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e8600-158">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="e8600-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e8600-159">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="e8600-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e8600-160">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="e8600-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e8600-161">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="e8600-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="e8600-162">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="e8600-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="e8600-163">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="e8600-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="e8600-164">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="e8600-165">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="e8600-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="e8600-166">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="e8600-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="e8600-167">Após um breve período, os usuários que você selecionou poderão iniciar esses aplicativos usando os métodos descritos na seção de descrição da solução.</span><span class="sxs-lookup"><span data-stu-id="e8600-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="e8600-168">Não é uma solicitação SAML válida</span><span class="sxs-lookup"><span data-stu-id="e8600-168">Not a valid SAML Request</span></span>

<span data-ttu-id="e8600-169">*Erro AADSTS75005: a solicitação não é uma mensagem de protocolo Saml2 válida.*</span><span class="sxs-lookup"><span data-stu-id="e8600-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="e8600-170">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="e8600-170">**Possible cause**</span></span>

<span data-ttu-id="e8600-171">O Azure AD não oferece suporte para a solicitação SAML enviada pelo aplicativo para logon único.</span><span class="sxs-lookup"><span data-stu-id="e8600-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="e8600-172">Alguns problemas comuns são:</span><span class="sxs-lookup"><span data-stu-id="e8600-172">Some common issues are:</span></span>

-   <span data-ttu-id="e8600-173">Campos obrigatórios ausentes na solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="e8600-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="e8600-174">Método codificado de solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="e8600-174">SAML request encoded method</span></span>

<span data-ttu-id="e8600-175">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="e8600-175">**Resolution**</span></span>

1.  <span data-ttu-id="e8600-176">Capturar solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="e8600-176">Capture SAML request.</span></span> <span data-ttu-id="e8600-177">siga o tutorial em [Como depurar o logon único baseado em SAML em aplicativos no Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) para saber mais sobre como capturar a solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="e8600-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="e8600-178">Contate o fornecedor do aplicativo e compartilhe:</span><span class="sxs-lookup"><span data-stu-id="e8600-178">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="e8600-179">Solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="e8600-179">SAML request</span></span>

   -   [<span data-ttu-id="e8600-180">Requisitos de protocolo SAML de logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8600-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="e8600-181">Eles devem validar que oferecem suporte à implementação do SAML do Azure AD para Logon Único.</span><span class="sxs-lookup"><span data-stu-id="e8600-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="e8600-182">Nenhum recurso na lista requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="e8600-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="e8600-183">*Erro AADSTS65005: o aplicativo cliente solicitou acesso ao recurso '00000002-0000-0000-c000-000000000000'. Essa solicitação falhou porque o cliente não especificou esse recurso na sua lista requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="e8600-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="e8600-184">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="e8600-184">**Possible cause**</span></span>

<span data-ttu-id="e8600-185">O objeto de aplicativo está corrompido.</span><span class="sxs-lookup"><span data-stu-id="e8600-185">The application object is corrupted.</span></span>

<span data-ttu-id="e8600-186">**Resolução: opção 1**</span><span class="sxs-lookup"><span data-stu-id="e8600-186">**Resolution: option 1**</span></span>

<span data-ttu-id="e8600-187">Para resolver o problema, adicione o valor do identificador exclusivo na configuração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span></span> <span data-ttu-id="e8600-188">Para adicionar um valor de identificador, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e8600-188">To add a Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="e8600-189">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="e8600-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8600-190">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="e8600-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8600-191">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8600-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8600-192">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8600-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8600-193">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e8600-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e8600-194">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="e8600-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e8600-195">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e8600-195">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e8600-196">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8600-196">Once the application loads, click on the **Single sign-on** from the application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="e8600-197">Na seção **Domínio e URL**, marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="e8600-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="e8600-198">Na caixa de texto **Identificador**, digite um identificador exclusivo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-198">in the **Identifier** textbox type a unique identifier for the application.</span></span>

10. <span data-ttu-id="e8600-199">**Salve** a configuração.</span><span class="sxs-lookup"><span data-stu-id="e8600-199">**Save** the configuration.</span></span>


<span data-ttu-id="e8600-200">**Resolução: opção 2**</span><span class="sxs-lookup"><span data-stu-id="e8600-200">**Resolution option 2**</span></span>

<span data-ttu-id="e8600-201">Se a opção 1 acima não funcionou, tente remover o aplicativo do diretório.</span><span class="sxs-lookup"><span data-stu-id="e8600-201">If option 1 above did not work for you, try removing the application from the directory.</span></span> <span data-ttu-id="e8600-202">Em seguida, adicione e reconfigurar o aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e8600-202">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="e8600-203">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="e8600-203">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8600-204">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="e8600-204">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8600-205">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8600-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8600-206">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8600-206">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8600-207">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e8600-207">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e8600-208">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="e8600-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e8600-209">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="e8600-209">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="e8600-210">Clique em **Excluir** na parte superior esquerda da folha **Visão Geral** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-210">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="e8600-211">Atualize o Azure AD e Adicione o aplicativo da galeria do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8600-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="e8600-212">Em seguida, Configure o aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8600-212">Then, Configure the application</span></span>

<span data-ttu-id="e8600-213"><span id="_Hlk477190176" class="anchor"></span>Após reconfigurar o aplicativo, deverá ser possível entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="e8600-214">Chave ou certificado não configurado</span><span class="sxs-lookup"><span data-stu-id="e8600-214">Certificate or key not configured</span></span>

<span data-ttu-id="e8600-215">*Erro AADSTS50003: nenhuma chave de assinatura configurada.*</span><span class="sxs-lookup"><span data-stu-id="e8600-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="e8600-216">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="e8600-216">**Possible cause**</span></span>

<span data-ttu-id="e8600-217">O objeto de aplicativo está corrompido e o Azure AD não reconhece o certificado configurado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="e8600-218">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="e8600-218">**Resolution**</span></span>

<span data-ttu-id="e8600-219">Para excluir e criar um novo certificado, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e8600-219">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="e8600-220">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="e8600-220">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8600-221">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="e8600-221">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8600-222">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8600-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8600-223">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8600-223">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8600-224">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e8600-224">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="e8600-225">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="e8600-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e8600-226">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="e8600-226">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="e8600-227">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8600-227">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e8600-228">clique em **Criar novo certificado** na seção **Certificado de Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="e8600-228">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="e8600-229">Selecione a data de validade.</span><span class="sxs-lookup"><span data-stu-id="e8600-229">Select Expiration date.</span></span> <span data-ttu-id="e8600-230">Em seguida, clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="e8600-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="e8600-231">Marque **Tornar o novo certificado ativo** para substituir o certificado ative.</span><span class="sxs-lookup"><span data-stu-id="e8600-231">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="e8600-232">Em seguida, clique em **Salvar** na parte superior da folha e aceite para ativar o certificado de substituição.</span><span class="sxs-lookup"><span data-stu-id="e8600-232">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="e8600-233">Na seção **Certificado de Autenticação SAML**, clique em **remover** para remover o certificado **Não Usado**.</span><span class="sxs-lookup"><span data-stu-id="e8600-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="e8600-234">Problema ao personalizar as declarações SAML enviadas para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8600-234">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="e8600-235">Para saber como personalizar as declarações de atributo SAML enviadas para seu aplicativo, consulte [Mapeamento de declarações no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e8600-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8600-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8600-236">Next steps</span></span>
[<span data-ttu-id="e8600-237">Como depurar o logon único baseado em SAML em aplicativos no do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8600-237">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
