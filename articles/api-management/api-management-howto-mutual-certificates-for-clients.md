---
title: "APIs de aaaSecure usando a autenticação de certificado de cliente no gerenciamento de API - gerenciamento de API do Azure | Microsoft Docs"
description: Saiba como toosecure acessar tooAPIs usando certificados de cliente
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="d6151-103">Como toosecure APIs usando o cliente de certificado autenticação no gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d6151-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="d6151-104">Gerenciamento de API fornece Olá recurso toosecure acesso tooAPIs (ou seja, cliente tooAPI gerenciamento) usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="d6151-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="d6151-105">No momento, você pode verificar a impressão digital de saudação de um certificado de cliente com um valor desejado.</span><span class="sxs-lookup"><span data-stu-id="d6151-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="d6151-106">Você também pode verificar a impressão digital de saudação em certificados existentes carregado tooAPI gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="d6151-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="d6151-107">Para obter informações sobre como proteger o acesso toohello serviço de back-end de uma API usando certificados de cliente (ou seja, gerenciamento de API tooback-end), consulte [como toosecure serviços de back-end usando o cliente de autenticação de certificado](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="d6151-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="d6151-108">Verificando a data de expiração de saudação</span><span class="sxs-lookup"><span data-stu-id="d6151-108">Checking hello expiration date</span></span>

<span data-ttu-id="d6151-109">Abaixo políticas pode ser configurado toocheck se Olá certificado expirou:</span><span class="sxs-lookup"><span data-stu-id="d6151-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="d6151-110">Verificação de assunto e emissor Olá</span><span class="sxs-lookup"><span data-stu-id="d6151-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="d6151-111">Abaixo políticas pode ser configurado toocheck Olá emissor e assunto de um certificado de cliente:</span><span class="sxs-lookup"><span data-stu-id="d6151-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="d6151-112">Verificando a impressão digital de saudação</span><span class="sxs-lookup"><span data-stu-id="d6151-112">Checking hello thumbprint</span></span>

<span data-ttu-id="d6151-113">Abaixo políticas pode ser configurado toocheck impressão digital de saudação de um certificado de cliente:</span><span class="sxs-lookup"><span data-stu-id="d6151-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="d6151-114">Verificar uma impressão digital em certificados carregados tooAPI gerenciamento</span><span class="sxs-lookup"><span data-stu-id="d6151-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="d6151-115">Olá exemplo a seguir mostra como a impressão digital de saudação toocheck de um certificado de cliente em relação a certificados carregado tooAPI gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="d6151-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="d6151-116">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="d6151-116">Next step</span></span>

*  [<span data-ttu-id="d6151-117">Como toosecure serviços de back-end usando o cliente de autenticação de certificado</span><span class="sxs-lookup"><span data-stu-id="d6151-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="d6151-118">Como os certificados tooupload</span><span class="sxs-lookup"><span data-stu-id="d6151-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

