---
title: "aaaLearn sobre Olá token diferente e declaração de tipos com suporte pelo AD do Azure | Microsoft Docs"
description: "Um guia para compreender e avaliar declarações Olá Olá SAML 2.0 e tokens JSON Web Tokens (JWT) emitidos pelo Azure Active Directory (AAD)"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Referência de token do Azure AD
Azure Active Directory (AD do Azure) emite vários tipos de tokens de segurança no processamento de saudação de cada fluxo de autenticação. Este documento descreve o formato de saudação, características de segurança e conteúdo de cada tipo de token.

## <a name="types-of-tokens"></a>Tipos de tokens
AD do Azure suporta Olá [protocolo de autorização do OAuth 2.0](active-directory-protocols-oauth-code.md), que usam access_tokens e refresh_tokens.  Ele também suporta autenticação e entrar via [OpenID Connect](active-directory-protocols-openid-connect-code.md), que apresenta um terceiro tipo de token, id_token de saudação.  Cada um desses tokens é representado como um "token de portador".

Um token de portador é o recurso protegido de um token de segurança leve que concede Olá tooa de acesso de "portador". Nesse sentido, Olá "portador" é qualquer parte que pode apresentar um token de saudação. Embora a autenticação com o AD do Azure é necessária no pedido tooreceive um token de portador, etapas devem ser seguidas interceptação de token, tooprevent toosecure Olá por uma parte não intencional. Como os tokens de portador não tem partes de tooprevent não autorizado um mecanismo interno de usá-las, eles devem ser transportados em um canal seguro, como segurança de camada de transporte (HTTPS). Se um token de portador for transmitido no hello criptografado, um ataque intermediária Olá man-in pode ser usado tooacquire Olá token e obter recursos de tooa protegido do acesso não autorizado. Olá mesmos princípios de segurança se aplicam ao armazenar ou armazenamento em cache os tokens de portador para uso posterior. Sempre se certifique de que seu aplicativo transmita e armazene tokens de portador de maneira segura. Para obter mais considerações de segurança sobre tokens de portador, consulte [RFC 6750 seção 5](http://tools.ietf.org/html/rfc6750).

Muitas das Olá tokens emitidos pelo AD do Azure são implementadas como JSON Web Tokens ou JWTs.  Um JWT é um meio compacto e protegido por URL de transferir informações entre duas partes.  informações de saudação contidas no JWTs são conhecidos como "declarações" ou asserções de informações sobre portador hello e assunto do token de saudação.  declarações de saudação em JWTs são objetos JSON codificado e serializado para transmissão.  Como JWTs Olá emitidos pelo AD do Azure são assinados, mas não criptografados, você pode facilmente inspecionar o conteúdo de saudação de um JWT para fins de depuração.  Há várias ferramentas disponíveis para isso, como [jwt.calebb.net](http://jwt.calebb.net). Para obter mais informações sobre JWTs, consulte toohello [especificação do JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Id_tokens
Id_tokens são uma forma de token de segurança de conexão que seu aplicativo recebe ao executar a autenticação usando o [OpenID Connect](active-directory-protocols-openid-connect-code.md).  Elas são representadas como [JWTs](#types-of-tokens)e contêm declarações que você pode usar para assinar o usuário Olá em seu aplicativo.  Você pode usar declarações de saudação em um id_token como desejar - geralmente são usadas para exibir informações de conta ou a tomada de decisões de controle de acesso em um aplicativo.

Atualmente, Id_tokens são assinados, mas não criptografados.  Quando seu aplicativo recebe um id_token, ele deverá [validar assinatura Olá](#validating-tokens) tooprove Olá autenticidade do token e validar algumas declarações em tooprove token Olá sua validade.  Olá validadas por um aplicativo de declarações variam dependendo dos requisitos do cenário, mas há alguns [comuns validações de declaração](#validating-tokens) que seu aplicativo deve executar em cada cenário.

Consulte a seguir para obter informações em declarações id_tokens, bem como id_token um exemplo de saudação.  Observe que as declarações Olá id_tokens não são retornadas em uma ordem específica.  Além disso, novas declarações podem ser introduzidas nos id_tokens a qualquer momento — o aplicativo não deve ser interrompido conforme novas declarações são introduzidas.  Olá lista a seguir inclui declarações Olá que seu aplicativo confiável pode interpretar no tempo de saudação da redação deste artigo.  Se necessário, até mesmo mais detalhes estão na Olá [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Exemplo de Id_Token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Para praticar, tente inspecionando Olá declarações no id_token do exemplo hello colando-o na [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Declarações em Id_Tokens
> [!div class="mx-codeBreakAll"]
| Declaração JWT | Nome | Descrição |
| --- | --- | --- |
| `appid` |ID do aplicativo |Identifica o aplicativo hello que está usando Olá token tooaccess um recurso. aplicativo Hello pode agir por ele mesmo ou em nome do usuário. ID do aplicativo Hello normalmente representa um objeto de aplicativo, mas ele também pode representar um objeto de entidade de serviço no AD do Azure. <br><br> **Valor de exemplo de JWT**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Público-alvo |Olá destinatário do token de saudação. aplicativo Hello que recebe o token Olá deve verificar se o valor de público Olá está correto e rejeitar todos os tokens destinados a um público diferente. <br><br> **Valor de exemplo de SAML**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Valor de exemplo de JWT**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Referência de classe de contexto de autenticação de aplicativo |Indica como Olá cliente foi autenticado. Para um cliente público, o valor de saudação é 0. Se a ID do cliente e o segredo do cliente são usadas, o valor de saudação é 1. <br><br> **Valor de exemplo de JWT**: <br> `"appidacr": "0"` |
| `acr` |Referência de classe de contexto de autenticação |Indica como o assunto de saudação foi autenticado, como cliente de toohello contrário na declaração de referência de classe de contexto de autenticação de aplicativo hello. Um valor de "0" indica que a autenticação do usuário final Olá não atendeu aos requisitos de saudação do ISO/IEC 29115. <br><br> **Valor de exemplo de JWT**: <br> `"acr": "0"` |
| Instante da autenticação |Registros Olá data e hora em que ocorreu a autenticação. <br><br> **Valor de exemplo de SAML**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Método de autenticação |Identifica como o assunto de saudação do token Olá foi autenticado. <br><br> **Valor de exemplo de SAML**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Valor de exemplo de JWT**: `“amr”: ["pwd"]` |
| `given_name` |Nome |Fornece Olá pela primeira vez ou "atribuído" nome de usuário Olá, conforme definido no objeto de usuário de saudação do AD do Azure. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `"given_name": "Frank"` |
| `groups` |Grupos |Fornece IDs de objetos que representam as associações de grupo da entidade hello. Esses valores são exclusivo (consulte a ID de objeto) e podem ser usados com segurança para gerenciar o acesso, como a imposição de autorização tooaccess um recurso. Olá incluídos na declaração de grupos de saudação configurados em uma base por aplicativo, por meio da propriedade "groupMembershipClaims" Olá Olá do manifesto do aplicativo. Um valor nulo exclui todos os grupos; já um valor "SecurityGroup" inclui somente os membros do grupo de segurança do Active Directory, enquanto um valor "All" inclui tanto grupos de segurança quanto listas de distribuição do Office 365. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Provedor de identidade |Registros Olá provedor de identidade que autenticou o assunto de saudação do token hello. Esse valor será de saudação emissor de declaração a menos que a conta de usuário hello está em um locatário diferente emissor Olá toohello idênticos. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Armazena o tempo de saudação em qual Olá token foi emitido. Geralmente é usado toomeasure atualização de token. <br><br> **Valor de exemplo de SAML**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Valor de exemplo de JWT**: <br> `"iat": 1390234181` |
| `iss` |Emissor |Identifica Olá serviço de token segurança (STS) que cria e retorna um token de saudação. Nos tokens de saudação que o AD do Azure retorna, o emissor de saudação é sts.windows.net. Olá, GUID no valor de declaração do emissor de saudação é Olá ID de locatário de diretório do AD do Azure hello. ID de locatário Olá é um identificador imutável e confiável do diretório de saudação. <br><br> **Valor de exemplo de SAML**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Valor de exemplo de JWT**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Sobrenome |Fornece o sobrenome Olá, sobrenome ou nome de família do usuário Olá conforme definido no objeto de usuário do AD do Azure hello. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `"family_name": "Miller"` |
| `unique_name` |Nome |Fornece um valor legível que identifica a entidade de saudação do token de saudação. Esse valor não é garantido toobe exclusivo dentro de um locatário e é projetado toobe usado apenas para fins de exibição. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |ID de objeto |Contém um identificador único de um objeto no Azure AD. Esse valor é imutável e não pode ser reatribuído nem reutilizado. Use tooidentify ID de objeto Olá um objeto tooAzure consultas AD. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Funções |Representa todas as funções de aplicativo hello assunto recebeu direta e indiretamente por meio da associação de grupo e pode ser usado tooenforce baseada em função de controle de acesso. Funções de aplicativo são definidas em uma base por aplicativo, por meio de saudação `appRoles` propriedade saudação do manifesto do aplicativo. Olá `value` propriedade de cada função de aplicativo é o valor de saudação que aparece na declaração de funções hello. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Escopo |Indica o aplicativo de cliente do hello representação permissões concedidas toohello. permissão de padrão de saudação é `user_impersonation`. proprietário de saudação do hello protegido recursos pode registrar valores adicionais no AD do Azure. <br><br> **Valor de exemplo de JWT**: <br> `"scp": "user_impersonation"` |
| `sub` |Assunto |Identifica a entidade de segurança Olá sobre quais Olá token declara informações, como usuário de saudação de um aplicativo. Esse valor é imutável e não pode ser reatribuído ou reutilizado, portanto pode ser usado tooperform verificações de autorização com segurança. Como entidade hello está sempre presente no hello Azure AD emite tokens de Olá, é recomendável usar esse valor em um sistema de autorização de finalidade geral. <br> `SubjectConfirmation` não é uma declaração. Ele descreve como o assunto de saudação do token de saudação é verificado. `Bearer`indica o que assunto Olá é confirmado pela sua posse do token de saudação. <br><br> **Valor de exemplo de SAML**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Valor de exemplo de JWT**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |ID do locatário |Um identificador imutável e não reutilizável que identifica o locatário de diretório Olá que emitiu o token de saudação. Você pode usar recursos de diretório específico do locatário de tooaccess esse valor em um aplicativo multilocatário. Por exemplo, você pode usar este locatário de saudação do valor tooidentify em toohello uma chamada de API do Graph. <br><br> **Valor de exemplo de SAML**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Valor de exemplo de JWT**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Tempo de vida do token |Define o intervalo de tempo de saudação no qual um token é válido. serviço Olá valida o token Olá deve verificar que Olá data atual está dentro Olá vida útil do token, pessoa, ele deverá rejeitar o token de saudação. Hello service pode permitir a minutos toofive além tooaccount de intervalo de vida útil do token Olá as diferenças na hora do relógio ("distorção de tempo") entre o Azure AD e o serviço de saudação. <br><br> **Valor de exemplo de SAML**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Valor de exemplo de JWT**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Nome UPN |Repositórios Olá nome do usuário de saudação principal.<br><br> **Valor de exemplo de JWT**: <br> `"upn": frankm@contoso.com` |
| `ver` |Versão |Armazena o número de versão de saudação do token de saudação. <br><br> **Valor de exemplo de JWT**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Tokens de acesso
Após a autenticação bem-sucedida, o AD do Azure retorna um token de acesso, que pode ser usado tooaccess protegido recursos. token de acesso de saudação é uma base 64 codificados JSON Web Token (JWT) e seu conteúdo pode ser inspecionado executando-o por meio de um decodificador.

Se seu aplicativo apenas *usa* tooget acesso tooAPIs de tokens de acesso, você pode (e deve) tratam os tokens de acesso como completamente opaco - elas são apenas cadeias de caracteres que seu aplicativo pode passar tooresources solicitações HTTP.

Quando você solicitar um token de acesso, o AD do Azure também retorna alguns metadados sobre o token de acesso de saudação para consumo do aplicativo.  Essas informações incluem o tempo de expiração de saudação do token de acesso de hello e escopos Olá para o qual ele é válido.  Isso permite que seu aplicativo tooperform inteligentes de cache de tokens de acesso sem ter que abrir o token de acesso de saudação próprio tooparse.

Se seu aplicativo é uma API protegida com o Azure AD que espera tokens de acesso em solicitações HTTP, você deve executar validação e a inspeção de tokens de saudação que receber. Seu aplicativo deve executar a validação de token de acesso de saudação antes de usar os recursos de tooaccess. Para obter mais informações sobre validação, consulte [Validando Tokens](#validating-tokens).  
Para obter detalhes sobre como toodo com .NET, consulte [proteger uma API da Web usando os tokens de portador do AD do Azure](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Tokens de atualização

Atualizar tokens são tokens de segurança, seu aplicativo pode usar tooacquire novos tokens de acesso em um fluxo de OAuth 2.0.  Ele permite que seu aplicativo tooachieve longo prazo tooresources de acesso em nome de um usuário sem a necessidade de interação de usuário de saudação.

Os tokens de atualização têm vários recursos.  Isso é toosay recebido de um token de atualização durante uma solicitação de token para um recurso pode ser resgatado para recursos completamente diferentes tooa de tokens de acesso. toodo, Olá conjunto `resource` parâmetro hello solicitação toohello recurso de destino.

Tokens de atualização são completamente opacos tooyour aplicativo. Eles são vida longa, mas seu aplicativo não deve ser escrito tooexpect durará um token de atualização para qualquer período de tempo.  Os tokens de atualização podem ser invalidados a qualquer momento por vários motivos.  Olá somente modo para tooknow seu aplicativo se um token de atualização é válido é tooattempt tooredeem-lo fazendo um solicitação de token tooAzure AD ponto de extremidade.

Quando você resgatar um token de atualização de um novo token de acesso, você receberá um novo token de atualização na resposta de token hello.  Você deve salvar o token de atualização Olá emitido recentemente, substituindo Olá usado na solicitação de saudação.  Isso garantirá que seus tokens de atualização permanecem válidos pelo máximo tempo possível.

## <a name="validating-tokens"></a>Validando tokens

Em ordem toovalidate um id_token ou um access_token, seu aplicativo deve validar declarações do token ambos Olá de assinatura e hello. Tokens de acesso toovalidate ordem, seu aplicativo também deve validar emissor hello, público hello e Olá tokens de assinatura. Será necessário toobe validado em relação a valores de saudação no documento de descoberta do OpenID hello. Por exemplo, a versão independente de locatário de saudação do documento hello está localizado em [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Middleware do AD do Azure tem recursos internos para validar tokens de acesso, e você pode procurar por meio de nosso [exemplos](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind na linguagem de saudação de sua escolha. Para obter mais informações sobre como tooexplicitly valida um token JWT, consulte Olá [manual exemplo de validação de JWT](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Fornecemos bibliotecas e exemplos de código que mostram como tooeasily lidam com a validação de token - Olá abaixo informações simplesmente é fornecido para os usuários que desejarem Olá toounderstand subjacente do processo.  Também há várias bibliotecas de software livre de terceiros disponíveis para validação de JWT; há pelo menos uma opção para quase todos os idiomas e plataformas. Para saber mais sobre bibliotecas de autenticação e exemplos de código do AD do Azure, veja [bibliotecas de autenticação do AD do Azure](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Validação de assinatura de saudação

Um JWT contém três segmentos, que são separados por Olá `.` caracteres.  primeiro segmento de saudação é conhecido como Olá **cabeçalho**, Olá segundo como Olá **corpo**e hello terceiro como Olá **assinatura**.  segmento de assinatura Olá pode ser usado toovalidate Olá autenticidade do token Olá para que ela pode ser confiável pelo seu aplicativo.

Os tokens emitidos pelo Azure AD são assinados usando algoritmos de criptografia assimétrica padrão do setor, como o RSA 256. cabeçalho Olá Olá JWT contém informações sobre a chave de saudação e método de criptografia usado o token de saudação toosign:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Olá `alg` declaração indica o algoritmo de saudação que era o token de saudação toosign usado, durante a saudação `x5t` declaração indica Olá determinada chave pública que foi usado toosign token de saudação.

Em qualquer ponto no tempo, o AD do Azure pode assinar um id_token usando qualquer um de um determinado conjunto de pares de chaves públicas-privadas. O AD do Azure gira possível o conjunto de chaves de forma periódica, Olá para que seu aplicativo deve ser gravado toohandle esses chave altera automaticamente.  Um toocheck frequência razoável para atualizações toohello pública as chaves usadas pelo AD do Azure é a cada 24 horas.

Você pode adquirir Olá assinatura de saudação toovalidate necessários dados de chave de assinatura usando Olá OpenID Connect documento de metadados localizado em:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Experimente essa URL em um navegador!
> 
> 

Este documento de metadados é um objeto JSON que contém várias partes úteis de informações, como a localização de saudação do hello vários pontos de extremidade necessários para realizar a autenticação do OpenID Connect.  

Ele também inclui um `jwks_uri`, que fornece o local de saudação do conjunto de saudação de chaves públicas usados toosign tokens.  documento JSON Olá localizado em Olá `jwks_uri` contém todas as informações de chave pública do hello em uso no momento determinado.  Seu aplicativo pode usar Olá `kid` um token específico de declaração em tooselect de cabeçalho do JWT Olá qual chave pública neste documento foi toosign usado.  Ele pode executar a validação de assinatura usando a chave pública correta de saudação e algoritmo indicado hello.

Executar a validação de assinatura está fora do escopo Olá deste documento - há muitas bibliotecas de código aberto disponíveis para ajudá-lo a fazer isso, se necessário.

#### <a name="validating-hello-claims"></a>Validando Olá declarações

Quando seu aplicativo recebe um token (uma id_token após a entrada do usuário, ou um token de acesso como um token de portador na solicitação HTTP de saudação) ele também deve executar algumas verificações em declarações Olá no token de saudação.  Elas incluem, mas sem limitação:

* Olá **público** declaração - tooverify Olá token foi pretendido toobe dado aplicativo tooyour.
* Olá **não antes** e **tempo de expiração** declarações - tooverify Olá token não expirou.
* Olá **emissor** declaração - tooverify Olá token foi emitido realmente tooyour aplicativo pelo AD do Azure.
* Olá **Nonce** -toomitigate um ataque de reprodução de token.
* e mais...

Para obter uma lista completa de seu aplicativo deve executar para Tokens de ID de validações de declaração, consulte toohello [OpenID Connect especificação](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Detalhes dos valores esperados de saudação para essas declarações são incluídos no hello anterior [id_token seção](#id-tokens) seção.

## <a name="sample-tokens"></a>Tokens de exemplo

Esta seção exibe exemplos de tokens SAML e JWT retornados pelo AD do Azure. Esses exemplos permitem ver Olá declarações no contexto.

### <a name="saml-token"></a>Token SAML

Este é um exemplo de um token SAML típico.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>Token JWT - representação de usuário
Este é um exemplo de um típico JWT (token Web JSON) usado em um fluxo de concessão de código de autorização.
Em adição tooclaims, token Olá inclui um número de versão no **ver** e **appidacr**, Olá autenticação contexto referência de classe, que indica como Olá cliente foi autenticado. Para um cliente público, o valor de saudação é 0. Se uma ID de cliente ou um segredo do cliente foi usado, o valor de saudação é 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Conteúdo relacionado
* Consulte hello Azure AD Graph [operações da política](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) e hello [entidade diretiva](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn mais sobre o gerenciamento de política de vida útil do token por meio de saudação do Azure AD Graph API.
* Para obter mais informações e exemplos sobre como gerenciar as políticas por meio de cmdlets do PowerShell, incluindo exemplos, consulte [Tempos de vida de token configuráveis no AD do Azure](../active-directory-configurable-token-lifetimes.md). 
