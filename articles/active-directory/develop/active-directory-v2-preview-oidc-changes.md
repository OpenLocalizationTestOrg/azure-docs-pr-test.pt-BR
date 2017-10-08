---
title: ponto de extremidade do aaaChanges toohello AD do Azure v 2.0 | Microsoft Docs
description: "Uma descrição das alterações que estão sendo feitas protocolos de visualização pública toohello aplicativo modelo v 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>V 2.0 de toohello importantes atualizações protocolos de autenticação
Atenção, desenvolvedores! Sobre Olá próximas duas semanas, realizaremos atualizações alguns protocolos de autenticação do tooour v 2.0 que podem significar últimas alterações para todos os aplicativos que foram gravadas durante o período de nossa visualização.  

## <a name="who-does-this-affect"></a>A quem isso afeta?
Todos os aplicativos que foram gravados v 2.0 do toouse Olá convergida ponto de extremidade de autenticação

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Obter mais informações sobre o ponto de extremidade do hello v 2.0 podem ser encontradas [aqui](active-directory-appmodel-v2-overview.md).

Se você criou um aplicativo usando o ponto de extremidade do hello v 2.0 codificando diretamente toohello v 2.0 protocol usando qualquer um dos nossos middlewares web OpenID Connect ou OAuth ou usando outros 3ª parte bibliotecas tooperform a autenticação, você deve estar preparado tootest seus projetos e verifique alterações necessárias.

## <a name="who-doesnt-this-affect"></a>A quem isso não afeta?
Todos os aplicativos que foram gravados em relação a saudação produção AD do Azure do ponto de extremidade,

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Esse protocolo é imutável e não terá qualquer alteração.

Além disso, se seu aplicativo **somente** usa a autenticação de tooperform nossa biblioteca ADAL, você não terá toochange nada.  ADAL tem blindado seu aplicativo de alterações de saudação.  

## <a name="what-are-hello-changes"></a>Quais são as alterações de Olá?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Removendo o valor de x5t Olá dos cabeçalhos JWT
o ponto de extremidade do Hello v 2.0 usa tokens JWT extensivamente, que contém uma seção de parâmetros de cabeçalho com metadados relevantes sobre token de saudação.  Se decodificar o cabeçalho de saudação de um dos nossos JWTs atuais, você deve encontrar algo como:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Onde ambas as propriedades de "x5t" e "kid" hello identificam a chave pública de saudação que deve ser assinatura do token de saudação toovalidate usado, conforme recuperados do ponto de extremidade de metadados de OpenID Connect hello.

alteração de saudação que estamos fazendo aqui é propriedade de hello "x5t" de tooremove.  Você pode continuar toouse Olá mesmo toovalidate de mecanismos de tokens, mas deve depender somente hello "kid" propriedade tooretrieve Olá chave pública correta, como especificado em Olá protocolo OpenID Connect. 

> [!IMPORTANT]
> **O trabalho: Verifique se seu aplicativo não depende da existência de saudação do valor de x5t hello.**
> 
> 

### <a name="removing-profileinfo"></a>Remover profile_info
Anteriormente, o ponto de extremidade do hello v 2.0 tem foi retornar um objeto JSON codificado na base64 em respostas de token chamadas `profile_info`.  Ao solicitar um token de acesso do ponto de extremidade do hello v 2.0 enviando uma solicitação para:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

resposta de saudação seria Olá objeto JSON a seguir:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Olá `profile_info` informações de valor contido sobre o usuário de saudação que assinou o aplicativo hello - seu nome de exibição, nome, sobrenome, endereço de email, identificador e assim por diante.  Primeiramente, Olá `profile_info` foi usado para o cache de token e fins de exibição.

Agora estamos removendo Olá `profile_info` valor – mas não se preocupe, ainda estamos fornecendo essa toodevelopers informações em um local ligeiramente diferente.  Em vez de `profile_info`, o ponto de extremidade do hello v 2.0 agora irá retornar um `id_token` em cada resposta do token:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Você pode decodificar e analisar Olá id_token tooretrieve Olá mesmas informações que você recebeu do profile_info.  Olá id_token é um JSON Web Token (JWT), com conteúdo conforme especificado pelas OpenID Connect.  Olá código para fazer isso deve ser bem semelhante – basta intermediária de saudação tooextract segmento (corpo Olá) da saudação id_token e base64 decodificá-la tooaccess objeto JSON hello dentro.

Sobre Olá próximas duas semanas, você deve codificar as informações do usuário do aplicativo tooretrieve Olá de qualquer Olá `id_token` ou `profile_info`; o que está presente.  Dessa forma, quando Olá alteração é feita, seu aplicativo pode lidar com transição de saudação do `profile_info` muito`id_token` sem interrupções.

> [!IMPORTANT]
> **O trabalho: Verifique se seu aplicativo não depende da existência de saudação do hello `profile_info` valor.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Remover id_token_expires_in
Semelhante muito`profile_info`, também estamos removendo Olá `id_token_expires_in` parâmetro de respostas.  Anteriormente, o ponto de extremidade do hello v 2.0 retornaria um valor para `id_token_expires_in` junto com cada resposta id_token, por exemplo, em uma resposta de autorização:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

Ou em uma resposta do token:

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Olá `id_token_expires_in` valor indicaria Olá quantos segundos Olá id_token permanecerá válido para.  Agora, estamos removendo Olá `id_token_expires_in` valor completamente.  Em vez disso, você pode usar o padrão de OpenID Connect Olá `nbf` e `exp` tooexamine validade de saudação de um id_token de declarações.  Consulte Olá [referência de token v 2.0](active-directory-v2-tokens.md) para obter mais informações sobre essas declarações.

> [!IMPORTANT]
> **O trabalho: Verifique se seu aplicativo não depende da existência de saudação do hello `id_token_expires_in` valor.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Alterando declarações Olá retornadas pelo escopo = openid
Essa alteração será hello mais significativa – na verdade, isso afetará a quase todos os aplicativos que usa o ponto de extremidade do hello v 2.0.  Muitos aplicativos enviar solicitações toohello v 2.0 ponto de extremidade usando Olá `openid` escopo, como:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Hoje, quando o usuário de saudação concede permissão para Olá `openid` escopo, seu aplicativo recebe uma grande quantidade de informações sobre o usuário Olá Olá resultante id_token.  As declarações em um id_token podem incluir o nome, nome de usuário preferido, endereço de email, ID do objeto e mais.

Nesta atualização, nós estamos alterando as informações de saudação que Olá `openid` escopo permite ao aplicativo acesso aos toobetter comform com hello especificação OpenID Connect.  Olá `openid` escopo será somente que seu aplicativo toosign Olá usuário e recebe um identificador específico do aplicativo para o usuário Olá no hello `sub` Olá id_token de declaração.  Olá declarações em um id_token com apenas Olá `openid` escopo concedido será não possui informações pessoalmente identificáveis.  Os exemplos de declarações do id_token são:

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Se você quiser tooobtain informações de identificação pessoal (PII) sobre o usuário Olá no seu aplicativo, seu aplicativo precisará de permissões adicionais de toorequest de usuário de saudação.  Estamos introduzindo o suporte para dois novos escopos de especificação de OpenID Connect hello – hello `email` e `profile` escopos – que permitem toodo.

* Olá `email` escopo é muito simples – ele permite que o endereço de email principal do usuário seu aplicativo acesso toohello via Olá `email` Olá id_token de declaração.  Observe que Olá `email` declaração não sempre estarão presente em id_tokens – ele só será incluído se disponíveis no perfil do usuário Olá.
* Olá `profile` escopo dá seu tooall de acesso do aplicativo outras informações básicas sobre o usuário hello – seu nome, o nome do usuário preferencial, a ID de objeto e assim por diante.

Isso permite toocode seu aplicativo de forma mínima divulgação – você pode pedir Olá usuário apenas o conjunto de saudação de informações que seu aplicativo requer toodo seu trabalho.  Se você quiser toocontinue obtenção Olá o conjunto completo de informações do usuário que seu aplicativo está recebendo, você deve incluir todos os três escopos em suas solicitações de autorização:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Seu aplicativo pode começar a enviar Olá `email` e `profile` escopos imediatamente e o ponto de extremidade do hello v 2.0 aceitar esses dois escopos e começar solicitando permissões de usuários, conforme necessário.  No entanto, a saudação alterar na interpretação Olá Olá `openid` escopo não entrarão em vigor para algumas semanas.

> [!IMPORTANT]
> **O trabalho: Adicionar Olá `profile` e `email` escopos se seu aplicativo requer informações sobre o usuário hello.**  Observe que o ADAL incluirá essas duas permissões nas solicitações por padrão. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Removendo Olá emissor barra à direita.
Anteriormente, o valor de emissor Olá que aparece em tokens do ponto de extremidade do hello v 2.0 levou formulário Olá

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Onde Olá guid foi tenantId de saudação do locatário de saudação do AD do Azure que emitiu o token de saudação.  Com essas alterações, o valor de emissor Olá torna-se

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

em ambos os tokens em documento de descoberta de OpenID Connect hello.

> [!IMPORTANT]
> **O trabalho: Verifique se seu aplicativo aceita o valor de emissor Olá com e sem uma barra à direita durante a validação do emissor.**
> 
> 

## <a name="why-change"></a>Por que alterar?
a principal motivação Olá para introduzir essas alterações é toobe compatível com hello especificação padrão OpenID Connect.  Ao ser OpenID Connect compatíveis, esperamos toominimize diferenças entre a integração com serviços de identidade da Microsoft e com outros serviços de identidade no setor de saudação.  Queremos tooenable desenvolvedores toouse suas bibliotecas de autenticação de software livre favorito sem a necessidade de diferenças de Microsoft tooalter Olá bibliotecas tooaccommodate.

## <a name="what-can-you-do"></a>O que você pode fazer?
A partir de hoje, você pode começar a fazer todas as alterações de saudação descritas acima.  Você deve imediatamente:

1. **Remova qualquer dependência no hello `x5t` parâmetro de cabeçalho.**
2. **Tratar normalmente a transição de saudação do `profile_info` muito`id_token` em respostas de token.**
3. **Remova qualquer dependência no hello `id_token_expires_in` parâmetro de resposta.**
4. **Adicionar Olá `profile` e `email` escopos tooyour aplicativo se seu aplicativo precisa de informações de usuário básica.**
5. **Aceite os valores do emissor nos tokens com e sem uma barra à direita.**

Nosso [v 2.0 documentação do protocolo](active-directory-v2-protocols.md) já foi atualizado tooreflect essas alterações, portanto você pode usá-lo como referência ajudar a atualizar seu código.

Se você tiver outras perguntas no escopo de saudação das alterações de hello, sinta-se livre tooreach out toous no Twitter em @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Com que frequência as alterações do protocolo ocorrerão?
Não podemos prever qualquer mais recentes alterações toohello protocolos de autenticação.  Podemos intencionalmente agrupará essas alterações em uma versão para que você não terá toogo por meio desse tipo de processo de atualização novamente a qualquer momento em breve.  Obviamente, vamos continuar tooadd recursos toohello convergido v 2.0 serviço de autenticação que você pode tirar proveito do, mas essas alterações devem ser aditivo e não quebra código existente.

Por fim, esperamos que toosay Obrigado por experimentar as coisas durante o período de visualização hello.  insights Hello e experiências de nossos usuários iniciais foram inestimáveis até o momento e esperamos que você continue tooshare suas opiniões e ideias.

Boa codificação!

Olá divisão de identidade da Microsoft

