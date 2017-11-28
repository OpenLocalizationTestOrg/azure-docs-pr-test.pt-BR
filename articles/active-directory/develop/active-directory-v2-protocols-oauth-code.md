---
title: "v 2.0 do AD de aaaAzure fluxo de código de autorização do OAuth | Microsoft Docs"
description: "Criando aplicativos da web usando a implementação do AD do Azure Olá OAuth 2.0 do protocolo de autenticação."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Protocolos v2.0 - Fluxo de código de autorização do OAuth 2.0
concessão de código de autorização Olá OAuth 2.0 pode ser usado em aplicativos que são instalados em um dispositivo toogain acessar tooprotected recursos, como APIs da web.  Usando a implementação de saudação aplicativo modelo v do 2.0 do OAuth 2.0, você pode adicionar entrar e API acessar tooyour aplicativos de desktop e móveis.  Este guia é independente de linguagem e descreve como toosend e receber mensagens HTTP sem usar qualquer uma das nossas bibliotecas de código-fonte aberto.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

Olá fluxo de código de autorização do OAuth 2.0 é descrito em [seção 4.1 da especificação de saudação OAuth 2.0](http://tools.ietf.org/html/rfc6749).  É usado tooperform autenticação e autorização na maioria de saudação dos tipos de aplicativo, incluindo [aplicativos web](active-directory-v2-flows.md#web-apps) e [aplicativos instalados nativamente](active-directory-v2-flows.md#mobile-and-native-apps).  Ele permite que aplicativos toosecurely adquirir access_tokens que pode ser usado tooaccess recursos que são protegidos usando o ponto de extremidade do hello v 2.0.  

## Diagrama de protocolo
Em um nível alto, o fluxo de autenticação completa Olá para um aplicativo nativo/mobile é um pouco semelhante a:

![Fluxo do código de autenticação do OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Solicitar um código de autorização
fluxo de código de autorização Olá começa com o cliente Olá direcionando Olá usuário toohello `/authorize` ponto de extremidade.  Nessa solicitação, o cliente de Olá indica Olá permissões tooacquire do usuário hello:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Clique o link da saudação abaixo tooexecute esta solicitação! Depois de entrar, seu navegador deve ser redirecionado muito`https://localhost/myapp/` com um `code` na barra de endereços de saudação.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário.  Para obter mais detalhes, consulte [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |obrigatório |Olá Id do aplicativo de portal de registro que hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a seu aplicativo. |
| response_type |obrigatório |Deve incluir `code` para fluxo de código de autorização de saudação. |
| redirect_uri |recomendável |Olá redirect_uri do seu aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo.  Ele deve corresponder exatamente uma saudação redirect_uris que você registrou no portal de hello, exceto que ele deve ser codificados de url.  Para aplicativos nativos e móveis, você deve usar o valor padrão Olá `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| scope |obrigatório |Uma lista separada por espaços de [escopos](active-directory-v2-scopes.md) que você deseja Olá usuário tooconsent para. |
| response_mode |recomendável |Especifica o método hello que deve ser usado toosend Olá resultante token tooyour back aplicativo.  Pode ser `query` ou `form_post`. |
| state |recomendável |Um valor incluído na solicitação de saudação que também será retornada na resposta de token hello.  Pode ser uma cadeia de caracteres de qualquer conteúdo desejado.  Um valor exclusivo gerado aleatoriamente que normalmente é usado para [impedir ataques de solicitação intersite forjada](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| prompt |opcional |Indica o tipo de saudação da interação do usuário é necessária.  Olá somente no momento, os valores válidos são 'logon', 'none', ' consente '.  `prompt=login`será force Olá usuário tooenter suas credenciais na solicitação, Negar logon único no.  `prompt=none`é Olá oposta - garantirá que o usuário Olá não é apresentado com qualquer prompt interativo natureza.  Se a solicitação Olá não pode ser concluída silenciosamente por meio de logon único, o ponto de extremidade do hello v 2.0 retornará um erro.  `prompt=consent`saudação de gatilho OAuth será consentimento caixa de diálogo após o usuário se autentica hello, solicitando Olá usuário toogrant permissões toohello aplicativo. |
| login_hint |opcional |Pode ser campo de endereço de email/nome de usuário usado toopre preenchimento Olá de saudação página de logon de usuário hello, se você souber o nome de usuário antecipadamente.  Aplicativos geralmente usará esse parâmetro durante a reautenticação, já ter extraído Olá nome de usuário de uma entrada anterior usando Olá `preferred_username` de declaração. |
| domain_hint |opcional |Pode ser `consumers` ou `organizations`.  Se incluído, ele ignorará o processo de descoberta baseada em email Olá que o usuário passa em Olá v 2.0 página de entrada, à esquerda tooa um pouco mais simples de experiência do usuário.  Aplicativos geralmente usará esse parâmetro durante a reautenticação, extraindo Olá `tid` de uma entrada anterior.  Se hello `tid` é de valor de declaração `9188040d-6c67-4c5b-b112-36a304b66dad`, você deve usar `domain_hint=consumers`.  Caso contrário, use `domain_hint=organizations`. |

Neste ponto, o usuário de saudação será solicitado tooenter suas credenciais e autenticação Olá concluída.  Hello ponto de extremidade v 2.0 também garantem que o usuário Olá consentiu permissões toohello indicadas no hello `scope` parâmetro de consulta.  Se o usuário Olá não consentiu tooany das permissões, solicitará Olá usuário tooconsent toohello necessárias permissões.  Os detalhes dos aplicativos quanto a [permissões, consentimento e multilocatário são fornecidos aqui](active-directory-v2-scopes.md).

Depois que o usuário Olá autentica e concede consentimento, o ponto de extremidade do hello v 2.0 retornará um aplicativo de tooyour de resposta em Olá indicado `redirect_uri`, usando o método hello especificado no hello `response_mode` parâmetro.

#### Resposta bem-sucedida
Uma resposta bem-sucedida usando `response_mode=query` tem a seguinte aparência:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| . | Descrição |
| --- | --- |
| código |Olá authorization_code que Olá aplicativo solicitado. Olá aplicativo pode usar toorequest código de autorização Olá um token de acesso do recurso de destino hello.  Authorization_codes têm uma duração bastante curta, geralmente, expirando depois de aproximadamente 10 minutos. |
| state |Se um parâmetro de estado é incluído na solicitação hello, hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que os valores de estado Olá Olá solicitação e resposta são idênticos. |

#### Resposta de erro
Respostas de erro também podem ser enviadas toohello `redirect_uri` para o aplicativo hello possa tratá-los adequadamente:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

#### Códigos de erro para erros de ponto de extremidade de autorização
Olá, tabela a seguir descreve Olá vários códigos de erro que podem ser retornados em Olá `error` parâmetro da resposta de erro hello.

| Código do Erro | Descrição | Ação do Cliente |
| --- | --- | --- |
| invalid_request |Erro de protocolo, como um parâmetro obrigatório ausente. |Corrija e reenvie a solicitação de saudação. Esse é um erro de desenvolvimento normalmente identificado durante os testes iniciais. |
| unauthorized_client |Olá aplicativo cliente não é permitido toorequest um código de autorização. |Isso geralmente ocorre quando o aplicativo de cliente hello não está registrado no AD do Azure ou não será adicionado o locatário do AD do Azure toohello do usuário. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |
| access_denied |Consentimento negado pelo proprietário do recurso |aplicativo de cliente Hello pode notificar o usuário de saudação que ele não pode continuar a menos que o consentimento do usuário hello. |
| unsupported_response_type |servidor de autorização de saudação não oferece suporte a tipo de resposta de saudação na solicitação de saudação. |Corrija e reenvie a solicitação de saudação. Esse é um erro de desenvolvimento normalmente identificado durante os testes iniciais. |
| server_error |servidor de saudação encontrou um erro inesperado. |Repita a solicitação de saudação. Esses erros podem resultar de condições temporárias. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a um erro temporário. |
| temporarily_unavailable |servidor de saudação está temporariamente solicitação de saudação toohandle muito ocupado. |Repita a solicitação de saudação. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a uma condição temporária. |
| invalid_resource |o recurso de destino Olá é inválido porque não existe, o AD do Azure não encontrou ou não está configurado corretamente. |Isso indica que o recurso hello, se ele existir, não foi configurado no locatário hello. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |

## Solicitar um token de acesso
Agora que você tiver adquirido um authorization_code e ter permissão concedida pelo usuário hello, você pode resgatar Olá `code` para um `access_token` toohello desejado recursos, enviando um `POST` solicitação toohello `/token` ponto de extremidade:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Tente executar a solicitação no Postman! (Não se esqueça de saudação tooreplace `code`) [ ![executados em carteiro](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário.  Para obter mais detalhes, consulte [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |obrigatório |Olá Id do aplicativo de portal de registro que hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a seu aplicativo. |
| grant_type |obrigatório |Deve ser `authorization_code` para fluxo de código de autorização de saudação. |
| scope |obrigatório |Uma lista de escopos separados por espaços.  escopos de saudação solicitado nesse segmento deve ser equivalente tooor um subconjunto dos escopos Olá solicitado no trecho primeiro hello.  Se o escopo de saudação especificado nesta solicitação abrangem vários servidores de recurso, o ponto de extremidade do hello v 2.0 retornará um token para o recurso de saudação especificado no escopo da primeira hello.  Para obter uma explicação mais detalhada de escopos, consulte muito[permissões, autorização e escopos](active-directory-v2-scopes.md). |
| código |obrigatório |Olá authorization_code que você copiou no trecho primeiro de saudação do fluxo de saudação. |
| redirect_uri |obrigatório |Olá igual ao valor redirect_uri que foi usado tooacquire Olá authorization_code. |
| client_secret |obrigatório para aplicativos Web |segredo do aplicativo Hello que você criou no portal de registro de aplicativo hello para seu aplicativo.  Ele não deve ser usado em um aplicativo nativo, pois client_secrets não podem ser armazenados de modo confiável em dispositivos.  Ele é necessário para aplicativos web e APIs, que têm Olá capacidade toostore Olá client_secret com segurança no lado do servidor de saudação da web. |

#### Resposta bem-sucedida
Uma resposta de token bem-sucedida se parecerá com esta:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parâmetro | Descrição |
| --- | --- |
| access_token |token de acesso solicitado Hello. Olá aplicativo pode usar este toohello tooauthenticate token protegido de recurso, como uma API da web. |
| token_type |Indica o valor do tipo de token de saudação. Olá, apenas o tipo que oferece suporte ao AD do Azure é portador |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |
| scope |escopos Olá Olá access_token é válido para. |
| refresh_token |Um token de atualização do OAuth 2.0. Olá aplicativo pode usar esse token adquirir tokens de acesso adicionais após a expiração do token de acesso atual hello.  Refresh_tokens são de vida longa e pode ser usado tooretain acesso tooresources por longos períodos de tempo.  Para obter mais detalhes, consulte toohello [referência de token v 2.0](active-directory-v2-tokens.md). |
| id_token |Um JWT (Token Web JSON) não assinado. Olá aplicativo pode base64Url decodificar segmentos Olá dessas informações de token toorequest sobre o usuário Olá conectado. Olá aplicativo pode armazenar em cache os valores hello e exibi-las, mas ele não deve confiar neles para qualquer autorização ou limites de segurança.  Para obter mais informações sobre id_tokens consulte Olá [referência de token de ponto de extremidade v 2.0](active-directory-v2-tokens.md). |

#### Resposta de erro
As respostas de erro serão parecidas com esta:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| error_codes |Uma lista de códigos de erro específicos do STS que pode ajudar no diagnóstico. |
| timestamp |tempo de saudação na qual ocorreu o erro de saudação. |
| trace_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico. |
| correlation_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico em componentes. |

#### Códigos de erro para erros de ponto de extremidade de token
| Código do Erro | Descrição | Ação do Cliente |
| --- | --- | --- |
| invalid_request |Erro de protocolo, como um parâmetro obrigatório ausente. |Corrija e reenvie a solicitação de saudação |
| invalid_grant |código de autorização de saudação é inválido ou expirou. |Tente um novo toohello de solicitação `/authorize` ponto de extremidade |
| unauthorized_client |Olá cliente autenticado não está autorizado toouse essa autorização conceder tipo. |Isso geralmente ocorre quando o aplicativo de cliente hello não está registrado no AD do Azure ou não será adicionado o locatário do AD do Azure toohello do usuário. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |
| invalid_client |Falha na autenticação de cliente. |as credenciais do cliente Olá não são válidas. toofix, o administrador do aplicativo hello atualiza credenciais hello. |
| unsupported_grant_type |servidor de autorização de saudação não dá suporte para o tipo de concessão de autorização de saudação. |Saudação de alteração conceder tipo na solicitação de saudação. Esse tipo de erro deve ocorrer somente durante o desenvolvimento e ser detectado durante os testes iniciais. |
| invalid_resource |o recurso de destino Olá é inválido porque não existe, o AD do Azure não encontrou ou não está configurado corretamente. |Isso indica que o recurso hello, se ele existir, não foi configurado no locatário hello. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |
| interaction_required |solicitação de saudação requer interação do usuário. Por exemplo, é necessária uma etapa de autenticação adicional. |Repita a solicitação Olá com hello mesmo recurso. |
| temporarily_unavailable |servidor de saudação está temporariamente solicitação de saudação toohandle muito ocupado. |Repita a solicitação de saudação. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a uma condição temporária. |

## Use o token de acesso Olá
Agora que você tenha adquirido com êxito um `access_token`, você pode usar o token Olá em solicitações tooWeb APIs, incluí-lo no hello `Authorization` cabeçalho:

> [!TIP]
> Execute essa solicitação no Postman! (Substitua Olá `Authorization` cabeçalho primeiro) [ ![executados em carteiro](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Atualizar o token de acesso de saudação
Access_tokens são curtas estiveram ativos e você deve atualizá-los depois que elas expirarem toocontinue acessar recursos.  Você pode fazer isso enviando outra `POST` solicitação toohello `/token` ponto de extremidade, desta vez oferecendo Olá `refresh_token` em vez da saudação `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Tente executar a solicitação no Postman! (Não se esqueça de saudação tooreplace `refresh_token`) [ ![executados em carteiro](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário.  Para obter mais detalhes, consulte [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |obrigatório |Olá Id do aplicativo de portal de registro que hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a seu aplicativo. |
| grant_type |obrigatório |Deve ser `refresh_token` para este segmento do fluxo de código de autorização de saudação. |
| scope |obrigatório |Uma lista de escopos separados por espaços.  escopos de saudação solicitado nesse segmento deve ser equivalente tooor um subconjunto dos escopos Olá solicitado no segmento de solicitação authorization_code original hello.  Se o escopo de saudação especificado nesta solicitação abrangem vários servidores de recurso, o ponto de extremidade do hello v 2.0 retornará um token para o recurso de saudação especificado no escopo da primeira hello.  Para obter uma explicação mais detalhada de escopos, consulte muito[permissões, autorização e escopos](active-directory-v2-scopes.md). |
| refresh_token |obrigatório |Olá refresh_token que você copiou no trecho de segundo de saudação do fluxo de saudação. |
| redirect_uri |obrigatório |Olá igual ao valor redirect_uri que foi usado tooacquire Olá authorization_code. |
| client_secret |obrigatório para aplicativos Web |segredo do aplicativo Hello que você criou no portal de registro de aplicativo hello para seu aplicativo.  Ele não deve ser usado em um aplicativo nativo, pois client_secrets não podem ser armazenados de modo confiável em dispositivos.  Ele é necessário para aplicativos web e APIs, que têm Olá capacidade toostore Olá client_secret com segurança no lado do servidor de saudação da web. |

#### Resposta bem-sucedida
Uma resposta de token bem-sucedida se parecerá com esta:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parâmetro | Descrição |
| --- | --- |
| access_token |token de acesso solicitado Hello. Olá aplicativo pode usar este toohello tooauthenticate token protegido de recurso, como uma API da web. |
| token_type |Indica o valor do tipo de token de saudação. Olá, apenas o tipo que oferece suporte ao AD do Azure é portador |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |
| scope |escopos Olá Olá access_token é válido para. |
| refresh_token |Um novo token de atualização OAuth 2.0. Você deve substituir atualização antigo Olá token com este tooensure de token de atualização recém-adquiridos seus tokens de atualização permanecem válidas por tempo possível. |
| id_token |Um JWT (Token Web JSON) não assinado. Olá aplicativo pode base64Url decodificar segmentos Olá dessas informações de token toorequest sobre o usuário Olá conectado. Olá aplicativo pode armazenar em cache os valores hello e exibi-las, mas ele não deve confiar neles para qualquer autorização ou limites de segurança.  Para obter mais informações sobre id_tokens consulte Olá [referência de token de ponto de extremidade v 2.0](active-directory-v2-tokens.md). |

#### Resposta de erro
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| error_codes |Uma lista de códigos de erro específicos do STS que pode ajudar no diagnóstico. |
| timestamp |tempo de saudação na qual ocorreu o erro de saudação. |
| trace_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico. |
| correlation_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico em componentes. |

Para obter uma descrição dos códigos de erro hello e Olá cliente ação recomendada, consulte [códigos de erro para erros de ponto de extremidade token](#error-codes-for-token-endpoint-errors).

