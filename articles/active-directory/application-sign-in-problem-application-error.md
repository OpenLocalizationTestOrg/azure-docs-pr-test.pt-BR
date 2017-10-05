---
title: "Erro em uma página de aplicativo após a entrada | Microsoft Docs"
description: "Como resolver problemas com a entrada do Azure AD quando o próprio aplicativo emite um erro"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="89905-103">Erro em uma página de aplicativo após a entrada</span><span class="sxs-lookup"><span data-stu-id="89905-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="89905-104">Nesse cenário, o Azure AD conectou o usuário mas o aplicativo está exibindo um erro que não permite ao usuário concluir o fluxo de entrada com êxito.</span><span class="sxs-lookup"><span data-stu-id="89905-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="89905-105">Nesse cenário, o aplicativo não está aceitando a resposta emitida pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="89905-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="89905-106">Há alguns motivos possíveis por que o aplicativo não aceitou a resposta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89905-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="89905-107">Se o erro no aplicativo não for suficientemente claro para saber o que está faltando na resposta, então:</span><span class="sxs-lookup"><span data-stu-id="89905-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="89905-108">Se o aplicativo for a Galeria do Azure AD, verifique se você seguiu todas as etapas do artigo [Como depurar o Logon único baseado em SAML para aplicativos no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="89905-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="89905-109">Use uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) para capturar solicitação SAML, resposta SAML e token SAML.</span><span class="sxs-lookup"><span data-stu-id="89905-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="89905-110">Compartilhe a resposta SAML com o fornecedor do aplicativo para saber o que está faltando.</span><span class="sxs-lookup"><span data-stu-id="89905-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="89905-111">Atributos ausentes na resposta SAML</span><span class="sxs-lookup"><span data-stu-id="89905-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="89905-112">Para adicionar um atributo na configuração do Azure AD para ser enviado na resposta do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="89905-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="89905-113">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="89905-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="89905-114">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="89905-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="89905-115">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89905-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="89905-116">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89905-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="89905-117">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="89905-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="89905-118">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="89905-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="89905-119">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="89905-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="89905-120">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89905-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="89905-121">clique em **Exibir e editar todos os outros atributos de usuário em** na seção **Atributos de Usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="89905-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="89905-122">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="89905-122">To add an attribute:</span></span>

   * <span data-ttu-id="89905-123">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="89905-123">click **Add attribute**.</span></span> <span data-ttu-id="89905-124">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="89905-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="89905-125">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="89905-125">Click **Save.**</span></span> <span data-ttu-id="89905-126">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="89905-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="89905-127">Salve a configuração.</span><span class="sxs-lookup"><span data-stu-id="89905-127">Save the configuration.</span></span>

<span data-ttu-id="89905-128">Na próxima vez em que o usuário entrar no aplicativo, o Azure AD enviará o novo atributo na resposta SAML.</span><span class="sxs-lookup"><span data-stu-id="89905-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="89905-129">O aplicativo espera um formato ou valor de Identificador de Usuário diferente</span><span class="sxs-lookup"><span data-stu-id="89905-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="89905-130">A entrada para o aplicativo está falhando porque na resposta SAML está faltando atributos como funções ou porque o aplicativo está esperando um formato diferente para o atributo EntityID.</span><span class="sxs-lookup"><span data-stu-id="89905-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="89905-131">Adicione um atributo na configuração do aplicativo do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="89905-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="89905-132">Para alterar o valor do Identificador de Usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="89905-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="89905-133">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="89905-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="89905-134">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="89905-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="89905-135">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89905-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="89905-136">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89905-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="89905-137">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="89905-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="89905-138">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="89905-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="89905-139">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="89905-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="89905-140">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89905-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="89905-141">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="89905-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="89905-142">Alterar o formato EntityID (Identificador de Usuário)</span><span class="sxs-lookup"><span data-stu-id="89905-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="89905-143">Se o aplicativo espera outro formato para o atributo EntityID.</span><span class="sxs-lookup"><span data-stu-id="89905-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="89905-144">Então, não será possível selecionar o formato EntityID (Identificador de Usuário) que o Azure AD envia para o aplicativo na resposta após a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="89905-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="89905-145">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="89905-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="89905-146">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="89905-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="89905-147">O aplicativo espera um método de assinatura diferente para a resposta SAML</span><span class="sxs-lookup"><span data-stu-id="89905-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="89905-148">Para alterar quais partes do token SAML são assinadas digitalmente pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="89905-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="89905-149">Siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="89905-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="89905-150">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="89905-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="89905-151">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="89905-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="89905-152">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89905-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="89905-153">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89905-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="89905-154">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="89905-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="89905-155">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="89905-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="89905-156">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="89905-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="89905-157">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89905-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="89905-158">Clique em **Mostrar configurações avançadas de assinatura de certificado** na seção **Certificado de Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="89905-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="89905-159">Selecione a **Opção de Assinatura** apropriada esperada pelo aplicativo:</span><span class="sxs-lookup"><span data-stu-id="89905-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="89905-160">Assinar resposta SAML</span><span class="sxs-lookup"><span data-stu-id="89905-160">Sign SAML response</span></span>

  * <span data-ttu-id="89905-161">Assinar resposta SAML e declaração</span><span class="sxs-lookup"><span data-stu-id="89905-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="89905-162">Assinar declaração SAML</span><span class="sxs-lookup"><span data-stu-id="89905-162">Sign SAML assertion</span></span>

<span data-ttu-id="89905-163">Na próxima vez em que o usuário entrar no aplicativo, o Azure AD assinará a parte da resposta SAML selecionada.</span><span class="sxs-lookup"><span data-stu-id="89905-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="89905-164">O aplicativo espera que o algoritmo de assinatura seja SHA-1</span><span class="sxs-lookup"><span data-stu-id="89905-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="89905-165">Por padrão, o Azure AD assina o token SAML usando o algoritmo de maior segurança.</span><span class="sxs-lookup"><span data-stu-id="89905-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="89905-166">Não é recomendável alterar o algoritmo de assinatura SHA-1, exceto se exigido pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89905-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="89905-167">Para alterar o algoritmo de assinatura, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="89905-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="89905-168">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="89905-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="89905-169">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="89905-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="89905-170">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89905-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="89905-171">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89905-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="89905-172">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="89905-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="89905-173">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="89905-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="89905-174">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="89905-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="89905-175">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89905-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="89905-176">Clique em **Mostrar configurações avançadas de assinatura de certificado** na seção **Certificado de Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="89905-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="89905-177">Selecione o SHA-1, no **Algoritmo de Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="89905-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="89905-178">Na próxima vez em que o usuário entrar no aplicativo, o Azure AD assinará o token SAML usando o algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="89905-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89905-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89905-179">Next steps</span></span>
[<span data-ttu-id="89905-180">Como depurar o logon único baseado em SAML em aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="89905-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
