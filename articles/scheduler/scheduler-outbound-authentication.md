---
title: "Autenticação de Saída do Agendador"
description: "Autenticação de Saída do Agendador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: e345b2e22daae5b24c23645f7d2636f66df630ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="7f61c-103">Autenticação de Saída do Agendador</span><span class="sxs-lookup"><span data-stu-id="7f61c-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="7f61c-104">Os trabalhos do Agendador podem precisar chamar serviços que requerem autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-104">Scheduler jobs may need to call out to services that require authentication.</span></span> <span data-ttu-id="7f61c-105">Dessa forma, um serviço chamado pode determinar se o trabalho do Agendador poderá acessar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="7f61c-105">This way, a called service can determine if the Scheduler job can access its resources.</span></span> <span data-ttu-id="7f61c-106">Alguns desses serviços incluem outros serviços do Azure, Salesforce.com, Facebook e sites seguros personalizados.</span><span class="sxs-lookup"><span data-stu-id="7f61c-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="7f61c-107">Adição e Remoção de Autenticação</span><span class="sxs-lookup"><span data-stu-id="7f61c-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="7f61c-108">Adicionar a autenticação para um trabalho do Agendador é simples: adicione um elemento filho JSON `authentication` para o elemento `request` ao criar ou atualizar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="7f61c-108">Adding authentication to a Scheduler job is simple – add a JSON child element `authentication` to the `request` element when creating or updating a job.</span></span> <span data-ttu-id="7f61c-109">Os segredos passados para o serviço do Agendador em uma solicitação PUT, PATCH ou POST, como parte do objeto `authentication` , nunca são retornados em respostas.</span><span class="sxs-lookup"><span data-stu-id="7f61c-109">Secrets passed to the Scheduler service in a PUT, PATCH, or POST request – as part of the `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="7f61c-110">Nas respostas, as informações secretas são definidas como nulo ou podem ter um token público que representa a entidade autenticada.</span><span class="sxs-lookup"><span data-stu-id="7f61c-110">In responses, secret information is set to null or may have a public token that represents the authenticated entity.</span></span>

<span data-ttu-id="7f61c-111">Para remover a autenticação, faça PUT ou PATCH do trabalho explicitamente, configurando o objeto `authentication` como nulo.</span><span class="sxs-lookup"><span data-stu-id="7f61c-111">To remove authentication, PUT or PATCH the job explicitly, setting the `authentication` object to null.</span></span> <span data-ttu-id="7f61c-112">Você não verá quaisquer propriedades de autenticação na resposta.</span><span class="sxs-lookup"><span data-stu-id="7f61c-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="7f61c-113">Atualmente, os únicos tipos de autenticação com suporte são o modelo `ClientCertificate` (para uso dos certificados de cliente SSL/TLS), o modelo `Basic` (para autenticação básica) e o modelo `ActiveDirectoryOAuth` (para autenticação OAuth do Active Directory.)</span><span class="sxs-lookup"><span data-stu-id="7f61c-113">Currently, the only supported authentication types are the `ClientCertificate` model (for using the SSL/TLS client certificates), the `Basic` model (for Basic authentication), and the `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="7f61c-114">Corpo da solicitação de autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7f61c-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="7f61c-115">Ao adicionar a autenticação usando o modelo `ClientCertificate` , especifique os seguintes elementos adicionais no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-115">When adding authentication using the `ClientCertificate` model, specify the following additional elements in the request body.</span></span>  

| <span data-ttu-id="7f61c-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="7f61c-116">Element</span></span> | <span data-ttu-id="7f61c-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f61c-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f61c-118">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="7f61c-118">*authentication (parent element)*</span></span> |<span data-ttu-id="7f61c-119">Objeto de autenticação para usar um certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="7f61c-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="7f61c-120">*tipo*</span><span class="sxs-lookup"><span data-stu-id="7f61c-120">*type*</span></span> |<span data-ttu-id="7f61c-121">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-121">Required.</span></span> <span data-ttu-id="7f61c-122">Tipo de autenticação. Para certificados de cliente SSL, o valor deve ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="7f61c-122">Type of authentication.For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="7f61c-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="7f61c-123">*pfx*</span></span> |<span data-ttu-id="7f61c-124">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-124">Required.</span></span> <span data-ttu-id="7f61c-125">Conteúdo codificado na Base64 do arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="7f61c-125">Base64-encoded contents of the PFX file.</span></span> |
| <span data-ttu-id="7f61c-126">*password*</span><span class="sxs-lookup"><span data-stu-id="7f61c-126">*password*</span></span> |<span data-ttu-id="7f61c-127">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-127">Required.</span></span> <span data-ttu-id="7f61c-128">Senha para acessar o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="7f61c-128">Password to access the PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="7f61c-129">Corpo da resposta para autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7f61c-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="7f61c-130">Quando uma solicitação é enviada com as informações de autenticação, a resposta contém os seguintes elementos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-130">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="7f61c-131">Elemento</span><span class="sxs-lookup"><span data-stu-id="7f61c-131">Element</span></span> | <span data-ttu-id="7f61c-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f61c-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f61c-133">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="7f61c-133">*authentication (parent element)*</span></span> |<span data-ttu-id="7f61c-134">Objeto de autenticação para usar um certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="7f61c-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="7f61c-135">*tipo*</span><span class="sxs-lookup"><span data-stu-id="7f61c-135">*type*</span></span> |<span data-ttu-id="7f61c-136">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-136">Type of authentication.</span></span> <span data-ttu-id="7f61c-137">Para certificados de cliente SSL, o valor é `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="7f61c-137">For SSL client certificates, the value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="7f61c-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="7f61c-138">*certificateThumbprint*</span></span> |<span data-ttu-id="7f61c-139">A impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="7f61c-139">The thumbprint of the certificate.</span></span> |
| <span data-ttu-id="7f61c-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="7f61c-140">*certificateSubjectName*</span></span> |<span data-ttu-id="7f61c-141">O nome distinto da entidade do certificado.</span><span class="sxs-lookup"><span data-stu-id="7f61c-141">The subject distinguished name of the certificate.</span></span> |
| <span data-ttu-id="7f61c-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="7f61c-142">*certificateExpiration*</span></span> |<span data-ttu-id="7f61c-143">A data de validade do certificado.</span><span class="sxs-lookup"><span data-stu-id="7f61c-143">The expiration date of the certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="7f61c-144">Exemplo de solicitação REST para autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7f61c-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="7f61c-145">Exemplo de resposta REST para autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7f61c-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="7f61c-146">Corpo da solicitação de autenticação básica</span><span class="sxs-lookup"><span data-stu-id="7f61c-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="7f61c-147">Ao adicionar a autenticação usando o modelo `Basic` , especifique os seguintes elementos adicionais no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-147">When adding authentication using the `Basic` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="7f61c-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="7f61c-148">Element</span></span> | <span data-ttu-id="7f61c-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f61c-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f61c-150">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="7f61c-150">*authentication (parent element)*</span></span> |<span data-ttu-id="7f61c-151">Objeto de autenticação para usar a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="7f61c-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="7f61c-152">*tipo*</span><span class="sxs-lookup"><span data-stu-id="7f61c-152">*type*</span></span> |<span data-ttu-id="7f61c-153">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-153">Required.</span></span> <span data-ttu-id="7f61c-154">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-154">Type of authentication.</span></span> <span data-ttu-id="7f61c-155">Para a autenticação básica, o valor deve ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="7f61c-155">For Basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="7f61c-156">*username*</span><span class="sxs-lookup"><span data-stu-id="7f61c-156">*username*</span></span> |<span data-ttu-id="7f61c-157">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-157">Required.</span></span> <span data-ttu-id="7f61c-158">Nome de usuário para autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-158">Username to authenticate.</span></span> |
| <span data-ttu-id="7f61c-159">*password*</span><span class="sxs-lookup"><span data-stu-id="7f61c-159">*password*</span></span> |<span data-ttu-id="7f61c-160">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-160">Required.</span></span> <span data-ttu-id="7f61c-161">Senha para autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-161">Password to authenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="7f61c-162">Corpo da resposta de autenticação básica</span><span class="sxs-lookup"><span data-stu-id="7f61c-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="7f61c-163">Quando uma solicitação é enviada com as informações de autenticação, a resposta contém os seguintes elementos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-163">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="7f61c-164">Elemento</span><span class="sxs-lookup"><span data-stu-id="7f61c-164">Element</span></span> | <span data-ttu-id="7f61c-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f61c-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f61c-166">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="7f61c-166">*authentication (parent element)*</span></span> |<span data-ttu-id="7f61c-167">Objeto de autenticação para usar a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="7f61c-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="7f61c-168">*tipo*</span><span class="sxs-lookup"><span data-stu-id="7f61c-168">*type*</span></span> |<span data-ttu-id="7f61c-169">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-169">Type of authentication.</span></span> <span data-ttu-id="7f61c-170">Para a autenticação básica, o valor é `Basic`.</span><span class="sxs-lookup"><span data-stu-id="7f61c-170">For Basic authentication, the value is `Basic`.</span></span> |
| <span data-ttu-id="7f61c-171">*username*</span><span class="sxs-lookup"><span data-stu-id="7f61c-171">*username*</span></span> |<span data-ttu-id="7f61c-172">O nome de usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="7f61c-172">The authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="7f61c-173">Exemplo de solicitação REST para autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="7f61c-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="7f61c-174">Exemplo de resposta REST para autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="7f61c-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7f61c-175">Corpo da solicitação de autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7f61c-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="7f61c-176">Ao adicionar a autenticação usando o modelo `ActiveDirectoryOAuth` , especifique os seguintes elementos adicionais no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-176">When adding authentication using the `ActiveDirectoryOAuth` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="7f61c-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="7f61c-177">Element</span></span> | <span data-ttu-id="7f61c-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f61c-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f61c-179">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="7f61c-179">*authentication (parent element)*</span></span> |<span data-ttu-id="7f61c-180">Objeto de autenticação para usar a autenticação ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="7f61c-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="7f61c-181">*tipo*</span><span class="sxs-lookup"><span data-stu-id="7f61c-181">*type*</span></span> |<span data-ttu-id="7f61c-182">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-182">Required.</span></span> <span data-ttu-id="7f61c-183">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-183">Type of authentication.</span></span> <span data-ttu-id="7f61c-184">Para autenticação de ActiveDirectoryOAuth, o valor deve ser `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="7f61c-184">For ActiveDirectoryOAuth authentication, the value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="7f61c-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="7f61c-185">*tenant*</span></span> |<span data-ttu-id="7f61c-186">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-186">Required.</span></span> <span data-ttu-id="7f61c-187">O identificador do locatário para o locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f61c-187">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="7f61c-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="7f61c-188">*audience*</span></span> |<span data-ttu-id="7f61c-189">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-189">Required.</span></span> <span data-ttu-id="7f61c-190">Isso é definido como https://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="7f61c-190">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="7f61c-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="7f61c-191">*clientId*</span></span> |<span data-ttu-id="7f61c-192">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-192">Required.</span></span> <span data-ttu-id="7f61c-193">Forneça o identificador de cliente para o aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61c-193">Provide the client identifier for the Azure AD application.</span></span> |
| <span data-ttu-id="7f61c-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="7f61c-194">*secret*</span></span> |<span data-ttu-id="7f61c-195">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f61c-195">Required.</span></span> <span data-ttu-id="7f61c-196">Segredo do cliente que está solicitando o token.</span><span class="sxs-lookup"><span data-stu-id="7f61c-196">Secret of the client that is requesting the token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="7f61c-197">Determinando o identificador do locatário</span><span class="sxs-lookup"><span data-stu-id="7f61c-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="7f61c-198">Você pode encontrar o identificador do locatário para o locatário do Azure AD executando `Get-AzureAccount` no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f61c-198">You can find the tenant identifier for the Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7f61c-199">Corpo da resposta de autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7f61c-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="7f61c-200">Quando uma solicitação é enviada com as informações de autenticação, a resposta contém os seguintes elementos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-200">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="7f61c-201">Elemento</span><span class="sxs-lookup"><span data-stu-id="7f61c-201">Element</span></span> | <span data-ttu-id="7f61c-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f61c-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f61c-203">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="7f61c-203">*authentication (parent element)*</span></span> |<span data-ttu-id="7f61c-204">Objeto de autenticação para usar a autenticação ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="7f61c-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="7f61c-205">*tipo*</span><span class="sxs-lookup"><span data-stu-id="7f61c-205">*type*</span></span> |<span data-ttu-id="7f61c-206">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7f61c-206">Type of authentication.</span></span> <span data-ttu-id="7f61c-207">Para autenticação de ActiveDirectoryOAuth, o valor é `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="7f61c-207">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="7f61c-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="7f61c-208">*tenant*</span></span> |<span data-ttu-id="7f61c-209">O identificador do locatário para o locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f61c-209">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="7f61c-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="7f61c-210">*audience*</span></span> |<span data-ttu-id="7f61c-211">Isso é definido como https://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="7f61c-211">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="7f61c-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="7f61c-212">*clientId*</span></span> |<span data-ttu-id="7f61c-213">O identificador de cliente para o aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61c-213">The client identifier for the Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7f61c-214">Exemplo de solicitação REST para autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7f61c-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="7f61c-215">Exemplo de resposta REST para autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="7f61c-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="7f61c-216">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7f61c-216">See Also</span></span>
 [<span data-ttu-id="7f61c-217">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="7f61c-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="7f61c-218">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="7f61c-219">Introdução à utilização do Agendador no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-219">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="7f61c-220">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="7f61c-221">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="7f61c-222">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="7f61c-223">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="7f61c-224">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="7f61c-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

