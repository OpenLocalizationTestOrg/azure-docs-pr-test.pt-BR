---
title: "Problemas ao entrar em um aplicativo inexistente na galeria configurado para logon único federado | Microsoft Docs"
description: "Diretrizes para os problemas específicos que você pode enfrentar ao entrar em um aplicativo configurado para o logon único federado baseado em SAML com Azure AD"
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
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="b95e8-103">Problemas ao entrar em um aplicativo inexistente na galeria configurado para logon único federado</span><span class="sxs-lookup"><span data-stu-id="b95e8-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="b95e8-104">Para solucionar o problema é necessário verificar a configuração do aplicativo no Azure AD, conforme a seguir:</span><span class="sxs-lookup"><span data-stu-id="b95e8-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="b95e8-105">Você seguiu todas as etapas de configuração do aplicativo na galeria do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b95e8-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="b95e8-106">O Identificador e a URL de Resposta configurados no AAD correspondem aos valores esperados no aplicativo</span><span class="sxs-lookup"><span data-stu-id="b95e8-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="b95e8-107">Você atribuiu os usuários para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="b95e8-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="b95e8-108">Aplicativo não encontrado no diretório</span><span class="sxs-lookup"><span data-stu-id="b95e8-108">Application not found in directory</span></span>

<span data-ttu-id="b95e8-109">*Erro AADSTS70001: aplicativo com o identificador ‘https://contoso.com’ não encontrado no diretório*.</span><span class="sxs-lookup"><span data-stu-id="b95e8-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="b95e8-110">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="b95e8-110">**Possible cause**</span></span>

<span data-ttu-id="b95e8-111">O atributo que o Emissor envia do aplicativo para o Azure AD na solicitação SAML não corresponde ao valor do Identificador configurado no aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b95e8-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="b95e8-112">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="b95e8-112">**Resolution**</span></span>

<span data-ttu-id="b95e8-113">Certifique-se de que o atributo Emissor na solicitação SAML corresponde ao valor do Identificador configurado no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b95e8-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="b95e8-114">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b95e8-115">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="b95e8-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b95e8-116">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b95e8-117">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b95e8-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b95e8-118">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e8-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b95e8-119">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b95e8-120">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b95e8-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="b95e8-121">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b95e8-122"><span id="_Hlk477190042" class="anchor"></span>Acesse a seção **Domínio e URLs**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="b95e8-123">Verifique se o valor na caixa de texto Identificador corresponde ao valor para o valor do identificador exibido no erro.</span><span class="sxs-lookup"><span data-stu-id="b95e8-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="b95e8-124">Após atualizar o valor do Identificador no Azure AD e correspondê-lo com o valor enviado pelo aplicativo na solicitação SAML, deverá ser possível entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="b95e8-125">O endereço de resposta não corresponde aos endereços de resposta configurados para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="b95e8-126">*Erro AADSTS50011: O endereço de resposta 'https://contoso.com' não corresponde aos endereços de resposta configurados para o aplicativo*</span><span class="sxs-lookup"><span data-stu-id="b95e8-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="b95e8-127">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="b95e8-127">**Possible cause**</span></span> 

<span data-ttu-id="b95e8-128">O valor de AssertionConsumerServiceURL na solicitação SAML não corresponde ao valor da URL de resposta ou ao padrão configurado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b95e8-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="b95e8-129">O valor de AssertionConsumerServiceURL na solicitação SAML é a URL que você vê no erro.</span><span class="sxs-lookup"><span data-stu-id="b95e8-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="b95e8-130">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="b95e8-130">**Resolution**</span></span> 

<span data-ttu-id="b95e8-131">Verifique se o valor de AssertionConsumerServiceURL na solicitação SAML corresponde ao valor da URL de resposta configurado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b95e8-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="b95e8-132">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="b95e8-133">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="b95e8-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="b95e8-134">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="b95e8-135">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b95e8-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="b95e8-136">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e8-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="b95e8-137">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="b95e8-138">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="b95e8-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="b95e8-139">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b95e8-140">Acesse a seção **Domínio e URLs**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="b95e8-141">Verifique ou atualize o valor na caixa de texto URL de Resposta para corresponder ao valor AssertionConsumerServiceURL na solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="b95e8-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="b95e8-142">Se você não vir a caixa de texto URL de Resposta, selecione a caixa de seleção **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="b95e8-143">Após atualizar o valor da URL de Resposta no Azure AD e correspondê-lo com o valor enviado pelo aplicativo na solicitação SAML, deverá ser possível entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="b95e8-144">Usuário não atribuído a uma função</span><span class="sxs-lookup"><span data-stu-id="b95e8-144">User not assigned a role</span></span>

<span data-ttu-id="b95e8-145">*Erro AADSTS50105: o usuário conectado 'brian@contoso.com' não está atribuído a uma função para o aplicativo*</span><span class="sxs-lookup"><span data-stu-id="b95e8-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="b95e8-146">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="b95e8-146">**Possible cause**</span></span>

<span data-ttu-id="b95e8-147">O usuário não teve acesso concedido para o aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b95e8-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="b95e8-148">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="b95e8-148">**Resolution**</span></span>

<span data-ttu-id="b95e8-149">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="b95e8-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="b95e8-150">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b95e8-151">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="b95e8-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b95e8-152">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b95e8-153">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b95e8-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b95e8-154">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e8-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b95e8-155">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b95e8-156">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="b95e8-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="b95e8-157">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b95e8-158">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b95e8-159">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b95e8-160">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b95e8-161">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="b95e8-162">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="b95e8-163">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="b95e8-164">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="b95e8-165">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="b95e8-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="b95e8-166">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="b95e8-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="b95e8-167">Após um breve período, os usuários que você selecionou poderão iniciar esses aplicativos usando os métodos descritos na seção de descrição da solução.</span><span class="sxs-lookup"><span data-stu-id="b95e8-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="b95e8-168">Não é uma solicitação SAML válida</span><span class="sxs-lookup"><span data-stu-id="b95e8-168">Not a valid SAML Request</span></span>

<span data-ttu-id="b95e8-169">*Erro AADSTS75005: a solicitação não é uma mensagem de protocolo Saml2 válida.*</span><span class="sxs-lookup"><span data-stu-id="b95e8-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="b95e8-170">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="b95e8-170">**Possible cause**</span></span>

<span data-ttu-id="b95e8-171">O Azure AD não oferece suporte para a solicitação SAML enviada pelo aplicativo para logon único.</span><span class="sxs-lookup"><span data-stu-id="b95e8-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="b95e8-172">Alguns problemas comuns são:</span><span class="sxs-lookup"><span data-stu-id="b95e8-172">Some common issues are:</span></span>

-   <span data-ttu-id="b95e8-173">Campos obrigatórios ausentes na solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="b95e8-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="b95e8-174">Método codificado de solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="b95e8-174">SAML request encoded method</span></span>

<span data-ttu-id="b95e8-175">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="b95e8-175">**Resolution**</span></span>

1.  <span data-ttu-id="b95e8-176">Capturar solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="b95e8-176">Capture SAML request.</span></span> <span data-ttu-id="b95e8-177">siga o tutorial em [como depurar o logon único baseado em SAML em aplicativos no Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) para saber mais sobre como capturar a solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="b95e8-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="b95e8-178">Contate o fornecedor do aplicativo e compartilhe:</span><span class="sxs-lookup"><span data-stu-id="b95e8-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="b95e8-179">Solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="b95e8-179">SAML request</span></span>

    -   [<span data-ttu-id="b95e8-180">Requisitos de protocolo SAML de logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b95e8-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="b95e8-181">Eles devem validar que oferecem suporte à implementação do SAML do Azure AD para Logon Único.</span><span class="sxs-lookup"><span data-stu-id="b95e8-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="b95e8-182">Nenhum recurso na lista requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="b95e8-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="b95e8-183">*Erro AADSTS65005: o aplicativo cliente solicitou acesso ao recurso '00000002-0000-0000-c000-000000000000'. Essa solicitação falhou porque o cliente não especificou esse recurso na sua lista requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="b95e8-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="b95e8-184">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="b95e8-184">**Possible cause**</span></span>

<span data-ttu-id="b95e8-185">O objeto de aplicativo está corrompido.</span><span class="sxs-lookup"><span data-stu-id="b95e8-185">The application object is corrupted.</span></span>

<span data-ttu-id="b95e8-186">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="b95e8-186">**Resolution**</span></span>

<span data-ttu-id="b95e8-187">Para resolver o problema, remova o aplicativo do diretório.</span><span class="sxs-lookup"><span data-stu-id="b95e8-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="b95e8-188">Em seguida, adicione e reconfigurar o aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="b95e8-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="b95e8-189">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b95e8-190">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="b95e8-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b95e8-191">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b95e8-192">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b95e8-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b95e8-193">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e8-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b95e8-194">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b95e8-195">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b95e8-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="b95e8-196">Clique em **Excluir** na parte superior esquerda da folha **Visão Geral** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="b95e8-197">Atualize o Azure AD e Adicione o aplicativo da galeria do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b95e8-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="b95e8-198">Em seguida, Configure novamente o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-198">Then, Configure the application again.</span></span>

<span data-ttu-id="b95e8-199">Após reconfigurar o aplicativo, deverá ser possível entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="b95e8-200">Chave ou certificado não configurado</span><span class="sxs-lookup"><span data-stu-id="b95e8-200">Certificate or key not configured</span></span>

<span data-ttu-id="b95e8-201">Erro AADSTS50003: nenhuma chave de assinatura configurada.</span><span class="sxs-lookup"><span data-stu-id="b95e8-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="b95e8-202">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="b95e8-202">**Possible cause**</span></span>

<span data-ttu-id="b95e8-203">O objeto de aplicativo está corrompido e o Azure AD não reconhece o certificado configurado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="b95e8-204">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="b95e8-204">**Resolution**</span></span>

<span data-ttu-id="b95e8-205">Para excluir e criar um novo certificado, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="b95e8-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="b95e8-206">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b95e8-207">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="b95e8-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b95e8-208">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b95e8-209">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b95e8-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b95e8-210">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e8-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b95e8-211">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b95e8-212">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b95e8-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="b95e8-213">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e8-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b95e8-214">clique em **Criar novo certificado** na seção **Certificado de Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="b95e8-215">Selecione a data de validade.</span><span class="sxs-lookup"><span data-stu-id="b95e8-215">Select Expiration date.</span></span> <span data-ttu-id="b95e8-216">Em seguida, clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b95e8-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="b95e8-217">Marque **Tornar o novo certificado ativo** para substituir o certificado ative.</span><span class="sxs-lookup"><span data-stu-id="b95e8-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="b95e8-218">Em seguida, clique em **Salvar** na parte superior da folha e aceite para ativar o certificado de substituição.</span><span class="sxs-lookup"><span data-stu-id="b95e8-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="b95e8-219">Na seção **Certificado de Autenticação SAML**, clique em **remover** para remover o certificado **Não Usado**.</span><span class="sxs-lookup"><span data-stu-id="b95e8-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="b95e8-220">Problema ao personalizar as declarações SAML enviadas para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="b95e8-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="b95e8-221">Para saber como personalizar as declarações de atributo SAML enviadas para seu aplicativo, consulte [Mapeamento de declarações no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b95e8-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b95e8-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b95e8-222">Next steps</span></span>
[<span data-ttu-id="b95e8-223">Requisitos de protocolo SAML de logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b95e8-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
