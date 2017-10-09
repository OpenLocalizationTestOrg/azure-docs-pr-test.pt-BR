---
title: "Fluxo de código de autorização – Azure AD B2C | Microsoft Docs"
description: "Saiba como toobuild aplicativos web usando o protocolo de autenticação do Azure AD B2C e OpenID Connect."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: fluxo de código de autorização OAuth 2.0
Você pode usar o hello OAuth 2.0 concessão de código de autorização em aplicativos instalados em um dispositivo toogain acessar tooprotected recursos, como APIs da web. Usando a implementação do hello Azure Active Directory B2C (Azure AD B2C) do OAuth 2.0, você pode adicionar a inscrição, entrar e outro gerenciamento de identidade tarefas tooyour aplicativos de desktop e móveis. Este artigo é independente de linguagem. Artigo hello, descreveremos como toosend e receber mensagens HTTP sem usar as bibliotecas de código-fonte aberto.

<!-- TODO: Need link toolibraries -->

Olá fluxo de código de autorização do OAuth 2.0 é descrita em [seção 4.1 da especificação de saudação OAuth 2.0](http://tools.ietf.org/html/rfc6749). Você pode usá-lo para autenticação e autorização na maioria dos tipos de aplicativo, incluindo [aplicativos Web](active-directory-b2c-apps.md#web-apps) e [aplicativos instalados nativamente](active-directory-b2c-apps.md#mobile-and-native-apps). Você pode usar o hello adquirir toosecurely de fluxo de código de autorização do OAuth 2.0 *tokens de acesso* para seus aplicativos, que pode ser usado tooaccess recursos que são protegidos por um [servidor de autorização](active-directory-b2c-reference-protocols.md#the-basics).

Este artigo enfoca Olá **clientes públicos** fluxo de código de autorização do OAuth 2.0. Um cliente público é qualquer aplicativo cliente que não pode ser confiável toosecurely manter a integridade de saudação de uma senha secreta. Isso inclui aplicativos móveis, aplicativos de desktop e essencialmente qualquer aplicativo que é executado em um dispositivo e precisa tooget tokens de acesso. 

> [!NOTE]
> aplicativo de web de tooa tooadd identity management usando o Azure AD B2C, use [OpenID Connect](active-directory-b2c-reference-oidc.md) em vez do OAuth 2.0.

B2C do AD do Azure estende padrão Olá que OAuth 2.0 flui toodo mais de autorização e autenticação simples. Ele apresenta Olá [parâmetro política](active-directory-b2c-reference-policies.md). Com as políticas internas, você pode usar o OAuth 2.0 experiências de usuário tooadd tooyour aplicativo, como se inscrever, entrar e gerenciamento de perfil. Neste artigo, mostramos como toouse tooimplement OAuth 2.0 e políticas de cada uma dessas experiências em seus aplicativos nativos. Também mostramos como APIs da web de tooget tokens de acesso para acessar.

Em solicitações HTTP do exemplo hello neste artigo, podemos usar o diretório do Azure AD B2C nosso exemplo, **fabrikamb2c.onmicrosoft.com**. Também usamos nosso aplicativo de exemplo e políticas. Você pode tentar Olá solicitações usando esses valores, ou você pode substituí-los com seus próprios valores.
Saiba como muito[obter seu próprio diretório Azure AD B2C, aplicativos e políticas](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Obter um código de autorização
fluxo de código de autorização Olá começa com o cliente Olá direcionando Olá usuário toohello `/authorize` ponto de extremidade. Isso faz parte de interativo de saudação do fluxo de Olá, onde o usuário Olá age. Nessa solicitação, o cliente Olá indica em Olá `scope` permissões de saudação de parâmetro que precisa de tooacquire de usuário de saudação. Em Olá `p` parâmetro indica Olá política tooexecute. Olá, três exemplos a seguir (com quebras de linha para facilitar a leitura) cada usam uma política diferente.

### <a name="use-a-sign-in-policy"></a>Usar uma política de entrada
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Usar uma política de inscrição
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Usar uma política de edição de perfil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| client_id |Obrigatório |ID do aplicativo Hello atribuído tooyour aplicativo hello [portal do Azure](https://portal.azure.com). |
| response_type |Obrigatório |tipo de resposta Hello, que deve incluir `code` para fluxo de código de autorização de saudação. |
| redirect_uri |Obrigatório |Olá redirecione o URI do aplicativo, onde as respostas de autenticação são enviadas e recebidas pelo seu aplicativo. Ele deve corresponder exatamente a um de redirecionamento Olá URIs registrados no portal de hello, exceto que ele deve ser codificado de URL. |
| scope |Obrigatório |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure do Active Directory (AD do Azure) ambas as permissões de saudação que estão sendo solicitados. Usando o cliente Olá ID como escopo Olá indica que seu aplicativo precisa de um token de acesso que pode ser usado em seu próprio serviço ou a API da web, representada pela Olá a mesma ID de cliente.  Olá `offline_access` escopo indica que seu aplicativo precisa de um token de atualização para tooresources de acesso e longa duração. Você também pode usar Olá `openid` escopo toorequest um token de ID do Azure AD B2C. |
| response_mode |Recomendadas |método Hello que você use tooyour back toosend Olá resultante autorização código aplicativo. Pode ser `query`, `form_post` ou `fragment`. |
| state |Recomendadas |Um valor incluído na solicitação de saudação que é retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo que você deseja toouse. Normalmente, é usado um valor exclusivo gerado aleatoriamente, tooprevent ataques de falsificação de solicitação entre sites. estado de Olá também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação Olá ocorreu. Por exemplo, usuário de saudação de página Olá na ou Olá política que estava sendo executada. |
| p |Obrigatório |política de saudação que é executada. Seu Olá nome de uma política que é criada no diretório do Azure AD B2C. valor de nome de política Olá deve começar com **b2c\_1\_**. toolearn mais sobre políticas, consulte [políticas internas do Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Opcional |tipo de saudação de interação do usuário é necessária. Atualmente, a saudação único valor válido é `login`, que força Olá usuário tooenter suas credenciais na solicitação. O logon único não terá efeito. |

Neste ponto, o usuário de Olá é solicitado fluxo de trabalho da política do toocomplete hello. Isso pode envolver usuário Olá inserir seu nome de usuário e senha, entrar com uma identidade de redes sociais, inscrever directory hello, ou qualquer outro número de etapas. Ações de usuário dependem de como a política de saudação é definida.

Após usuário Olá política hello, o AD do Azure retorna um aplicativo de tooyour de resposta no valor Olá usado para `redirect_uri`. Ele usa o método hello especificado no hello `response_mode` parâmetro. resposta de saudação é exatamente hello mesmo para cada um dos cenários de ação usuário hello, independentes da política de saudação que foi executada.

Uma resposta bem-sucedida que usa `response_mode=query` tem esta aparência:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parâmetro | Descrição |
| --- | --- |
| código |código de autorização Olá Olá aplicativo solicitado. saudação de aplicativo pode usar toorequest código de autorização Olá um token de acesso para um recurso de destino. Os códigos de autorização têm uma duração muito curta. Normalmente, eles expiram depois de cerca de 10 minutos. |
| state |Consulte a descrição completa Olá na tabela Olá Olá anterior de seção. Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos. |

Respostas de erro também podem ser enviadas toohello URI de redirecionamento para que hello aplicativo possa tratá-los adequadamente:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que você pode usar tooclassify Olá tipos de erros que ocorrem. Você também pode usar Olá tooerrors de tooreact de cadeia de caracteres. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| state |Consulte a descrição completa Olá no hello anterior da tabela. Se um `state` parâmetro está incluído na solicitação de saudação hello mesmo valor deve aparecer na resposta de saudação. Olá aplicativo deve verificar que Olá `state` valores hello solicitação e resposta são idênticos. |

## <a name="2-get-a-token"></a>2. Obter um token
Agora que você tiver adquirido um código de autorização, você pode resgatar Olá `code` para um token toohello se destina a recursos, enviando um toohello de solicitação POST `/token` ponto de extremidade. No Azure AD B2C, hello somente os recursos que você pode solicitar um token é sua API de web de back-end do aplicativo. convenção de saudação que é usada para solicitar um token tooyourself é toouse a ID de cliente do aplicativo como escopo de saudação:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| p |Obrigatório |Olá política que foi usado tooacquire Olá autorização código. Você não poderá usar uma política diferente nessa solicitação. Observe que você adicionar esse parâmetro toohello *cadeia de caracteres de consulta*, mas não em Olá corpo da POSTAGEM. |
| client_id |Obrigatório |ID do aplicativo Hello atribuído tooyour aplicativo hello [portal do Azure](https://portal.azure.com). |
| grant_type |Obrigatório |tipo de saudação de concessão. Para o fluxo de código de autorização hello, tipo de concessão Olá deve ser `authorization_code`. |
| scope |Recomendadas |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure AD ambas as permissões de saudação que estão sendo solicitados. Usando o cliente Olá ID como escopo Olá indica que seu aplicativo precisa de um token de acesso que pode ser usado em seu próprio serviço ou a API da web, representada pela Olá a mesma ID de cliente.  Olá `offline_access` escopo indica que seu aplicativo precisa de um token de atualização para tooresources de acesso e longa duração.  Você também pode usar Olá `openid` escopo toorequest um token de ID do Azure AD B2C. |
| código |Obrigatório |código de autorização de saudação que você copiou no trecho primeiro de saudação do fluxo de saudação. |
| redirect_uri |Obrigatório |Olá redirecione o URI do aplicativo hello em que você recebeu o código de autorização de saudação. |

Uma resposta de token bem-sucedido tem esta aparência:

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
| token_type |valor de tipo de token de saudação. Olá digite somente do AD do Azure suporta é portador. |
| access_token |Olá assinado JSON Web Token (JWT) que você solicitou. |
| scope |escopos de Olá Olá token é válido para. Você também pode usar os tokens de toocache escopos para uso posterior. |
| expires_in |Olá período de tempo que Olá token é válido (em segundos). |
| refresh_token |Um token de atualização do OAuth 2.0. Olá aplicativo pode usar este tokens adicionais do token tooacquire após Olá atual expire. Os tokens de atualização têm uma vida longa. Você pode usá-los tooretain acesso tooresources por longos períodos de tempo. Para obter mais informações, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). |

As respostas de erro tem esta aparência:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que você pode usar tooclassify Olá tipos de erros que ocorrem. Você também pode usar Olá tooerrors de tooreact de cadeia de caracteres. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |

## <a name="3-use-hello-token"></a>3. Use o token de saudação
Agora que você tenha adquirido com êxito um token de acesso, você pode usar o token Olá em APIs da web do back-end solicitações tooyour, incluí-lo no hello `Authorization` cabeçalho:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Olá token de atualização
Os tokens de acesso e os tokens de ID tem curta duração. Depois de ele expirarem, você deve atualizá-los toocontinue tooaccess recursos. toodo isso, envie outro toohello de solicitação POST `/token` ponto de extremidade. Desta vez, fornecer Olá `refresh_token` em vez da saudação `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Parâmetro | Obrigatório? | Descrição |
| --- | --- | --- |
| p |Obrigatório |Olá política de token de atualização original Olá tooacquire usado. Você não poderá usar uma política diferente nessa solicitação. Observe que você adicionar esse parâmetro toohello *cadeia de caracteres de consulta*, mas não em Olá corpo da POSTAGEM. |
| client_id |Recomendadas |ID do aplicativo Hello atribuído tooyour aplicativo hello [portal do Azure](https://portal.azure.com). |
| grant_type |Obrigatório |tipo de saudação de concessão. Para este segmento do fluxo de código de autorização hello, tipo de concessão Olá deve ser `refresh_token`. |
| scope |Recomendadas |Uma lista de escopos separados por espaços. Um valor único escopo indica tooAzure AD ambas as permissões de saudação que estão sendo solicitados. Usando o cliente Olá ID como escopo Olá indica que seu aplicativo precisa de um token de acesso que pode ser usado em seu próprio serviço ou a API da web, representada pela Olá a mesma ID de cliente.  Olá `offline_access` escopo indica que seu aplicativo precisará de um token de atualização para tooresources de acesso e longa duração.  Você também pode usar Olá `openid` escopo toorequest um token de ID do Azure AD B2C. |
| redirect_uri |Opcional |Olá redirecione o URI do aplicativo hello em que você recebeu o código de autorização de saudação. |
| refresh_token |Obrigatório |Olá original token de atualização que você copiou no trecho de segundo de saudação do fluxo de saudação. |

Uma resposta de token bem-sucedido tem esta aparência:

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
| token_type |valor de tipo de token de saudação. Olá digite somente do AD do Azure suporta é portador. |
| access_token |Olá assinado JWT que você solicitou. |
| scope |escopos de Olá Olá token é válido para. Você também pode usar os tokens de toocache Olá escopos para uso posterior. |
| expires_in |Olá período de tempo que Olá token é válido (em segundos). |
| refresh_token |Um token de atualização do OAuth 2.0. Olá aplicativo pode usar este tokens adicionais do token tooacquire após Olá atual expire. Atualizar tokens são de vida longa e pode ser usado tooretain acesso tooresources por longos períodos de tempo. Para obter mais informações, consulte Olá [referência de token do Azure AD B2C](active-directory-b2c-reference-tokens.md). |

As respostas de erro tem esta aparência:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que você pode usar tooclassify tipos de erros que ocorrem. Você também pode usar Olá tooerrors de tooreact de cadeia de caracteres. |
| error_description |Uma mensagem de erro específicas que pode ajudar a identificar a causa de saudação de um erro de autenticação. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Use seu próprio diretório do Azure AD B2C
tootry essas solicitações por conta própria, Olá completo seguindo as etapas. Substitua os valores de exemplo hello que usamos neste artigo com seus próprios valores.

1. [Criar um diretório do Azure AD B2C](active-directory-b2c-get-started.md). Use o nome do seu diretório em solicitações de saudação hello.
2. [Criar um aplicativo](active-directory-b2c-app-registration.md) tooobtain uma ID de aplicativo e um URI de redirecionamento. Inclua um cliente nativo em seu aplicativo.
3. [Criar suas diretivas](active-directory-b2c-reference-policies.md) tooobtain seus nomes de política.

