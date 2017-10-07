---
title: "aaaAzure do Active Directory v 2.0 escopos, permissões e consentimento | Microsoft Docs"
description: "Uma descrição de autorização no ponto de extremidade v 2.0 de saudação do AD do Azure, incluindo escopos, permissões e consentimento."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Escopos de permissões e consentimento no ponto de extremidade do hello Active Directory do Azure v 2.0
Os aplicativos que se integram ao Azure AD (Azure Active Directory) seguem um modelo de autorização que fornece aos usuários controle sobre como um aplicativo pode acessar seus dados. implementação de v 2.0 de saudação do modelo de autorização Olá foi atualizada e muda como um aplicativo deve interagir com o Azure AD. Este artigo aborda os conceitos básicos de saudação desse modelo de autorização, incluindo escopos, permissões e consentimento.

> [!NOTE]
> o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure. toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Permissões e escopos
O AD do Azure implementa Olá [OAuth 2.0](active-directory-v2-protocols.md) protocolo de autorização. O OAuth 2.0 é um método pelo qual um aplicativo de terceiros pode acessar recursos hospedados na Web em nome do usuário. Qualquer recurso hospedado na Web que se integre ao Azure AD terá um identificador de recurso, ou *URI de ID de Aplicativo*. Por exemplo, alguns dos recursos hospedados na Web da Microsoft incluem:

* Olá API do Office 365 Unificação de mensagens:`https://outlook.office.com`
* Olá API do Azure AD Graph:`https://graph.windows.net`
* Microsoft Graph: `https://graph.microsoft.com`

Olá que mesmo é verdadeiro para todos os recursos de terceiros que foram integrados ao AD do Azure. Além disso, qualquer um desses recursos pode definir um conjunto de permissões que podem ser usados toodivide a funcionalidade de saudação do recurso em partes menores. Por exemplo, [Microsoft Graph](https://graph.microsoft.io) definiu Olá de toodo permissões seguintes tarefas, entre outros:

* Ler o calendário de um usuário
* Gravação tooa calendário de usuário
* Enviar email como um usuário

Ao definir esses tipos de permissões, o recurso de saudação tem controle refinado sobre seus dados e como os dados de saudação são expostos. Um aplicativo de terceiros pode solicitar essas permissões de um usuário do aplicativo. usuário do aplicativo Hello deve aprovar permissões Olá antes que o aplicativo hello pode agir em nome do usuário hello. A funcionalidade do recurso de saudação em conjuntos menores de agrupamento, aplicativos de terceiros podem ser criados toorequest somente Olá permissões específicas que precisam tooperform sua função. Os usuários do aplicativo podem saber exatamente como um aplicativo usará seus dados e podem ser mais seguro que o aplicativo hello não está se comportando mal-intencionadas.

No Azure AD e no OAuth, esses tipos de permissões são chamados de *escopos*. Às vezes também forem chamados tooas *oAuth2Permissions*. Um escopo é representado no AD do Azure como um valor de cadeia de caracteres. Continuando com o exemplo do Microsoft Graph hello, valor de escopo de saudação para cada permissão é:

* Ler o calendário de um usuário usando o `Calendar.Read`
* Gravar tooa calendário de usuário usando`Mail.ReadWrite`
* Enviar email como um usuário usando `Mail.Send`

Um aplicativo pode solicitar essas permissões, especificando escopos Olá no ponto de extremidade solicitações toohello v 2.0.

## <a name="openid-connect-scopes"></a>Escopos do OpenID Connect
Olá v 2.0 implementação OpenID Connect tem alguns escopos bem definidos que não se aplicam a recursos específicos de tooa: `openid`, `email`, `profile`, e `offline_access`.

### <a name="openid"></a>openid
Se um aplicativo executa entrar usando [OpenID Connect](active-directory-v2-protocols.md), ele deve solicitar Olá `openid` escopo. Olá `openid` mostra como escopo na conta de trabalho Olá página de consentimento como hello "Entrar" permissão e na conta pessoal da Microsoft hello página de consentimento como Olá permissão "Exibir seu perfil e conectar tooapps e serviços usando sua conta da Microsoft". Com essa permissão, um aplicativo pode receber um identificador exclusivo para o usuário Olá na forma de saudação de saudação `sub` de declaração. Ele também fornece o ponto de extremidade do hello aplicativo acesso toohello UserInfo. Olá `openid` escopo pode ser usado em Olá v 2.0 ponto de extremidade token tooacquire ID tokens, que podem ser usado toosecure HTTP chamadas entre diferentes componentes de um aplicativo.

### <a name="email"></a>email
Olá `email` escopo pode ser usado com hello `openid` escopo e outras. Ele fornece o endereço de email principal do usuário do toohello acesso aplicativo hello na forma de saudação de saudação `email` de declaração. Olá `email` declaração é incluída em um token somente se um endereço de email está associado à conta de usuário de saudação, que não é sempre o caso de saudação. Se usar Olá `email` escopo, seu aplicativo deve ser preparado toohandle um caso no qual Olá `email` declaração não existe no token de saudação.

### <a name="profile"></a>Perfil
Olá `profile` escopo pode ser usado com hello `openid` escopo e outras. Ele fornece Olá aplicativo acesso tooa quantidade significativa de informações sobre o usuário hello. informações de saudação pode acessar incluem, mas não são limitadas para Olá preferencial do nome de usuário, sobrenome, nome do usuário e ID de objeto Para obter uma lista completa de saudação de declarações de perfil disponíveis no parâmetro de id_tokens Olá para um usuário específico, consulte Olá [v 2.0 tokens referência](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Olá [ `offline_access` escopo](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) fornece seu tooresources de acesso do aplicativo em nome de usuário de saudação por um longo período. Na página de consentimento de conta de trabalho Olá, esse escopo é exibida como Olá permissão "Acessar seus dados a qualquer momento". Em Olá pessoal consentimento página da conta Microsoft, ele é exibido como Olá permissão "Acessar suas informações a qualquer momento". Quando um usuário aprova Olá `offline_access` escopo, seu aplicativo pode receber tokens de atualização do ponto de extremidade token Olá v 2.0. Os tokens de atualização têm uma vida longa. Seu aplicativo pode obter novos tokens de acesso quando os mais antigos expirarem.

Se seu aplicativo não solicitar Olá `offline_access` escopo, ele não receberá atualizações de tokens. Isso significa que quando você resgatar um código de autorização no hello [fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols.md), você receberá um token de acesso de saudação `/token` ponto de extremidade. token de acesso de saudação é válido por um curto período. o token de acesso Olá geralmente expira em uma hora. Nesse ponto, seu aplicativo precisa tooredirect Olá usuário back toohello `/authorize` tooget de ponto de extremidade um novo código de autorização. Durante esse redirecionamento, dependendo do tipo de saudação do aplicativo, usuário Olá pode precisar tooenter suas credenciais novamente ou consentimento novamente toopermissions.

Para obter mais informações sobre como tooget e use tokens de atualização, consulte Olá [referência de protocolo v 2.0](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Solicitando consentimento de usuário individual
Em um [OpenID Connect ou OAuth 2.0](active-directory-v2-protocols.md) solicitação de autorização, um aplicativo pode solicitar permissões de saudação precisa usando Olá `scope` parâmetro de consulta. Por exemplo, quando um usuário entra no aplicativo tooan, o aplicativo hello envia uma solicitação como Olá exemplo a seguir (com quebras de linha adicionadas para legibilidade):

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Olá `scope` parâmetro é uma lista separada por espaços de escopos que Olá aplicativo está solicitando. Cada escopo é indicado por acrescentar o identificador do recurso do toohello valor escopo hello (Olá URI da ID do aplicativo). No exemplo de solicitação hello, aplicativo hello precisa de permissão tooread Olá calendário de usuário e enviar um email como usuário hello.

Depois que o usuário Olá insere suas credenciais, o ponto de extremidade do hello v 2.0 verifica um registro correspondente de *consentimento do usuário*. Se o usuário Olá não consentiu tooany de saudação solicitadas permissões no hello anterior, Olá usuário toogrant solicita que o ponto de extremidade do hello v 2.0 Olá solicitadas permissões.

![Consentimento de conta de trabalho](../../media/active-directory-v2-flows/work_account_consent.png)

Quando o usuário Olá aprova permissão hello, consentimento Olá é registrado para que hello usuário não tem tooconsent novamente em logons subsequentes de conta.

## <a name="requesting-consent-for-an-entire-tenant"></a>Solicitando consentimento para um locatário inteiro
Geralmente, quando uma organização adquire uma licença ou assinatura de um aplicativo, Olá organização deseja que aplicativo de hello provisionar toofully para seus funcionários. Como parte desse processo, um administrador pode conceder consentimento para Olá aplicativo tooact em nome de um funcionário. Se Olá administrador concede permissão para o locatário todo hello, Olá funcionários não verão uma página de consentimento para o aplicativo hello.

consentimento toorequest para todos os usuários em um locatário, seu aplicativo pode usar o ponto de extremidade do Olá administrador consentimento.

## <a name="admin-restricted-scopes"></a>Escopos restritos ao administrador
Algumas permissões com alto privilégio no ecossistema do Microsoft hello podem ser definidas muito*restringido pelo administrador*. Exemplos desses tipos de escopos incluem hello as seguintes permissões:

* Ler dados do diretório da organização usando `Directory.Read`
* Gravar o diretório da organização de tooan dados usando`Directory.ReadWrite`
* Ler grupos de segurança no diretório da organização usando o `Groups.Read.All`

Embora um usuário de consumidor pode conceder um toothis de acesso do aplicativo, tipo de dados, os usuários organizacionais são impedidos de conceder acesso toohello mesmo conjunto de dados confidenciais da empresa. Se seu aplicativo solicita acesso tooone dessas permissões de um usuário organizacional, usuário Olá recebe uma mensagem de erro que diz que não são permissões do aplicativo de tooyour tooconsent autorizados.

Se seu aplicativo requer acesso restrito tooadmin escopos para as organizações, você deve solicitá-las diretamente de um administrador da empresa, também usando Olá consentimento do ponto de extremidade administrador, descrito a seguir.

Quando um administrador concede que essas permissões Olá administrador por meio do ponto de extremidade de consentimento, consentimento é concedido para todos os usuários no locatário hello.

## <a name="using-hello-admin-consent-endpoint"></a>Usando o ponto de extremidade de autorização do Olá administrador
Se você seguir estas etapas, seu aplicativo poderá obter permissões para todos os usuários em um locatário, incluindo escopos restringidos pelo administrador. toosee um exemplo de código que implementa etapas hello, consulte Olá [exemplo escopos restringido pelo administrador](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Solicitar permissões Olá no portal de registro de aplicativo hello
1. Vá tooyour aplicativo hello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou [criar um aplicativo](active-directory-v2-app-registration.md) se ainda não o fez.
2. Localizar Olá **Microsoft Graph permissões** seção e, em seguida, adicione permissões de saudação que seu aplicativo requer.
3. Verifique se você **salvar** Olá o registro do aplicativo.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Recomendado: Usuário de saudação entrar no aplicativo tooyour
Normalmente, quando você cria um aplicativo que usa o ponto de extremidade de autorização de administrador hello, Olá aplicativo precisa de uma página ou exibição na qual Olá administrador pode aprovar permissões do aplicativo hello. Esta página pode ser parte do fluxo de inscrição do aplicativo hello, parte de configurações do aplicativo hello, ou pode ser dedicado "conectar" fluxo. Em muitos casos, faz sentido para Olá aplicativo tooshow isso "conectar" modo de exibição somente depois que um usuário tiver se conectado com um trabalho ou escola conta da Microsoft.

Quando você entrar usuário Olá no aplicativo tooyour, você pode identificar a organização Olá toowhich Olá administrador pertence antes solicitando que eles as permissões necessárias tooapprove hello. Embora não seja estritamente necessário, isso pode ajudá-lo a criar uma experiência mais intuitiva para os usuários empresariais. usuário de saudação toosign in, siga nosso [tutoriais de protocolo v 2.0](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Saudação de solicitar permissões de um administrador de diretório
Quando você estiver pronto toorequest permissões de administrador de sua organização, você pode redirecionar v 2.0 do hello usuário toohello *ponto de extremidade de autorização administrador*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parâmetro | Condição | Descrição |
| --- | --- | --- |
| locatário |Obrigatório |locatário do diretório Olá que você deseja toorequest permissão do. Pode ser fornecido no formato de nome amigável ou de GUID. |
| client_id |Obrigatório |Olá aplicativo ID que Olá [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) atribuído tooyour aplicativo. |
| redirect_uri |Obrigatório |Olá redirecione o URI em que você deseja Olá resposta toobe enviado para seu aplicativo toohandle. Ele deve corresponder exatamente um redirecionamento Olá URIs que você registrou no portal de registro de aplicativo hello. |
| state |Recomendadas |Um valor incluído na solicitação de saudação que também será retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo desejado. Use informações de tooencode de estado de saudação sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como exibição ou página Olá estivesse em. |

Neste ponto, AD do Azure requer um toosign do administrador de locatário na solicitação de saudação toocomplete. administrador de saudação é solicitado tooapprove que todos Olá permissões solicitadas para seu aplicativo no portal de registro de aplicativo hello.

#### <a name="successful-response"></a>Resposta bem-sucedida
Se Olá administrador aprovar permissões Olá para seu aplicativo, resposta bem-sucedida Olá terá esta aparência:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parâmetro | Descrição |
| --- | --- | --- |
| locatário |locatário do diretório Olá concedidas as permissões do aplicativo hello solicitados, no formato GUID. |
| state |Um valor incluído na solicitação de saudação que também será retornada na resposta de token hello. Pode ser uma cadeia de caracteres de qualquer conteúdo desejado. estado de saudação é usado tooencode informações sobre o estado do usuário Olá no aplicativo hello antes de solicitação de autenticação hello, como página hello ou exibição que estavam no. |
| admin_consent |Será definido muito**true**. |

#### <a name="error-response"></a>Resposta de erro
Se Olá administrador aprove permissões Olá para seu aplicativo, Olá falha resposta esta aparência:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parâmetro | Descrição |
| --- | --- | --- |
| error |Uma cadeia de código de erro que pode ser usados tooclassify tipos de erros que ocorrem e pode ser usado tooreact tooerrors. |
| error_description |Uma mensagem de erro específicas que um desenvolvedor pode ajudar a identificar a causa de saudação de um erro. |

Depois que você recebeu uma resposta bem-sucedida do ponto de extremidade de autorização de admin hello, seu aplicativo ganhou permissões Olá solicitada. Em seguida, você pode solicitar um token para o recurso de saudação desejado.

## <a name="using-permissions"></a>Usando permissões
Após o consentimento do usuário Olá toopermissions para seu aplicativo, seu aplicativo pode obter tokens de acesso que representam tooaccess de permissão do aplicativo um recurso em alguma capacidade. Um token de acesso pode ser usado apenas para um único recurso, mas codificadas no token de acesso de saudação é cada permissão que seu aplicativo tenha sido concedido para esse recurso. tooacquire um token de acesso, o aplicativo pode fazer um solicitação toohello v 2.0 token ponto de extremidade, como este:

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

Você pode usar o token de acesso resultante Olá no recurso de toohello de solicitações HTTP. Ele indica confiável toohello recursos que seu aplicativo tenha Olá devida permissão tooperform uma tarefa específica.  

Para obter mais informações sobre Olá OAuth 2.0 do protocolo e como tooget tokens de acesso, consulte Olá [referência de protocolo do ponto de extremidade v 2.0](active-directory-v2-protocols.md).
