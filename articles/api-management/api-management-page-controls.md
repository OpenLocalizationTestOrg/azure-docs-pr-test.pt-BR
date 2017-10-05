---
title: "Controles de página do Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre os controles de página disponíveis para uso em modelos de portal do desenvolvedor no Gerenciamento de API do Azure."
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
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="b9ae5-103">Controles de página do Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ae5-103">Azure API Management page controls</span></span>
<span data-ttu-id="b9ae5-104">O Gerenciamento de API do Azure fornece os controles a seguir para uso em modelos de portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="b9ae5-105">Para usar um controle, coloque-o no local desejado no modelo do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="b9ae5-106">Alguns controles, como o [app-actions](#app-actions), têm parâmetros, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="b9ae5-107">Os valores para os parâmetros são passados como parte do modelo de dados do modelo.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="b9ae5-108">Na maioria dos casos, você pode simplesmente colar o exemplo fornecido para cada controle para que ele funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="b9ae5-109">Para obter mais informações sobre os valores de parâmetro, você pode ver a seção de modelo de dados de cada modelo no qual um controle pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="b9ae5-110">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="b9ae5-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="b9ae5-111">Controles de página do modelo do portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="b9ae5-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="b9ae5-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="b9ae5-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="b9ae5-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="b9ae5-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="b9ae5-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="b9ae5-115">providers</span><span class="sxs-lookup"><span data-stu-id="b9ae5-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="b9ae5-116">search-control</span><span class="sxs-lookup"><span data-stu-id="b9ae5-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="b9ae5-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="b9ae5-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="b9ae5-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="b9ae5-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="b9ae5-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="b9ae5-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="b9ae5-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="b9ae5-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="b9ae5-121">O controle `app-actions` fornece uma interface de usuário para interação com aplicativos na página de perfil do usuário no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b9ae5-122">![controle app&#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "controle app-actions do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-123">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-124">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-124">Parameters</span></span>  
  
|<span data-ttu-id="b9ae5-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b9ae5-125">Parameter</span></span>|<span data-ttu-id="b9ae5-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9ae5-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="b9ae5-127">appId</span><span class="sxs-lookup"><span data-stu-id="b9ae5-127">appId</span></span>|<span data-ttu-id="b9ae5-128">A ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-129">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-129">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-130">O controle `app-actions` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-131">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="b9ae5-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="b9ae5-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="b9ae5-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="b9ae5-133">O controle `basic-signin` fornece um controle para coletar informações de entrada do usuário na página de entrada do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="b9ae5-134">![controle basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "controle basic-signin do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-135">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-136">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-136">Parameters</span></span>  
 <span data-ttu-id="b9ae5-137">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-138">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-138">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-139">O controle `basic-signin` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-140">Entrar</span><span class="sxs-lookup"><span data-stu-id="b9ae5-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="b9ae5-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="b9ae5-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="b9ae5-142">O `paging-control` fornece funcionalidade de paginação nas páginas do portal do desenvolvedor que exibem uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="b9ae5-143">![controle paging](./media/api-management-page-controls/APIM-paging-control.png "controle paging do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-144">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-145">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-145">Parameters</span></span>  
 <span data-ttu-id="b9ae5-146">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-147">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-147">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-148">O controle `paging-control` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-149">Lista de APIs</span><span class="sxs-lookup"><span data-stu-id="b9ae5-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="b9ae5-150">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="b9ae5-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="b9ae5-151">Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="b9ae5-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="b9ae5-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="b9ae5-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="b9ae5-153">O controle `providers` fornece um controle para seleção de provedores de autenticação na página de entrada do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="b9ae5-154">![controle providers](./media/api-management-page-controls/APIM-providers-control.png "controle providers do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-155">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-156">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-156">Parameters</span></span>  
 <span data-ttu-id="b9ae5-157">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-158">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-158">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-159">O controle `providers` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-160">Entrar</span><span class="sxs-lookup"><span data-stu-id="b9ae5-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="b9ae5-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="b9ae5-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="b9ae5-162">O `search-control` fornece funcionalidade de pesquisa nas páginas do portal do desenvolvedor que exibem uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="b9ae5-163">![controle search](./media/api-management-page-controls/APIM-search-control.png "controle search do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-164">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-165">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-165">Parameters</span></span>  
 <span data-ttu-id="b9ae5-166">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-167">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-167">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-168">O controle `search-control` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-169">Lista de APIs</span><span class="sxs-lookup"><span data-stu-id="b9ae5-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="b9ae5-170">Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="b9ae5-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="b9ae5-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="b9ae5-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="b9ae5-172">O controle `sign-up` fornece um controle para coletar informações de perfil do usuário na página de entrada do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="b9ae5-173">![controle sign&#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "controle sign-up do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-174">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-175">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-175">Parameters</span></span>  
 <span data-ttu-id="b9ae5-176">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-177">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-177">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-178">O controle `sign-up` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-179">Inscrever-se</span><span class="sxs-lookup"><span data-stu-id="b9ae5-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="b9ae5-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="b9ae5-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="b9ae5-181">O `subscribe-button` fornece um controle de assinatura de um usuário para um produto.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="b9ae5-182">![controle subscribe&#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "controle subscribe-button do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-183">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-184">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-184">Parameters</span></span>  
 <span data-ttu-id="b9ae5-185">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-186">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-186">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-187">O controle `subscribe-button` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-188">Produto</span><span class="sxs-lookup"><span data-stu-id="b9ae5-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="b9ae5-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="b9ae5-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="b9ae5-190">O controle `subscription-cancel` fornece um controle para cancelar uma assinatura de um produto na página de perfil do usuário no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b9ae5-191">![controle subscription&#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "controle subscription-cancel do APIM")</span><span class="sxs-lookup"><span data-stu-id="b9ae5-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="b9ae5-192">Uso</span><span class="sxs-lookup"><span data-stu-id="b9ae5-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="b9ae5-193">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b9ae5-193">Parameters</span></span>  
  
|<span data-ttu-id="b9ae5-194">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b9ae5-194">Parameter</span></span>|<span data-ttu-id="b9ae5-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9ae5-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="b9ae5-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b9ae5-196">subscriptionId</span></span>|<span data-ttu-id="b9ae5-197">A ID da assinatura a ser cancelada.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="b9ae5-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="b9ae5-198">cancelUrl</span></span>|<span data-ttu-id="b9ae5-199">A URL de cancelamento da assinatura.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="b9ae5-200">Modelos de portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="b9ae5-200">Developer portal templates</span></span>  
 <span data-ttu-id="b9ae5-201">O controle `subscription-cancel` pode ser usado nos modelos de portal do desenvolvedor a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9ae5-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="b9ae5-202">Produto</span><span class="sxs-lookup"><span data-stu-id="b9ae5-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="b9ae5-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9ae5-203">Next steps</span></span>
<span data-ttu-id="b9ae5-204">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b9ae5-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>