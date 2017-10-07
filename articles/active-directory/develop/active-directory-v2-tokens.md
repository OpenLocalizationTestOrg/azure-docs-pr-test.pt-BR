---
title: "referência de tokens de v 2.0 do Active Directory aaaAzure | Microsoft Docs"
description: "tipos de saudação de tokens e declarações emitidas pelo ponto de extremidade do hello AD do Azure v 2.0"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Referência de tokens do Azure Active Directory v2.0
o ponto de extremidade do Azure Active Directory (AD do Azure) v 2.0 Hello emite vários tipos de tokens de segurança em cada [fluxo de autenticação](active-directory-v2-flows.md). Esta referência descreve o formato de saudação, características de segurança e conteúdo de cada tipo de token.

> [!NOTE]
> o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure. toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Tipos de tokens
Olá ponto de extremidade v 2.0 dá suporte a saudação [protocolo de autorização do OAuth 2.0](active-directory-v2-protocols.md), que usa tokens de acesso e tokens de atualização. o ponto de extremidade do Hello v 2.0 também oferece suporte a autenticação e entrar via [OpenID Connect](active-directory-v2-protocols.md). OpenID Connect apresenta um terceiro tipo de token de ID do token, Olá. Cada um desses tokens é representado como um token de *portador*.

Um token de portador é o recurso protegido de um token de segurança leve que concede Olá tooa de acesso de portador. portador Olá é qualquer parte que pode apresentar um token de saudação. Embora uma parte deve ser autenticado com o token de portador de saudação do AD do Azure tooreceive, se etapas não são obtidas token de saudação toosecure durante a transmissão e o armazenamento, pode ser interceptado e usado por uma parte não pretendida. Alguns tokens de segurança têm partes de tooprevent não autorizado um mecanismo interno que usa-los, mas não de tokens de portador não. Os tokens de portador devem ser transportados em um canal seguro, como segurança da camada de transporte (HTTPS). Se um token de portador for transmitido sem esse tipo de segurança, um terceiro mal-intencionado pode usar um token de hello "ataque man-in-the-middle" tooacquire e usá-lo para o recurso de tooa protegido do acesso não autorizado. Olá mesmos princípios de segurança se aplicam ao armazenar ou armazenamento em cache os tokens de portador para uso posterior. Sempre verifique se o aplicativo transmite e armazena tokens de portador com segurança. Para obter mais considerações de segurança sobre tokens de portador, confira [RFC 6750 seção 5](http://tools.ietf.org/html/rfc6750).

Muitas das Olá tokens emitidos pelo ponto de extremidade do hello v 2.0 são implementadas como JSON Web Tokens (JWTs). Um JWT é uma informação de tootransfer de modo compacto, URL segura entre duas partes. informações de saudação em um JWT são chamadas um *declaração*. É uma asserção de informações sobre o portador hello e assunto do token de saudação. Olá declarações em um JWT são objetos de notação JSON (JavaScript Object) que são codificados e serializados para transmissão. Olá JWTs emitido por ponto de extremidade do hello v 2.0 são assinados, mas não criptografado, você pode facilmente inspecionar o conteúdo de saudação de um JWT para fins de depuração. Para obter mais informações sobre JWTs, consulte Olá [especificação do JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Tokens de ID
Um token de ID é uma forma de token de segurança de entrada que o aplicativo recebe quando ele executa a autenticação usando [OpenID Connect](active-directory-v2-protocols.md). Tokens de ID são representados como [JWTs](#types-of-tokens), e eles contêm declarações que você pode usar o usuário de saudação toosign no aplicativo tooyour. Você pode usar o hello declarações em um token de ID de várias maneiras. Normalmente, administradores usam informações de conta do ID tokens toodisplay ou toomake decisões de controle de acesso em um aplicativo. o ponto de extremidade do Hello v 2.0 emite apenas um tipo de token de ID, que tem um conjunto consistente de declarações, independentemente do tipo de saudação do usuário que está conectado. formato de saudação e o conteúdo dos tokens de ID são Olá mesmo para usuários de conta Microsoft pessoais e para contas corporativas ou de estudante.

Atualmente, os tokens de ID são assinados, mas não criptografados. Quando seu aplicativo recebe um token de ID, ele deverá [validar assinatura Olá](#validating-tokens) tooprove Olá autenticidade do token e validar algumas declarações em tooprove token Olá sua validade. Olá validadas por um aplicativo de declarações variam dependendo dos requisitos do cenário, mas seu aplicativo deve executar algumas [comuns validações de declaração](#validating-tokens) em cada cenário.

Nós lhe detalhes completos Olá declarações em tokens de ID no Olá seguintes seções, além de token de ID de exemplo tooa. Observe que as declarações em tokens de ID não são retornadas em uma ordem específica. Além disso, novas declarações podem ser introduzidas em tokens de ID a qualquer momento. O aplicativo não deve ser interrompido quando novas declarações são introduzidas. Olá lista a seguir inclui declarações Olá que seu aplicativo atualmente confiável pode interpretar. Você pode encontrar mais detalhes no hello [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Token de ID de exemplo
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Para praticar, tooinspect Olá declarações no token de ID do exemplo hello, cole o token de ID do exemplo hello em [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Declarações em tokens de ID
| Nome | Declaração | Valor de exemplo | Descrição |
| --- | --- | --- | --- |
| audiência |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Identifica o destinatário Olá pretendido do token de saudação. Nos tokens de ID público de saudação é ID de aplicativo do seu aplicativo, atribuído tooyour aplicativo hello Portal de registro de aplicativo do Microsoft. Seu aplicativo deve validar esse valor e rejeitar o token de saudação se Olá valor não corresponde. |
| emissor |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Identifica Olá serviço de token segurança (STS) que cria e retorna o token hello e locatário do AD do Azure Olá no qual Olá usuário foi autenticado. Seu aplicativo deve validar a declaração do emissor Olá tooensure Olá token veio do ponto de extremidade do hello v 2.0. Ele também deve usar parte do hello GUID do conjunto de saudação do hello declaração toorestrict de locatários pode entrar no aplicativo toohello. GUID que indica que o usuário Olá Olá é um usuário de consumidor de uma conta da Microsoft `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| emitido em |`iat` |`1452285331` |tempo de saudação em qual Olá token foi emitido, representado em vez de época. |
| hora de expiração |`exp` |`1452289231` |tempo de saudação na qual Olá token se torna inválido, representado em vez de época. Seu aplicativo deve usar essa validade de saudação tooverify declaração de vida útil do token hello. |
| não antes de |`nbf` |`1452285331` |tempo de saudação na qual Olá token se torna válido, são representados em vez de época. É geralmente Olá mesmo como o tempo de emissão de saudação. Seu aplicativo deve usar essa validade de saudação tooverify declaração de vida útil do token hello. |
| version |`ver` |`2.0` |versão de saudação do token de ID hello, conforme definido pelo AD do Azure. Ponto de extremidade Olá v 2.0, o valor de saudação é `2.0`. |
| ID do locatário |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |Um GUID que representa o locatário de saudação do AD do Azure que Olá usuário é de. Para contas corporativas e de estudantes, Olá GUID é locatário imutável hello, ID de organização Olá Olá usuário pertence. Para contas pessoais, valor de saudação é `9188040d-6c67-4c5b-b112-36a304b66dad`. Olá `profile` escopo é necessário em ordem tooreceive esta declaração. |
| hash de código |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hash de código Hello está incluída nos tokens de ID somente quando o token de ID de saudação é emitida com um código de autorização OAuth 2.0. Ele pode ser usado toovalidate Olá autenticidade de um código de autorização. Para obter detalhes sobre como executar essa validação, consulte Olá [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html). |
| hash de token de acesso |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hash de token de acesso de saudação está incluída nos tokens de ID somente quando o token de ID de saudação é emitida com um token de acesso OAuth 2.0. Ele pode ser usado toovalidate Olá autenticidade de um token de acesso. Para obter detalhes sobre como executar essa validação, consulte Olá [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html). |
| nonce |`nonce` |`12345` |nonce Olá é uma estratégia para mitigar ataques de reprodução de token. Seu aplicativo pode especificar um valor de uso único em uma solicitação de autorização usando Olá `nonce` parâmetro de consulta. valor Olá fornecer na solicitação de saudação é emitida no token de ID a saudação `nonce` declaração, sem modificações. Seu aplicativo pode verificar o valor de saudação com valor de saudação que ele especificado na solicitação de saudação, que associa a sessão de saudação do aplicativo com um token de ID específico. Seu aplicativo deve executar essa validação durante o processo de validação de token de ID de saudação. |
| name |`name` |`Babe Ruth` |declaração de nome Hello fornece um valor legível que identifica a entidade de saudação do token de saudação. valor de saudação não é garantida toobe exclusivo é mutável, e é projetado toobe usado apenas para fins de exibição. Olá `profile` escopo é necessário em ordem tooreceive esta declaração. |
| email |`email` |`thegreatbambino@nyy.onmicrosoft.com` |endereço de email principal Olá associado à conta de usuário do hello, se houver. Seu valor é mutável e pode ser alterado ao longo do tempo. Olá `email` escopo é necessário em ordem tooreceive esta declaração. |
| nome de usuário preferencial |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Olá nome de usuário principal que representa o usuário Olá no ponto de extremidade do hello v 2.0. Ele pode ser um endereço de email, número de telefone ou nome de usuário genérico sem um formato especificado. Seu valor é mutável e pode ser alterado ao longo do tempo. Olá `profile` escopo é necessário em ordem tooreceive esta declaração. |
| subject |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | Olá principal sobre qual Olá token declara informações, como usuário de saudação de um aplicativo. Esse valor é imutável e não pode ser reatribuído nem reutilizado. Pode ser usado tooperform verificações de autorização com segurança, como quando o token de saudação é tooaccess usado um recurso e pode ser usado como uma chave nas tabelas de banco de dados. Como o assunto hello está sempre presente nos tokens de saudação que o Azure AD emite, é recomendável usar esse valor em um sistema de autorização de uso geral. Olá assunto é, no entanto, um identificador de par - é a ID de aplicativo específico tooa exclusivo.  Portanto, se um usuário entra em dois aplicativos diferentes com duas IDs de cliente diferente, esses aplicativos receberá dois valores diferentes para a declaração do assunto de saudação.  Isso pode ou não ser desejável, dependendo dos requisitos de arquitetura e de privacidade. |
| ID do objeto |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | Olá identificador imutável de um objeto Olá Microsoft identidade System, nesse caso, uma conta de usuário.  Ele também pode ser usado tooperform verificações de autorização com segurança e como uma chave nas tabelas de banco de dados. Essa ID identifica exclusivamente o usuário Olá em aplicativos - dois aplicativos diferentes entrar Olá receberá o mesmo usuário Olá mesmo valor em Olá `oid` de declaração.  Isso significa que ele pode ser usado ao fazer consultas serviços on-line de tooMicrosoft, como Olá Microsoft Graph.  Olá Microsoft Graph retornará a ID como Olá `id` propriedade para uma determinada conta de usuário.  Porque Olá `oid` permite que vários aplicativos toocorrelate os usuários, hello `profile` escopo é necessário em ordem tooreceive esta declaração. Observe que, se um único usuário existir em vários locatários, usuário Olá conterá uma ID de objeto diferentes em cada locatário - elas são consideradas contas diferentes, embora Olá usuário faz logon em cada conta com hello mesmas credenciais. |

### <a name="access-tokens"></a>Tokens de acesso
Atualmente, os tokens de acesso emitidos pelo ponto de extremidade do hello v 2.0 podem ser consumidos apenas pelo Microsoft Services. Os aplicativos não é necessário tooperform qualquer validação ou a inspeção dos tokens de acesso para qualquer um dos cenários de saudação tem suporte no momento. Você pode tratar os tokens de acesso como completamente opacos. Eles são apenas cadeias de caracteres que seu aplicativo pode passar tooMicrosoft em solicitações HTTP.

Olá próximo v 2.0 de saudação futuras, ponto de extremidade apresentará capacidade Olá para seus tokens de acesso do aplicativo tooreceive de outros clientes. Nesse momento, informações Olá neste tópico de referência serão atualizadas com informações de saudação que é necessário para a validação de token de acesso do aplicativo tooperform e outras tarefas semelhantes.

Quando você solicitar um token de acesso do ponto de extremidade do hello v 2.0, o ponto de extremidade do hello v 2.0 também retorna metadados sobre o token de acesso de saudação para toouse seu aplicativo. Essas informações incluem o tempo de expiração de saudação do token de acesso de hello e escopos Olá para o qual ele é válido. Seu aplicativo usa esse tooperform inteligente cache de metadados de tokens de acesso sem a necessidade de token de acesso de saudação abrir tooparse em si.

### <a name="refresh-tokens"></a>Tokens de atualização
Tokens de atualização são tokens de segurança que seu aplicativo pode usar tooget novos tokens de acesso em um fluxo de OAuth 2.0. Seu aplicativo pode usar a atualização tokens tooachieve longo prazo acesso tooresources em nome de um usuário sem a necessidade de interação com o usuário hello.

Os tokens de atualização têm vários recursos. Um token de atualização recebido durante uma solicitação de token para um recurso pode ser resgatado para recursos completamente diferente de tooa de tokens de acesso.

tooreceive uma atualização em uma resposta de token, seu aplicativo deve solicitar e receber Olá `offline_acesss` escopo. toolearn mais sobre Olá `offline_access` escopo, consulte Olá [consentimento e escopos](active-directory-v2-scopes.md) artigo.

Tokens de atualização são e sempre será, aplicativo tooyour completamente opaco. Eles são emitidos pelo ponto de extremidade do hello AD do Azure v 2.0 e podem somente ser inspecionados e interpretados pelo ponto de extremidade do hello v 2.0. Eles são vida longa, mas seu aplicativo não deve ser escrito tooexpect durará um token de atualização para qualquer período de tempo. Tokens de atualização podem ser invalidados a qualquer momento por vários motivos. Olá somente modo para tooknow seu aplicativo se um token de atualização é válido é tooattempt tooredeem-lo fazendo um ponto de extremidade do token de solicitação toohello v 2.0.

Quando você resgatar um token de atualização de um novo token de acesso (e, se seu aplicativo foi concedido Olá `offline_access` escopo), você recebe um novo token de atualização na resposta de token hello. Salve Olá recentemente emitido atualização Olá tooreplace token, você usou na solicitação de saudação. Isso garante que os tokens de atualização permaneçam válidos pelo tempo máximo possível.

## <a name="validating-tokens"></a>Validando tokens
Atualmente, Olá somente validação de token se precisar de seus aplicativos tooperform está validando tokens de ID. toovalidate um token de ID, seu aplicativo deve validar declarações do token de ID ambos Olá de assinatura e hello no token de ID de saudação.

<!-- TODO: Link -->
A Microsoft fornece exemplos de código que mostram como tooeasily lidam com a validação de token e bibliotecas. Nas seções de Avançar hello, descrevemos Olá subjacente do processo. Várias bibliotecas de software livre de terceiros também estão disponíveis para validação de JWT. Há pelo menos uma opção de biblioteca para quase todas as plataformas e idiomas.

### <a name="validate-hello-signature"></a>Validar assinatura Olá
Um JWT contém três segmentos, que são separados por Olá `.` caracteres. primeiro segmento de saudação é conhecido como Olá *cabeçalho*, segundo segmento de saudação é hello *corpo*, e segmento terceiro Olá Olá *assinatura*. segmento de assinatura Olá pode ser usado toovalidate Olá autenticidade do token de ID de saudação para que ela pode ser confiável pelo seu aplicativo.

Os tokens de ID são assinados usando algoritmos de criptografia assimétrica padrão do setor, como RSA 256. cabeçalho do token de ID de saudação Hello tem informações sobre a chave de saudação e método de criptografia usado toosign token de saudação. Por exemplo:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Olá `alg` declaração indica o algoritmo de saudação que era o token de saudação toosign usado. Olá `kid` declaração indica Olá pública chave do token de saudação toosign usado.

A qualquer momento, o ponto de extremidade do hello v 2.0 pode assinar um token de ID, usando qualquer um de um conjunto específico de pares de chaves públicas-privadas. o ponto de extremidade do Hello v 2.0 periodicamente gira possível o conjunto de chaves, Olá para que seu aplicativo deve ser gravado toohandle esses principais mudanças automaticamente. Um toocheck frequência razoável para atualizações toohello pública as chaves usadas pelo ponto de extremidade do hello v 2.0 é a cada 24 horas.

Você pode adquirir Olá assinar dados de chave que você precisa assinatura de saudação toovalidate usando Olá OpenID Connect documento de metadados localizado em:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Tente Olá URL em um navegador!
>
>

Este documento de metadados é um objeto JSON que tem várias partes útil obter informações, como local de saudação do hello vários pontos de extremidade necessários para autenticação do OpenID Connect.  Olá documento também inclui um *jwks_uri*, que fornece o local de saudação do conjunto de saudação de chaves públicas usados toosign tokens. documento JSON Olá localizado em jwks_uri Olá tem todos os Olá informações da chave pública que está atualmente em uso. Seu aplicativo pode usar Olá `kid` um token de declaração em tooselect de cabeçalho do JWT Olá qual chave pública neste documento foi toosign usado. Ele executa a validação de assinatura usando a chave pública correta de saudação e algoritmo indicado hello.

Executar a validação de assinatura está fora do escopo Olá deste documento. Muitas bibliotecas de código-fonte aberto são toohelp disponível com isso.

### <a name="validate-hello-claims"></a>Validar Olá declarações
Quando seu aplicativo recebe um token de ID na entrada do usuário, ele também deve executar algumas verificações contra Olá declarações no token de ID de saudação. Elas incluem, mas sem limitação:

* **público-alvo** de declaração, tooverify que Olá token de ID foi pretendido toobe dado aplicativo tooyour
* **não antes** e **tempo de expiração** declarações, tooverify que Olá token de ID não expirou
* **emissor** de declaração, tooverify Olá token foi emitido tooyour aplicativo pelo ponto de extremidade do hello v 2.0
* **nonce**, como uma redução do ataque de reprodução do token

Para obter uma lista completa de validações de declaração que seu aplicativo deve executar, consulte Olá [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

Detalhes dos valores esperados de saudação para essas declarações são incluídos no hello [tokens ID](# ID tokens) seção.

## <a name="token-lifetimes"></a>Tempos de vida do token
Fornecemos Olá tempos de vida de token para apenas as informações a seguir. Olá informações podem ajudá-lo a desenvolver e depurar aplicativos. Os aplicativos não devem ser gravados tooexpect qualquer constante de tooremain esses tempos de vida. Os tempos de vida de token podem mudar e mudarão a qualquer momento.

| A criptografia do token | Tempo de vida | Descrição |
| --- | --- | --- |
| Tokens de ID (contas corporativos ou de estudante) |1 hora |Tokens de ID normalmente são válidos por uma hora. Seu aplicativo web pode usar esse mesmo toomaintain de tempo de vida sua própria sessão com usuário hello (recomendado) ou você pode escolher um tempo de vida da sessão completamente diferentes. Se seu aplicativo precisa tooget um novo token de ID, ele precisa toomake uma entrada nova solicitação v 2.0 do toohello autorizar o ponto de extremidade. Se o usuário Olá tem uma sessão de navegador válida com o ponto de extremidade do hello v 2.0, o usuário Olá talvez não seja necessário tooenter suas credenciais novamente. |
| Tokens de ID (contas pessoais) |24 horas |Tokens de ID para contas pessoais geralmente são válidos por 24 horas. Seu aplicativo web pode usar esse mesmo toomaintain de tempo de vida sua própria sessão com usuário hello (recomendado) ou você pode escolher um tempo de vida da sessão completamente diferentes. Se seu aplicativo precisa tooget um novo token de ID, ele precisa toomake uma entrada nova solicitação v 2.0 do toohello autorizar o ponto de extremidade. Se o usuário Olá tem uma sessão de navegador válida com o ponto de extremidade do hello v 2.0, o usuário Olá talvez não seja necessário tooenter suas credenciais novamente. |
| Tokens de acesso (contas corporativas ou de estudante) |1 hora |Indicado no token respostas como parte dos metadados de token hello. |
| Tokens de acesso (contas pessoais) |1 hora |Indicado no token respostas como parte dos metadados de token hello. Tokens de acesso que são emitidos em nome de contas pessoais podem ser configurados com um tempo de vida diferente, mas o valor típico é uma hora. |
| Tokens de atualização (conta corporativa ou de estudante) |Backup too14 dias |Um único token de atualização é válido para um máximo de 14 dias. No entanto, o token de atualização Olá poderão se tornar inválido a qualquer momento por várias razões, para que seu aplicativo deve continuar tootry toouse um token de atualização até que ele falhar, ou até que seu aplicativo substitui por um novo token de atualização. Um token de atualização também se torna inválido se foram 90 dias desde que o usuário Olá inserir suas credenciais. |
| Tokens de atualização (contas pessoais) |O ano de too1 |Um único token de atualização é válido para um máximo de 1 ano. No entanto, o token de atualização Olá pode se tornar inválido a qualquer momento por várias razões, para que seu aplicativo deve continuar tootry toouse um token de atualização até que ela falhará. |
| Códigos de autorização (contas corporativas ou de estudante) |10 minutos |Códigos de autorização são propositadamente curta duração e devem ser resgatados imediatamente para tokens de acesso e tokens de atualização quando os tokens de saudação são recebidos. |
| Códigos de autorização (contas pessoais) |5 minutos |Códigos de autorização são propositadamente curta duração e devem ser resgatados imediatamente para tokens de acesso e tokens de atualização quando os tokens de saudação são recebidos. Códigos de autorização que são emitidos em nome de contas pessoais são para uso ocasional. |
