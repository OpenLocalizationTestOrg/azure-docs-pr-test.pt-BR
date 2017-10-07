---
title: "Azure Active Directory B2C: referência de token | Microsoft Docs"
description: "tipos de saudação de tokens emitidos no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: Referência de token
O Azure AD B2C (Azure Active Directory B2C) emite vários tipos de tokens de segurança ao processar cada [fluxo de autenticação](active-directory-b2c-apps.md). Este documento descreve o formato de saudação, características de segurança e conteúdo de cada tipo de token.

## <a name="types-of-tokens"></a>Tipos de tokens
B2C do Azure AD oferece suporte a saudação [protocolo de autorização do OAuth 2.0](active-directory-b2c-reference-protocols.md), que faz uso de ambos os tokens de acesso e tokens de atualização. Ele também suporta autenticação e entrar via [OpenID Connect](active-directory-b2c-reference-protocols.md), que apresenta um terceiro tipo de token: token de ID de saudação. Cada um desses tokens é representado como um token de portador.

Um token de portador é o recurso protegido de um token de segurança leve que concede Olá tooa de acesso de "portador". portador Olá é qualquer parte que pode apresentar um token de saudação. Primeiro, o Azure AD deve autenticar uma parte para que ela possa receber um token de portador. Mas se Olá necessárias não são as etapas seguidas token de saudação toosecure durante a transmissão e armazenamento, pode ser interceptado e usado por uma parte não pretendida. Alguns tokens de segurança têm um mecanismo interno para impedir que partes não autorizadas os usem, mas os tokens de portador não têm esse mecanismo. Eles devem ser transportados em um canal seguro, como segurança da camada de transporte (HTTPS).

Se um token de portador for transmitido fora de um canal seguro, um terceiro mal-intencionado pode usar um token de saudação do ataque man-in-the-middle tooacquire e usar o recurso de tooa protegido de acesso toogain não autorizado. Olá mesmos princípios de segurança se aplicam quando os tokens de portador são armazenados ou armazenado em cache para uso posterior. Sempre se certifique de que seu aplicativo transmita e armazene tokens de portador de maneira segura.

Para obter considerações de segurança adicionais sobre tokens de portador, consulte [RFC 6750 Seção 5](http://tools.ietf.org/html/rfc6750).

Muitos dos tokens de saudação do Azure AD B2C emite são implementados como tokens de web JSON (JWTs). Um JWT é um meio compacto e protegido por URL de transferir informações entre duas partes. Os JWTs contêm informações conhecidas como declarações. Esses são asserções de informações sobre o portador hello e assunto de saudação do token de saudação. declarações de saudação em JWTs são objetos JSON codificados e serializados para transmissão. Porque Olá JWTs emitidos pelo Azure AD B2C estiver assinado, mas não criptografado, você pode inspecionar facilmente conteúdo de saudação do toodebug JWT-lo. Estão disponíveis várias ferramentas que podem fazer isso, incluindo [calebb.net](http://calebb.net). Para obter mais informações sobre JWTs, consulte muito[especificações de JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Tokens de ID
Um token de ID é uma forma de token de segurança que seu aplicativo recebe de saudação do Azure AD B2C `authorize` e `token` pontos de extremidade. Tokens de ID são representados como [JWTs](#types-of-tokens), e eles contêm declarações que você pode usar tooidentify usuários em seu aplicativo. Quando os tokens de ID são adquiridos de saudação `authorize` ponto de extremidade, elas geralmente são toosign usado em aplicativos de tooweb de usuários. Quando os tokens de ID são adquiridos de saudação `token` ponto de extremidade, eles podem ser enviados nas solicitações HTTP durante a comunicação entre dois componentes de saudação mesmo aplicativo ou serviço. Você pode usar declarações de saudação em um token de ID como desejar. Elas são usadas toodisplay conta informações ou toomake acesso decisões de controle em um aplicativo.  

Os tokens de ID são assinados, mas não são criptografados atualmente. Quando seu aplicativo ou a API recebe um token de ID, ele deverá [validar assinatura Olá](#token-validation) tooprove Olá token é autêntica. Seu aplicativo ou a API também deve validar algumas declarações em Olá tooprove de token é válido. Dependendo dos requisitos do cenário de hello, declarações de saudação validadas por um aplicativo podem variar, mas seu aplicativo deve executar algumas [comuns validações de declaração](#token-validation) em cada cenário.

#### <a name="sample-id-token"></a>Token de ID de exemplo
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Tokens de acesso
Um token de acesso também é uma forma de token de segurança que seu aplicativo recebe de saudação do Azure AD B2C `authorize` e `token` pontos de extremidade. Tokens de acesso também são representados como [JWTs](#types-of-tokens), e eles contêm declarações que você pode usar o hello tooidentify concedida permissões tooyour APIs. Os tokens de acesso são assinados, mas não são criptografados atualmente. Tokens de acesso devem ser servidores de tooAPIs e recursos de acesso de tooprovide usado. Saiba mais sobre como muito[usar tokens de acesso](active-directory-b2c-access-tokens.md). 

Quando sua API recebe um token de acesso, ele deverá [validar assinatura Olá](#token-validation) tooprove Olá token é autêntica. Sua API também deve validar algumas declarações em Olá tooprove de token é válido. Dependendo dos requisitos do cenário de hello, declarações de saudação validadas por um aplicativo podem variar, mas seu aplicativo deve executar algumas [comuns validações de declaração](#token-validation) em cada cenário.

### <a name="claims-in-id-and-access-tokens"></a>Declarações em tokens de ID e de acesso
Quando você usa o Azure AD B2C, você tem controle refinado sobre o conteúdo da saudação de seus tokens. Você pode configurar [políticas](active-directory-b2c-reference-policies.md) toosend determinado conjuntos de dados de usuário em declarações que seu aplicativo requer para suas operações. Essas declarações podem incluir propriedades padrão como usuário Olá `displayName` e `emailAddress`. Também podem incluir [atributos de usuário personalizados](active-directory-b2c-reference-custom-attr.md) que você pode definir no diretório do B2C. Cada token de ID e de acesso que você recebe contém um determinado conjunto de declarações relacionadas à segurança. Os aplicativos podem usar essas declarações toosecurely autenticar usuários e solicitações.

Observe que Olá declarações nos tokens de ID não são retornadas em uma ordem específica. Além disso, novas declarações podem ser introduzidas em tokens de ID a qualquer momento. Seu aplicativo não deve ser interrompido à medida que novas declarações são introduzidas. Aqui estão Olá declarações que você espera que tooexist nos tokens de acesso e ID emitidos pelo Azure AD B2C. As declarações adicionais são determinadas por políticas. Para praticar, tente inspecionando Olá declarações no token de ID do exemplo hello colando-o na [calebb.net](http://calebb.net). Mais detalhes podem ser encontradas no hello [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html).

| Nome | Declaração | Valor de exemplo | Descrição |
| --- | --- | --- | --- |
| Público-alvo |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Uma declaração de público identifica destinatário Olá pretendido do token de saudação. Para o Azure AD B2C, público Olá é ID de aplicativo do seu aplicativo, como aplicativo tooyour atribuído no portal de registro de aplicativo hello. Seu aplicativo deve validar esse valor e rejeitar o token de saudação se ela não corresponde. |
| Emissor |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |Esta declaração identifica Olá serviço de token segurança (STS) que cria e retorna um token de saudação. Ele também identifica Olá diretório AD do Azure no qual Olá usuário foi autenticado. Seu aplicativo deve validar a declaração do emissor Olá tooensure Olá token veio do ponto de extremidade do hello Active Directory do Azure v 2.0. |
| Emitido em |`iat` |`1438535543` |Esta declaração é tempo de saudação em qual Olá token foi emitido, representado em vez de época. |
| Hora de expiração |`exp` |`1438539443` |Olá, declaração de tempo de expiração é tempo de saudação na qual Olá token se torna inválido, representado em vez de época. Seu aplicativo deve usar essa validade de saudação tooverify declaração de vida útil do token hello. |
| Não antes de |`nbf` |`1438535543` |Esta declaração é tempo de saudação na qual Olá token se torna válido, representado em vez de época. Isso é geralmente Olá mesmo como Olá tempo Olá token foi emitido. Seu aplicativo deve usar essa validade de saudação tooverify declaração de vida útil do token hello. |
| Versão |`ver` |`1.0` |Essa é a versão de saudação do token de ID hello, conforme definido pelo AD do Azure. |
| Hash de código |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Um hash de código é incluído em um token de ID apenas quando Olá token é emitido junto com um código de autorização OAuth 2.0. Um hash de código pode ser usado toovalidate Olá autenticidade de um código de autorização. Para obter mais detalhes sobre como tooperform dessa validação, consulte Olá [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html).  |
| Hash de token de acesso |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Um hash de token de acesso é incluído em um token de ID apenas quando Olá token é emitido junto com um token de acesso OAuth 2.0. Um hash de token de acesso pode ser usado toovalidate Olá autenticidade de um token de acesso. Para obter mais detalhes sobre como tooperform dessa validação, consulte Olá [especificação OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)  |
| Nonce |`nonce` |`12345` |Um valor de uso único é que uma estratégia usada toomitigate ataques de reprodução de token. Seu aplicativo pode especificar um valor de uso único em uma solicitação de autorização usando Olá `nonce` parâmetro de consulta. valor de saudação fornecer na solicitação de saudação será emitido sem modificações no hello `nonce` de declaração de um token de ID. Isso permite que o valor do aplicativo tooverify Olá com valor de saudação que ele especificado na solicitação de saudação, que associa a sessão de saudação do aplicativo com um token de ID especificado. Seu aplicativo deve executar essa validação durante o processo de validação de token de ID de saudação. |
| Assunto |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Este é o principal Olá sobre quais Olá token declara informações, como usuário de saudação de um aplicativo. Esse valor é imutável e não pode ser reatribuído nem reutilizado. Pode ser usado tooperform verificações de autorização com segurança, como quando o token hello está tooaccess usado um recurso. Por padrão, declaração do assunto Olá é preenchida com a ID de objeto de saudação do usuário Olá no diretório de saudação. mais, consulte toolearn [do Azure Active Directory B2C: Token de sessão e configuração de logon único](active-directory-b2c-token-session-sso.md). |
| Referência de classe de contexto de autenticação |`acr` |Não aplicável |Não usado no momento, exceto no caso de saudação de políticas mais antigos. mais, consulte toolearn [do Azure Active Directory B2C: Token de sessão e configuração de logon único](active-directory-b2c-token-session-sso.md). |
| Política de estrutura confiável |`tfp` |`b2c_1_sign_in` |Este é o nome de saudação do política Olá de token de ID de saudação tooacquire usado. |
| Hora da autenticação |`auth_time` |`1438535543` |Esta declaração é tempo de saudação em que um usuário último inserido as credenciais, representado em vez de época. |

### <a name="refresh-tokens"></a>Tokens de atualização
Atualizar tokens são tokens de segurança que seu aplicativo pode usar os novos tokens de ID tooacquire tokens de acesso e em um fluxo de OAuth 2.0. Eles fornecem seu aplicativo com tooresources de acesso de longo prazo em nome dos usuários sem a necessidade de interação com os usuários.

tooreceive um token de atualização em uma resposta de token, seu aplicativo deve solicitar Olá `offline_acesss` escopo. toolearn mais sobre Olá `offline_access` escopo, consulte toohello [referência de protocolo do Azure AD B2C](active-directory-b2c-reference-protocols.md).

Tokens de atualização são e sempre será, aplicativo tooyour completamente opaco. Eles são emitidos pelo Azure AD e só podem ser inspecionados e interpretados por ele. Eles são vida longa, mas seu aplicativo não deve ser escrito com expectativa de saudação que um token de atualização irão durar por um período de tempo específico. Os tokens de atualização podem ser invalidados a qualquer momento por vários motivos. Olá somente modo para tooknow seu aplicativo se um token de atualização é válido é tooattempt tooredeem-lo fazendo uma solicitação de token de tooAzure AD.

Quando você resgatar um token de atualização de um novo token (e se seu aplicativo tiver sido concedido Olá `offline_access` escopo), você receberá um novo token de atualização na resposta de token hello. Você deve salvar o token de atualização Olá emitido recentemente. Ele deve substituir o token de atualização de saudação usado anteriormente na solicitação de saudação. Isso ajuda a garantir que seus tokens de atualização permaneçam válidos pelo máximo tempo possível.

## <a name="token-validation"></a>Validação de token
toovalidate um token, seu aplicativo deve verificar assinatura hello e declarações do token de saudação.

Muitas bibliotecas de software livre estão disponíveis para validação de JWTs, dependendo da linguagem preferencial. É recomendável explorar essas opções em vez de implementar sua própria lógica de validação. Olá informações neste guia podem ajudá-lo a aprender como tooproperly usar essas bibliotecas.

### <a name="validate-hello-signature"></a>Validar assinatura Olá
Um JWT contém três segmentos, separados por Olá `.` caracteres. Olá primeiro segmento é Olá *cabeçalho*, Olá segundo é hello *corpo*, e Olá terceiro é hello *assinatura*. segmento de assinatura Olá pode ser usado toovalidate Olá autenticidade do token Olá para que ela pode ser confiável pelo seu aplicativo.

Os tokens do Azure AD B2C são assinados usando algoritmos de criptografia assimétrica padrão do setor, como o RSA 256. cabeçalho de saudação do token Olá contém informações sobre chave hello e token de saudação toosign do método de criptografia usado:

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Olá `alg` declaração indica o algoritmo de saudação que era o token de saudação toosign usado. Olá `kid` declaração indica Olá determinada chave pública que foi usado toosign token de saudação.

A qualquer momento, o Azure AD pode assinar um token usando qualquer opção de determinado conjunto de pares de chaves públicas-privadas. AD do Azure gira possível o conjunto de chaves Olá periodicamente, para que seu aplicativo deve ser gravado toohandle esses chave muda automaticamente. Um toocheck frequência razoável para atualizações toohello pública as chaves usadas pelo AD do Azure é a cada 24 horas.

O Azure AD B2C tem um ponto de extremidade de metadados OpenID Connect. Isso permite que aplicativos informações toofetch sobre o Azure AD B2C em tempo de execução. Essas informações incluem pontos de extremidade, conteúdos de token e chaves de assinatura de token. O diretório B2C contém um documento de metadados JSON para cada política. Por exemplo, o documento de metadados Olá para Olá `b2c_1_sign_in` política no `fabrikamb2c.onmicrosoft.com` está localizado em:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`diretório Olá B2C usada usuário Olá tooauthenticate e `b2c_1_sign_in` política Olá usada tooacquire token de saudação. toodetermine qual política foi toosign usado um token (e onde toogo toofetch Olá metadados), você tem duas opções. Primeiro, o nome da política hello está incluído no hello `acr` declaração no token de saudação. Você pode analisar declarações fora do corpo de saudação do hello JWT pelo corpo Olá decodificação de base 64 e saudação de desserialização JSON de cadeia de caracteres resultante. Olá `acr` declaração será o nome de saudação do política Olá de token de saudação tooissue usado.  A outra opção é a política de saudação tooencode no valor Olá Olá `state` parâmetro quando você emite a solicitação de saudação e decodificá-la toodetermine qual política foi usada. Ambos os métodos são válidos.

documento de metadados de saudação é um objeto JSON que contém várias informações úteis. Esses incluem o local de saudação de saudação de pontos de extremidade necessários tooperform autenticação OpenID Connect. Eles também incluem `jwks_uri`, que fornece o local de saudação do conjunto de saudação de chaves públicas que são tokens de toosign usado. Esse local é fornecido aqui, mas é melhor local de saudação toofetch dinamicamente usando o documento de metadados hello e analisando `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

documento JSON Olá localizado na seguinte URL contém todos os Olá informações de chave pública em uso em um momento específico. Seu aplicativo pode usar Olá `kid` um token específico de declaração em Olá JWT cabeçalho tooselect Olá chave pública no documento JSON de saudação toosign usado. Ele pode executar a validação de assinatura usando a chave pública correta de saudação e algoritmo indicado hello.

Uma descrição de como validação de assinatura tooperform está fora do escopo Olá deste documento. Muitas bibliotecas de código-fonte aberto são toohelp disponível com esse se você precisa dele.

### <a name="validate-hello-claims"></a>Validar Olá declarações
Quando seu aplicativo ou a API recebe um token de ID, ele também deve executar diversas verificações em relação a saudação declarações no token de ID de saudação. Elas incluem, mas sem limitação:

* Olá **público** de declaração: Isso verifica esse token de ID Olá foi pretendido toobe dado aplicativo tooyour.
* Olá **não antes** e **tempo de expiração** declarações: esses verificar esse token de ID de saudação não expirou.
* Olá **emissor** de declaração: Isso verifica esse token Olá foi emitido tooyour aplicativo pelo AD do Azure.
* Olá **nonce**: esta é uma estratégia de mitigação de ataque de reprodução de token.

Para obter uma lista completa de validações de seu aplicativo deve executar, consulte toohello [OpenID Connect especificação](https://openid.net). Detalhes dos valores esperados de saudação para essas declarações são incluídos no hello anterior [token seção](#types-of-tokens).  

## <a name="token-lifetimes"></a>Tempos de vida do token
Olá tempos de vida de token a seguir é fornecidos toofurther seu conhecimento. Eles poderão ajudá-lo quando você desenvolver e depurar aplicativos. Observe que os aplicativos não devem ser gravados tooexpect qualquer constante de tooremain esses tempos de vida. Eles podem e vão ser alterados. Leia mais sobre Olá [personalização de vidas úteis de token](active-directory-b2c-token-session-sso.md) no Azure AD B2C.

| Token | Tempo de vida | Descrição |
| --- | --- | --- |
| Tokens de ID |Uma hora |Tokens de ID normalmente são válidos por uma hora. Seu aplicativo web pode usar esse tempo de vida toomaintain seus próprio sessões com os usuários (recomendados). Também é possível escolher um tempo de vida de sessão diferente. Se seu aplicativo precisa tooget um novo token de ID, ele precisa simplesmente toomake um novo tooAzure de solicitação de entrada AD. Se um usuário tiver uma sessão do navegador válido com o Azure AD, esse usuário não pode ser tooenter necessárias credenciais novamente. |
| Tokens de atualização |Backup too14 dias |Um único token de atualização é válido para um máximo de 14 dias. No entanto, um token de atualização pode se tornar inválido a qualquer momento por vários motivos. Seu aplicativo deve continuar tootry toouse um token de atualização até que a falha de solicitação de saudação ou seu aplicativo substitui o token de atualização de saudação com um novo. Um token de atualização também pode se tornar inválido se 90 dias passaram desde que o usuário Olá última as credenciais inseridas. |
| Códigos de autorização |Cinco minutos |Intencionalmente, os códigos de autorização são de curta duração. Eles devem ser resgatados imediatamente para tokens de acesso, tokens de ID ou tokens de atualização ao serem recebidos. |

