---
title: "Olá aaaUnderstand OpenID Connect fluxo de código de autenticação no AD do Azure | Microsoft Docs"
description: "Este artigo descreve como toouse HTTP mensagens tooauthorize acessar tooweb aplicativos e APIs da web em seu locatário usando o Active Directory do Azure e OpenID Connect."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Autorizar o acesso tooweb aplicativos usando o OpenID Connect e o Active Directory do Azure
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) é uma camada de identidade simples criada com base no protocolo de saudação OAuth 2.0. OAuth 2.0 define tooobtain de mecanismos e use **tokens de acesso** tooaccess protegidos recursos, mas eles não definem as informações de identidade tooprovide métodos padrão. OpenID Connect implementa autenticação como uma extensão toohello o processo de autorização OAuth 2.0. Ele fornece informações sobre o usuário final de saudação na forma de saudação de um `id_token` que verifica a identidade de saudação do usuário hello e fornece informações de perfil básico sobre usuário hello.

O OpenID Connect é a nossa recomendação se você estiver criando um aplicativo Web hospedado em um servidor e acessado por meio de um navegador.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Fluxo de autenticação usando o OpenID Connect
Olá mais básica do fluxo de entrada contém Olá etapas - cada um deles é descrita em detalhes abaixo.

![Fluxo de autenticação usando o OpenId Connect](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Documento de metadados do OpenID Connect

OpenID Connect descreve um documento de metadados que contém a maioria das informações de saudação necessárias para um aplicativo tooperform entrar no sistema. Isso inclui informações como Olá URLs toouse e local de saudação de chaves públicas de assinatura do serviço de saudação. documento de metadados de OpenID Connect Olá pode ser encontrado em:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
saudação de metadados são um documento de JSON JavaScript Object Notation () simples. Consulte Olá trecho de código para obter um exemplo a seguir. Olá conteúdo do trecho totalmente descrito Olá [OpenID Connect especificação](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Enviar solicitação de entrada hello
Quando seu aplicativo web precisa de usuário do tooauthenticate Olá, ele deve direcionar Olá usuário toohello `/authorize` ponto de extremidade. Essa solicitação é semelhante trecho primeiro de toohello de saudação [fluxo de código de autorização do OAuth 2.0](active-directory-protocols-oauth-code.md), com algumas diferenças importantes:

* solicitação de saudação deve incluir o escopo de saudação `openid` em Olá `scope` parâmetro.
* Olá `response_type` parâmetro deve incluir `id_token`.
* solicitação de saudação deve incluir Olá `nonce` parâmetro.

Dessa forma, uma solicitação de exemplo teria esta aparência:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são identificadores de locatário, por exemplo, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` ou `common` para tokens independente de locatário |
| client_id |obrigatório |Olá Id de aplicativo atribuído tooyour aplicativo ao registrar com o Azure AD. Você pode encontrar isso na Olá Portal do Azure. Clique em **Active Directory do Azure**, clique em **registros do aplicativo**, escolha o aplicativo hello e localizar Olá Id do aplicativo na página de aplicativo hello. |
| response_type |obrigatório |Deve incluir `id_token` para conexão do OpenID Connect.  Também pode incluir outros response_types, como `code`. |
| scope |obrigatório |Uma lista de escopos separados por espaços.  Para OpenID Connect, ele deve incluir o escopo de saudação `openid`, que converte toohello permissão de "Entrar" na interface do usuário de consentimento de saudação.  Você também pode incluir outros escopos nesta solicitação para solicitar o consentimento. |
| nonce |obrigatório |Um valor incluído na solicitação hello, gerada pelo aplicativo hello, que está incluído no hello resultante `id_token` como uma declaração.  aplicativo Hello, em seguida, pode verificar a que ataques de reprodução do token toomitigate esse valor.  valor de saudação normalmente é uma cadeia de caracteres aleatória e exclusiva ou um GUID que pode ser usado tooidentify Olá origem da solicitação de saudação. |
| redirect_uri |recomendável |Olá redirect_uri do seu aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo.  Ele deve corresponder exatamente uma saudação redirect_uris que você registrou no portal de hello, exceto que ele deve ser codificados de url. |
| response_mode |recomendável |Especifica o método hello que deve ser usado toosend Olá resultante authorization_code tooyour back aplicativo.  Os valores com suporte são `form_post` para *postagem no formato HTTP* ou `fragment` para *fragmento de URL*.  Para aplicativos web, é recomendável usar `response_mode=form_post` tooensure Olá transferência mais segura do aplicativo de tooyour de tokens. |
| state |recomendável |Um valor incluído na solicitação de saudação que é retornada na resposta de token hello.  Pode ser uma cadeia de caracteres de qualquer conteúdo desejado.  Um valor exclusivo gerado aleatoriamente que normalmente é usado para [impedir ataques de solicitação intersite forjada](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| prompt |opcional |Indica o tipo de saudação da interação do usuário é necessária.  Olá no momento, somente os valores válidos são 'logon', 'none', ' consente '.  `prompt=login`força Olá usuário tooenter suas credenciais na solicitação, Negar logon único.  `prompt=none`é Olá oposta - garante que o usuário Olá não é apresentado com qualquer interativa solicitar qualquer.  Se Olá não pode ser concluída silenciosamente por meio de logon único, o ponto de extremidade Olá retornará um erro.  `prompt=consent`dispara Olá OAuth consentimento caixa de diálogo após o usuário se autentica hello, solicitando Olá usuário toogrant permissões toohello aplicativo. |
| login_hint |opcional |Pode ser o campo de endereço de email/nome de usuário usado toopre preenchimento Olá de saudação página de entrada de usuário Olá, se você souber o nome de usuário antecipadamente.  Aplicativos geralmente usam esse parâmetro durante a reautenticação, já ter extraído Olá nome de usuário de uma entrada anterior usando Olá `preferred_username` de declaração. |

Neste ponto, o usuário Olá é solicitado tooenter suas credenciais e autenticação Olá concluída.

### Resposta de exemplo
Um exemplo de resposta, depois Olá usuário autenticado, pode ser semelhante a:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parâmetro | Descrição |
| --- | --- |
| id_token |Olá `id_token` que o aplicativo hello solicitado. Você pode usar o hello `id_token` tooverify Olá a identidade do usuário e iniciar uma sessão de usuário de saudação. |
| state |Um valor incluído na solicitação de saudação que também é retornada na resposta de token hello. Um valor exclusivo gerado aleatoriamente que normalmente é usado para [impedir ataques de solicitação intersite forjada](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |

### Resposta de erro
Respostas de erro também podem ser enviadas toohello `redirect_uri` para o aplicativo hello possa tratá-los adequadamente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

#### Códigos de erro para erros de ponto de extremidade de autorização
Olá, tabela a seguir descreve Olá vários códigos de erro que podem ser retornados em Olá `error` parâmetro da resposta de erro hello.

| Código do Erro | Descrição | Ação do Cliente |
| --- | --- | --- |
| invalid_request |Erro de protocolo, como um parâmetro obrigatório ausente. |Corrija e reenvie a solicitação de saudação. Esse é um erro de desenvolvimento que, normalmente, é capturado durante os testes iniciais. |
| unauthorized_client |Olá aplicativo cliente não é permitido toorequest um código de autorização. |Isso geralmente ocorre quando o aplicativo de cliente hello não está registrado no AD do Azure ou não será adicionado o locatário do AD do Azure toohello do usuário. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |
| access_denied |Consentimento negado pelo proprietário do recurso |aplicativo de cliente Hello pode notificar o usuário de saudação que ele não pode continuar a menos que o consentimento do usuário hello. |
| unsupported_response_type |servidor de autorização de saudação não oferece suporte a tipo de resposta de saudação na solicitação de saudação. |Corrija e reenvie a solicitação de saudação. Esse é um erro de desenvolvimento que, normalmente, é capturado durante os testes iniciais. |
| server_error |servidor de saudação encontrou um erro inesperado. |Repita a solicitação de saudação. Esses erros podem resultar de condições temporárias. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a erro temporário tooa. |
| temporarily_unavailable |servidor de saudação está temporariamente solicitação de saudação toohandle muito ocupado. |Repita a solicitação de saudação. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a condição temporária tooa. |
| invalid_resource |o recurso de destino Olá é inválido porque não existe, o AD do Azure não encontrou ou não está configurado corretamente. |Isso indica que o recurso hello, se ele existir, não foi configurado no locatário hello. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |

## Validar Olá id_token
Receber apenas um `id_token` não é suficiente tooauthenticate Olá usuário deve validar assinatura hello e verificar declarações Olá Olá `id_token` por requisitos do seu aplicativo. o ponto de extremidade do Hello AD do Azure usa JSON Web Tokens (JWTs) e tokens de toosign de criptografia de chave pública e verificar se eles são válidos.

Você pode escolher Olá toovalidate `id_token` no código do cliente, mas uma prática comum é Olá toosend `id_token` tooa servidor de back-end e executar validações hello. Quando você validar assinatura Olá Olá `id_token`, há algumas declarações são tooverify necessária.

Você também poderá toovalidate declarações adicionais dependendo do cenário. Algumas validações comuns incluem:

* Garantindo a organização da usuário Olá tiver se inscrito para o aplicativo hello.
* Usuário de saudação garantindo tem autorização/privilégios apropriados
* Garantir que uma determinada intensidade de autenticação tenha ocorrido, como autenticação multifator.

Após validar Olá `id_token`, você pode iniciar uma sessão de usuário hello e use declarações Olá Olá `id_token` tooobtain informações sobre o usuário Olá em seu aplicativo. Essas informações podem ser usadas para exibição, registros, autorizações, etc. Para obter mais informações sobre tipos de token hello e declarações, leia [tipos de declaração e Token com suporte](active-directory-token-and-claims.md).

## Enviar uma solicitação de saída
Quando desejar que o usuário de saudação toosign fora do aplicativo hello, é tooclear insuficiência cookies do seu aplicativo ou caso contrário, encerrar a sessão de saudação com usuário hello.  Você também deve redirecionar Olá usuário toohello `end_session_endpoint` para saída.  Se você não toodo, portanto, o usuário de saudação será capaz de tooreauthenticate tooyour aplicativo sem inserir suas credenciais novamente, porque eles terão uma único logon sessão válida com o ponto de extremidade do hello AD do Azure.

Você pode redirecionar simplesmente Olá usuário toohello `end_session_endpoint` listados no documento de metadados de OpenID Connect hello:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| post_logout_redirect_uri |recomendável |URL Olá Olá usuário deve estar logout bem-sucedida tooafter redirecionado.  Se não estiver incluído, o usuário Olá é mostrado uma mensagem genérica. |

## Logout único
Quando você redirecionar Olá usuário toohello `end_session_endpoint`, o AD do Azure limpa Olá sessão de usuário do navegador de saudação. No entanto, o usuário Olá ainda poderá ser conectado em tooother aplicativos que usam o AD do Azure para autenticação. tooenable toosign esses aplicativos Olá usuário out simultaneamente, o AD do Azure envia uma solicitação de HTTP GET toohello registrado `LogoutUrl` de todos os aplicativos de saudação usuário hello está atualmente conectado ao. Aplicativos devem responder solicitação toothis desmarcando qualquer sessão que identifica o usuário hello e retornando um `200` resposta.  Se você quiser sair toosupport o logon único em seu aplicativo, você deve implementar um `LogoutUrl` no código do aplicativo.  Você pode definir Olá `LogoutUrl` de saudação portal do Azure:

1. Navegue toohello [Portal do Azure](https://portal.azure.com).
2. Escolha seu Active Directory, clique em sua conta no canto superior direito de saudação da página de saudação.
3. No painel de navegação à esquerda hello, escolha **Active Directory do Azure**, em seguida, escolha **registros do aplicativo** e selecione seu aplicativo.
4. Clique em **propriedades** e localize Olá **URL de Logout** caixa de texto. 

## Aquisição de token
Muitos aplicativos da web precisam toonot somente entrada hello usuário, mas também acessar um serviço da web em nome de usuário usando o OAuth. Este cenário combina OpenID Connect para a autenticação de usuário ao adquirir o simultaneamente um `authorization_code` que pode ser usado tooget `access_tokens` usando Olá fluxo de código de autorização do OAuth.

## Obter tokens de acesso
tooacquire tokens de acesso, você precisa toomodify Olá solicitação de entrada acima:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Incluindo escopos de permissão na solicitação hello e usando `response_type=code+id_token`, Olá `authorize` ponto de extremidade garante que o usuário Olá consentiu permissões toohello indicadas no hello `scope` parâmetro de consulta e retornar um código de autorização de seu aplicativo tooexchange para um token de acesso.

### Resposta bem-sucedida
Uma resposta bem-sucedida usando `response_mode=form_post` tem a seguinte aparência:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| . | Descrição |
| --- | --- |
| id_token |Olá `id_token` que o aplicativo hello solicitado. Você pode usar o hello `id_token` tooverify Olá a identidade do usuário e iniciar uma sessão de usuário de saudação. |
| código |Olá authorization_code que Olá aplicativo solicitado. Olá aplicativo pode usar toorequest código de autorização Olá um token de acesso do recurso de destino hello. Authorization_codes têm uma duração curta e, geralmente, expiram depois de aproximadamente 10 minutos. |
| state |Se um parâmetro de estado é incluído na solicitação hello, hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que os valores de estado Olá Olá solicitação e resposta são idênticos. |

### Resposta de erro
Respostas de erro também podem ser enviadas toohello `redirect_uri` para o aplicativo hello possa tratá-los adequadamente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

Para obter uma descrição de saudação possíveis códigos de erro e sua ação recomendada do cliente, consulte [códigos de erro para erros de ponto de extremidade de autorização](#error-codes-for-authorization-endpoint-errors).

Depois que uma autorização `code` e um `id_token`, você pode entrar usuário hello e obter tokens de acesso em seu nome.  toosign Olá usuário, você deve validar Olá `id_token` exatamente conforme descrito acima. tooget tokens de acesso, você pode seguir etapas Olá descritas na seção "Usar toorequest de código de autorização de saudação um token de acesso" de saudação do nosso [documentação do protocolo OAuth](active-directory-protocols-oauth-code.md).
