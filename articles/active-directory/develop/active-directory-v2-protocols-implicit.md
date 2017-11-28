---
title: "aplicativos de única página aaaSecure usando fluxo implícito do hello AD do Azure v 2.0 | Microsoft Docs"
description: "Criando aplicativos de web usando a implementação de v 2.0 do AD do Azure de fluxo implícito Olá para aplicativos de única página."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# v 2.0 protocolos - SPAs usando fluxo implícito Olá
Com o ponto de extremidade Olá v 2.0, você pode assinar os usuários em seus aplicativos de única página com contas pessoais e de trabalho/escola do Microsoft.  Página única e outros aplicativos JavaScript que executam principalmente em uma face de navegador interessantes alguns desafios ao vem tooauthentication:

* características de segurança Olá esses aplicativos são significativamente diferentes de aplicativos da web de servidor tradicionais com base.
* Muitos servidores de autorização e provedores de identidade não dão suporte a solicitações CORS.
* Redirecionamentos do navegador de página inteira para fora do aplicativo hello se tornar a experiência do usuário toohello particularmente invasivo.

Para esses aplicativos (pense: AngularJS, Ember.js, React.js, etc) do AD do Azure dá suporte ao fluxo de concessão implícita do OAuth 2.0 hello.  fluxo implícito Olá Olá descrito [especificação do OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.2).  O principal benefício é que ele permite tokens de tooget do aplicativo de saudação do AD do Azure sem realizar uma troca de credenciais do servidor de back-end.  Isso permite Olá aplicativo toosign no usuário hello, manter a sessão e obter tokens tooother APIs da web dentro de código de JavaScript do cliente de saudação.  Há alguns tootake considerações de segurança importantes em consideração ao usar fluxo implícito do hello - especificamente em torno [cliente](http://tools.ietf.org/html/rfc6749#section-10.3) e [representação de usuário](http://tools.ietf.org/html/rfc6749#section-10.3).

Se você quiser fluxo implícito do toouse hello e aplicativo do Azure AD tooadd autenticação tooyour JavaScript, é recomendável que você use nossa biblioteca de JavaScript do código-fonte aberto, [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Há alguns tutoriais do AngularJS [aqui](active-directory-appmodel-v2-overview.md#getting-started) toohelp começar.  

No entanto, se você preferir não toouse uma biblioteca em suas mensagens de protocolo de aplicativo e enviar de página única por conta própria, siga as etapas de gerais de saudação abaixo.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## Diagrama de protocolo
Olá toda entrada implícita no fluxo parecida com esta - cada Olá etapas são descritas em detalhes abaixo.

![Raias do OpenId Connect](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Enviar solicitação de entrada hello
sinal de tooinitially hello usuário em seu aplicativo, você pode enviar um [OpenID Connect](active-directory-v2-protocols-oidc.md) solicitação de autorização e obter um `id_token` do ponto de extremidade do hello v 2.0:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Clique o link da saudação abaixo tooexecute esta solicitação! Depois de entrar, seu navegador deve ser redirecionado muito`https://localhost/myapp/` com um `id_token` na barra de endereços de saudação.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário.  Para obter mais detalhes, consulte [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |obrigatório |Olá Id do aplicativo de portal de registro que hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a seu aplicativo. |
| response_type |obrigatório |Deve incluir `id_token` para conexão do OpenID Connect.  Ele também pode incluir Olá response_type `token`. Usando `token` aqui permitirá que seu tooreceive aplicativo extremidade de autorização de um token de acesso imediatamente da saudação sem ter que toomake autorizar um segundo toohello de solicitação ponto de extremidade.  Se você usar o hello `token` response_type, Olá `scope` parâmetro deve conter um escopo que indica qual recurso tooissue Olá o token para. |
| redirect_uri |recomendável |Olá redirect_uri do seu aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo.  Ele deve corresponder exatamente uma saudação redirect_uris que você registrou no portal de hello, exceto que ele deve ser codificados de url. |
| scope |obrigatório |Uma lista de escopos separados por espaços.  Para OpenID Connect, ele deve incluir o escopo de saudação `openid`, que converte toohello permissão de "Entrar" na interface do usuário de consentimento de saudação.  Opcionalmente, você também pode desejar Olá tooinclude `email` ou `profile` [escopos](active-directory-v2-scopes.md) para obter dados de usuário do access tooadditional.  Você também pode incluir outros escopos nesta solicitação para solicitar o consentimento toovarious recursos. |
| response_mode |recomendável |Especifica o método hello que deve ser usado toosend Olá resultante token tooyour back aplicativo.  Deve ser `fragment` para fluxo implícito hello. |
| state |recomendável |Um valor incluído na solicitação de saudação que também será retornada na resposta de token hello.  Pode ser uma cadeia de caracteres de qualquer conteúdo desejado.  Um valor exclusivo gerado aleatoriamente que normalmente é usado para [impedir ataques de solicitação intersite forjada](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| nonce |obrigatório |Um valor incluído na solicitação hello, gerada pelo aplicativo hello, que será incluído no id_token resultante de saudação como uma declaração.  aplicativo Hello, em seguida, pode verificar a que ataques de reprodução do token toomitigate esse valor.  Olá valor costuma ser uma cadeia de caracteres aleatória e exclusiva que pode ser usado tooidentify Olá origem da solicitação de saudação. |
| prompt |opcional |Indica o tipo de saudação da interação do usuário é necessária.  Olá somente no momento, os valores válidos são 'logon', 'none', ' consente '.  `prompt=login`será force Olá usuário tooenter suas credenciais na solicitação, Negar logon único no.  `prompt=none`é Olá oposta - garantirá que o usuário Olá não é apresentado com qualquer prompt interativo natureza.  Se a solicitação Olá não pode ser concluída silenciosamente por meio de logon único, o ponto de extremidade do hello v 2.0 retornará um erro.  `prompt=consent`saudação de gatilho OAuth será consentimento caixa de diálogo após o usuário se autentica hello, solicitando Olá usuário toogrant permissões toohello aplicativo. |
| login_hint |opcional |Pode ser campo de endereço de email/nome de usuário usado toopre preenchimento Olá de saudação página de logon de usuário hello, se você souber o nome de usuário antecipadamente.  Aplicativos geralmente usará esse parâmetro durante a reautenticação, já ter extraído Olá nome de usuário de uma entrada anterior usando Olá `preferred_username` de declaração. |
| domain_hint |opcional |Pode ser `consumers` ou `organizations`.  Se incluído, ele ignorará o processo de descoberta baseada em email Olá que o usuário passa em Olá v 2.0 página de entrada, à esquerda tooa um pouco mais simples de experiência do usuário.  Aplicativos geralmente usará esse parâmetro durante a reautenticação, extraindo Olá `tid` Olá id_token de declaração.  Se hello `tid` é de valor de declaração `9188040d-6c67-4c5b-b112-36a304b66dad`, você deve usar `domain_hint=consumers`.  Caso contrário, use `domain_hint=organizations`. |

Neste ponto, o usuário de saudação será solicitado tooenter suas credenciais e autenticação Olá concluída.  Hello ponto de extremidade v 2.0 também garantem que o usuário Olá consentiu permissões toohello indicadas no hello `scope` parâmetro de consulta.  Se o usuário Olá não consentiu tooany das permissões, solicitará Olá usuário tooconsent toohello necessárias permissões.  Os detalhes dos aplicativos quanto a [permissões, consentimento e multilocatário são fornecidos aqui](active-directory-v2-scopes.md).

Depois que o usuário Olá autentica e concede consentimento, o ponto de extremidade do hello v 2.0 retornará um aplicativo de tooyour de resposta em Olá indicado `redirect_uri`, usando o método hello especificado no hello `response_mode` parâmetro.

#### Resposta bem-sucedida
Uma resposta bem-sucedida usando `response_mode=fragment` e `response_type=id_token+token` aparência a seguir hello, quebras de linha para legibilidade:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Parâmetro | Descrição |
| --- | --- |
| access_token |Incluído se `response_type` incluir `token`. token de acesso Olá Olá aplicativo solicitado, nesse caso para Olá Microsoft Graph.  token de acesso de saudação não deve ser decodificado ou inspecionadas de outra forma, ele pode ser tratado como uma cadeia de caracteres opaca. |
| token_type |Incluído se `response_type` incluir `token`.  Sempre será `Bearer`. |
| expires_in |Incluído se `response_type` incluir `token`.  Indica o número de saudação de segundos Olá token for válido, para fins de cache. |
| scope |Incluído se `response_type` incluir `token`.  Indica a saudação escopo (s) para o qual Olá access_token será válido. |
| id_token |Olá id_token que Olá aplicativo solicitado. Você pode usar a identidade do usuário do hello id_token tooverify hello e iniciar uma sessão de usuário de saudação.  Para obter mais detalhes id_tokens e seu conteúdo está incluído no hello [referência de token de ponto de extremidade v 2.0](active-directory-v2-tokens.md). |
| state |Se um parâmetro de estado é incluído na solicitação hello, hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que os valores de estado Olá Olá solicitação e resposta são idênticos. |

#### Resposta de erro
Respostas de erro também podem ser enviadas toohello `redirect_uri` para o aplicativo hello possa tratá-los adequadamente:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

## Validar Olá id_token
Receber apenas um id_token não é suficiente tooauthenticate Olá usuário Você deve validar assinatura do hello id_token e verificar Olá declarações no token Olá por requisitos do seu aplicativo.  o ponto de extremidade do Hello v 2.0 usa [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e público tokens de toosign de criptografia de chave e verificar se eles são válidos.

Você pode escolher Olá toovalidate `id_token` no código do cliente, mas uma prática comum é Olá toosend `id_token` tooa servidor de back-end e executar validações hello.  Depois de validado assinatura Olá Olá id_token, existem algumas declarações, que será necessário tooverify.  Consulte Olá [referência de token v 2.0](active-directory-v2-tokens.md) para obter mais informações, incluindo [Validando Tokens](active-directory-v2-tokens.md#validating-tokens) e [importantes informações sobre assinatura de substituição de chave](active-directory-v2-tokens.md#validating-tokens).  Há, pelo menos, uma disponível para a maioria das linguagens e plataformas.
<!--TODO: Improve hello information on this-->

Você também poderá toovalidate declarações adicionais dependendo do cenário.  Algumas validações comuns incluem:

* Garantindo a organização da usuário Olá tiver se inscrito para o aplicativo hello.
* Usuário de saudação garantindo tem autorização/privilégios apropriados
* Garantir que uma determinada intensidade de autenticação tenha ocorrido, como autenticação multifator.

Para obter mais informações sobre declarações de saudação em um id_token, consulte Olá [referência de token de ponto de extremidade v 2.0](active-directory-v2-tokens.md).

Após validar completamente id_token Olá, você pode iniciar uma sessão de usuário de saudação e usar declarações de saudação em Olá id_token tooobtain saber usuário Olá em seu aplicativo.  Essas informações podem ser usadas para exibição, registros, autorizações, etc.

## Obter tokens de acesso
Agora que você tenha assinado usuário Olá em seu aplicativo de página única, você pode obter tokens de acesso para web chamar APIs protegido pelo AD do Azure, como Olá [Microsoft Graph](https://graph.microsoft.io).  Mesmo se você já recebeu um token usando Olá `token` response_type, você pode usar recursos de tooadditional este método tooacquire tokens sem ter que tooredirect Olá usuário toosign novamente.

No fluxo normal de OpenID Connect/OAuth hello, você faria isso fazendo uma toohello de solicitação v 2.0 `/token` ponto de extremidade.  No entanto, o ponto de extremidade do hello v 2.0 não não suporte a solicitações CORS, para fazer AJAX chama tooget e tokens de atualização está fora da pergunta hello.  Em vez disso, você pode usar fluxo implícito Olá em um iframe oculto tooget novos tokens para outros APIs da web: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Tente copiar e colar Olá abaixo solicitação em uma guia do navegador! (Não se esqueça de saudação tooreplace `domain_hint` e hello `login_hint` valores com hello corrigir os valores para o usuário)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário.  Para obter mais detalhes, consulte [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |obrigatório |Olá Id do aplicativo de portal de registro que hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) atribuído a seu aplicativo. |
| response_type |obrigatório |Deve incluir `id_token` para conexão do OpenID Connect.  Também pode incluir outros response_types, como `code`. |
| redirect_uri |recomendável |Olá redirect_uri do seu aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo.  Ele deve corresponder exatamente uma saudação redirect_uris que você registrou no portal de hello, exceto que ele deve ser codificados de url. |
| scope |obrigatório |Uma lista de escopos separados por espaços.  Para obter tokens, inclua todos os [escopos](active-directory-v2-scopes.md) você precisa para o recurso de saudação de interesse. |
| response_mode |recomendável |Especifica o método hello que deve ser usado toosend Olá resultante token tooyour back aplicativo.  Pode ser `query`, `form_post` ou `fragment`. |
| state |recomendável |Um valor incluído na solicitação de saudação que também será retornada na resposta de token hello.  Pode ser uma cadeia de caracteres de qualquer conteúdo desejado.  Um valor exclusivo gerado aleatoriamente que normalmente é usado para impedir ataques de solicitação intersite forjada.  estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| nonce |obrigatório |Um valor incluído na solicitação hello, gerada pelo aplicativo hello, que será incluído no id_token resultante de saudação como uma declaração.  aplicativo Hello, em seguida, pode verificar a que ataques de reprodução do token toomitigate esse valor.  Olá valor costuma ser uma cadeia de caracteres aleatória e exclusiva que pode ser usado tooidentify Olá origem da solicitação de saudação. |
| prompt |obrigatório |Para atualizar e obter tokens em um iframe oculto, você deve usar `prompt=none` tooensure que Olá iframe não pare de responder na página de entrada de Olá v 2.0 e retorna imediatamente. |
| login_hint |obrigatório |Para atualizar e obter tokens em um iframe oculto, você deve incluir o nome de usuário de saudação do usuário Olá nessa dica em ordem toodistinguish entre várias sessões de usuário Olá pode ter em um determinado ponto no tempo. Você pode extrair o nome de usuário de saudação de uma entrada anterior usando Olá `preferred_username` de declaração. |
| domain_hint |obrigatório |Pode ser `consumers` ou `organizations`.  Para atualizar e obter tokens em um iframe oculto, você deve incluir Olá domain_hint na solicitação de saudação.  Você deve extrair Olá `tid` toouse qual valor de declaração de saudação id_token de uma entrada toodetermine anterior.  Se hello `tid` é de valor de declaração `9188040d-6c67-4c5b-b112-36a304b66dad`, você deve usar `domain_hint=consumers`.  Caso contrário, use `domain_hint=organizations`. |

Obrigado toohello `prompt=none` parâmetro, essa solicitação seja bem-sucedida ou falhará imediatamente e retornará tooyour aplicativo.  Uma resposta bem-sucedida será enviada tooyour aplicativo à saudação indicada `redirect_uri`, usando o método hello especificado no hello `response_mode` parâmetro.

#### Resposta bem-sucedida
Uma resposta bem-sucedida usando `response_mode=fragment` tem a seguinte aparência:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| . | Descrição |
| --- | --- |
| access_token |saudação de token que o aplicativo hello solicitado. |
| token_type |Sempre será `Bearer`. |
| state |Se um parâmetro de estado é incluído na solicitação hello, hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que os valores de estado Olá Olá solicitação e resposta são idênticos. |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |
| scope |escopos Olá Olá token de acesso é válido para. |

#### Resposta de erro
Respostas de erro também podem ser enviadas toohello `redirect_uri` para o aplicativo hello possa tratá-los corretamente.  No caso de saudação de `prompt=none`, será um erro esperado:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

Se você receber esse erro na solicitação de iframe hello, Olá usuário deve interativamente entrar novamente tooretrieve um novo token.  Você pode escolher toohandle neste caso, de forma que faz sentido para o seu aplicativo.

## Atualizando tokens
Ambos `id_token`s e `access_token`s expirará após um curto período de tempo, para que seu aplicativo deve estar preparado toorefresh esses tokens periodicamente.  toorefresh o tipo de token, você pode executar Olá mesma solicitação iframe oculto acima usando Olá `prompt=none` parâmetro comportamento toocontrol do AD do Azure.  Se você quiser tooreceive um novo `id_token`, ser toouse se `response_type=id_token` e `scope=openid`, bem como um `nonce` parâmetro.

## Enviar uma solicitação de desconexão
Olá OpenIdConnect `end_session_endpoint` permite que seu aplicativo toosend um tooend de ponto de extremidade solicitação toohello v 2.0 limpar cookies e a sessão de um usuário definidos pelo ponto de extremidade do hello v 2.0.  toofully Inscreva-se um usuário de um aplicativo da web, seu aplicativo deve terminar sua própria sessão com o usuário de saudação (geralmente por limpar um cache de token ou descartando cookies) e redirecionar o navegador Olá para:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são `common`, `organizations`, `consumers`e identificadores de locatário.  Para obter mais detalhes, consulte [noções básicas de protocolo](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | recomendável | URL Olá Olá usuário deve ser retornado tooafter logout é concluída. Esse valor deve corresponder a um redirecionamento Olá que URIs registrados para o aplicativo hello. Se não estiver incluído, Olá usuário receberá uma mensagem genérica pelo ponto de extremidade do hello v 2.0. |
