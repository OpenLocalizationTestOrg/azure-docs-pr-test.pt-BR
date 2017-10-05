---
title: "Políticas de autenticação de Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre as políticas de autenticação disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="3ef21-103">Políticas de autenticação de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="3ef21-103">API Management authentication policies</span></span>
<span data-ttu-id="3ef21-104">Este tópico fornece uma referência para as políticas de Gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ef21-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="3ef21-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="3ef21-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="3ef21-106"><a name="AuthenticationPolicies"></a> Políticas de autenticação</span><span class="sxs-lookup"><span data-stu-id="3ef21-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="3ef21-107">[Autenticar com o Basic](api-management-authentication-policies.md#Basic) - Autenticar com um serviço de back-end usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="3ef21-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="3ef21-108">[Autenticar com o certificado de cliente](api-management-authentication-policies.md#ClientCertificate) - Autenticar com um serviço de back-end usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="3ef21-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="3ef21-109"><a name="Basic"></a> Autenticar com o Basic</span><span class="sxs-lookup"><span data-stu-id="3ef21-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="3ef21-110">Use a política `authentication-basic` para autenticar com um serviço de back-end usando a autenticação do Basic.</span><span class="sxs-lookup"><span data-stu-id="3ef21-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="3ef21-111">Essa política define efetivamente o cabeçalho de autorização HTTP para o valor correspondente às credenciais fornecidas na política.</span><span class="sxs-lookup"><span data-stu-id="3ef21-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3ef21-112">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="3ef21-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="3ef21-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3ef21-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="3ef21-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="3ef21-114">Elements</span></span>  
  
|<span data-ttu-id="3ef21-115">Nome</span><span class="sxs-lookup"><span data-stu-id="3ef21-115">Name</span></span>|<span data-ttu-id="3ef21-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ef21-116">Description</span></span>|<span data-ttu-id="3ef21-117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3ef21-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3ef21-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="3ef21-118">authentication-basic</span></span>|<span data-ttu-id="3ef21-119">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="3ef21-119">Root element.</span></span>|<span data-ttu-id="3ef21-120">Sim</span><span class="sxs-lookup"><span data-stu-id="3ef21-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3ef21-121">Atributos</span><span class="sxs-lookup"><span data-stu-id="3ef21-121">Attributes</span></span>  
  
|<span data-ttu-id="3ef21-122">Nome</span><span class="sxs-lookup"><span data-stu-id="3ef21-122">Name</span></span>|<span data-ttu-id="3ef21-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ef21-123">Description</span></span>|<span data-ttu-id="3ef21-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3ef21-124">Required</span></span>|<span data-ttu-id="3ef21-125">Padrão</span><span class="sxs-lookup"><span data-stu-id="3ef21-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3ef21-126">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="3ef21-126">username</span></span>|<span data-ttu-id="3ef21-127">Especifica o nome de usuário da credencial do Basic.</span><span class="sxs-lookup"><span data-stu-id="3ef21-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="3ef21-128">Sim</span><span class="sxs-lookup"><span data-stu-id="3ef21-128">Yes</span></span>|<span data-ttu-id="3ef21-129">N/D</span><span class="sxs-lookup"><span data-stu-id="3ef21-129">N/A</span></span>|  
|<span data-ttu-id="3ef21-130">Senha</span><span class="sxs-lookup"><span data-stu-id="3ef21-130">password</span></span>|<span data-ttu-id="3ef21-131">Especifica a senha da credencial do Basic.</span><span class="sxs-lookup"><span data-stu-id="3ef21-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="3ef21-132">Sim</span><span class="sxs-lookup"><span data-stu-id="3ef21-132">Yes</span></span>|<span data-ttu-id="3ef21-133">N/D</span><span class="sxs-lookup"><span data-stu-id="3ef21-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3ef21-134">Uso</span><span class="sxs-lookup"><span data-stu-id="3ef21-134">Usage</span></span>  
 <span data-ttu-id="3ef21-135">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ef21-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3ef21-136">**Seções de política:** entrada</span><span class="sxs-lookup"><span data-stu-id="3ef21-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3ef21-137">**Escopos de política:** API</span><span class="sxs-lookup"><span data-stu-id="3ef21-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="3ef21-138"><a name="ClientCertificate"></a> Autenticar com o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="3ef21-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="3ef21-139">Use a política `authentication-certificate` para autenticar com um serviço de back-end usando um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="3ef21-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="3ef21-140">O certificado precisa ser [instalado no Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=511599) primeiro e é identificado por sua impressão digital.</span><span class="sxs-lookup"><span data-stu-id="3ef21-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3ef21-141">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="3ef21-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="3ef21-142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3ef21-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="3ef21-143">Elementos</span><span class="sxs-lookup"><span data-stu-id="3ef21-143">Elements</span></span>  
  
|<span data-ttu-id="3ef21-144">Nome</span><span class="sxs-lookup"><span data-stu-id="3ef21-144">Name</span></span>|<span data-ttu-id="3ef21-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ef21-145">Description</span></span>|<span data-ttu-id="3ef21-146">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3ef21-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3ef21-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="3ef21-147">authentication-certificate</span></span>|<span data-ttu-id="3ef21-148">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="3ef21-148">Root element.</span></span>|<span data-ttu-id="3ef21-149">Sim</span><span class="sxs-lookup"><span data-stu-id="3ef21-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3ef21-150">Atributos</span><span class="sxs-lookup"><span data-stu-id="3ef21-150">Attributes</span></span>  
  
|<span data-ttu-id="3ef21-151">Nome</span><span class="sxs-lookup"><span data-stu-id="3ef21-151">Name</span></span>|<span data-ttu-id="3ef21-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ef21-152">Description</span></span>|<span data-ttu-id="3ef21-153">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3ef21-153">Required</span></span>|<span data-ttu-id="3ef21-154">Padrão</span><span class="sxs-lookup"><span data-stu-id="3ef21-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3ef21-155">impressão digital</span><span class="sxs-lookup"><span data-stu-id="3ef21-155">thumbprint</span></span>|<span data-ttu-id="3ef21-156">A impressão digital do certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="3ef21-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="3ef21-157">Sim</span><span class="sxs-lookup"><span data-stu-id="3ef21-157">Yes</span></span>|<span data-ttu-id="3ef21-158">N/D</span><span class="sxs-lookup"><span data-stu-id="3ef21-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3ef21-159">Uso</span><span class="sxs-lookup"><span data-stu-id="3ef21-159">Usage</span></span>  
 <span data-ttu-id="3ef21-160">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ef21-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3ef21-161">**Seções de política:** entrada</span><span class="sxs-lookup"><span data-stu-id="3ef21-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3ef21-162">**Escopos de política:** API</span><span class="sxs-lookup"><span data-stu-id="3ef21-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="3ef21-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ef21-163">Next steps</span></span>
<span data-ttu-id="3ef21-164">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3ef21-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  