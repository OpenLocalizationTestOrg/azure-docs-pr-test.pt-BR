---
title: credenciais aaaCertificate no AD do Azure | Microsoft Docs
description: "Este artigo aborda registro hello e usar credenciais de certificados para autenticação de aplicativo"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="6ff36-103">Credenciais de certificado para autenticação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="6ff36-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="6ff36-104">Active Directory do Azure permite que um aplicativo toouse suas próprias credenciais para autenticação, por exemplo, no fluxo de concessão de credenciais de cliente OAuth 2.0 hello e Olá em nome de fluxo.</span><span class="sxs-lookup"><span data-stu-id="6ff36-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="6ff36-105">Uma forma de credencial que pode ser usado é uma declaração de Token(JWT) de Web JSON assinada com um certificado que o aplicativo hello possui.</span><span class="sxs-lookup"><span data-stu-id="6ff36-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="6ff36-106">Formato da asserção Olá</span><span class="sxs-lookup"><span data-stu-id="6ff36-106">Format of hello assertion</span></span>
<span data-ttu-id="6ff36-107">declaração de saudação toocompute, provavelmente você desejará toouse uma saudação muitos [JSON Web Token](https://jwt.io/) bibliotecas no idioma de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="6ff36-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="6ff36-108">informações de saudação executadas pelo token de saudação são:</span><span class="sxs-lookup"><span data-stu-id="6ff36-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="6ff36-109">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="6ff36-109">Header</span></span>

| <span data-ttu-id="6ff36-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6ff36-110">Parameter</span></span> |  <span data-ttu-id="6ff36-111">Comentário</span><span class="sxs-lookup"><span data-stu-id="6ff36-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="6ff36-112">Deve ser **RS256**</span><span class="sxs-lookup"><span data-stu-id="6ff36-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="6ff36-113">Deve ser **JWT**</span><span class="sxs-lookup"><span data-stu-id="6ff36-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="6ff36-114">Deve ser a impressão digital do certificado de x. 509 SHA-1 Olá</span><span class="sxs-lookup"><span data-stu-id="6ff36-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="6ff36-115">Declarações (carga)</span><span class="sxs-lookup"><span data-stu-id="6ff36-115">Claims (Payload)</span></span>

| <span data-ttu-id="6ff36-116">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6ff36-116">Parameter</span></span> |  <span data-ttu-id="6ff36-117">Comentário</span><span class="sxs-lookup"><span data-stu-id="6ff36-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="6ff36-118">Público-alvo: deve ser **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="6ff36-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="6ff36-119">Data de vencimento: data de saudação quando o token de saudação expira.</span><span class="sxs-lookup"><span data-stu-id="6ff36-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="6ff36-120">tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até a validade do token de Olá Olá tempo expira.</span><span class="sxs-lookup"><span data-stu-id="6ff36-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="6ff36-121">Emissor: deve ser Olá client_id (Id do aplicativo de serviço de saudação do cliente)</span><span class="sxs-lookup"><span data-stu-id="6ff36-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="6ff36-122">GUID: Olá ID do JWT</span><span class="sxs-lookup"><span data-stu-id="6ff36-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="6ff36-123">Não antes: Olá data antes da qual Olá token não pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="6ff36-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="6ff36-124">tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até Olá tempo Olá token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="6ff36-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="6ff36-125">Assunto: para `iss`, deve ser Olá client_id (Id do aplicativo de serviço de saudação do cliente)</span><span class="sxs-lookup"><span data-stu-id="6ff36-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="6ff36-126">Signature</span><span class="sxs-lookup"><span data-stu-id="6ff36-126">Signature</span></span>
<span data-ttu-id="6ff36-127">assinatura de saudação é calculada aplicando certificado hello, conforme descrito em Olá [especificação JSON Web Token RFC7519](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="6ff36-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="6ff36-128">Exemplo de uma declaração JWT decodificada</span><span class="sxs-lookup"><span data-stu-id="6ff36-128">Example of a decoded JWT assertion</span></span>
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="6ff36-129">Exemplo de uma declaração JWT codificada</span><span class="sxs-lookup"><span data-stu-id="6ff36-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="6ff36-130">saudação de cadeia de caracteres a seguir está um exemplo de asserção codificado.</span><span class="sxs-lookup"><span data-stu-id="6ff36-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="6ff36-131">Se você olhar com cuidado, você observe três seções separadas por pontos (.).</span><span class="sxs-lookup"><span data-stu-id="6ff36-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="6ff36-132">primeira seção do Hello codifica cabeçalho hello, Olá segundo Olá de carga, e Olá por último é computada com certificados de saudação do conteúdo de saudação do primeiro duas seções de saudação de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ff36-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="6ff36-133">Registrar o certificado com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ff36-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="6ff36-134">credenciais de certificado tooassociate Olá com o aplicativo de cliente hello no AD do Azure, você precisa de manifesto do aplicativo hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="6ff36-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="6ff36-135">Com a retenção de um certificado, você precisa toocompute:</span><span class="sxs-lookup"><span data-stu-id="6ff36-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="6ff36-136">`$base64Thumbprint`, que é Olá codificação base64 do certificado Olá Hash</span><span class="sxs-lookup"><span data-stu-id="6ff36-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="6ff36-137">`$base64Value`, que é Olá a codificação base64 de dados brutos do certificado Olá</span><span class="sxs-lookup"><span data-stu-id="6ff36-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="6ff36-138">Você também precisa tooprovide uma chave de saudação do GUID tooidentify no manifesto de aplicativo hello (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="6ff36-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="6ff36-139">No hello o registro do aplicativo do Azure para o aplicativo de cliente hello, abra o manifesto do aplicativo hello e substitua Olá *keyCredentials* propriedade com as novas informações de certificado usando Olá esquema a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

<span data-ttu-id="6ff36-140">Salvar o manifesto do aplicativo hello edições toohello e carregar tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="6ff36-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="6ff36-141">propriedade de keyCredentials de saudação é múltiplos, portanto você pode carregar vários certificados de gerenciamento de chaves mais rico.</span><span class="sxs-lookup"><span data-stu-id="6ff36-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
