---
title: "Olá aaaUnderstand fluxo de código de autorização OAuth 2.0 no AD do Azure | Microsoft Docs"
description: "Este artigo descreve como toouse HTTP mensagens tooauthorize acessar tooweb aplicativos e APIs da web em seu locatário usando o Azure Active Directory e OAuth 2.0."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Autorizar o acesso tooweb aplicativos usando OAuth 2.0 e o Active Directory do Azure
Azure Active Directory (AD do Azure) usa OAuth 2.0 tooenable tooauthorize acesso tooweb aplicativos e APIs da web em seu locatário do AD do Azure. Este guia é independente de linguagem e descreve como toosend e receber mensagens HTTP sem usar qualquer uma das nossas bibliotecas de código-fonte aberto.

Olá fluxo de código de autorização do OAuth 2.0 é descrita em [seção 4.1 da especificação de saudação OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-4.1). É usado tooperform autenticação e autorização na maioria dos tipos de aplicativo, incluindo aplicativos web e aplicativos instalados nativamente.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Fluxo de autorização do OAuth 2.0
Em um nível alto, o fluxo de autorização inteiro Olá para um aplicativo é um pouco semelhante a:

![Fluxo do código de autenticação do OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Solicitar um código de autorização
fluxo de código de autorização Olá começa com o cliente Olá direcionando Olá usuário toohello `/authorize` ponto de extremidade. Nessa solicitação, o cliente de Olá indica Olá permissões tooacquire do usuário hello. Você pode obter pontos de extremidade Olá OAuth 2.0 na página do seu aplicativo no Portal clássico do Azure, em Olá **exibir pontos de extremidade** botão na gaveta inferior de saudação.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são identificadores de locatário, por exemplo, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` ou `common` para tokens independente de locatário |
| client_id |obrigatório |Olá Id de aplicativo atribuído tooyour aplicativo ao registrar com o Azure AD. Você pode encontrar isso na Olá Portal do Azure. Clique em **do Active Directory**, clique em diretório hello, escolha o aplicativo hello e clique em **configurar** |
| response_type |obrigatório |Deve incluir `code` para fluxo de código de autorização de saudação. |
| redirect_uri |recomendável |Olá redirect_uri do seu aplicativo, onde as respostas de autenticação podem ser enviadas e recebidas pelo seu aplicativo.  Ele deve corresponder exatamente uma saudação redirect_uris que você registrou no portal de hello, exceto que ele deve ser codificados de url.  Para aplicativos nativos e móveis, você deve usar o valor padrão Olá `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |recomendável |Especifica o método hello que deve ser usado toosend Olá resultante token tooyour back aplicativo.  Pode ser `query` ou `form_post`. |
| state |recomendável |Um valor incluído na solicitação de saudação que também é retornada na resposta de token hello. Um valor exclusivo gerado aleatoriamente que normalmente é usado para [impedir ataques de solicitação intersite forjada](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de saudação também é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| recurso |opcional |Olá URI de ID do aplicativo de saudação API web (recurso seguro). Olá toofind URI de ID do aplicativo de saudação API da web, em Olá Portal do Azure, clique em **do Active Directory**, clique em diretório hello, clique em aplicativo hello e, em seguida, clique em **configurar**. |
| prompt |opcional |Indique o tipo de saudação da interação do usuário é necessária.<p> Os valores válidos são: <p> *logon*: usuário Olá deve ser tooreauthenticate solicitada. <p> *consentimento*: consentimento do usuário tiver recebido, mas precisa toobe atualizado. usuário Olá deve ser tooconsent solicitada. <p> *admin_consent*: um administrador deve ser tooconsent solicitada em nome de todos os usuários em sua organização |
| login_hint |opcional |Pode ser o campo de endereço de email/nome de usuário usado toopre preenchimento Olá de saudação página de entrada de usuário Olá, se você souber o nome de usuário antecipadamente.  Aplicativos geralmente usam esse parâmetro durante a reautenticação, já ter extraído Olá nome de usuário de uma entrada anterior usando Olá `preferred_username` de declaração. |
| domain_hint |opcional |Fornece uma dica sobre o locatário hello ou domínio que Olá usuário deve usar toosign no. valor Olá Olá domain_hint é um domínio registrado para o locatário hello. Se locatário Olá é o diretório de local de tooan federado, AAD redirecionará toohello servidor de Federação do locatário especificado. |

> [!NOTE]
> Se o usuário Olá faz parte de uma organização, um administrador da organização Olá pode consentimento recusar em nome do usuário de saudação ou permitir Olá tooconsent de usuário. Olá usuário recebe Olá opção tooconsent somente quando o administrador o hello permite.
>
>

Neste ponto, o usuário Olá é solicitado tooenter suas credenciais e permissões do consentimento toohello indicado no hello `scope` parâmetro de consulta. Depois que o usuário Olá autentica e concede consentimento, o AD do Azure envia um aplicativo de tooyour de resposta em Olá `redirect_uri` endereço em sua solicitação.

### Resposta bem-sucedida
Uma resposta bem-sucedida se parece com esta:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Parâmetro | Descrição |
| --- | --- |
| admin_consent |valor de saudação será True se um administrador tiver consentido tooa prompt de solicitação de consentimento. |
| código |código de autorização de Olá Olá aplicativo solicitado. aplicativo Hello pode usar toorequest de código de autorização de saudação um token de acesso do recurso de destino hello. |
| session_state |Um valor exclusivo que identifica a sessão atual do usuário hello. Esse valor é um GUID, mas deve ser tratado como um valor opaco que é transmitido sem verificação. |
| state |Se um parâmetro de estado é incluído na solicitação hello, hello mesmo valor deve aparecer na resposta de saudação. É uma boa prática para Olá tooverify de aplicativo que os valores de estado Olá Olá solicitação e resposta são idênticos antes de usar a resposta de saudação. Isso ajuda a toodetect [ataques de falsificação de solicitação entre sites (CSRF)](https://tools.ietf.org/html/rfc6749#section-10.12) no cliente de saudação. |

### Resposta de erro
Respostas de erro também podem ser enviadas toohello `redirect_uri` para que o aplicativo hello possa tratá-los corretamente.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parâmetro | Descrição |
| --- | --- |
| error |Um valor de código de erro definido na seção 5.2 da saudação [estrutura de autorização do OAuth 2.0](http://tools.ietf.org/html/rfc6749). tabela próxima Olá descreve códigos de erro de saudação do AD do Azure retorna. |
| error_description |Uma descrição mais detalhada do erro de saudação. Esta mensagem não se destina toobe amigável de usuário final. |
| state |valor de estado de saudação é um valor não reutilizado gerado aleatoriamente que é enviado na solicitação hello e retornado na Olá resposta tooprevent solicitação intersite forjada (CSRF) ataques. |

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

## Use toorequest código de autorização Olá um token de acesso
Agora que você tiver adquirido um código de autorização e ter permissão concedida pelo usuário hello, você pode resgatar o código de saudação para um recurso de token toohello desejado de acesso, enviando um toohello de solicitação POST `/token` ponto de extremidade:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Parâmetro |  | Descrição |
| --- | --- | --- |
| locatário |obrigatório |Olá `{tenant}` valor no caminho de saudação da solicitação Olá pode ser usado toocontrol quem pode entrar no aplicativo hello.  Olá valores permitidos são identificadores de locatário, por exemplo, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` ou `common` para tokens independente de locatário |
| client_id |obrigatório |Olá Id de aplicativo atribuído tooyour aplicativo ao registrar com o Azure AD. Você pode encontrar isso na Olá Portal clássico do Azure. Clique em **do Active Directory**, clique em diretório hello, escolha o aplicativo hello e clique em **configurar** |
| grant_type |obrigatório |Deve ser `authorization_code` para fluxo de código de autorização de saudação. |
| código |obrigatório |Olá `authorization_code` que você copiou na seção anterior Olá |
| redirect_uri |obrigatório |Olá mesmo `redirect_uri` valor que foi usado tooacquire Olá `authorization_code`. |
| client_secret |obrigatório para aplicativos Web |segredo do aplicativo Hello que você criou no portal de registro de aplicativo hello para seu aplicativo.  Ele não deve ser usado em um aplicativo nativo, pois client_secrets não podem ser armazenados de modo confiável em dispositivos.  Ele é necessário para aplicativos web e APIs, que têm Olá Olá de toostore de capacidade da web `client_secret` com segurança no lado do servidor de saudação. |
| recurso |necessário se especificado na solicitação de código de autorização, caso contrário, é opcional |Olá URI de ID do aplicativo de saudação API web (recurso seguro). |

Olá toofind URI de ID do aplicativo no hello Portal de gerenciamento do Azure, clique em **do Active Directory**, clique em diretório hello, clique em aplicativo hello e, em seguida, clique em **configurar**.

### Resposta bem-sucedida
O Azure AD retorna um token de acesso após uma resposta bem-sucedida. chamadas de rede de toominimize do aplicativo de cliente hello e sua latência associada, aplicativo de cliente hello deve armazenar em cache os tokens de acesso para Olá vida útil do token que é especificado no hello resposta OAuth 2.0. toodetermine Olá vida útil do token, use o hello `expires_in` ou `expires_on` valores de parâmetro.

Se um recurso da API web retorna um `invalid_token` código de erro, isso pode indicar que o recurso de saudação determinou que Olá token tiver expirado. Se horas dos relógios do cliente e o recurso Olá são diferentes (conhecido como "diferença de horário"), recursos de saudação considere toobe token Olá expirou antes do hello token seja removido do cache do cliente de saudação. Se isso ocorrer, desmarque o token de saudação do cache Olá, mesmo se ele ainda estiver dentro de seu tempo de vida calculado.

Uma resposta bem-sucedida se parece com esta:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Parâmetro | Descrição |
| --- | --- |
| access_token |token de acesso solicitado Hello. Olá aplicativo pode usar este toohello tooauthenticate token protegido de recurso, como uma API da web. |
| token_type |Indica o valor do tipo de token de saudação. Olá digite somente do AD do Azure suporta é portador. Para saber mais sobre os tokens de portador, confira [Estrutura de autorização do OAuth 2.0: uso do token de portador (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |Quanto tempo o token de acesso de saudação é válido (em segundos). |
| expires_on |tempo de saudação quando o token de acesso de saudação expira. Data de saudação é representada como número de saudação de segundos de 1970-01-01T0:0:0Z UTC até o tempo de expiração de saudação. Esse valor é usado toodetermine o tempo de vida de Olá de tokens em cache. |
| recurso |Olá URI de ID do aplicativo de saudação API web (recurso seguro). |
| scope |Permissões de representação concedidas toohello aplicativo de cliente. permissão de padrão de saudação é `user_impersonation`. proprietário de saudação do hello protegido recursos pode registrar valores adicionais no AD do Azure. |
| refresh_token |Um token de atualização do OAuth 2.0. Olá aplicativo pode usar esse token tooacquire os tokens de acesso adicionais após a expiração do token de acesso atual hello.  Atualizar tokens são de vida longa e pode ser usado tooretain acesso tooresources por longos períodos de tempo. |
| id_token |Um JWT (Token Web JSON) não assinado. Olá aplicativo pode base64Url decodificar segmentos Olá dessas informações de token toorequest sobre o usuário Olá conectado. Olá aplicativo pode armazenar em cache os valores hello e exibi-las, mas ele não deve confiar neles para qualquer autorização ou limites de segurança. |

### Declarações de token JWT
token JWT de saudação no valor Olá Olá `id_token` parâmetro pode ser decodificado para Olá declarações a seguir:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Para obter mais informações sobre tokens da web JSON, consulte Olá [especificação de rascunho JWT IETF](http://go.microsoft.com/fwlink/?LinkId=392344). Para obter mais informações sobre tipos de token hello e declarações, leia [tipos de declaração e Token com suporte](active-directory-token-and-claims.md)

Olá `id_token` inclui o parâmetro hello tipos de declaração a seguir:

| Tipo de declaração | Descrição |
| --- | --- |
| aud |Público-alvo do token de saudação. Quando o token de saudação é emitido tooa aplicativo de cliente, público Olá é hello `client_id` do cliente de saudação. |
| exp |Hora de expiração. tempo de saudação quando o token de saudação expira. Para Olá token toobe válido, Olá data/hora atual deve ser menor ou igual toohello `exp` valor. tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até Olá tempo Olá token foi emitido. |
| family_name |Sobrenome do usuário. aplicativo Hello pode exibir esse valor. |
| given_name |Nome do usuário. aplicativo Hello pode exibir esse valor. |
| iat |Hora da emissão. tempo de saudação quando Olá JWT foi emitido. tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até Olá tempo Olá token foi emitido. |
| iss |Identifica o emissor do token Olá |
| nbf |Não antes de. tempo de saudação quando Olá token entrou em vigor. Para Olá token toobe válido, Olá data/hora atual deve ser toohello maior que ou igual Nbf valor. tempo de saudação é representado como número de saudação de segundos de 1º de janeiro de 1970 (1970-01-01T0:0:0Z) UTC até Olá tempo Olá token foi emitido. |
| oid |Identificador de objeto (ID) do objeto de usuário de saudação no AD do Azure. |
| sub |Identificador do assunto do token. Este é um identificador persistente e imutável para o usuário Olá Olá token descreve. Use esse valor na lógica de cache. |
| tid |Identificador (ID) do locatário de saudação do AD do Azure que emitiu o token de saudação do locatário. |
| unique_name |Um identificador exclusivo para o que pode ser exibido toohello usuário. Geralmente é um nome de usuário principal (UPN). |
| upn |Nome principal do usuário hello. |
| ver |Versão. versão de saudação do token JWT hello, normalmente 1.0. |

### Resposta de erro
erros de ponto de extremidade de emissão de tokens de saudação são códigos de erro HTTP, como chamadas de cliente Olá Olá ponto de extremidade de emissão de tokens diretamente. Além disso toohello HTTP de código de status, o ponto de extremidade de emissão de token de AD do Azure Olá também retorna um documento JSON com objetos que descrevem o erro hello.

Uma resposta de erro de exemplo se parece com esta:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| error_codes |Uma lista de códigos de erro específicos do STS que pode ajudar no diagnóstico. |
| timestamp |tempo de saudação na qual ocorreu o erro de saudação. |
| trace_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico. |
| correlation_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico em componentes. |

#### Códigos de status HTTP
Olá, tabela a seguir lista os códigos de status Olá HTTP Olá retorna de ponto de extremidade de emissão de token. Em alguns casos, o código de erro de saudação é suficiente resposta de saudação toodescribe, mas se houver erros, você precisa Olá tooparse que acompanha o JSON de documento e examine o código de erro.

| Código HTTP | Descrição |
| --- | --- |
| 400 |Código HTTP padrão. Usado na maioria dos casos e geralmente é devido a solicitação malformada tooa. Corrija e reenvie a solicitação de saudação. |
| 401 |Falha na autenticação. Por exemplo, solicitação de saudação é Olá client_secret parâmetro ausente. |
| 403 |Falha na autorização. Por exemplo, usuário Olá não tem recursos de saudação tooaccess permissão. |
| 500 |Erro interno no serviço de saudação. Repita a solicitação de saudação. |

#### Códigos de erro para erros de ponto de extremidade de token
| Código do Erro | Descrição | Ação do Cliente |
| --- | --- | --- |
| invalid_request |Erro de protocolo, como um parâmetro obrigatório ausente. |Corrija e reenvie a solicitação de saudação |
| invalid_grant |código de autorização de saudação é inválido ou expirou. |Tente um novo toohello de solicitação `/authorize` ponto de extremidade |
| unauthorized_client |Olá cliente autenticado não está autorizado toouse essa autorização conceder tipo. |Isso geralmente ocorre quando o aplicativo de cliente hello não está registrado no AD do Azure ou não será adicionado o locatário do AD do Azure toohello do usuário. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |
| invalid_client |Falha na autenticação de cliente. |as credenciais do cliente Olá não são válidas. toofix, o administrador do aplicativo hello atualiza credenciais hello. |
| unsupported_grant_type |servidor de autorização de saudação não dá suporte para o tipo de concessão de autorização de saudação. |Saudação de alteração conceder tipo na solicitação de saudação. Esse tipo de erro deve ocorrer somente durante o desenvolvimento e ser detectado durante os testes iniciais. |
| invalid_resource |o recurso de destino Olá é inválido porque não existe, o AD do Azure não encontrou ou não está configurado corretamente. |Isso indica que o recurso hello, se ele existir, não foi configurado no locatário hello. aplicativo Hello pode solicitar o usuário Olá com instruções para instalar o aplicativo hello e adicioná-lo tooAzure AD. |
| interaction_required |solicitação de saudação requer interação do usuário. Por exemplo, é necessária uma etapa de autenticação adicional. | Em vez de uma solicitação não interativo, tente novamente com uma solicitação de autorização interativa para Olá mesmo recurso. |
| temporarily_unavailable |servidor de saudação está temporariamente solicitação de saudação toohandle muito ocupado. |Repita a solicitação de saudação. aplicativo de cliente Hello pode explicar toohello usuário que sua resposta está atrasada devido a condição temporária tooa. |

## Usar Olá acesso tooaccess token Olá recurso
Agora que você tenha adquirido com êxito um `access_token`, você pode usar o token Olá em solicitações tooWeb APIs, incluindo-o em Olá `Authorization` cabeçalho. Olá [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) especificação explica como os tokens de portador toouse no tooaccess de solicitações HTTP de recursos protegidos.

### Solicitação de exemplo
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Resposta de erro
Recursos protegidos que implementam RFC 6750 emitem códigos de status HTTP. Se a solicitação de saudação não tem credenciais de autenticação ou está faltando o token, resposta de Olá Olá inclui um `WWW-Authenticate` cabeçalho. Quando uma solicitação falhar, o servidor de saudação do recurso responde com código de status HTTP hello e um código de erro.

a seguir Olá é um exemplo de uma resposta bem-sucedida quando a solicitação de saudação do cliente inclui um token de portador hello:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Parâmetros de erro
| Parâmetro | Descrição |
| --- | --- |
| authorization_uri |Olá URI (ponto de extremidade físico) do servidor de autorização de saudação. Esse valor também é usado como uma pesquisa de chave tooget para obter mais informações sobre o servidor de saudação de um ponto de extremidade de descoberta. <p><p> cliente Olá deve validar esse Olá servidor de autorização é confiável. Quando o recurso de saudação é protegido pelo AD do Azure, é suficiente tooverify que Olá URL começa com https://login.microsoftonline.com ou outro nome de host que oferece suporte ao AD do Azure. Um recurso específico de locatário sempre deve retornar um URI de autorização específico de locatário. |
| error |Um valor de código de erro definido na seção 5.2 da saudação [estrutura de autorização do OAuth 2.0](http://tools.ietf.org/html/rfc6749). |
| error_description |Uma descrição mais detalhada do erro de saudação. Esta mensagem não se destina toobe amigável de usuário final. |
| resource_id |Retorna Olá identificador exclusivo do recurso de saudação. aplicativo de cliente Hello pode usar esse identificador como valor de saudação do hello `resource` parâmetro quando ele solicita um token para o recurso de saudação. <p><p> É importante para Olá tooverify do aplicativo cliente esse valor, caso contrário, um serviço mal-intencionado pode ser capaz de tooinduce um **elevação de privilégios** ataque <p><p> Olá recomendado estratégia para evitar um ataque é tooverify Olá `resource_id` correspondências Olá Olá web API URL base que está sendo acessado. Por exemplo, se estiver sendo acessado https://service.contoso.com/data, Olá `resource_id` pode ser htttps://service.contoso.com/. aplicativo de cliente Hello deve rejeitar um `resource_id` que não começam com hello URL de base a menos que haja uma id de saudação de tooverify de maneira confiável alternativa. |

#### Códigos de erro de esquema de portador
Olá especificação RFC 6750 define Olá para recursos que usam o cabeçalho WWW-Authenticate de saudação e o esquema portador na resposta Olá os erros a seguir.

| Código de status HTTP | Código do Erro | Descrição | Ação do Cliente |
| --- | --- | --- | --- |
| 400 |invalid_request |solicitação de saudação não está bem formada. Por exemplo, ele pode estar faltando um parâmetro ou usando Olá mesmo parâmetro duas vezes. |Corrija o erro de saudação e repita a solicitação de saudação. Esse tipo de erro deve ocorrer somente durante o desenvolvimento e deve ser detectado nos testes iniciais. |
| 401 |invalid_token |o token de acesso Hello está ausente, inválido ou foi revogado. valor de saudação do parâmetro de error_description Olá fornece detalhes adicionais. |Solicite um novo token de saudação do servidor de autorização. Se o novo token de saudação falhar, um erro inesperado ocorreu. Enviar um usuário de toohello de mensagem de erro e tente novamente após intervalos aleatórios. |
| 403 |insufficient_scope |token de acesso de saudação não contém o recurso de saudação do hello representação permissões tooaccess necessária. |Envie um novo ponto de extremidade autorização autorização solicitação toohello. Se resposta Olá contém o parâmetro de escopo Olá, use o valor do escopo Olá no recurso de toohello de solicitação de saudação. |
| 403 |insufficient_access |assunto de saudação do token de saudação não tem permissões de saudação que sejam necessárias tooaccess saudação do recurso. |Olá Avisar usuário toouse uma conta diferente ou toorequest permissões toohello o recurso especificado. |

## Atualizando os tokens de acesso Olá
Tokens de acesso são de curta duração e devem ser atualizados depois que eles expiram toocontinue acessar recursos. Você pode atualizar Olá `access_token` enviando outra `POST` solicitação toohello `/token` ponto de extremidade, mas desta vez fornecendo Olá `refresh_token` em vez da saudação `code`.

Os tokens de atualização não têm um tempo de vida especificado. Normalmente, os tempos de vida de saudação de tokens de atualização serão relativamente longos. No entanto, em alguns casos, tokens de atualização expirarem, são revogados ou não tem privilégios suficientes para a ação de saudação desejada. Seu aplicativo precisa tooexpect e o manipulador de erros retornados pelo ponto de extremidade de emissão de token Olá corretamente.

Quando você receber uma resposta com um erro de token de atualização, descarte Olá token de atualização atual e solicite um novo código de autorização ou token de acesso. Em particular, quando usando uma atualização de token em Olá fluxo de concessão de código de autorização, se você receber uma resposta com hello `interaction_required` ou `invalid_grant` códigos de erro, descarte o token de atualização hello e solicite um novo código de autorização.

Um toohello de solicitação de exemplo **específico do locatário** ponto de extremidade (você também pode usar o hello **comuns** ponto de extremidade) tooget um novo token de acesso usando um token de atualização tem esta aparência:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Resposta bem-sucedida
Uma resposta de token bem-sucedida se parecerá com esta:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Parâmetro | Descrição |
| --- | --- |
| token_type |tipo de token Hello. valor de saudação só tem suportada é **portador**. |
| expires_in |Olá restante do tempo de vida do token de saudação em segundos. Um valor típico é 3600 (uma hora). |
| expires_on |Data de saudação e a hora em que o token de saudação expira. Data de saudação é representada como número de saudação de segundos de 1970-01-01T0:0:0Z UTC até o tempo de expiração de saudação. |
| recurso |Identifica Olá protegidos recurso esse token de acesso de saudação pode ser usado tooaccess. |
| scope |Permissões de representação concedidas toohello aplicativo de cliente nativo. permissão de padrão de saudação é **user_impersonation**. proprietário de saudação do recurso de destino Olá pode registrar valores alternativos no AD do Azure. |
| access_token |Olá novo token de acesso que foi solicitado. |
| refresh_token |Um novo refresh_token de OAuth 2.0 que pode ser usado toorequest novos tokens de acesso quando Olá nesta resposta expira. |

### Resposta de erro
Uma resposta de erro de exemplo se parece com esta:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Parâmetro | Descrição |
| --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro de autenticação. |
| error_codes |Uma lista de códigos de erro específicos do STS que pode ajudar no diagnóstico. |
| timestamp |tempo de saudação na qual ocorreu o erro de saudação. |
| trace_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico. |
| correlation_id |Um identificador exclusivo para a solicitação de saudação que pode ajudar no diagnóstico em componentes. |

Para obter uma descrição dos códigos de erro hello e Olá cliente ação recomendada, consulte [códigos de erro para erros de ponto de extremidade token](#error-codes-for-token-endpoint-errors).
