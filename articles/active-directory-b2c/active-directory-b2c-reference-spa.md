---
title: "Azure Active Directory B2C: Aplicativos de página única utilizando fluxo implícito | Microsoft Docs"
description: "Saiba como aplicativos de única página toobuild diretamente usando OAuth 2.0 implícita fluem com o Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C: Aplicativo de página única utilizando fluxo implícito do OAuth 2.0

> [!NOTE]
> Essa funcionalidade está em visualização.
> 

Muitos aplicativos modernos têm um aplicativo de página única front-end que é escrito principalmente em JavaScript. Muitas vezes, o aplicativo hello é gravado usando uma estrutura como AngularJS, Ember.js ou Durandal. Os aplicativos de página única e outros aplicativos JavaScript que são executados principalmente em um navegador possuem alguns desafios adicionais para autenticação:

* características de segurança Olá esses aplicativos são significativamente diferentes de aplicativos web tradicionais baseados em servidor.
* Muitos servidores de autorização e provedores de identidade não dão suporte para solicitações CORS (compartilhamento de recursos entre origens).
* Redirecionamentos de página inteira do navegador para fora do aplicativo hello podem ser significativamente invasivo toohello experiência do usuário.

toosupport esses aplicativos, o Azure Active Directory B2C (Azure AD B2C) usa o fluxo implícito Olá OAuth 2.0. fluxo de concessão implícita de autorização de saudação OAuth 2.0 é descrito em [seção 4.2 da especificação de saudação OAuth 2.0](http://tools.ietf.org/html/rfc6749). No fluxo implícito, o aplicativo hello recebe tokens diretamente de saudação do Azure Active Directory (AD do Azure) autorizar o ponto de extremidade, sem qualquer servidor para o servidor exchange. Todas as lógica de autenticação e a sessão tratamento leva coloque inteiramente no cliente de JavaScript hello, sem redirecionamentos de página adicionais.

B2C do AD do Azure estende toomore fluxo implícitos OAuth 2.0 de saudação padrão de autorização e autenticação simples. B2C do AD do Azure apresenta Olá [parâmetro política](active-directory-b2c-reference-policies.md). Com parâmetro de política hello, você pode usar o OAuth 2.0 experiências de usuário tooadd tooyour aplicativo, como se inscrever, entrar e gerenciamento de perfil. Neste artigo, mostramos como toouse Olá fluxo implícito e o AD do Azure tooimplement cada dessas experiências em seus aplicativos de única página. toohelp começar, dê uma olhada no nosso [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) e [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) exemplos.

Em solicitações HTTP do exemplo hello neste artigo, podemos usar o diretório do Azure AD B2C nosso exemplo, **fabrikamb2c.onmicrosoft.com**. Além disso, utilizamos nosso próprio aplicativo de exemplo e políticas. Você pode tentar Olá solicitações usando esses valores, ou você pode substituí-los com seus próprios valores.
Saiba como muito[obter seu próprio diretório Azure AD B2C, aplicativos e políticas](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Diagrama de protocolo

fluxo de entrada implícita Olá parecida com hello figura a seguir. Cada etapa é descrita em detalhes posteriormente neste artigo hello.

![Raias do OpenID Connect](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Enviar solicitações de autenticação
Quando seu aplicativo web precisa de usuário de saudação tooauthenticate e executar uma política, ele direciona Olá usuário toohello `/authorize` ponto de extremidade. Isso é parte interativa Olá fluxo Olá, qual usuário Olá agirão, dependendo da política de saudação. usuário Olá obtém uma ID de token do ponto de extremidade do hello AD do Azure.

Nessa solicitação, o cliente Olá indica em Olá `scope` permissões de saudação de parâmetro que precisa de tooacquire de usuário de saudação. Em Olá `p` parâmetro indica Olá política tooexecute. Olá, três exemplos a seguir (com quebras de linha para facilitar a leitura) cada usam uma política diferente. tooget uma ideia de como cada solicitação funciona, tente a solicitação de saudação de colá-lo em um navegador e executá-lo.

### <a name="use-a-sign-in-policy"></a>Usar uma política de entrada
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Usar uma política de inscrição
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Usar uma política de edição de perfil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| client_id |Obrigatório |ID do aplicativo Hello atribuído tooyour aplicativo hello [portal do Azure](https://portal.azure.com). |
| response_type |Obrigatório |Deve incluir `id_token` para conexão do OpenID Connect. Ele também pode incluir o tipo de resposta Olá `token`. Se você usar `token`, seu aplicativo pode receber imediatamente um token de acesso Olá autorizar o ponto de extremidade, sem fazer uma segunda toohello de solicitação a extremidade de autorização.  Se você usar o hello `token` tipo de resposta, Olá `scope` parâmetro deve conter um escopo que indica qual recurso tooissue Olá o token para. |
| redirect_uri |Recomendadas |Olá redirecione o URI do aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo. Ele deve corresponder exatamente a um de redirecionamento Olá URIs registrados no portal de hello, exceto que ele deve ser codificado de URL. |
| response_mode |Recomendadas |Especifica a saudação método toouse toosend Olá resultante token tooyour back aplicativo.  Para fluxos implícitos, utilize `fragment`. |
| scope |Obrigatório |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure AD ambas as permissões de saudação que estão sendo solicitados. Olá `openid` escopo indica um toosign permissão nos dados de usuário e get hello sobre usuário Olá na forma de saudação de tokens de ID. (Falaremos sobre isso mais posteriormente no artigo hello.) Olá `offline_access` escopo é opcional para aplicativos web. Indica que seu aplicativo precisa de um token de atualização para tooresources de acesso e longa duração. |
| state |Recomendadas |Um valor incluído na solicitação de saudação que também é retornado na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo que você deseja toouse. Normalmente, é usado um valor exclusivo gerado aleatoriamente, tooprevent ataques de falsificação de solicitação entre sites. Olá estado é também usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de ocorrer a solicitação de autenticação hello, como página Olá estivesse em. |
| nonce |Obrigatório |Um valor incluído na solicitação de saudação (gerada pelo aplicativo hello) que está incluída no token de ID resultante hello como uma declaração. aplicativo Hello, em seguida, pode verificar a que ataques de reprodução do token toomitigate esse valor. Geralmente, o valor de saudação é uma cadeia de caracteres aleatória e exclusiva que pode ser usado tooidentify Olá origem da solicitação de saudação. |
| p |Obrigatório |Olá tooexecute de política. Seu Olá nome de uma política que é criada no seu locatário do Azure AD B2C. valor de nome de política Olá deve começar com **b2c\_1\_**. Para obter mais informações, consulte [Políticas internas do Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Opcional |tipo de saudação de interação do usuário necessária. Atualmente, a saudação único valor válido é `login`. Isso força a saudação usuário tooenter suas credenciais na solicitação. O logon único não terá efeito. |

Neste ponto, o usuário de Olá é solicitado fluxo de trabalho da política do toocomplete hello. Isso pode envolver usuário Olá inserir seu nome de usuário e senha, entrar com uma identidade de redes sociais, inscrever directory hello, ou qualquer outro número de etapas. Ações de usuário dependem de como a política de saudação é definida.

Após usuário Olá política hello, o AD do Azure retorna um aplicativo de tooyour de resposta no valor Olá usado para `redirect_uri`. Ele usa o método hello especificado no hello `response_mode` parâmetro. resposta de saudação é exatamente hello mesmo para cada um dos cenários de ação usuário hello, independentes da política de saudação que foi executada.

### <a name="successful-response"></a>Resposta bem-sucedida
Uma resposta bem-sucedida usa `response_mode=fragment` e `response_type=id_token+token` aparência a seguir hello, quebras de linha para legibilidade:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Parâmetro | Descrição |
| --- | --- |
| access_token |token de acesso de Olá Olá aplicativo solicitado.  token de acesso de saudação não deve ser decodificada ou inspecionadas de outra forma. É possível tratá-lo como uma cadeia de caracteres opaca. |
| token_type |valor de tipo de token de saudação. Olá digite somente do AD do Azure suporta é portador. |
| expires_in |Olá período de tempo que Olá token de acesso é válido (em segundos). |
| scope |escopos de Olá Olá token é válido para. Você também pode usar os tokens de toocache escopos para uso posterior. |
| id_token |Olá token de ID que Olá aplicativo solicitado. Você pode usar a identidade do usuário do hello ID tooverify token hello e iniciar uma sessão de usuário de saudação. Para obter mais informações sobre tokens de ID e seu conteúdo, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| state |Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos. |

### <a name="error-response"></a>Resposta de erro
Respostas de erro também podem ser enviadas toohello URI de redirecionamento para que hello aplicativo possa tratá-los adequadamente:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de caracteres do código de erro usado tooclassify tipos de erros que ocorrem. Você também pode usar o código de erro Olá para tratamento de erros. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| state |Consulte a descrição completa Olá no hello anterior da tabela. Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos.|

## <a name="validate-hello-id-token"></a>Validar o token de ID de saudação
Receber um token de ID não é suficiente tooauthenticate hello. Você deve validar a assinatura do token de ID hello e verificar Olá declarações no token Olá por requisitos do seu aplicativo. B2C do Azure AD usa [JSON Web Tokens (JWTs)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e público tokens de toosign de criptografia de chave e verificar se eles são válidos.

Muitas bibliotecas de código-fonte estão disponíveis para validação JWTs, dependendo da linguagem Olá preferir toouse. Considere explorar bibliotecas de software livre disponíveis em vez de implementar sua própria lógica de validação. Você pode usar informações de saudação na toohelp neste artigo, você aprenderá como tooproperly usar essas bibliotecas.

O Azure AD B2C tem um ponto de extremidade de metadados OpenID Connect. Um aplicativo pode usar informações de toofetch de ponto de extremidade de saudação sobre o Azure AD B2C em tempo de execução. Essas informações incluem pontos de extremidade, conteúdos de token e chaves de assinatura de token. Há um documento de metadados JSON para cada política no locatário do Azure AD B2C. Por exemplo, o documento de metadados de Olá para política de b2c_1_sign_in Olá no locatário de fabrikamb2c.onmicrosoft.com hello está localizado em:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Uma das propriedades de saudação deste documento de configuração é hello `jwks_uri`. valor Olá Olá mesma diretiva seria:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine qual política foi toosign usado um token de ID (e onde toofetch Olá metadados do), você tem duas opções. Primeiro, o nome da política hello está incluído no hello `acr` de declaração em `id_token`. Para obter informações sobre como tooparse Olá declarações de um token de ID, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). A outra opção é a política de saudação tooencode no valor Olá Olá `state` parâmetro quando você emitir a solicitação de saudação. Em seguida, decodificar Olá `state` toodetermine parâmetro qual política foi usada. Ambos os métodos são válidos.

Depois que tiver adquirido o documento de metadados de saudação do ponto de extremidade de metadados de OpenID Connect hello, você pode usar o hello RSA-256 (localizadas neste ponto de extremidade) de chaves públicas toovalidate Olá assinatura de token de ID de saudação. Poderá haver várias chaves listadas nesse ponto de extremidade em qualquer momento, cada uma identificada por um `kid`. cabeçalho de saudação do `id_token` também contém um `kid` de declaração. Ele indica que essas chaves foi usado toosign token de ID de saudação. Para obter mais informações, incluindo o aprendizado sobre [Validando tokens](active-directory-b2c-reference-tokens.md#token-validation), consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Depois de validar a assinatura de saudação do token de ID de saudação, várias declarações exigem verificação. Por exemplo:

* Validar Olá `nonce` tooprevent ataques de reprodução de token de declaração. Seu valor deve ser especificado na solicitação de entrada hello.
* Validar Olá `aud` declaração tooensure que Olá token de ID foi emitido para seu aplicativo. Seu valor deve ser o ID do aplicativo de saudação do seu aplicativo.
* Validar Olá `iat` e `exp` declarações tooensure que Olá token de ID não expirou.

Vários validações mais que você deve executar são descritas em detalhes no hello [OpenID conectar Core especificação](http://openid.net/specs/openid-connect-core-1_0.html). Você também poderá toovalidate de declarações adicionais, dependendo do cenário. Algumas validações comuns incluem:

* Garantindo que usuário hello ou organização tiver se inscrito para o aplicativo hello.
* Garantir que o usuário Olá tem autorização adequada e os privilégios.
* Garanta que uma determina força de autenticação tenha ocorrido como, por exemplo, utilizando a autenticação multifator do Azure.

Para obter mais informações sobre declarações de saudação em um token de ID, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md).

Após validar completamente o token de ID Olá, você pode começar uma sessão com usuário hello. Em seu aplicativo use declarações de saudação nas informações de token tooobtain ID Olá sobre usuário hello. Essas informações podem ser usadas para exibição, registros, autorizações e outros.

## <a name="get-access-tokens"></a>Obter tokens de acesso
Se a única coisa que Olá seu toodo de necessidades de aplicativos da web é executar políticas, você pode ignorar Olá próximas seções. informações Olá Olá seções a seguir são aplicáveis somente tooweb nos aplicativos que precisam de API da web do toomake autenticado chamadas tooa, e que é protegido pelo Azure AD B2C.

Agora que você tenha assinado usuário Olá no aplicativo de página única tooyour, você pode obter tokens de acesso para chamar APIs da web que são protegidos pelo AD do Azure. Mesmo se você já recebeu um token usando Olá `token` tipo de resposta, você pode usar tokens de tooacquire este método para obter recursos adicionais sem redirecionando Olá usuário toosign em novamente.

Em um fluxo de aplicativo web típico, você faria isso fazendo uma solicitação toohello `/token` ponto de extremidade.  No entanto, o ponto de extremidade de saudação não não suporte a solicitações CORS, para fazer AJAX chama tooget e tokens de atualização não é uma opção. Em vez disso, você pode usar fluxo implícito Olá em um oculto HTML iframe elemento tooget novos tokens para outros APIs da web. A seguir está um exemplo, com quebras de linha para legibilidade:

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| client_id |Obrigatório |ID do aplicativo Hello atribuído tooyour aplicativo hello [portal do Azure](https://portal.azure.com). |
| response_type |Obrigatório |Deve incluir `id_token` para conexão do OpenID Connect.  Ele também pode incluir o tipo de resposta Olá `token`. Se você usar `token` aqui, seu aplicativo pode receber imediatamente um token de acesso de saudação autorizar o ponto de extremidade, sem fazer uma segunda toohello de solicitação a extremidade de autorização. Se você usar o hello `token` tipo de resposta, Olá `scope` parâmetro deve conter um escopo que indica qual recurso tooissue Olá o token para. |
| redirect_uri |Recomendadas |Olá redirecione o URI do aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo. Ele deve corresponder exatamente a um de redirecionamento Olá URIs registrados no portal de hello, exceto que ele deve ser codificado de URL. |
| scope |Obrigatório |Uma lista de escopos separados por espaços.  Para obter tokens, inclua todos os escopos que você precisa para o recurso de saudação que se destina. |
| response_mode |Recomendadas |Especifica o método de saudação que é usado toosend Olá resultante token tooyour back aplicativo.  Pode ser `query`, `form_post` ou `fragment`. |
| state |Recomendadas |Um valor incluído na solicitação de saudação que é retornada na resposta de token hello.  Pode ser uma cadeia de caracteres de qualquer conteúdo que você deseja toouse.  Normalmente, é usado um valor exclusivo gerado aleatoriamente, tooprevent ataques de falsificação de solicitação entre sites.  estado de Olá também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação Olá ocorreu. Por exemplo, do usuário Olá página ou exibição Olá foi em. |
| nonce |Obrigatório |Um valor incluído na solicitação hello, gerada pelo aplicativo hello, que está incluído no token de ID resultante hello como uma declaração.  aplicativo Hello, em seguida, pode verificar a que ataques de reprodução do token toomitigate esse valor. Geralmente, o valor de saudação é uma cadeia de caracteres aleatória exclusiva que identifica a origem de saudação da solicitação de saudação. |
| prompt |Obrigatório |use tokens toorefresh e get em um iframe oculto, `prompt=none` tooensure que Olá iframe não fique preso na página de entrada hello e retorna imediatamente. |
| login_hint |Obrigatório |tokens toorefresh e get em um iframe oculto, incluir nome de usuário de saudação do usuário Olá em toodistinguish essa dica entre várias sessões de usuário de saudação pode ter em um determinado momento. Você pode extrair Olá nome de usuário de uma entrada anterior usando Olá `preferred_username` de declaração. |
| domain_hint |Obrigatório |Pode ser `consumers` ou `organizations`.  Para atualizar e obter tokens em um iframe oculto, você deve incluir Olá `domain_hint` valor na solicitação de saudação.  Extrair Olá `tid` toouse qual valor de declaração de token de ID de saudação de um anteriormente entrar toodetermine.  Se hello `tid` é de valor de declaração `9188040d-6c67-4c5b-b112-36a304b66dad`, use `domain_hint=consumers`.  Caso contrário, use `domain_hint=organizations`. |

Por definição Olá `prompt=none` parâmetro, essa solicitação seja bem-sucedida ou falhará imediatamente e retorna tooyour aplicativo.  Uma resposta bem-sucedida é enviada tooyour aplicativo em Olá indicado redirecionar URI, usando o método hello especificado no hello `response_mode` parâmetro.

### <a name="successful-response"></a>Resposta bem-sucedida
Uma resposta bem-sucedida utilizando `response_mode=fragment` é semelhante à seguinte:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Parâmetro | Descrição |
| --- | --- |
| access_token |saudação de token que o aplicativo hello solicitado. |
| token_type |tipo de token Olá sempre será portador. |
| state |Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos. |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |
| scope |escopos Olá Olá token de acesso é válido para. |

### <a name="error-response"></a>Resposta de erro
Respostas de erro também podem ser enviadas toohello URI de redirecionamento para que hello aplicativo possa tratá-los corretamente.  Para `prompt=none`, um erro esperado é semelhante ao seguinte:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem. Você também pode usar Olá tooerrors de tooreact de cadeia de caracteres. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |

Se você receber esse erro na solicitação de iframe hello, Olá usuário deve interativamente entrar novamente tooretrieve um novo token. Você pode fazer isso de maneira que faça sentido para seu aplicativo.

## <a name="refresh-tokens"></a>Tokens de atualização
Os tokens de ID e tokens de acesso expiram após um curto período de tempo. Seu aplicativo deve estar preparado toorefresh esses tokens periodicamente.  Executar de qualquer tipo de token, toorefresh Olá mesma solicitação iframe oculto que foram usados no exemplo anterior, usando Olá `prompt=none` etapas do parâmetro toocontrol AD do Azure.  tooreceive um novo `id_token` valor, ser toouse se `response_type=id_token` e `scope=openid`e um `nonce` parâmetro.

## <a name="send-a-sign-out-request"></a>Enviar uma solicitação de saída
Quando você desejar toosign Olá usuário fora do aplicativo hello, redirecione Olá usuário tooAzure AD toosign-out. Se você não fizer isso, o usuário Olá pode ser capaz de tooreauthenticate tooyour aplicativo sem inserir suas credenciais novamente. Isso ocorre porque eles terão uma sessão de logon único válida com o Azure AD.

Você pode redirecionar simplesmente Olá usuário toohello `end_session_endpoint` que é listado na Olá mesmo documento de metadados do OpenID Connect descrito em [validar token de ID de saudação](#validate-the-id-token). Por exemplo:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| p |Obrigatório |usuário Olá política toouse toosign Olá fora do seu aplicativo. |
| post_logout_redirect_uri |Recomendadas |Olá URL que o usuário Olá deve ser redirecionado tooafter bem-sucedida logout. Se não for incluído, B2C do Azure AD exibirá um usuário de toohello mensagem genérica. |

> [!NOTE]
> Direcionando Olá usuário toohello `end_session_endpoint` limpa alguns saudação do único logon de estado do usuário com o Azure AD B2C. No entanto, ele não assinar o usuário Olá fora da sessão do provedor de identidade de redes sociais do usuário hello. Se o usuário Olá selecionará Olá mesmo identificar provedor durante uma entrada subsequente, usuário Olá seja autenticado novamente, sem inserir suas credenciais. Se um usuário quiser toosign fora do seu aplicativo do Azure AD B2C, ele não significa necessariamente que desejarem toocompletely sair da sua conta do Facebook, por exemplo. No entanto, para contas locais, sessão de saudação do usuário será finalizada corretamente.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Utilize seu próprio locatário do Azure AD B2C
tootry essas solicitações por conta própria, concluir Olá três etapas a seguir. Substitua os valores de exemplo hello que usamos neste artigo com seus próprios valores:

1. [Criar um locatário do Azure AD B2C](active-directory-b2c-get-started.md). Use o nome do seu locatário em solicitações Olá Olá.
2. [Criar um aplicativo](active-directory-b2c-app-registration.md) tooobtain uma ID de aplicativo e um `redirect_uri` valor. Inclua um aplicativo Web ou uma API Web em seu aplicativo. Opcionalmente, é possível criar um segredo de aplicativo.
3. [Criar suas diretivas](active-directory-b2c-reference-policies.md) tooobtain seus nomes de política.

## <a name="samples"></a>Exemplos

* [Criar um aplicativo de página única usando Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Criar um aplicativo de página única usando .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

