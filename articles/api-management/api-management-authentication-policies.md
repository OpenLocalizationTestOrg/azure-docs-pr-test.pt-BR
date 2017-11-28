---
title: "políticas de autenticação de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre as políticas de autenticação Olá disponíveis para uso no gerenciamento de API do Azure."
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
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="adab9-103">Políticas de autenticação de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="adab9-103">API Management authentication policies</span></span>
<span data-ttu-id="adab9-104">Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="adab9-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="adab9-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="adab9-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="adab9-106"><a name="AuthenticationPolicies"></a> Políticas de autenticação</span><span class="sxs-lookup"><span data-stu-id="adab9-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="adab9-107">[Autenticar com o Basic](api-management-authentication-policies.md#Basic) - Autenticar com um serviço de back-end usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="adab9-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="adab9-108">[Autenticar com o certificado de cliente](api-management-authentication-policies.md#ClientCertificate) - Autenticar com um serviço de back-end usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="adab9-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="adab9-109"><a name="Basic"></a> Autenticar com o Basic</span><span class="sxs-lookup"><span data-stu-id="adab9-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="adab9-110">Saudação de uso `authentication-basic` tooauthenticate de política com um serviço de back-end usando a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="adab9-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="adab9-111">Essa política define efetivamente toohello de cabeçalho de autorização HTTP Olá valor correspondente toohello as credenciais fornecidas na política de saudação.</span><span class="sxs-lookup"><span data-stu-id="adab9-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="adab9-112">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="adab9-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="adab9-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="adab9-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="adab9-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="adab9-114">Elements</span></span>  
  
|<span data-ttu-id="adab9-115">Nome</span><span class="sxs-lookup"><span data-stu-id="adab9-115">Name</span></span>|<span data-ttu-id="adab9-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="adab9-116">Description</span></span>|<span data-ttu-id="adab9-117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="adab9-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="adab9-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="adab9-118">authentication-basic</span></span>|<span data-ttu-id="adab9-119">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="adab9-119">Root element.</span></span>|<span data-ttu-id="adab9-120">Sim</span><span class="sxs-lookup"><span data-stu-id="adab9-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="adab9-121">Atributos</span><span class="sxs-lookup"><span data-stu-id="adab9-121">Attributes</span></span>  
  
|<span data-ttu-id="adab9-122">Nome</span><span class="sxs-lookup"><span data-stu-id="adab9-122">Name</span></span>|<span data-ttu-id="adab9-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="adab9-123">Description</span></span>|<span data-ttu-id="adab9-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="adab9-124">Required</span></span>|<span data-ttu-id="adab9-125">Padrão</span><span class="sxs-lookup"><span data-stu-id="adab9-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="adab9-126">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="adab9-126">username</span></span>|<span data-ttu-id="adab9-127">Especifica o nome de usuário de saudação da credencial básica hello.</span><span class="sxs-lookup"><span data-stu-id="adab9-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="adab9-128">Sim</span><span class="sxs-lookup"><span data-stu-id="adab9-128">Yes</span></span>|<span data-ttu-id="adab9-129">N/D</span><span class="sxs-lookup"><span data-stu-id="adab9-129">N/A</span></span>|  
|<span data-ttu-id="adab9-130">Senha</span><span class="sxs-lookup"><span data-stu-id="adab9-130">password</span></span>|<span data-ttu-id="adab9-131">Especifica a senha de saudação da credencial básica hello.</span><span class="sxs-lookup"><span data-stu-id="adab9-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="adab9-132">Sim</span><span class="sxs-lookup"><span data-stu-id="adab9-132">Yes</span></span>|<span data-ttu-id="adab9-133">N/D</span><span class="sxs-lookup"><span data-stu-id="adab9-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="adab9-134">Uso</span><span class="sxs-lookup"><span data-stu-id="adab9-134">Usage</span></span>  
 <span data-ttu-id="adab9-135">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="adab9-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="adab9-136">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="adab9-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="adab9-137">**Escopos de política:** API</span><span class="sxs-lookup"><span data-stu-id="adab9-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="adab9-138"><a name="ClientCertificate"></a> Autenticar com o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="adab9-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="adab9-139">Saudação de uso `authentication-certificate` tooauthenticate de política com um serviço de back-end usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="adab9-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="adab9-140">certificado Olá precisa toobe [instalado no gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=511599) primeiro e é identificado por sua impressão digital.</span><span class="sxs-lookup"><span data-stu-id="adab9-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="adab9-141">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="adab9-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="adab9-142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="adab9-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="adab9-143">Elementos</span><span class="sxs-lookup"><span data-stu-id="adab9-143">Elements</span></span>  
  
|<span data-ttu-id="adab9-144">Nome</span><span class="sxs-lookup"><span data-stu-id="adab9-144">Name</span></span>|<span data-ttu-id="adab9-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="adab9-145">Description</span></span>|<span data-ttu-id="adab9-146">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="adab9-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="adab9-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="adab9-147">authentication-certificate</span></span>|<span data-ttu-id="adab9-148">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="adab9-148">Root element.</span></span>|<span data-ttu-id="adab9-149">Sim</span><span class="sxs-lookup"><span data-stu-id="adab9-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="adab9-150">Atributos</span><span class="sxs-lookup"><span data-stu-id="adab9-150">Attributes</span></span>  
  
|<span data-ttu-id="adab9-151">Nome</span><span class="sxs-lookup"><span data-stu-id="adab9-151">Name</span></span>|<span data-ttu-id="adab9-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="adab9-152">Description</span></span>|<span data-ttu-id="adab9-153">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="adab9-153">Required</span></span>|<span data-ttu-id="adab9-154">Padrão</span><span class="sxs-lookup"><span data-stu-id="adab9-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="adab9-155">impressão digital</span><span class="sxs-lookup"><span data-stu-id="adab9-155">thumbprint</span></span>|<span data-ttu-id="adab9-156">Olá a impressão digital do certificado de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="adab9-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="adab9-157">Sim</span><span class="sxs-lookup"><span data-stu-id="adab9-157">Yes</span></span>|<span data-ttu-id="adab9-158">N/D</span><span class="sxs-lookup"><span data-stu-id="adab9-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="adab9-159">Uso</span><span class="sxs-lookup"><span data-stu-id="adab9-159">Usage</span></span>  
 <span data-ttu-id="adab9-160">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="adab9-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="adab9-161">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="adab9-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="adab9-162">**Escopos de política:** API</span><span class="sxs-lookup"><span data-stu-id="adab9-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="adab9-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adab9-163">Next steps</span></span>
<span data-ttu-id="adab9-164">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="adab9-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  