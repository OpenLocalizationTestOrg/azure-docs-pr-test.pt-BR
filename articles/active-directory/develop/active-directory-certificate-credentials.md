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
# <a name="certificate-credentials-for-application-authentication"></a>Credenciais de certificado para autenticação do aplicativo

Active Directory do Azure permite que um aplicativo toouse suas próprias credenciais para autenticação, por exemplo, no fluxo de concessão de credenciais de cliente OAuth 2.0 hello e Olá em nome de fluxo.
Uma forma de credencial que pode ser usado é uma declaração de Token(JWT) de Web JSON assinada com um certificado que o aplicativo hello possui.

## <a name="format-of-hello-assertion"></a>Formato da asserção Olá
declaração de saudação toocompute, provavelmente você desejará toouse uma saudação muitos [JSON Web Token](https://jwt.io/) bibliotecas no idioma de saudação de sua escolha. informações de saudação executadas pelo token de saudação são:

#### <a name="header"></a>Cabeçalho

| Parâmetro |  Comentário |
| --- | --- | --- |
| `alg` | Deve ser **RS256** |
| `typ` | Deve ser **JWT** |
| `x5t` | Deve ser a impressão digital do certificado de x. 509 SHA-1 Olá |

#### <a name="claims-payload"></a>Declarações (carga)

| Parâmetro |  Comentário |
| --- | --- | --- |
| `aud` | Público-alvo: deve ser **https://login.microsoftonline.com/*tenant_Id*/oauth2/token** |
| `exp` | Data de vencimento: data de saudação quando o token de saudação expira. tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até a validade do token de Olá Olá tempo expira.|
| `iss` | Emissor: deve ser Olá client_id (Id do aplicativo de serviço de saudação do cliente) |
| `jti` | GUID: Olá ID do JWT |
| `nbf` | Não antes: Olá data antes da qual Olá token não pode ser usado. tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até Olá tempo Olá token foi emitido. |
| `sub` | Assunto: para `iss`, deve ser Olá client_id (Id do aplicativo de serviço de saudação do cliente) |

#### <a name="signature"></a>Signature
assinatura de saudação é calculada aplicando certificado hello, conforme descrito em Olá [especificação JSON Web Token RFC7519](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Exemplo de uma declaração JWT decodificada
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

### <a name="example-of-an-encoded-jwt-assertion"></a>Exemplo de uma declaração JWT codificada
saudação de cadeia de caracteres a seguir está um exemplo de asserção codificado. Se você olhar com cuidado, você observe três seções separadas por pontos (.).
primeira seção do Hello codifica cabeçalho hello, Olá segundo Olá de carga, e Olá por último é computada com certificados de saudação do conteúdo de saudação do primeiro duas seções de saudação de assinatura de saudação.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Registrar o certificado com o Azure AD
credenciais de certificado tooassociate Olá com o aplicativo de cliente hello no AD do Azure, você precisa de manifesto do aplicativo hello tooedit.
Com a retenção de um certificado, você precisa toocompute:
- `$base64Thumbprint`, que é Olá codificação base64 do certificado Olá Hash
- `$base64Value`, que é Olá a codificação base64 de dados brutos do certificado Olá

Você também precisa tooprovide uma chave de saudação do GUID tooidentify no manifesto de aplicativo hello (`$keyId`)

No hello o registro do aplicativo do Azure para o aplicativo de cliente hello, abra o manifesto do aplicativo hello e substitua Olá *keyCredentials* propriedade com as novas informações de certificado usando Olá esquema a seguir:
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

Salvar o manifesto do aplicativo hello edições toohello e carregar tooAzure AD. propriedade de keyCredentials de saudação é múltiplos, portanto você pode carregar vários certificados de gerenciamento de chaves mais rico.
