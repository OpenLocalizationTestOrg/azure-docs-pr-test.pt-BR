---
title: "aaaUse AD do Azure v 2.0 tooaccess proteger recursos sem interação do usuário | Microsoft Docs"
description: "Crie aplicativos web usando a implementação de saudação do AD do Azure Olá OAuth 2.0 do protocolo de autenticação."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Fluem do Azure Active Directory v 2.0 e hello OAuth 2.0 as credenciais do cliente
Você pode usar o hello [as credenciais do cliente OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.4), às vezes chamado *duas pernas OAuth*, tooaccess web hospedada recursos usando a identidade de saudação do aplicativo. Esse tipo de concessão normalmente é usado para interações de servidor-para-servidor que devem ser executado em segundo plano hello, sem interação imediato a um usuário. Esses tipos de aplicativos geralmente são chamados tooas *daemons* ou *contas de serviço*.

> [!NOTE]
> o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure. toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>
>

Em hello mais comum *3 pernas OAuth*, um aplicativo cliente é concedido permissão tooaccess um recurso em nome de um usuário específico. permissão de saudação é recebido do aplicativo de toohello usuário hello, geralmente durante a saudação [consentimento](active-directory-v2-scopes.md) processo. No entanto, no fluxo de credenciais de cliente hello, permissões são concedidas diretamente aplicativo toohello em si. Quando o aplicativo hello apresenta um recurso de token tooa, o recurso Olá impõe que aplicativo hello em si tem autorização tooperform uma ação, e não Olá usuário tem autorização.

## Diagrama de protocolo
fluxo de credenciais de cliente inteiro Olá parece semelhante toohello próximo diagrama. Descrevemos cada uma das etapas Olá posteriormente neste artigo.

![Fluxo de credenciais do cliente](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Obter autorização direta
Um aplicativo normalmente recebe autorização direta tooaccess um recurso em uma das duas maneiras: por meio de uma lista de controle de acesso (ACL) no recurso hello, ou por meio de atribuição de permissão de aplicativo no Azure Active Directory (AD do Azure). Esses dois métodos são hello mais comuns no AD do Azure, e recomendamos para os clientes e recursos que executam o fluxo de credenciais saudação do cliente. Um recurso pode escolher tooauthorize seus clientes de outras maneiras, no entanto. Cada servidor de recursos pode escolher método hello que faz mais sentido para seus aplicativos de saudação.

### Listas de controle de acesso
Um provedor de recursos pode impor uma verificação de autorização com base em uma lista de IDs de Aplicativo que ele conhece e conceder nível de acesso específico. Quando o recurso Olá recebe um token de ponto de extremidade do hello v 2.0, pode decodificar token hello e extrair a ID do aplicativo do cliente Olá Olá `appid` e `iss` declarações. Em seguida, ele compara o aplicativo hello em relação a uma ACL que mantém. Olá granularidade da ACL e método pode variar significativamente entre os recursos.

Um caso de uso comum é toouse toorun uma ACL testes para um aplicativo da web ou para uma API da Web. Olá API da Web pode conceder apenas um subconjunto de cliente específico de tooa permissões completas. testes de ponta a ponta de toorun em Olá API, crie um cliente de teste que adquire tokens do ponto de extremidade do hello v 2.0 e, em seguida, envia toohello API. Olá API e verificações Olá ACL para Olá teste ID do aplicativo do cliente para acesso completo funcionalidade todo toohello da API. Se você usar esse tipo de ACL, certifique-se de que toovalidate Olá não apenas do chamador `appid` valor. Também valida que Olá `iss` valor Olá token é confiável.

Esse tipo de autorização é comum daemons e contas de serviço que precisam de dados de tooaccess usuários do consumidor que têm contas da Microsoft pessoais. Para dados de propriedade de organizações, recomendamos que você obtenha a autorização necessária Olá por meio de permissões de aplicativo.

### Permissões de aplicativo
Em vez de usar ACLs, você pode usar as APIs tooexpose um conjunto de permissões do aplicativo. Uma permissão de aplicativo é concedida tooan aplicativo pelo administrador da organização, e podem ser usado tooaccess somente dados pertencentes a organização e seus funcionários. Por exemplo, o Microsoft Graph expõe várias aplicativo permissões toodo Olá a seguir:

* Ler emails em todas as caixas de correio
* Ler e gravar mensagens em todas as caixas de correio
* Enviar emails como qualquer usuário
* Ler dados do diretório

Para obter mais informações sobre permissões de aplicativo, vá muito[Microsoft Graph](https://graph.microsoft.io).

permissões de aplicativo toouse em seu aplicativo, Olá etapas discutimos próximas seções de saudação.

#### Solicitar permissões Olá no portal de registro de aplicativo hello
1. Vá tooyour aplicativo hello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou [criar um aplicativo](active-directory-v2-app-registration.md), se ainda não o fez. Você precisará toouse pelo menos um segredo do aplicativo quando você criar seu aplicativo.
2. Localizar Olá **permissões diretas de aplicativo** seção e, em seguida, adicione permissões de saudação que seu aplicativo requer.
3. **Salvar** Olá o registro do aplicativo.

#### Recomendado: Usuário de saudação entrar no aplicativo tooyour
Normalmente, quando você cria um aplicativo que usa permissões do aplicativo, o aplicativo de saudação requer uma página ou exibição na qual Olá administrador aprova permissões do aplicativo hello. Esta página pode fazer parte de fluxo de entrada saudação do aplicativo, parte das configurações do aplicativo hello, ou pode ser dedicado "conectar" fluxo. Em muitos casos, faz sentido para Olá aplicativo tooshow isso "conectar" modo de exibição somente depois que um usuário tiver se conectado com um trabalho ou escola conta da Microsoft.

Se você assinar usuário Olá no aplicativo tooyour, você pode identificar a organização Olá usuário de saudação toowhich pertence antes de você perguntar Olá usuário tooapprove permissões de aplicativo hello. Embora não seja estritamente necessário, isso pode ajudá-lo a criar uma experiência mais intuitiva para os usuários. usuário de saudação toosign in, siga nosso [tutoriais de protocolo v 2.0](active-directory-v2-protocols.md).

#### Saudação de solicitar permissões de um administrador de diretório
Quando você estiver pronto toorequest permissões de administrador da organização hello, você pode redirecionar v 2.0 do hello usuário toohello *ponto de extremidade de autorização administrador*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parâmetro | Condição | Descrição |
| --- | --- | --- |
| locatário |Obrigatório |locatário do diretório Olá que você deseja toorequest permissão do. Pode estar no formato de nome amigável ou de GUID. Se você não souber qual usuário do locatário Olá pertence tooand deseja toolet-los entrar com qualquer locatário, use `common`. |
| client_id |Obrigatório |Olá aplicativo ID que Olá [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) atribuído tooyour aplicativo. |
| redirect_uri |Obrigatório |Olá redirecione o URI em que você deseja Olá resposta toobe enviado para seu aplicativo toohandle. Ele deve corresponder exatamente a um de redirecionamento Olá URIs registrados no portal de hello, exceto que ele deve ser codificados de URL e pode ter segmentos de caminho adicionais. |
| state |Recomendadas |Um valor que é incluído na solicitação de saudação que também é retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo desejado. estado de saudação é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |

Neste ponto, o AD do Azure impõe que somente um administrador de locatários pode entrar na solicitação de saudação toocomplete. administrador de saudação deverá tooapprove que todos Olá permissões aplicação direta que você solicitou para seu aplicativo no portal de registro de aplicativo hello.

##### Resposta bem-sucedida
Se Olá administrador aprovar permissões Olá para seu aplicativo, resposta bem-sucedida Olá terá esta aparência:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parâmetro | Descrição |
| --- | --- | --- |
| locatário |locatário do diretório Olá que permissões seu aplicativo hello que solicitados, no formato GUID. |
| state |Um valor que é incluído na solicitação de saudação que também é retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo desejado. estado de saudação é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| admin_consent |Definir muito**true**. |

##### Resposta de erro
Se Olá administrador aprove permissões Olá para seu aplicativo, Olá falha resposta esta aparência:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parâmetro | Descrição |
| --- | --- | --- |
| error |Uma cadeia de caracteres de código de erro que você pode usar tooclassify tipos de erros e que você pode usar tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação do erro. |

Depois que você recebeu uma resposta bem-sucedida do ponto de extremidade de provisionamento de aplicativo hello, seu aplicativo ganhou permissões de aplicação direta de saudação solicitada. Agora você pode solicitar um token de recurso de saudação que você deseja.

## Obter um token
Após a autorização necessária Olá adquiridas para seu aplicativo, vá para a aquisição de tokens de acesso para APIs. tooget um token usando Olá concessão de credenciais de cliente, enviar um toohello de solicitação POST `/token` v 2.0 de ponto de extremidade:

### Na primeira ocorrência: solicitação de token de acesso com um segredo compartilhado

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Parâmetro | Condição | Descrição |
| --- | --- | --- |
| client_id |Obrigatório |Olá aplicativo ID que Olá [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) atribuído tooyour aplicativo. |
| scope |Obrigatório |passado um valor Olá para Olá `scope` parâmetro nesta solicitação deve ser o identificador de recurso de saudação (URI de ID de aplicativo) do recurso de saudação desejado, afixado com hello `.default` sufixo. Por exemplo, Microsoft Graph hello, o valor de saudação é `https://graph.microsoft.com/.default`. Esse valor informa o ponto de extremidade do hello v 2.0 que de todas as permissões de aplicação direta hello, que você configurou para seu aplicativo, ele deve emitir um token para Olá aqueles associado ao recurso de saudação desejado toouse. |
| client_secret |Obrigatório |Olá segredo do aplicativo que é gerado para seu aplicativo no portal de registro de aplicativo hello. |
| grant_type |Obrigatório |Deve ser `client_credentials`. |

### Segundo caso: solicitação de token de acesso com um certificado

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Parâmetro | Condição | Descrição |
| --- | --- | --- |
| client_id |Obrigatório |Olá aplicativo ID que Olá [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) atribuído tooyour aplicativo. |
| scope |Obrigatório |passado um valor Olá para Olá `scope` parâmetro nesta solicitação deve ser o identificador de recurso de saudação (URI de ID de aplicativo) do recurso de saudação desejado, afixado com hello `.default` sufixo. Por exemplo, Microsoft Graph hello, o valor de saudação é `https://graph.microsoft.com/.default`. Esse valor informa o ponto de extremidade do hello v 2.0 que de todas as permissões de aplicação direta hello, que você configurou para seu aplicativo, ele deve emitir um token para Olá aqueles associado ao recurso de saudação desejado toouse. |
| client_assertion_type |obrigatório |Olá valor deve ser`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |obrigatório | Uma asserção (um JSON Web Token) que você precisa toocreate e entrar com hello certificado registrado como credenciais para o seu aplicativo. Leia sobre [credenciais de certificado](active-directory-certificate-credentials.md) toolearn como tooregister seu formato de certificado e hello declaração hello.|
| grant_type |Obrigatório |Deve ser `client_credentials`. |

Observe que os parâmetros de saudação quase Olá igual ao caso de saudação da solicitação de saudação o por segredo compartilhado exceto que o parâmetro de client_secret hello é substituído por dois parâmetros: um client_assertion_type e client_assertion.

### Resposta bem-sucedida
Uma resposta bem-sucedida tem a seguinte aparência:

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Parâmetro | Descrição |
| --- | --- |
| access_token |token de acesso solicitado Hello. Olá aplicativo pode usar este toohello tooauthenticate token protegido de recurso, como tooa API da Web. |
| token_type |Indica o valor do tipo de token de saudação. Olá somente tipo de AD do Azure oferece suporte a `bearer`. |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |

### Resposta de erro
Uma resposta de erro tem esta aparência:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que você pode usar tooclassify tipos de erros que ocorrem e tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudá-lo a identificar a causa de saudação de um erro de autenticação. |
| error_codes |Uma lista de códigos de erro específicos do STS que pode ajudar no diagnóstico. |
| timestamp |tempo de saudação na qual ocorreu o erro de saudação. |
| trace_id |Um identificador exclusivo para a solicitação de saudação que possam ajudar com o diagnóstico. |
| correlation_id |Um identificador exclusivo para a solicitação de saudação que possam ajudar com o diagnóstico em componentes. |

## Usar um token
Agora que você tiver adquirido um token, use Olá toomake token solicitações toohello recursos. Quando Olá token expirar, repita Olá solicitação toohello `/token` tooacquire de ponto de extremidade um token de acesso de novo.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Exemplo de código
toosee um exemplo de um aplicativo que implementa Olá concessão de credenciais de cliente usando o ponto de extremidade de Olá administrador consentimento, consulte nosso [exemplo de código de daemon v 2.0](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
