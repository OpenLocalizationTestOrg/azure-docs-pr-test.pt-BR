---
title: "aaaAzure AD serviço tooservice auth usando OAuth 2.0 especificação em nome de rascunho | Microsoft Docs"
description: "Este artigo descreve como toouse HTTP mensagens tooimplement autenticação de serviço tooservice usando Olá OAuth 2.0 no nome de fluxo."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Chamadas de serviço tooservice usando a identidade do usuário delegado em hello em nome de fluxo
Olá fluxo do nome do OAuth 2.0 serve caso de uso de saudação onde um aplicativo invoca um serviço/API da web, que por sua vez deve toocall outro serviço/API da web. ideia Olá é toopropagate Olá delegada a identidade do usuário e permissões por meio da cadeia de solicitações de saudação. Olá serviço de camada intermediária toomake autenticado solicitações toohello downstream do serviço, ele precisa toosecure um token de acesso do Azure Active Directory (AD do Azure), em nome de usuário de saudação.

## Diagrama do fluxo em nome de
Suponha que esse usuário Olá tenha sido autenticado em um aplicativo usando Olá [fluxo de concessão de código de autorização do OAuth 2.0](active-directory-protocols-oauth-code.md). Neste ponto, o aplicativo hello tem um token de acesso (um token) com declarações do usuário hello e o consentimento tooaccess Olá intermediária API da web (A API). Agora, A API precisa toomake uma solicitação autenticada toohello downstream web API (API B).

etapas de saudação seguir constituem o fluxo de saudação em nome de e são explicadas com ajuda Olá Olá diagrama a seguir.

![Fluxo Em nome de do OAuth2.0](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. aplicativo de cliente Hello torna tooAPI uma solicitação com a token Olá
2. A API autentica toohello ponto de extremidade de emissão de tokens do AD do Azure e solicita um token tooaccess API B.
3. ponto de extremidade de emissão de token de AD do Azure Olá valida as credenciais de API A com um token e problemas hello token de acesso para API B (token B).
4. o token de saudação B é definido no cabeçalho de autorização de saudação da saudação solicitação tooAPI B.
5. Dados de saudação protegido recursos são retornados pela API B.

## Registrar o aplicativo hello e serviço no AD do Azure
Registre o aplicativo de cliente hello e o serviço de camada intermediária Olá no AD do Azure.
### Registrar o serviço de camada intermediária Olá
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e escolha **Novo registro do aplicativo**.
5. Insira um nome amigável para o aplicativo hello e selecione o tipo de aplicativo hello. Com base no tipo de aplicativo hello conjunto Olá URL de entrada ou a URL de redirecionamento toohello URL base. Clique em **criar** aplicativo hello de toocreate.
6. Ainda na Olá portal do Azure, escolha o seu aplicativo e clique em **configurações**. No menu de configurações de saudação, escolha **chaves** e adicionar uma chave - selecione uma duração de chave do ano 1 ou 2 anos. Quando você salvar esta página, o valor de chave hello serão exibidos, copie e salve o valor Olá em um local seguro - você vai precisar essa chave posterior tooconfigure Olá configurações do aplicativo em sua implementação - esse valor de chave não será exibido novamente, nem recuperáveis por qualquer outros meios, portanto, o registro-lo assim que ela é visível do hello Portal do Azure.

### Registrar o aplicativo de cliente hello
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e escolha **Novo registro do aplicativo**.
5. Insira um nome amigável para o aplicativo hello e selecione o tipo de aplicativo hello. Com base no tipo de aplicativo hello conjunto Olá URL de entrada ou a URL de redirecionamento toohello URL base. Clique em **criar** aplicativo hello de toocreate.
6. Configurar permissões para o seu aplicativo - no menu de configurações de saudação, escolha Olá **as permissões necessárias** seção, clique em **adicionar**, em seguida, **selecionar uma API**e tipo hello nome do serviço de camada intermediária Olá na caixa de texto de saudação. Em seguida, clique em **Selecionar Permissões** e selecione 'Acessar *nome do serviço*'.

### Configurar aplicativos cliente conhecidos
Nesse cenário, o serviço de camada intermediária Olá não tem nenhuma interação tooobtain Olá de usuário do usuário consentimento tooaccess Olá downstream API. Portanto, Olá opção toogrant acesso toohello downstream API deve ser apresentado inicial como parte da etapa de consentimento Olá durante a autenticação.
tooachieve, etapas a seguir Olá abaixo de registro do aplicativo do cliente Olá ligação tooexplicitly no AD do Azure com o registro do serviço de camada intermediária hello, que mescla exigido pelo cliente hello e de camada intermediária em uma única caixa de diálogo de consentimento de Olá Olá.
1. Navegue toohello registro de serviço de camada intermediária e clique em **manifesto** editor de manifesto do tooopen hello.
2. No manifesto hello, localize Olá `knownClientApplications` propriedade de matriz e adicionar Olá ID do cliente do aplicativo de cliente hello como um elemento.
3. Salve o manifesto de saudação clicando Olá botão Salvar.

## Solicitação de token de acesso do serviço tooservice
toorequest um token de acesso, fazer um ponto de extremidade HTTP POST toohello específico de locatário do AD do Azure com hello parâmetros a seguir.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Há dois casos, dependendo se o aplicativo de cliente hello escolhe toobe protegido por um segredo compartilhado ou um certificado.

### Na primeira ocorrência: solicitação de token de acesso com um segredo compartilhado
Ao usar um segredo compartilhado, uma solicitação de token de acesso de serviço a serviço contém Olá parâmetros a seguir:

| Parâmetro |  | Descrição |
| --- | --- | --- |
| grant_type |obrigatório | tipo de saudação da solicitação de token hello. Para uma solicitação usando um JWT, o valor de saudação deve ser **urn: ietf:params:oauth:grant-tipo: jwt-portador**. |
| asserção |obrigatório | valor Olá Olá token usado na solicitação de saudação. |
| client_id |obrigatório | Olá ID do aplicativo atribuído serviço chamada toohello durante o registro com o Azure AD. Olá toofind ID do aplicativo no hello Portal de gerenciamento do Azure, clique em **do Active Directory**, clique em diretório hello e, em seguida, clique em nome do aplicativo hello. |
| client_secret |obrigatório | chave de saudação registrada para Olá chamando o serviço no AD do Azure. Esse valor foi observado no tempo de saudação do registro. |
| recurso |obrigatório | Olá URI de ID do aplicativo da saudação (recurso seguro) do serviço de recebimento. Olá toofind URI de ID do aplicativo no hello Portal de gerenciamento do Azure, clique em **do Active Directory**, clique em diretório hello, clique em nome do aplicativo hello **todas as configurações** e, em seguida, clique em **propriedades** . |
| requested_token_use |obrigatório | Especifica como a solicitação de saudação deve ser processada. Olá em nome de fluxo, o valor de saudação deve ser **on_behalf_of**. |
| scope |obrigatório | Lista de escopos para solicitação de token Olá separada por espaço. Para o OpenID Connect, Olá escopo **openid** deve ser especificado.|

#### Exemplo
Olá HTTP POST a seguir solicita um token de acesso para API da web de https://graph.windows.net hello. Olá `client_id` identifica Olá serviço que solicita o token de acesso de saudação.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### Segundo caso: solicitação de token de acesso com um certificado
Uma solicitação de token de acesso de serviço a serviço com um certificado contém Olá parâmetros a seguir:

| Parâmetro |  | Descrição |
| --- | --- | --- |
| grant_type |obrigatório | tipo de saudação da solicitação de token hello. Para uma solicitação usando um JWT, o valor de saudação deve ser **urn: ietf:params:oauth:grant-tipo: jwt-portador**. |
| asserção |obrigatório | valor Olá Olá token usado na solicitação de saudação. |
| client_id |obrigatório | Olá ID do aplicativo atribuído serviço chamada toohello durante o registro com o Azure AD. Olá toofind ID do aplicativo no hello Portal de gerenciamento do Azure, clique em **do Active Directory**, clique em diretório hello e, em seguida, clique em nome do aplicativo hello. |
| client_assertion_type |obrigatório |Olá valor deve ser`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |obrigatório | Uma asserção (um JSON Web Token) que você precisa toocreate e entrar com hello certificado registrado como credenciais para o seu aplicativo.  Leia sobre [credenciais de certificado](active-directory-certificate-credentials.md) toolearn como tooregister seu formato de certificado e hello declaração hello.|
| recurso |obrigatório | Olá URI de ID do aplicativo da saudação (recurso seguro) do serviço de recebimento. Olá toofind URI de ID do aplicativo no hello Portal de gerenciamento do Azure, clique em **do Active Directory**, clique em diretório hello, clique em nome do aplicativo hello **todas as configurações** e, em seguida, clique em **propriedades** . |
| requested_token_use |obrigatório | Especifica como a solicitação de saudação deve ser processada. Olá em nome de fluxo, o valor de saudação deve ser **on_behalf_of**. |
| scope |obrigatório | Lista de escopos para solicitação de token Olá separada por espaço. Para o OpenID Connect, Olá escopo **openid** deve ser especificado.|

Observe que os parâmetros de saudação quase Olá igual ao caso de saudação da solicitação de saudação o por segredo compartilhado exceto que o parâmetro de client_secret hello é substituído por dois parâmetros: um client_assertion_type e client_assertion.

#### Exemplo
Olá HTTP POST a seguir solicita um token de acesso para Olá https://graph.windows.net API da web com um certificado. Olá `client_id` identifica Olá serviço que solicita o token de acesso de saudação.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Resposta de token de acesso do serviço tooservice
Uma resposta bem-sucedida é uma resposta JSON OAuth 2.0 com hello parâmetros a seguir.

| Parâmetro | Descrição |
| --- | --- |
| token_type |Indica o valor do tipo de token de saudação. Olá somente tipo de AD do Azure oferece suporte a **portador**. Para obter mais informações sobre tokens de portador, consulte Olá [estrutura de autorização do OAuth 2.0: uso de Token de portador (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| scope |escopo de saudação de acesso concedido em um token de saudação. |
| expires_in |comprimento de saudação do token de acesso de saudação do tempo é válido (em segundos). |
| expires_on |tempo de saudação quando o token de acesso de saudação expira. Data de saudação é representada como número de saudação de segundos de 1970-01-01T0:0:0Z UTC até o tempo de expiração de saudação. Esse valor é usado toodetermine o tempo de vida de Olá de tokens em cache. |
| recurso |Olá URI de ID do aplicativo da saudação (recurso seguro) do serviço de recebimento. |
| access_token |token de acesso solicitado Hello. Olá chamando o serviço pode usar esse serviço de recebimento toohello tooauthenticate token. |
| id_token |token de id solicitada Hello. Olá chamando o serviço pode usar a tooverify Olá identidade do usuário e iniciar uma sessão de usuário de saudação. |
| refresh_token |token de atualização de saudação para Olá solicitou o token de acesso. Olá chamando o serviço pode usar esse token toorequest outro token de acesso após a expiração do token de acesso atual hello. |

### Exemplo de resposta de êxito
Hello exemplo a seguir mostra uma solicitação de tooa de resposta de êxito de um token de acesso para API da web de https://graph.windows.net hello.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Exemplo de resposta de erro
Uma resposta de erro é retornada pelo ponto de extremidade de token do AD do Azure durante a tentativa de tooacquire um token de acesso para a API de downstream hello, se a API de downstream Olá tem uma política de acesso condicional, como autenticação multifator definido nele. o serviço de camada intermediária Olá deve superfície este aplicativo de cliente de toohello de erro para que o aplicativo de cliente hello pode fornecer a política de acesso condicional saudação do toosatisfy de interação de usuário hello.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Use Olá Olá de tooaccess token de acesso protegido de recurso
Agora o serviço de camada intermediária Olá pode usar toohello de solicitações de token toomake adquiridos acima autenticado Olá downstream web API, por configuração de token de saudação em hello `Authorization` cabeçalho.

### Exemplo
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Próximas etapas
Saiba mais sobre o protocolo de saudação OAuth 2.0 e outra autenticação de tooservice serviço de maneira de tooperform, usando as credenciais do cliente.
* [Serviço tooservice autenticação usando a concessão de credenciais de cliente OAuth 2.0 no AD do Azure](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 no Azure AD](active-directory-protocols-oauth-code.md)
