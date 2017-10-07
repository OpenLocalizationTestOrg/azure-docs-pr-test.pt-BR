---
title: Entrada na Web com o OpenID Connect - Azure AD B2C | Microsoft Docs
description: "Criando aplicativos da web usando a implementação do Active Directory do Azure Olá Olá OpenID Connect do protocolo de autenticação"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: entrada na Web com o OpenID Connect
OpenID Connect é um protocolo de autenticação, criado com base em OAuth 2.0, que pode ser usado toosecurely conectar usuários tooweb aplicativos. Por usando hello Azure Active Directory B2C (Azure AD B2C) implementação de OpenID Connect, você pode terceirizar a inscrição, entrar e passa por outro gerenciamento de identidade em seu tooAzure de aplicativos web do Active Directory (AD do Azure). Este guia mostra como toodo caso de maneira independente de linguagem. Descreve como toosend e receber mensagens HTTP sem usar qualquer uma das nossas bibliotecas de código-fonte aberto.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) estende Olá OAuth 2.0 *autorização* protocolo para uso como um *autenticação* protocolo. Isso permite que você tooperform o logon único usando OAuth. Ele apresenta o conceito de saudação de um *token de ID*, que é um token de segurança que permite Olá cliente tooverify Olá a identidade do usuário hello e obter informações de perfil básico sobre usuário hello.

Porque ele estende o OAuth 2.0, ele também permite que aplicativos adquirir toosecurely *tokens de acesso*. Você pode usar access_tokens tooaccess recursos que são protegidos por um [servidor de autorização](active-directory-b2c-reference-protocols.md#the-basics). Nós recomendamos o OpenID Connect se você estiver criando um aplicativo Web que fica hospedado em um servidor e é acessado por meio de um navegador. Se você quiser tooadd identity management tooyour aplicativos móveis ou área de trabalho usando o Azure AD B2C, você deve usar [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) em vez de OpenID Connect.

B2C do AD do Azure estende saudação padrão OpenID Connect protocolo toodo mais de autenticação simples e autorização. Ele apresenta Olá [parâmetro política](active-directory-b2c-reference-policies.md), que permite que você toouse OpenID Connect tooadd experiências do usuário – como inscrição, entrar e gerenciamento de perfil – tooyour aplicativo. Aqui, mostramos como toouse tooimplement OpenID Connect e políticas de cada uma dessas experiências em seus aplicativos web. Também mostraremos como APIs da web de tooget tokens de acesso para acessar.

solicitações HTTP do exemplo Hello na próxima seção, Olá usam diretório do B2C nosso exemplo, fabrikamb2c.onmicrosoft.com, bem como nosso aplicativo de exemplo, https://aadb2cplayground.azurewebsites.net e políticas. Você tem liberdade tootry out Olá solicitações por conta própria usando esses valores ou você pode substituí-los com seus próprios.
Saiba como muito[obter seu próprio locatário B2C, aplicativos e políticas](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Enviar solicitações de autenticação
Quando seu aplicativo web precisa de usuário de saudação tooauthenticate e executar uma política, ele pode direcionar Olá usuário toohello `/authorize` ponto de extremidade. Isso é parte interativa Olá fluxo Olá, qual usuário Olá agirão, dependendo da política de saudação.

Nessa solicitação, o cliente de saudação indica permissões Olá que precisa de tooacquire de usuário Olá Olá `scope` tooexecute de política de parâmetro e hello em Olá `p` parâmetro. Três exemplos são fornecidos no hello seguintes seções (com quebras de linha para facilitar a leitura), cada um usando uma política diferente. tooget uma ideia de como cada solicitação funciona, tente a solicitação de saudação de colá-lo em um navegador e executá-lo.

#### <a name="use-a-sign-in-policy"></a>Usar uma política de entrada
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Usar uma política de inscrição
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Usar uma política de edição de perfil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| client_id |Obrigatório |aplicativo Hello ID que Olá [portal do Azure](https://portal.azure.com/) atribuído tooyour aplicativo. |
| response_type |Obrigatório |tipo de resposta Hello, que deve incluir um token de ID para OpenID Connect. Se seu aplicativo Web também precisa de tokens para chamar uma API Web, você pode usar `code+id_token`, como fizemos aqui. |
| redirect_uri |Recomendadas |Olá `redirect_uri` parâmetro do aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo. Ele deve corresponder exatamente uma saudação `redirect_uri` parâmetros que você registrou no portal de hello, exceto que ele deve ser codificados de URL. |
| scope |Obrigatório |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure AD ambas as permissões que estão sendo solicitados. Olá `openid` escopo indica um toosign permissão nos dados de usuário e get hello sobre usuário Olá na forma de saudação de tokens de ID (mais toocome neste artigo Olá). Olá `offline_access` escopo é opcional para aplicativos web. Indica que seu aplicativo precisará de um *token de atualização* para tooresources de acesso e longa duração. |
| response_mode |Recomendadas |método Hello que deve ser usado toosend Olá resultante autorização código back tooyour aplicativo. Ele pode ser `query`, `form_post` ou `fragment`.  Olá `form_post` resposta é recomendado para melhor segurança. |
| state |Recomendadas |Um valor incluído na solicitação de saudação que também é retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo desejado. Um valor exclusivo gerado aleatoriamente que normalmente é usado para impedir ataques de solicitação intersite forjada. estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página Olá estivesse em. |
| nonce |Obrigatório |Um valor incluído na solicitação de saudação (gerada pelo aplicativo hello) que será incluída no token de ID resultante hello como uma declaração. aplicativo Hello, em seguida, pode verificar a que ataques de reprodução do token toomitigate esse valor. Olá valor costuma ser uma cadeia de caracteres aleatória exclusiva que pode ser usado tooidentify Olá origem da solicitação de saudação. |
| p |Obrigatório |política de saudação que será executada. Ele é o nome de saudação de uma política que é criada no seu locatário B2C. valor de nome de política Olá deve começar com `b2c\_1\_`. Saiba mais sobre as políticas e Olá [estrutura da política extensível](active-directory-b2c-reference-policies.md). |
| prompt |Opcional |tipo de saudação de interação do usuário é necessária. Olá valor só é válida no momento é `login`, que força Olá usuário tooenter suas credenciais na solicitação. O logon único não terá efeito. |

Neste ponto, o usuário de Olá é solicitado fluxo de trabalho da política do toocomplete hello. Isso pode envolver usuário Olá inserir seu nome de usuário e senha, entrar com uma identidade de redes sociais, inscrever directory hello, ou qualquer outro número de etapas, dependendo de como a política de saudação é definida.

Após usuário Olá política hello, o AD do Azure retorna um aplicativo de tooyour de resposta em Olá indicado `redirect_uri` parâmetro, usando o método hello especificado no hello `response_mode` parâmetro. resposta de saudação é Olá mesmo para cada saudação anterior casos, independentes da política de saudação que é executada.

Uma resposta bem-sucedida usando `response_mode=fragment` se parece com esta:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parâmetro | Descrição |
| --- | --- |
| id_token |Olá token de ID que Olá aplicativo solicitado. Você pode usar a identidade do usuário do hello ID tooverify token hello e iniciar uma sessão de usuário de saudação. Mais detalhes sobre tokens de ID e seus conteúdos são incluídos no hello [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| código |Olá código de autorização que o aplicativo hello solicitado, se você usou `response_type=code+id_token`. saudação de aplicativo pode usar toorequest código de autorização Olá um token de acesso para um recurso de destino. Os códigos de autorização têm uma duração muito curta. Normalmente, eles expiram depois de cerca de 10 minutos. |
| state |Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos. |

Respostas de erro também podem ser enviadas toohello `redirect_uri` parâmetro para que o aplicativo hello possa tratá-los adequadamente:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de caracteres de código de erro que pode ser usado tooclassify tipos de erros que ocorrem e que pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| state |Consulte a descrição completa Olá na primeira tabela Olá nesta seção. Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos. |

## <a name="validate-hello-id-token"></a>Validar o token de ID de saudação
Receber apenas um token de ID não é suficiente tooauthenticate hello. Você deve validar a assinatura do token de ID hello e verificar Olá declarações no token Olá por requisitos do seu aplicativo. B2C do Azure AD usa [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e público tokens de toosign de criptografia de chave e verificar se eles são válidos.

Há muitas bibliotecas de software livre para validar JWTs dependendo do idioma de preferência. Recomendamos que você explore essas opções em vez de implementar a sua própria lógica de validação. informações de saudação aqui serão úteis para descobrir como tooproperly usar essas bibliotecas.

B2C do AD do Azure tem uma extremidade de metadados OpenID Connect, que permite que o aplicativo toofetch informações sobre o Azure AD B2C em tempo de execução. Essas informações incluem pontos de extremidade, conteúdos de token e chaves de assinatura de token. Há um documento de metadados JSON para cada política no seu locatário de B2C. Por exemplo, o documento de metadados Olá para Olá `b2c_1_sign_in` política no `fabrikamb2c.onmicrosoft.com` está localizado em:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Uma das propriedades de saudação deste documento de configuração é `jwks_uri`, cujo valor Olá mesma diretiva seria:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine a diretiva que foi usada em um token de ID de assinatura (e de onde toofetch Olá metadados), você tem duas opções. Primeiro, o nome da política hello está incluído no hello `acr` declaração no token de ID de saudação. Para obter informações sobre como tooparse Olá declarações de um token de ID, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). A outra opção é a política de saudação tooencode no valor Olá Olá `state` parâmetro quando você emite a solicitação de saudação e decodificá-la toodetermine qual política foi usada. Ambos os métodos são válidos.

Depois que tiver adquirido o documento de metadados de saudação do ponto de extremidade de metadados de OpenID Connect hello, você pode usar as chaves públicas de saudação RSA 256 (que estão localizadas nesse ponto de extremidade) toovalidate assinatura de saudação do token de ID de saudação. Poderá haver várias chaves listadas nesse ponto de extremidade em qualquer ponto no tempo, cada uma identificada por uma declaração `kid`. Olá cabeçalho do token de ID de saudação também contém um `kid` de declaração, que indica que essas chaves foi token de ID de saudação toosign usado. Para obter mais informações, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md) (Olá seção em [Validando tokens](active-directory-b2c-reference-tokens.md#token-validation), em particular).
<!--TODO: Improve hello information on this-->

Depois que tiver validado assinatura de saudação do token de ID hello, há várias declarações que você precisa tooverify. Por exemplo:

* Você deve validar Olá `nonce` tooprevent ataques de reprodução de token de declaração. Seu valor deve ser especificado na solicitação de entrada hello.
* Você deve validar Olá `aud` declaração tooensure que Olá token de ID foi emitido para seu aplicativo. Seu valor deve ser o ID do aplicativo de saudação do seu aplicativo.
* Você deve validar Olá `iat` e `exp` declarações tooensure que Olá token de ID não expirou.

Também há várias outras validações que devem ser realizadas. Elas são descritas detalhadamente no hello [OpenID conectar Core especificação](http://openid.net/specs/openid-connect-core-1_0.html).  Você também poderá toovalidate de declarações adicionais, dependendo do cenário. Algumas validações comuns incluem:

* Garantir que Olá/organização do usuário tiver se inscrito para o aplicativo hello.
* Garantir que o usuário Olá tenha autorização/privilégios apropriados.
* A garantia de que uma determinada intensidade de autenticação tenha ocorrido, como o Azure Multi-Factor Authentication.

Para obter mais informações sobre declarações de saudação em um token de ID, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md).

Após validar o token de ID hello, pode iniciar uma sessão de usuário hello. Você pode usar declarações de saudação nas informações de token tooobtain ID Olá sobre usuário Olá em seu aplicativo. Os usos para essas informações incluem exibição, registros e autorização.

## <a name="get-a-token"></a>Obter um token
Se você precisar de sua tooonly de aplicativo web executar políticas, você pode ignorar Olá próximas seções. Essas seções são aplicativos de tooweb somente aplicável que precisam de API da web do toomake autenticado chamadas tooa e também são protegidos pelo Azure AD B2C.

Você pode resgatar o código de autorização de saudação que você adquiriu (usando `response_type=code+id_token`) para um token toohello desejado recurso enviando um `POST` solicitação toohello `/token` ponto de extremidade. Atualmente, hello somente os recursos que você pode solicitar um token é sua API de web de back-end do aplicativo. convenção de saudação para solicitar um token tooyourself é toouse a ID de cliente do aplicativo como escopo de saudação:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| p |Obrigatório |Olá política que foi usado tooacquire Olá autorização código. Você não poderá usar uma política diferente nessa solicitação. Observe que você adicionar essa cadeia de caracteres de consulta do parâmetro toohello, não toohello `POST` corpo. |
| client_id |Obrigatório |aplicativo Hello ID que Olá [portal do Azure](https://portal.azure.com/) atribuído tooyour aplicativo. |
| grant_type |Obrigatório |Olá tipo de concessão, que deve ser `authorization_code` para fluxo de código de autorização de saudação. |
| scope |Recomendadas |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure AD ambas as permissões que estão sendo solicitados. Olá `openid` escopo indica um toosign permissão nos dados de usuário e get hello sobre usuário Olá na forma de saudação de id_token parâmetros. Ele pode ser usado tooget tokens tooyour do aplicativo back-end API da web, que é representado por Olá mesma identificação de aplicativo cliente hello. Olá `offline_access` escopo indica que seu aplicativo precisará de um token de atualização para tooresources de acesso e longa duração. |
| código |Obrigatório |código de autorização de saudação que você copiou no trecho primeiro de saudação do fluxo de saudação. |
| redirect_uri |Obrigatório |Olá `redirect_uri` parâmetro do aplicativo hello em que você recebeu o código de autorização de saudação. |
| client_secret |Obrigatório |segredo do aplicativo Hello geradas no hello [portal do Azure](https://portal.azure.com/). O segredo do aplicativo é um artefato de segurança importante. Você deve armazená-lo com segurança no servidor. Você também deve circular esse segredo do cliente em intervalos periódicos. |

Uma resposta de token bem-sucedida tem a seguinte aparência:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parâmetro | Descrição |
| --- | --- |
| not_before |tempo de saudação no qual Olá token é considerado válido, em vez de época. |
| token_type |valor de tipo de token de saudação. Olá somente tipo de AD do Azure oferece suporte a `Bearer`. |
| access_token |Olá assinou o token JWT que você solicitou. |
| scope |escopos de saudação para o qual Olá token é válido. Eles podem ser usados para o cache de tokens para uso posterior. |
| expires_in |Olá período de tempo que Olá token de acesso é válido (em segundos). |
| refresh_token |Um token de atualização do OAuth 2.0. Olá aplicativo pode usar este tokens adicionais do token tooacquire após Olá atual expire. Atualizar tokens são de vida longa e pode ser usado tooretain acesso tooresources por longos períodos de tempo. Para obter mais detalhes, consulte toohello [referência de token B2C](active-directory-b2c-reference-tokens.md). Observe que você deve ter usado o escopo de saudação `offline_access` no token e de autorização de saudação solicitações em ordem tooreceive um token de atualização. |

As respostas de erro se parecem com:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de caracteres de código de erro que pode ser usado tooclassify tipos de erros que ocorrem e que pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

## <a name="use-hello-token"></a>Use o token de saudação
Agora que você tenha adquirido com êxito um token de acesso, você pode usar o token Olá em APIs da web do back-end solicitações tooyour, incluí-lo no hello `Authorization` cabeçalho:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Olá token de atualização
Os tokens de ID têm vida curta. Você deve atualizá-los depois que elas expirarem toocontinue sendo tooaccess capaz de recursos. Você pode fazer isso enviando outra `POST` solicitação toohello `/token` ponto de extremidade. Desta vez, fornecer Olá `refresh_token` parâmetro em vez da saudação `code` parâmetro:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Parâmetro | Obrigatório | Descrição |
| --- | --- | --- |
| p |Obrigatório |Olá política de token de atualização original Olá tooacquire usado. Você não poderá usar uma política diferente nessa solicitação. Observe que você adicionar essa cadeia de caracteres de consulta do parâmetro toohello, o corpo do POST não toohello. |
| client_id |Obrigatório |aplicativo Hello ID que Olá [portal do Azure](https://portal.azure.com/) atribuído tooyour aplicativo. |
| grant_type |Obrigatório |tipo de saudação de concessão, que deve ser um token de atualização para este segmento do fluxo de código de autorização de saudação. |
| scope |Recomendadas |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure AD ambas as permissões que estão sendo solicitados. Olá `openid` escopo indica um toosign permissão nos dados de usuário e get hello sobre usuário Olá na forma de saudação de tokens de ID. Ele pode ser usado tooget tokens tooyour do aplicativo back-end API da web, que é representado por Olá mesma identificação de aplicativo cliente hello. Olá `offline_access` escopo indica que seu aplicativo precisará de um token de atualização para tooresources de acesso e longa duração. |
| redirect_uri |Recomendadas |Olá `redirect_uri` parâmetro do aplicativo hello em que você recebeu o código de autorização de saudação. |
| refresh_token |Obrigatório |Olá original token de atualização que você copiou no trecho de segundo de saudação do fluxo de saudação. Observe que você deve ter usado o escopo de saudação `offline_access` no token e de autorização de saudação solicitações em ordem tooreceive um token de atualização. |
| client_secret |Obrigatório |segredo do aplicativo Hello geradas no hello [portal do Azure](https://portal.azure.com/). O segredo do aplicativo é um artefato de segurança importante. Você deve armazená-lo com segurança no servidor. Você também deve circular esse segredo do cliente em intervalos periódicos. |

Uma resposta de token bem-sucedida tem a seguinte aparência:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parâmetro | Descrição |
| --- | --- |
| not_before |tempo de saudação no qual Olá token é considerado válido, em vez de época. |
| token_type |valor de tipo de token de saudação. Olá somente tipo de AD do Azure oferece suporte a `Bearer`. |
| access_token |Olá assinou o token JWT que você solicitou. |
| scope |escopo de Olá Olá token é válido, que pode ser usado para armazenar em cache os tokens para uso posterior. |
| expires_in |Olá período de tempo que Olá token de acesso é válido (em segundos). |
| refresh_token |Um token de atualização do OAuth 2.0. Olá aplicativo pode usar este tokens adicionais do token tooacquire após Olá atual expire.  Atualizar tokens são de vida longa e pode ser usado tooretain acesso tooresources por longos períodos de tempo. Para obter mais detalhes, consulte toohello [referência de token B2C](active-directory-b2c-reference-tokens.md). |

As respostas de erro se parecem com:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de caracteres de código de erro que pode ser usado tooclassify tipos de erros que ocorrem e que pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |

## <a name="send-a-sign-out-request"></a>Enviar uma solicitação de saída
Quando você desejar toosign Olá usuário fora do aplicativo hello, é insuficiente tooclear cookies do seu aplicativo ou caso contrário, encerrar a sessão de saudação com usuário hello. Você também deve redirecionar Olá usuário tooAzure AD toosign-out. Se você não toodo, portanto, o usuário Olá pode ser capaz de tooreauthenticate tooyour aplicativo sem inserir suas credenciais novamente. Isso ocorre porque eles terão uma sessão de logon único válida com o Azure AD.

Você pode redirecionar simplesmente Olá usuário toohello `end_session` ponto de extremidade que está listado no documento de metadados de OpenID Connect Olá descrito anteriormente hello "Validar o token de ID hello" seção:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| p |Obrigatório |política de saudação que você deseja o usuário de saudação do toouse toosign fora do seu aplicativo. |
| post_logout_redirect_uri |Recomendadas |Olá URL que o usuário Olá deve ser redirecionado tooafter bem-sucedida logout. Se não for incluída, o Azure AD B2C mostra usuário Olá uma mensagem genérica. |

> [!NOTE]
> Embora direcionando Olá usuário toohello `end_session` ponto de extremidade removerá alguns saudação do único logon de estado do usuário com o Azure AD B2C, ele não se conectará usuário Olá fora de sua sessão de IDP (provedor) da identidade de redes sociais. Se o usuário Olá seleciona Olá IDP mesmo durante uma entrada subsequente, eles serão ser reautenticados, sem inserir suas credenciais. Se um usuário quiser toosign fora do seu aplicativo B2C, ele não significa necessariamente que desejam toosign fora da sua conta do Facebook. No entanto, no caso de saudação de contas locais, sessão de saudação do usuário será finalizada corretamente.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Usar seu próprio locatário B2C
Se você quiser tootry essas solicitações por conta própria, deve primeiro executar estas três etapas e, em seguida, substituir valores de exemplo hello descritos anteriormente com seu próprio:

1. [Criar um locatário B2C](active-directory-b2c-get-started.md)e usar o nome de saudação do seu locatário em solicitações de saudação.
2. [Criar um aplicativo](active-directory-b2c-app-registration.md) tooobtain uma ID de aplicativo. Inclui um aplicativo Web/uma API Web em seu aplicativo. Opcionalmente, criar um segredo do aplicativo.
3. [Criar suas diretivas](active-directory-b2c-reference-policies.md) tooobtain seus nomes de política.

