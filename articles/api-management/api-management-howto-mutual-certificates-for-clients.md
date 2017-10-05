---
title: "Proteger APIs usando a autenticação de certificado do cliente no Gerenciamento de API — Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como proteger o acesso às APIs usando certificados do cliente"
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
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="1387b-103">Como proteger APIs usando a autenticação de certificado do cliente no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="1387b-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="1387b-104">O Gerenciamento de API fornece a capacidade de proteger o acesso às APIs (isto é, cliente para Gerenciamento de API) usando certificados do cliente.</span><span class="sxs-lookup"><span data-stu-id="1387b-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="1387b-105">No momento, você pode verificar a impressão digital de um certificado do cliente em relação a um valor desejado.</span><span class="sxs-lookup"><span data-stu-id="1387b-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="1387b-106">Também é possível verificar a impressão digital em relação a certificados existentes carregados no Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="1387b-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="1387b-107">Para saber mais sobre como proteger o acesso ao serviço de back-end de uma API usando certificados do cliente (isto é, Gerenciamento de API para back-end), confira [Como garantir serviços de back-end usando autenticação de certificado do cliente](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="1387b-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="1387b-108">Verificando a data de validade</span><span class="sxs-lookup"><span data-stu-id="1387b-108">Checking the expiration date</span></span>

<span data-ttu-id="1387b-109">As políticas abaixo podem ser configuradas para verificar se o certificado está expirado:</span><span class="sxs-lookup"><span data-stu-id="1387b-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="1387b-110">Verificando o emissor e a entidade</span><span class="sxs-lookup"><span data-stu-id="1387b-110">Checking the issuer and subject</span></span>

<span data-ttu-id="1387b-111">As políticas abaixo podem ser configuradas para verificar o emissor e a entidade de um certificado do cliente:</span><span class="sxs-lookup"><span data-stu-id="1387b-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="1387b-112">Verificando a impressão digital</span><span class="sxs-lookup"><span data-stu-id="1387b-112">Checking the thumbprint</span></span>

<span data-ttu-id="1387b-113">Veja abaixo que as políticas podem ser configuradas para verificar a impressão digital de um certificado do cliente:</span><span class="sxs-lookup"><span data-stu-id="1387b-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="1387b-114">Verificação de uma impressão digital em relação a certificados carregados no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="1387b-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="1387b-115">O exemplo a seguir mostra como verificar a impressão digital de um certificado do cliente em relação a certificados carregados no Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="1387b-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="1387b-116">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="1387b-116">Next step</span></span>

*  [<span data-ttu-id="1387b-117">Como garantir serviços de back-end usando autenticação de certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="1387b-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="1387b-118">Como carregar certificados</span><span class="sxs-lookup"><span data-stu-id="1387b-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

