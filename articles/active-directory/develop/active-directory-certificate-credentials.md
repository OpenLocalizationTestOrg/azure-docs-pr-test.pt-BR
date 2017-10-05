---
title: Credenciais de certificado no Azure AD | Microsoft Docs
description: "Este artigo aborda o registro e uso de credenciais de certificado para autenticação do aplicativo"
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
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="3db8b-103">Credenciais de certificado para autenticação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3db8b-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="3db8b-104">O Azure Active Directory permite que um aplicativo use suas próprias credenciais para autenticação, por exemplo, nos fluxos Concessão de Credenciais de Cliente e Em Nome de do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3db8b-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="3db8b-105">Uma forma de credencial que pode ser usada é uma declaração JWT (Token Web JSON) assinada com um certificado que o aplicativo possui.</span><span class="sxs-lookup"><span data-stu-id="3db8b-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="3db8b-106">Formato da asserção</span><span class="sxs-lookup"><span data-stu-id="3db8b-106">Format of the assertion</span></span>
<span data-ttu-id="3db8b-107">Para calcular a declaração, provavelmente, você desejará usar uma das muitas bibliotecas [Token Web JSON](https://jwt.io/) no idioma de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="3db8b-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="3db8b-108">A informação transferida por token é:</span><span class="sxs-lookup"><span data-stu-id="3db8b-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="3db8b-109">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="3db8b-109">Header</span></span>

| <span data-ttu-id="3db8b-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3db8b-110">Parameter</span></span> |  <span data-ttu-id="3db8b-111">Comentário</span><span class="sxs-lookup"><span data-stu-id="3db8b-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="3db8b-112">Deve ser **RS256**</span><span class="sxs-lookup"><span data-stu-id="3db8b-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="3db8b-113">Deve ser **JWT**</span><span class="sxs-lookup"><span data-stu-id="3db8b-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="3db8b-114">Deve ser a impressão digital do certificado de x. 509 SHA-1</span><span class="sxs-lookup"><span data-stu-id="3db8b-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="3db8b-115">Declarações (carga)</span><span class="sxs-lookup"><span data-stu-id="3db8b-115">Claims (Payload)</span></span>

| <span data-ttu-id="3db8b-116">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3db8b-116">Parameter</span></span> |  <span data-ttu-id="3db8b-117">Comentário</span><span class="sxs-lookup"><span data-stu-id="3db8b-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="3db8b-118">Público-alvo: deve ser **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="3db8b-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="3db8b-119">Data de expiração: a data de expiração do token.</span><span class="sxs-lookup"><span data-stu-id="3db8b-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="3db8b-120">A hora é representada como o número de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até a hora em que a validade do token expira.</span><span class="sxs-lookup"><span data-stu-id="3db8b-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="3db8b-121">Emissor: deve ser a client_id (Id do aplicativo de serviço do cliente)</span><span class="sxs-lookup"><span data-stu-id="3db8b-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="3db8b-122">GUID: a ID de JWT</span><span class="sxs-lookup"><span data-stu-id="3db8b-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="3db8b-123">Não Antes de: a data anterior à qual o token não pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="3db8b-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="3db8b-124">A hora é representada como o número de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até a hora em que o token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="3db8b-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="3db8b-125">Assunto: para `iss`, deve ser o client_id (Id do aplicativo de serviço do cliente)</span><span class="sxs-lookup"><span data-stu-id="3db8b-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="3db8b-126">Signature</span><span class="sxs-lookup"><span data-stu-id="3db8b-126">Signature</span></span>
<span data-ttu-id="3db8b-127">A assinatura é calculada aplicando o certificado conforme descrito na [especificação Token Web JSON RFC7519](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="3db8b-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="3db8b-128">Exemplo de uma declaração JWT decodificada</span><span class="sxs-lookup"><span data-stu-id="3db8b-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="3db8b-129">Exemplo de uma declaração JWT codificada</span><span class="sxs-lookup"><span data-stu-id="3db8b-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="3db8b-130">A cadeia de caracteres a seguir é um exemplo de asserção codificado.</span><span class="sxs-lookup"><span data-stu-id="3db8b-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="3db8b-131">Se você olhar com cuidado, você observe três seções separadas por pontos (.).</span><span class="sxs-lookup"><span data-stu-id="3db8b-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="3db8b-132">A primeira seção codifica o cabeçalho, o segundo a carga e o último é a assinatura computada com os certificados do conteúdo das duas primeiras seções.</span><span class="sxs-lookup"><span data-stu-id="3db8b-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="3db8b-133">Registrar o certificado com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="3db8b-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="3db8b-134">Para associar as credenciais de certificado com o aplicativo cliente no AD do Azure, você precisa editar o manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3db8b-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="3db8b-135">Com a suspensão de um certificado, você precisa calcular:</span><span class="sxs-lookup"><span data-stu-id="3db8b-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="3db8b-136">`$base64Thumbprint`, que é o base64 codificação do certificado Hash</span><span class="sxs-lookup"><span data-stu-id="3db8b-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="3db8b-137">`$base64Value`, que é o base64 codificação dos dados brutos do certificado</span><span class="sxs-lookup"><span data-stu-id="3db8b-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="3db8b-138">Você também precisa fornecer um GUID para identificar a chave no manifesto do aplicativo (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="3db8b-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="3db8b-139">No registro de aplicativo do Azure do aplicativo cliente, abra o manifesto do aplicativo e substitua a propriedade *keyCredentials* pelas novas informações de certificado usando o seguinte esquema:</span><span class="sxs-lookup"><span data-stu-id="3db8b-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
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

<span data-ttu-id="3db8b-140">Salve as edições no manifesto do aplicativo e carregue-o no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3db8b-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="3db8b-141">A propriedade keycredentials tem valores múltiplos, portanto você pode carregar vários certificados de gerenciamento de chave mais avançados.</span><span class="sxs-lookup"><span data-stu-id="3db8b-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
