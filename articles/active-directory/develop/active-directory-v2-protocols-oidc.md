---
title: "aaaAzure protocolo v 2.0 e Olá OpenID Connect do Active Directory | Microsoft Docs"
description: "Crie aplicativos web usando Olá AD do Azure v 2.0 implementação Olá OpenID Connect do protocolo de autenticação."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v 2.0 e hello protocolo OpenID Connect
OpenID Connect é um protocolo de autenticação baseado no OAuth 2.0 que você pode usar o sinal de toosecurely em um aplicativo de web de tooa do usuário. Quando você usa a implementação de saudação v 2.0 do ponto de extremidade do OpenID Connect, você pode adicionar entrada e os aplicativos baseados na web da API acesso tooyour. Neste artigo, mostramos como toodo nesse independente do idioma. Descrevemos como toosend e receber mensagens HTTP sem usar quaisquer bibliotecas de código-fonte aberto da Microsoft.

> [!NOTE]
> o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure. toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) estende Olá OAuth 2.0 *autorização* toouse de protocolo como uma *autenticação* de protocolo, para que você possa executar único logon usando OAuth. OpenID Connect apresenta o conceito de saudação de um *token de ID*, que é um token de segurança que permite que o cliente Olá tooverify identidade de saudação do usuário hello. token de ID de saudação também obtém informações de perfil básico sobre usuário hello. Porque o OpenID Connect estende o OAuth 2.0, os aplicativos com segurança podem adquirir *tokens de acesso*, que pode ser usado tooaccess recursos que são protegidos por um [servidor de autorização](active-directory-v2-protocols.md#the-basics). É recomendável que você use o OpenID Connect se estiver criando um [aplicativo Web](active-directory-v2-flows.md#web-apps) que fica hospedado em um servidor e é acessado por meio de um navegador.

## Diagrama de protocolo: Entrar
Hello fluxo de entrada mais básico tem etapas Olá mostradas no diagrama seguinte hello. Descrevemos cada etapa detalhadamente neste artigo.

![Protocolo OpenID Connect: entrar](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Obter documento de metadados de OpenID Connect Olá
OpenID Connect descreve um documento de metadados que contém a maioria das informações de saudação necessárias para um aplicativo tooperform entrar no sistema. Isso inclui informações como Olá URLs toouse e local de saudação de chaves públicas de assinatura do serviço de saudação. Ponto de extremidade Olá v 2.0, isso é Olá OpenID Connect documento de metadados que devem usar:

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Olá `{tenant}` pode assumir um dos quatro valores:

| Valor | Descrição |
| --- | --- |
| `common` |Os usuários com uma conta pessoal da Microsoft e uma conta corporativa ou escolar do Azure Active Directory (AD do Azure) podem entrar no aplicativo toohello. |
| `organizations` |Somente os usuários com o trabalham ou contas de estudante do AD do Azure podem entrar no aplicativo toohello. |
| `consumers` |Somente os usuários com uma conta pessoal da Microsoft podem entrar no aplicativo toohello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` |Somente os usuários com uma conta corporativa ou escolar um AD do Azure específico do locatário pode entrar no aplicativo toohello. O nome de domínio amigável de Olá Olá locatário do Azure AD ou identificador GUID do locatário Olá pode ser usado. |

saudação de metadados são um documento de JSON JavaScript Object Notation () simples. Consulte Olá trecho de código para obter um exemplo a seguir. Olá conteúdo do trecho totalmente descrito Olá [OpenID Connect especificação](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

Normalmente, você usaria este documento de metadados tooconfigure uma biblioteca de OpenID Connect ou SDK; biblioteca de saudação usaria Olá metadados toodo seu trabalho. No entanto, se você não estiver usando uma biblioteca de OpenID Connect de pré-compilação, você pode seguir etapas Olá Olá restante neste artigo tooperform entrar em um aplicativo web usando o ponto de extremidade do hello v 2.0.

## Enviar solicitação de entrada hello
Quando seu aplicativo web precisa de usuário de saudação tooauthenticate, ele pode direcionar Olá usuário toohello `/authorize` ponto de extremidade. Essa solicitação é semelhante trecho primeiro de toohello de saudação [fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md), com estas diferenças importantes:

* solicitação de saudação deve incluir Olá `openid` escopo Olá `scope` parâmetro.
* Olá `response_type` parâmetro deve incluir `id_token`.
* solicitação de saudação deve incluir Olá `nonce` parâmetro.

Por exemplo:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Clique em Olá tooexecute de link a seguir esta solicitação. Depois que você entrar, seu navegador será redirecionado toohttps://localhost/myapp/, com um token de ID na barra de endereços de saudação. Observe que esta solicitação usa `response_mode=query` (somente para fins de demonstração). É recomendável usar o `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parâmetro | Condição | Descrição |
| --- | --- | --- |
| locatário |Obrigatório |Você pode usar o hello `{tenant}` valor no caminho de saudação do hello solicitação toocontrol quem pode entrar no aplicativo toohello. Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário. Para saber mais, veja [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obrigatório |Olá aplicativo ID que Olá [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) atribuído tooyour aplicativo. |
| response_type |Obrigatório |Deve incluir `id_token` para conexão do OpenID Connect. Ele também pode incluir outros `response_types` valores, como `code`. |
| redirect_uri |Recomendadas |Olá redirecione o URI do aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo. Ele deve corresponder exatamente um redirecionamento Olá URIs que você registrou no portal de hello, exceto que ele deve ser uma URL codificada. |
| scope |Obrigatório |Uma lista de escopos separados por espaços. Para OpenID Connect, ele deve incluir o escopo de saudação `openid`, que converte toohello permissão de "Entrar" na interface do usuário de consentimento de saudação. Você também pode incluir outros escopos nesta solicitação para solicitar o consentimento. |
| nonce |Obrigatório |Um valor incluído na solicitação hello, gerada pelo aplicativo hello, que será incluído no valor resultante de id_token hello como uma declaração. Olá aplicativo pode verificar que os ataques de reprodução do token toomitigate esse valor. valor de saudação normalmente é uma cadeia de caracteres aleatória e exclusiva que pode ser usado tooidentify Olá origem da solicitação de saudação. |
| response_mode |Recomendadas |Especifica o método hello que deve ser usado toosend Olá resultante autorização código back tooyour aplicativo. Pode ser `query`, `form_post` ou `fragment`. Para aplicativos web, é recomendável usar `response_mode=form_post`, tooensure Olá transferência mais segura do aplicativo de tooyour de tokens. |
| state |Recomendadas |Um valor incluído na solicitação de saudação que também será retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo desejado. Um valor exclusivo gerado aleatoriamente é usado normalmente muito[impedir ataques de falsificação de solicitação entre sites](http://tools.ietf.org/html/rfc6749#section-10.12). estado de saudação é também usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de ocorrer a solicitação de autenticação Olá, como Olá página ou modo de exibição de usuário de saudação estava em. |
| prompt |Opcional |Indica o tipo de saudação da interação do usuário é necessária. Olá somente os valores válidos no momento são `login`, `none`, e `consent`. Olá `prompt=login` declaração força Olá usuário tooenter suas credenciais na solicitação, que nega o logon único. Olá `prompt=none` declaração é hello oposta. Esta declaração garante que o usuário Olá não é apresentado com qualquer prompt interativo natureza. Se Olá não pode ser concluída silenciosamente por meio de logon único, o ponto de extremidade do hello v 2.0 retornará um erro. Olá `prompt=consent` declaração gatilhos Olá a caixa de diálogo de consentimento de OAuth depois Olá usuário faz logon. caixa de diálogo de saudação solicita Olá usuário toogrant permissões toohello aplicativo. |
| login_hint |Opcional |Você pode usar esse parâmetro toopre preenchimento Olá nome de usuário e email campo de endereço da página de entrada hello para usuário hello, se você souber o nome de usuário Olá antecipadamente. Frequentemente, aplicativos usam esse parâmetro durante a reautenticação, depois de extrair já Olá nome de usuário de uma entrada anterior usando Olá `preferred_username` de declaração. |
| domain_hint |Opcional |Esse valor pode ser `consumers` ou `organizations`. Se for incluído, ele ignora o processo de descoberta baseada em email Olá usuário Olá atravessa Olá v 2.0 página de entrada, para uma experiência de usuário um pouco mais simples. Frequentemente, aplicativos usam esse parâmetro durante a autenticação novamente por meio da extração Olá `tid` declaração de token de ID de saudação. Se hello `tid` é de valor de declaração `9188040d-6c67-4c5b-b112-36a304b66dad`, use `domain_hint=consumers`. Caso contrário, use `domain_hint=organizations`. |

Neste ponto, o usuário Olá é tooenter solicitada suas credenciais e autenticação Olá concluída. Hello ponto de extremidade v 2.0 verifica que o usuário Olá consentiu permissões toohello indicadas no hello `scope` parâmetro de consulta. Se o usuário Olá não consentiu tooany das permissões, o ponto de extremidade do hello v 2.0 solicita Olá tooconsent toohello necessárias permissões. Você pode ler mais sobre [aplicativos multilocatários, autorização e permissões](active-directory-v2-scopes.md).

Depois que o usuário Olá autentica e concede consentimento, Olá v 2.0 ponto de extremidade retorna um aplicativo de tooyour de resposta em Olá indicado URI de redirecionamento usando o método hello especificado no hello `response_mode` parâmetro.

### Resposta bem-sucedida
Uma resposta bem-sucedida ao usar `response_mode=form_post` tem esta aparência:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parâmetro | Descrição |
| --- | --- |
| id_token |Olá token de ID que Olá aplicativo solicitado. Você pode usar o hello `id_token` tooverify parâmetro hello a identidade do usuário e iniciar uma sessão de usuário de saudação. Para obter mais detalhes sobre tokens de ID e seu conteúdo, consulte Olá [referência de tokens de ponto de extremidade v 2.0](active-directory-v2-tokens.md). |
| state |Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que os valores de estado Olá Olá solicitação e resposta são idênticos. |

### Resposta de erro
Respostas de erro também podem enviadas toohello URI de redirecionamento para que hello aplicativo pode lidar com eles. Uma resposta de erro tem esta aparência:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que você pode usar tooclassify tipos de erros que ocorrem e tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |

### Códigos de erro para erros de ponto de extremidade de autorização
Olá, tabela a seguir descreve os códigos de erro que podem ser retornados em Olá `error` parâmetro da resposta de erro hello:

| Código do erro | Descrição | Ação do cliente |
| --- | --- | --- |
| invalid_request |Erro de protocolo, como um parâmetro obrigatório ausente. |Corrija e reenvie a solicitação de saudação. Esse é um erro de desenvolvimento normalmente identificado durante os testes iniciais. |
| unauthorized_client |aplicativo de cliente Hello não é possível solicitar um código de autorização. |Isso geralmente ocorre quando o aplicativo de cliente hello não está registrado no AD do Azure ou não será adicionado o locatário do AD do Azure toohello do usuário. aplicativo Hello pode solicitar Olá usuário com o aplicativo de hello tooinstall instruções e adicioná-lo tooAzure AD. |
| access_denied |consentimento negado pelo proprietário do recurso de saudação. |aplicativo de cliente Hello pode notificar o usuário de saudação que ele não pode continuar a menos que o consentimento do usuário hello. |
| unsupported_response_type |servidor de autorização de saudação não oferece suporte a tipo de resposta de saudação na solicitação de saudação. |Corrija e reenvie a solicitação de saudação. Esse é um erro de desenvolvimento normalmente identificado durante os testes iniciais. |
| server_error |servidor de saudação encontrou um erro inesperado. |Repita a solicitação de saudação. Esses erros podem resultar de condições temporárias. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a erro temporário tooa. |
| temporarily_unavailable |servidor de saudação está temporariamente solicitação de saudação toohandle muito ocupado. |Repita a solicitação de saudação. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a condição temporária tooa. |
| invalid_resource |o recurso de destino Olá é inválido porque não existe, o AD do Azure não encontrou ou não está configurado corretamente. |Isso indica que recursos hello, se ele existir, não foi configurado no locatário hello. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |

## Validar o token de ID de saudação
Receber um token de ID não é suficiente tooauthenticate hello. Você também deve validar a assinatura do token de ID hello e verificar Olá declarações no token Olá por requisitos do seu aplicativo. o ponto de extremidade do Hello v 2.0 usa [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e público tokens de toosign de criptografia de chave e verificar se eles são válidos.

Você pode escolher o token de ID de saudação toovalidate no código do cliente, mas uma prática comum é o servidor de back-end do toosend Olá ID tooa token e executar validações hello. Depois que tiver validado assinatura de saudação do token de ID hello, você precisará tooverify algumas declarações. Para obter mais informações, incluindo mais sobre [Validando tokens](active-directory-v2-tokens.md#validating-tokens) e [informações importantes sobre substituição de chave de assinatura](active-directory-v2-tokens.md#validating-tokens), consulte Olá [v 2.0 tokens referência](active-directory-v2-tokens.md). Recomendamos usar uma biblioteca tooparse e validar tokens. Há pelo menos uma dessas bibliotecas disponível para a maioria das linguagens e plataformas.
<!--TODO: Improve hello information on this-->

Você também poderá toovalidate de declarações adicionais, dependendo do cenário. Algumas validações comuns incluem:

* Certifique-se de que Olá usuário ou a organização tiver se inscrito para o aplicativo hello.
* Certifique-se de que o usuário Olá exigiu privilégios ou autorização.
* Garanta que uma determinada intensidade de autenticação tenha ocorrido, como autenticação multifator.

Para obter mais informações sobre declarações de saudação em um token de ID, consulte Olá [referência de tokens de ponto de extremidade v 2.0](active-directory-v2-tokens.md).

Após validar completamente o token de ID Olá, você pode começar uma sessão com usuário hello. Use declarações Olá Olá ID tooget token saber usuário Olá em seu aplicativo. Você pode usar essas informações para exibição, registros, autorizações e assim por diante.

## Enviar uma solicitação de saída
Quando desejar toosign usuário saudação do seu aplicativo, ele não é suficiente tooclear cookies do seu aplicativo ou caso contrário terminar sessão saudação do usuário. Você também deve redirecionar o usuário Olá toohello toosign de ponto de extremidade v 2.0-out. Se você não fizer isso, o usuário Olá autentica novamente tooyour aplicativo sem inserir suas credenciais novamente, porque eles terão uma única entrada sessão válida com o ponto de extremidade do hello v 2.0.

Você pode redirecionar Olá usuário toohello `end_session_endpoint` listados no documento de metadados de OpenID Connect hello:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Parâmetro | Condição | Descrição |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Recomendadas | URL Olá Olá usuário é redirecionado tooafter sair com êxito. Se o parâmetro hello não for incluído, usuário Olá é mostrado uma mensagem genérica que é gerada pelo ponto de extremidade do hello v 2.0. Essa URL deve corresponder a um de redirecionamento Olá que URIs registrados para seu aplicativo no portal de registro de aplicativo hello.  |

## Logout único
Quando você redirecionar Olá usuário toohello `end_session_endpoint`, o ponto de extremidade do hello v 2.0 limpa Olá sessão de usuário do navegador de saudação. No entanto, o usuário Olá ainda poderá ser conectado em tooother aplicativos que usam contas da Microsoft para autenticação. tooenable desses usuários de saudação aplicativos toosign out simultaneamente, Olá v 2.0 ponto de extremidade envia uma solicitação de HTTP GET toohello registrado `LogoutUrl` de todos os aplicativos de saudação usuário hello está atualmente conectado ao. Aplicativos devem responder solicitação toothis desmarcando qualquer sessão que identifica o usuário hello e retornando um `200` resposta.  Se você quiser sair toosupport o logon único em seu aplicativo, você deve implementar um `LogoutUrl` no código do aplicativo.  Você pode definir Olá `LogoutUrl` do portal de registro de aplicativo hello.

## Diagrama de Protocolos: aquisição de Token
Muitos aplicativos da web precisam toonot somente entrada hello usuário, mas também tooaccess um serviço web em nome de usuário hello usando OAuth. Este cenário combina OpenID Connect para a autenticação de usuário ao obter simultaneamente uma autorização código que você pode usar o acesso de tooget tokens se você estiver usando o fluxo de código de autorização de OAuth hello.

Olá completo OpenID Connect entrar e fluxo de aquisição de token parece semelhante toohello próximo diagrama. Descrevemos cada etapa em detalhes nas seções de saudação próximas artigo hello.

![Protocolo OpenID Connect: aquisição de token](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Obter tokens de acesso
tokens de acesso tooacquire, modificar a solicitação de entrada hello:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Clique em Olá tooexecute de link a seguir esta solicitação. Depois que você entrar, seu navegador é redirecionado toohttps://localhost/myapp/, com um token de ID e um código na barra de endereços de saudação. Observe que esta solicitação usa `response_mode=query` (somente para fins de demonstração). É recomendável usar o `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

Com a inclusão de escopos de permissão na solicitação hello e usando `response_type=id_token code`, o ponto de extremidade do hello v 2.0 garante que o usuário Olá consentiu permissões toohello indicadas no hello `scope` parâmetro de consulta. Ele retorna um tooexchange de aplicativo autorização código tooyour para um token de acesso.

### Resposta bem-sucedida
Uma resposta bem-sucedida do uso do `response_mode=form_post` tem a seguinte aparência:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parâmetro | Descrição |
| --- | --- |
| id_token |Olá token de ID que Olá aplicativo solicitado. Você pode usar a identidade do usuário do hello ID tooverify token hello e iniciar uma sessão de usuário de saudação. Você encontrará mais detalhes sobre tokens de ID e seu conteúdo Olá [referência de tokens de ponto de extremidade v 2.0](active-directory-v2-tokens.md). |
| código |código de autorização Olá Olá aplicativo solicitado. Olá aplicativo pode usar toorequest código de autorização Olá um token de acesso do recurso de destino hello. Um código de autorização tem uma duração muito curta. Normalmente, um código de autorização expira em cerca de 10 minutos. |
| state |Se um parâmetro de estado é incluído na solicitação hello, hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que os valores de estado Olá Olá solicitação e resposta são idênticos. |

### Resposta de erro
Respostas de erro também podem enviadas toohello URI de redirecionamento para que hello aplicativo possa tratá-los corretamente. Uma resposta de erro tem esta aparência:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que você pode usar tooclassify tipos de erros que ocorrem e tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |

Para obter uma descrição dos possíveis códigos de erro e as respostas recomendadas do cliente, veja [Códigos de erro para erros de ponto de extremidade de autorização](#error-codes-for-authorization-endpoint-errors).

Quando você tiver um código de autorização e um token de ID, você pode entrar usuário hello e obter tokens de acesso em seu nome. toosign Olá usuário, você deve validar o token de ID Olá [exatamente conforme descrito](#validate-the-id-token). tooget tokens de acesso, execute as etapas de saudação descritas em nosso [documentação do protocolo OAuth](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
