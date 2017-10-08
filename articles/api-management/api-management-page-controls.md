---
title: "controles de página de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os controles de página Olá disponíveis para uso em modelos de portal do desenvolvedor no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="244e8-103">Controles de página do Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="244e8-103">Azure API Management page controls</span></span>
<span data-ttu-id="244e8-104">Gerenciamento de API do Azure fornece Olá controles para uso em modelos portal do desenvolvedor Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="244e8-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="244e8-105">toouse um controle, colocá-lo no local de saudação desejada no modelo de portal de desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="244e8-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="244e8-106">Alguns controles, como Olá [ações de aplicativo](#app-actions) controlar, tiver parâmetros, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="244e8-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="244e8-107">valores Hello para parâmetros de saudação são passados como parte do modelo de dados Olá para o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="244e8-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="244e8-108">Na maioria dos casos, você poderá simplesmente colar em Olá fornecido exemplo para cada controle para que ele toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="244e8-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="244e8-109">Para obter mais informações sobre valores de parâmetro hello, você pode ver a seção de modelo de dados Olá para cada modelo no qual um controle pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="244e8-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="244e8-110">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="244e8-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="244e8-111">Controles de página do modelo do portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="244e8-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="244e8-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="244e8-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="244e8-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="244e8-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="244e8-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="244e8-115">providers</span><span class="sxs-lookup"><span data-stu-id="244e8-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="244e8-116">search-control</span><span class="sxs-lookup"><span data-stu-id="244e8-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="244e8-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="244e8-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="244e8-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="244e8-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="244e8-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="244e8-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="244e8-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="244e8-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="244e8-121">Olá `app-actions` controle fornece uma interface do usuário para interagir com aplicativos na página de perfil de usuário Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="244e8-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="244e8-122">![controle app&#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "controle app-actions do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-123">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-124">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-124">Parameters</span></span>  
  
|<span data-ttu-id="244e8-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="244e8-125">Parameter</span></span>|<span data-ttu-id="244e8-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="244e8-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="244e8-127">appId</span><span class="sxs-lookup"><span data-stu-id="244e8-127">appId</span></span>|<span data-ttu-id="244e8-128">id de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="244e8-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-129">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-129">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-130">Olá `app-actions` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-131">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="244e8-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="244e8-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="244e8-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="244e8-133">Olá `basic-signin` controle fornece um controle de entrada do usuário coleta informações Olá entrar na página no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="244e8-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="244e8-134">![controle basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "controle basic-signin do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-135">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-136">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-136">Parameters</span></span>  
 <span data-ttu-id="244e8-137">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="244e8-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-138">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-138">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-139">Olá `basic-signin` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-140">Entrar</span><span class="sxs-lookup"><span data-stu-id="244e8-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="244e8-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="244e8-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="244e8-142">Olá `paging-control` fornece funcionalidade de paginação desenvolvedor páginas do portal que exibem uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="244e8-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="244e8-143">![controle paging](./media/api-management-page-controls/APIM-paging-control.png "controle paging do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-144">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-145">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-145">Parameters</span></span>  
 <span data-ttu-id="244e8-146">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="244e8-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-147">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-147">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-148">Olá `paging-control` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-149">Lista de APIs</span><span class="sxs-lookup"><span data-stu-id="244e8-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="244e8-150">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="244e8-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="244e8-151">Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="244e8-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="244e8-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="244e8-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="244e8-153">Olá `providers` controle fornece um controle para seleção de provedores de autenticação na página no portal do desenvolvedor Olá Olá entrada.</span><span class="sxs-lookup"><span data-stu-id="244e8-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="244e8-154">![controle providers](./media/api-management-page-controls/APIM-providers-control.png "controle providers do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-155">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-156">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-156">Parameters</span></span>  
 <span data-ttu-id="244e8-157">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="244e8-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-158">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-158">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-159">Olá `providers` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-160">Entrar</span><span class="sxs-lookup"><span data-stu-id="244e8-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="244e8-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="244e8-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="244e8-162">Olá `search-control` fornece funcionalidade de pesquisa em desenvolvedor páginas do portal que exibem uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="244e8-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="244e8-163">![controle search](./media/api-management-page-controls/APIM-search-control.png "controle search do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-164">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-165">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-165">Parameters</span></span>  
 <span data-ttu-id="244e8-166">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="244e8-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-167">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-167">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-168">Olá `search-control` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-169">Lista de APIs</span><span class="sxs-lookup"><span data-stu-id="244e8-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="244e8-170">Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="244e8-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="244e8-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="244e8-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="244e8-172">Olá `sign-up` controle fornece um controle para coletar informações de perfil do usuário na página no portal do desenvolvedor Olá de inscrição hello.</span><span class="sxs-lookup"><span data-stu-id="244e8-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="244e8-173">![controle sign&#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "controle sign-up do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-174">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-175">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-175">Parameters</span></span>  
 <span data-ttu-id="244e8-176">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="244e8-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-177">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-177">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-178">Olá `sign-up` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-179">Inscrever-se</span><span class="sxs-lookup"><span data-stu-id="244e8-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="244e8-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="244e8-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="244e8-181">Olá `subscribe-button` fornece um controle de assinatura de um produto de tooa do usuário.</span><span class="sxs-lookup"><span data-stu-id="244e8-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="244e8-182">![controle subscribe&#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "controle subscribe-button do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-183">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-184">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-184">Parameters</span></span>  
 <span data-ttu-id="244e8-185">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="244e8-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-186">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-186">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-187">Olá `subscribe-button` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-188">Produto</span><span class="sxs-lookup"><span data-stu-id="244e8-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="244e8-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="244e8-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="244e8-190">Olá `subscription-cancel` controle fornece um controle para cancelar um produto de tooa de assinatura na página de perfil de usuário Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="244e8-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="244e8-191">![controle subscription&#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "controle subscription-cancel do APIM")</span><span class="sxs-lookup"><span data-stu-id="244e8-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="244e8-192">Uso</span><span class="sxs-lookup"><span data-stu-id="244e8-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="244e8-193">parâmetros</span><span class="sxs-lookup"><span data-stu-id="244e8-193">Parameters</span></span>  
  
|<span data-ttu-id="244e8-194">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="244e8-194">Parameter</span></span>|<span data-ttu-id="244e8-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="244e8-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="244e8-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="244e8-196">subscriptionId</span></span>|<span data-ttu-id="244e8-197">id de saudação do hello toocancel de assinatura.</span><span class="sxs-lookup"><span data-stu-id="244e8-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="244e8-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="244e8-198">cancelUrl</span></span>|<span data-ttu-id="244e8-199">Cancelar a assinatura Olá URL.</span><span class="sxs-lookup"><span data-stu-id="244e8-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="244e8-200">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="244e8-200">Developer portal templates</span></span>  
 <span data-ttu-id="244e8-201">Olá `subscription-cancel` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="244e8-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="244e8-202">Produto</span><span class="sxs-lookup"><span data-stu-id="244e8-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="244e8-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="244e8-203">Next steps</span></span>
<span data-ttu-id="244e8-204">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="244e8-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
