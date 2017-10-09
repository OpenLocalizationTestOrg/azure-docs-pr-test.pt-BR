---
title: "aaaScheduler autenticação de saída"
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
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="2b9ed-103">Autenticação de Saída do Agendador</span><span class="sxs-lookup"><span data-stu-id="2b9ed-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="2b9ed-104">Trabalhos do Agendador talvez seja necessário toocall out tooservices que requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="2b9ed-105">Dessa forma, um serviço chamado pode determinar se o trabalho do Agendador Olá poderá acessar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="2b9ed-106">Alguns desses serviços incluem outros serviços do Azure, Salesforce.com, Facebook e sites seguros personalizados.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="2b9ed-107">Adição e Remoção de Autenticação</span><span class="sxs-lookup"><span data-stu-id="2b9ed-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="2b9ed-108">Adicionando o trabalho do Agendador tooa autenticação é simple: Adicione um elemento filho JSON `authentication` toohello `request` elemento ao criar ou atualizar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="2b9ed-109">Segredos passados toohello serviço do Agendador em uma solicitação PUT, PATCH ou POST – como parte da saudação `authentication` objeto – nunca são retornados em respostas.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="2b9ed-110">Nas respostas, informações secretas estão definidas toonull ou podem ter um token público que representa a entidade Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="2b9ed-111">autenticação tooremove, PUT ou PATCH trabalho Olá explicitamente, definindo Olá `authentication` toonull do objeto.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="2b9ed-112">Você não verá quaisquer propriedades de autenticação na resposta.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="2b9ed-113">Atualmente, os tipos de autenticação Olá só tem suportada estão Olá `ClientCertificate` modelo (para usar certificados de cliente SSL/TLS Olá), Olá `Basic` de modelo (para autenticação básica) e Olá `ActiveDirectoryOAuth` modelo (para o Active Directory OAuth autenticação).</span><span class="sxs-lookup"><span data-stu-id="2b9ed-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="2b9ed-114">Corpo da solicitação de autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="2b9ed-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="2b9ed-115">Ao adicionar a autenticação usando Olá `ClientCertificate` de modelo, especifique Olá elementos adicionais no corpo da solicitação Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="2b9ed-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b9ed-116">Element</span></span> | <span data-ttu-id="2b9ed-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b9ed-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2b9ed-118">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-118">*authentication (parent element)*</span></span> |<span data-ttu-id="2b9ed-119">Objeto de autenticação para usar um certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="2b9ed-120">*tipo*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-120">*type*</span></span> |<span data-ttu-id="2b9ed-121">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-121">Required.</span></span> <span data-ttu-id="2b9ed-122">Tipo de autenticação. Para certificados de cliente SSL, o valor de saudação deve ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="2b9ed-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-123">*pfx*</span></span> |<span data-ttu-id="2b9ed-124">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-124">Required.</span></span> <span data-ttu-id="2b9ed-125">Conteúdo codificado na Base64 do arquivo PFX de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="2b9ed-126">*password*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-126">*password*</span></span> |<span data-ttu-id="2b9ed-127">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-127">Required.</span></span> <span data-ttu-id="2b9ed-128">Arquivo PFX do senha tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="2b9ed-129">Corpo da resposta para autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="2b9ed-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="2b9ed-130">Quando uma solicitação é enviada com informações de autenticação, a resposta de saudação contém Olá elementos de autenticação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="2b9ed-131">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b9ed-131">Element</span></span> | <span data-ttu-id="2b9ed-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b9ed-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2b9ed-133">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-133">*authentication (parent element)*</span></span> |<span data-ttu-id="2b9ed-134">Objeto de autenticação para usar um certificado de cliente SSL.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="2b9ed-135">*tipo*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-135">*type*</span></span> |<span data-ttu-id="2b9ed-136">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-136">Type of authentication.</span></span> <span data-ttu-id="2b9ed-137">Para certificados de cliente SSL, o valor de saudação é `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="2b9ed-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-138">*certificateThumbprint*</span></span> |<span data-ttu-id="2b9ed-139">impressão digital de saudação do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="2b9ed-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-140">*certificateSubjectName*</span></span> |<span data-ttu-id="2b9ed-141">Olá nome diferenciado do assunto do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="2b9ed-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-142">*certificateExpiration*</span></span> |<span data-ttu-id="2b9ed-143">Data de expiração de saudação do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="2b9ed-144">Exemplo de solicitação REST para autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="2b9ed-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="2b9ed-145">Exemplo de resposta REST para autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="2b9ed-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="2b9ed-146">Corpo da solicitação de autenticação básica</span><span class="sxs-lookup"><span data-stu-id="2b9ed-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="2b9ed-147">Ao adicionar a autenticação usando Olá `Basic` de modelo, especifique Olá elementos adicionais no corpo da solicitação Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="2b9ed-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b9ed-148">Element</span></span> | <span data-ttu-id="2b9ed-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b9ed-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2b9ed-150">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-150">*authentication (parent element)*</span></span> |<span data-ttu-id="2b9ed-151">Objeto de autenticação para usar a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="2b9ed-152">*tipo*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-152">*type*</span></span> |<span data-ttu-id="2b9ed-153">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-153">Required.</span></span> <span data-ttu-id="2b9ed-154">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-154">Type of authentication.</span></span> <span data-ttu-id="2b9ed-155">Para a autenticação básica, o valor de saudação deve ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="2b9ed-156">*username*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-156">*username*</span></span> |<span data-ttu-id="2b9ed-157">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-157">Required.</span></span> <span data-ttu-id="2b9ed-158">Nome de usuário tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="2b9ed-159">*password*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-159">*password*</span></span> |<span data-ttu-id="2b9ed-160">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-160">Required.</span></span> <span data-ttu-id="2b9ed-161">Senha tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="2b9ed-162">Corpo da resposta de autenticação básica</span><span class="sxs-lookup"><span data-stu-id="2b9ed-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="2b9ed-163">Quando uma solicitação é enviada com informações de autenticação, a resposta de saudação contém Olá elementos de autenticação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="2b9ed-164">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b9ed-164">Element</span></span> | <span data-ttu-id="2b9ed-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b9ed-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2b9ed-166">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-166">*authentication (parent element)*</span></span> |<span data-ttu-id="2b9ed-167">Objeto de autenticação para usar a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="2b9ed-168">*tipo*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-168">*type*</span></span> |<span data-ttu-id="2b9ed-169">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-169">Type of authentication.</span></span> <span data-ttu-id="2b9ed-170">Para a autenticação básica, o valor de saudação é `Basic`.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="2b9ed-171">*username*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-171">*username*</span></span> |<span data-ttu-id="2b9ed-172">Olá autenticado o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="2b9ed-173">Exemplo de solicitação REST para autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="2b9ed-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="2b9ed-174">Exemplo de resposta REST para autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="2b9ed-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="2b9ed-175">Corpo da solicitação de autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="2b9ed-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="2b9ed-176">Ao adicionar a autenticação usando Olá `ActiveDirectoryOAuth` de modelo, especifique Olá elementos adicionais no corpo da solicitação Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="2b9ed-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b9ed-177">Element</span></span> | <span data-ttu-id="2b9ed-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b9ed-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2b9ed-179">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-179">*authentication (parent element)*</span></span> |<span data-ttu-id="2b9ed-180">Objeto de autenticação para usar a autenticação ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="2b9ed-181">*tipo*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-181">*type*</span></span> |<span data-ttu-id="2b9ed-182">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-182">Required.</span></span> <span data-ttu-id="2b9ed-183">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-183">Type of authentication.</span></span> <span data-ttu-id="2b9ed-184">Para autenticação do ActiveDirectoryOAuth, o valor de saudação deve ser `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="2b9ed-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-185">*tenant*</span></span> |<span data-ttu-id="2b9ed-186">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-186">Required.</span></span> <span data-ttu-id="2b9ed-187">Identificador do locatário Olá para o locatário de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="2b9ed-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-188">*audience*</span></span> |<span data-ttu-id="2b9ed-189">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-189">Required.</span></span> <span data-ttu-id="2b9ed-190">Isso é definido toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="2b9ed-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-191">*clientId*</span></span> |<span data-ttu-id="2b9ed-192">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-192">Required.</span></span> <span data-ttu-id="2b9ed-193">Forneça o identificador de saudação do cliente para Olá aplicativo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="2b9ed-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-194">*secret*</span></span> |<span data-ttu-id="2b9ed-195">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-195">Required.</span></span> <span data-ttu-id="2b9ed-196">Segredo do cliente Olá que está solicitando o token hello.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="2b9ed-197">Determinando o identificador do locatário</span><span class="sxs-lookup"><span data-stu-id="2b9ed-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="2b9ed-198">Você pode encontrar o identificador do locatário Olá para o locatário de saudação do AD do Azure executando `Get-AzureAccount` no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="2b9ed-199">Corpo da resposta de autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="2b9ed-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="2b9ed-200">Quando uma solicitação é enviada com informações de autenticação, a resposta de saudação contém Olá elementos de autenticação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="2b9ed-201">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b9ed-201">Element</span></span> | <span data-ttu-id="2b9ed-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b9ed-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2b9ed-203">*autenticação (elemento pai)*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-203">*authentication (parent element)*</span></span> |<span data-ttu-id="2b9ed-204">Objeto de autenticação para usar a autenticação ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="2b9ed-205">*tipo*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-205">*type*</span></span> |<span data-ttu-id="2b9ed-206">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-206">Type of authentication.</span></span> <span data-ttu-id="2b9ed-207">Para autenticação do ActiveDirectoryOAuth, o valor de saudação é `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="2b9ed-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-208">*tenant*</span></span> |<span data-ttu-id="2b9ed-209">Identificador do locatário Olá para o locatário de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="2b9ed-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-210">*audience*</span></span> |<span data-ttu-id="2b9ed-211">Isso é definido toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="2b9ed-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="2b9ed-212">*clientId*</span></span> |<span data-ttu-id="2b9ed-213">Olá identificador de cliente para o aplicativo hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9ed-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="2b9ed-214">Exemplo de solicitação REST para autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="2b9ed-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="2b9ed-215">Exemplo de resposta REST para autenticação ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="2b9ed-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="2b9ed-216">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2b9ed-216">See Also</span></span>
 [<span data-ttu-id="2b9ed-217">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="2b9ed-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="2b9ed-218">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="2b9ed-219">Começar a usar o Agendador no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="2b9ed-220">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="2b9ed-221">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="2b9ed-222">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="2b9ed-223">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="2b9ed-224">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="2b9ed-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

