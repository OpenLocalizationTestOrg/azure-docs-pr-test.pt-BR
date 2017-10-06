---
title: "aaaAzure tooService de serviço do AD Auth usando OAuth 2.0 | Microsoft Docs"
description: "Este artigo descreve como toouse HTTP mensagens tooimplement serviço tooservice autenticação usando o fluxo de concessão de credenciais de cliente do hello OAuth 2.0."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Chamadas de tooservice de serviço usando as credenciais do cliente (segredo compartilhado ou certificado)
saudação de fluxo de concessão de credenciais OAuth 2.0 cliente permite que um serviço web (*cliente confidencial*) toouse suas próprias credenciais em vez de representar um usuário, tooauthenticate ao chamar outro serviço de web. Nesse cenário, o cliente de saudação é geralmente um serviço web de camada intermediária, um serviço daemon ou um site da web. Para um nível mais alto de garantia, AD do Azure também permite Olá chamando toouse serviço um certificado (em vez de um segredo compartilhado) como uma credencial.

## Fluxo de concessão de credenciais do cliente
Olá diagrama a seguir explica como as credenciais do cliente Olá conceder fluxo funciona no Azure Active Directory (AD do Azure).

![Fluxo de concessão de credenciais de cliente do OAuth2.0](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. aplicativo de cliente Hello autentica toohello ponto de extremidade de emissão de tokens do AD do Azure e solicita um token de acesso.
2. problemas de ponto de extremidade de emissão de tokens de saudação do AD do Azure Olá token de acesso.
3. token de acesso de saudação é usado tooauthenticate toohello protegido recursos.
4. Dados de saudação protegido recursos são retornados toohello aplicativo de web.

## Registrar Olá serviços no AD do Azure
Registre Olá chamando o serviço e Olá recebendo o serviço no Azure Active Directory (AD do Azure). Para obter instruções detalhadas, consulte [Integrando aplicativos com o Azure Active Directory](active-directory-integrating-applications.md).

## Solicitar um token de acesso
toorequest um token de acesso, use um ponto de extremidade HTTP POST toohello específico de locatário do AD do Azure.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Solicitação de token de acesso de serviço para serviço
Há dois casos, dependendo se o aplicativo de cliente hello escolhe toobe protegido por um segredo compartilhado ou um certificado.

### Na primeira ocorrência: solicitação de token de acesso com um segredo compartilhado
Ao usar um segredo compartilhado, uma solicitação de token de acesso de serviço a serviço contém Olá parâmetros a seguir:

| Parâmetro |  | Descrição |
| --- | --- | --- |
| grant_type |obrigatório |Especifica a saudação solicitada tipo de concessão. Em um fluxo de concessão de credenciais de cliente, o valor de saudação deve ser **client_credentials**. |
| client_id |obrigatório |Especifica a id do cliente do AD do Azure Olá de saudação chamando o serviço web. Olá toofind chamando o ID do cliente do aplicativo, em Olá [portal do Azure](https://portal.azure.com), clique em **do Active Directory**, alterne o diretório, clique em aplicativo hello. Olá client_id é hello *ID do aplicativo* |
| client_secret |obrigatório |Insira uma chave registrada para Olá chamando o aplicativo web de serviço ou daemon no AD do Azure. toocreate uma chave, em Olá portal do Azure, clique **do Active Directory**, alterne o diretório, clique em aplicativo hello, **configurações**, clique em **chaves**, e adicione uma chave.|
| recurso |obrigatório |Digite hello URI de ID do aplicativo de saudação recebendo o serviço web. Olá toofind URI de ID do aplicativo no hello portal do Azure, clique em **do Active Directory**, alterne o diretório, clique em aplicativo de serviço hello e, em seguida, clique em **configurações** e **propriedades** |

#### Exemplo
Olá HTTP POST a seguir solicita um token de acesso para o serviço de web https://service.contoso.com/ hello. Olá `client_id` identifica o serviço web de saudação que solicita o token de acesso de saudação.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### Segundo caso: solicitação de token de acesso com um certificado
Uma solicitação de token de acesso de serviço a serviço com um certificado contém Olá parâmetros a seguir:

| Parâmetro |  | Descrição |
| --- | --- | --- |
| grant_type |obrigatório |Especifica Olá solicitou o tipo de resposta. Em um fluxo de concessão de credenciais de cliente, o valor de saudação deve ser **client_credentials**. |
| client_id |obrigatório |Especifica a id do cliente do AD do Azure Olá de saudação chamando o serviço web. Olá toofind chamando o ID do cliente do aplicativo, em Olá [portal do Azure](https://portal.azure.com), clique em **do Active Directory**, alterne o diretório, clique em aplicativo hello. Olá client_id é hello *ID do aplicativo* |
| client_assertion_type |obrigatório |Olá valor deve ser`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |obrigatório | Uma asserção (um JSON Web Token) que você precisa toocreate e entrar com hello certificado registrado como credenciais para o seu aplicativo. Leia sobre [credenciais de certificado](active-directory-certificate-credentials.md) toolearn como tooregister seu formato de certificado e hello declaração hello.|
| recurso | obrigatório |Digite hello URI de ID do aplicativo de saudação recebendo o serviço web. Olá toofind URI de ID do aplicativo no hello portal do Azure, clique em **do Active Directory**, clique em diretório hello, clique em aplicativo hello e, em seguida, clique em **configurar**. |

Observe que os parâmetros de saudação quase Olá igual ao caso de saudação da solicitação de saudação o por segredo compartilhado exceto que o parâmetro de client_secret hello é substituído por dois parâmetros: um client_assertion_type e client_assertion.

#### Exemplo
Olá HTTP POST a seguir solicita um token de acesso para o serviço de web https://service.contoso.com/ Olá com um certificado. Olá `client_id` identifica o serviço web de saudação que solicita o token de acesso de saudação.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Resposta de token de acesso de serviço para serviço

Uma resposta bem-sucedida contém uma resposta JSON OAuth 2.0 com hello parâmetros a seguir:

| Parâmetro | Descrição |
| --- | --- |
| access_token |token de acesso solicitado Hello. Olá chamando o serviço web pode usar este toohello tooauthenticate token recebendo o serviço web. |
| token_type |Indica o valor do tipo de token de saudação. Olá somente tipo de AD do Azure oferece suporte a **portador**. Para obter mais informações sobre tokens de portador, consulte Olá [estrutura de autorização do OAuth 2.0: uso de Token de portador (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |
| expires_on |tempo de saudação quando o token de acesso de saudação expira. Data de saudação é representada como número de saudação de segundos de 1970-01-01T0:0:0Z UTC até o tempo de expiração de saudação. Esse valor é usado toodetermine o tempo de vida de Olá de tokens em cache. |
| not_before |tempo de saudação do qual Olá token de acesso se tornará utilizável. Data de saudação é representada como número de saudação de segundos de 1970-01-01T0:0:0Z UTC até o tempo de validade do token hello.|
| recurso |Olá URI de ID do aplicativo de saudação recebendo o serviço web. |

#### Exemplo de resposta
Olá, exemplo a seguir mostra uma solicitação de tooa de resposta de êxito para um serviço de web de tooa de token de acesso.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Consulte também
* [OAuth 2.0 no Azure AD](active-directory-protocols-oauth-code.md)
* [Exemplo em c# Olá tooservice da chamada de serviço com um segredo compartilhado](https://github.com/Azure-Samples/active-directory-dotnet-daemon) e [exemplo em c# Olá tooservice da chamada de serviço com um certificado](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
