---
title: Diretrizes para acesso condicional do Azure Active Directory de aaaDeveloper | Microsoft Docs
description: "Diretrizes do desenvolvedor e cenários para acesso condicional do Azure AD"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Diretrizes do desenvolvedor para acesso condicional do Azure Active Directory

Azure AD (Active Directory) oferece toosecure de várias maneiras de seu aplicativo e proteger um serviço.  Um desses recursos exclusivos é o acesso condicional.  Acesso condicional permite que os desenvolvedores e os serviços de tooprotect de clientes corporativos em várias maneiras, incluindo:

* Autenticação multifator
* Permitindo que apenas o Intune registrados serviços específicos de tooaccess de dispositivos
* Restrição de locais de usuário e intervalos de IP

Para obter mais informações sobre recursos completos de saudação do acesso condicional, consulte [acesso condicional no portal clássico do Azure de saudação](../active-directory-conditional-access.md). 

Neste artigo, vamos nos concentrar no que acesso condicional significa toodevelopers criando aplicativos do AD do Azure.  O artigo pressupõe o conhecimento de aplicativos de [único locatário](active-directory-integrating-applications.md) e [multilocatário](active-directory-devhowto-multi-tenant-overview.md), além de [padrões comuns de autenticação](active-directory-authentication-scenarios.md).

Nos aprofundaremos nas impacto de saudação de acessar os recursos que você não tem controle sobre o que podem ter políticas de acesso condicional aplicadas.  Além disso, exploraremos implicações de saudação do acesso condicional no hello em nome de fluxo, os aplicativos web, acessando Olá Microsoft Graph e chamar APIs.

## <a name="how-does-conditional-access-impact-an-app"></a>Como o acesso condicional afeta um aplicativo?

### <a name="app-topologies-impacted"></a>Topologias de aplicativo afetadas

Na maioria dos casos, o acesso condicional não altera o comportamento do aplicativo ou requer alterações de desenvolvedor hello.  Somente em determinados casos quando um aplicativo indiretamente ou silenciosamente solicita um token para um serviço, um aplicativo requer alterações no código toohandle condicional "desafios ao acesso".  O que pode ser tão simples quanto executar uma solicitação de entrada interativa. 

Especificamente, hello cenários a seguir exigem acesso condicional do código toohandle "desafios": 

* Aplicativos que estão acessando Olá Microsoft Graph
* Aplicativos de execução de fluxo de saudação em nome de
* Aplicativos acessando vários serviços/recursos
* Aplicativos de única página usando ADAL.js

Políticas de acesso condicional pode ser aplicado toohello aplicativo, mas também pode ser aplicado tooa web API seu aplicativo acessa. Saiba mais sobre toolearn como tooconfigure uma política de acesso condicional, consulte [guia de Introdução ao acesso condicional do Azure Active Directory](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

Dependendo do cenário de saudação, um cliente empresarial pode aplicar e remover as políticas de acesso condicional a qualquer momento.  Para o funcionamento de toocontinue de seu aplicativo quando uma nova política é aplicada, é necessário o tratamento de desafio"tooimplement Olá". Olá exemplos a seguir ilustra o tratamento de desafio. 

### <a name="conditional-access-examples"></a>Exemplos de acesso condicional

Alguns cenários exigem alterações de código toohandle acesso condicional, enquanto outros funcionam como está.  Aqui estão alguns cenários usando a autenticação multifator do acesso condicional toodo que fornece informações sobre diferença hello.

* Você está criando um aplicativo iOS de único locatário e aplica uma política de acesso condicional.  aplicativo Hello entra em um usuário e não solicitar acesso tooan API.  Quando Olá usuário faz logon, política de saudação é invocada automaticamente e usuário Olá precisa tooperform autenticação de multifator (MFA). 
* Você está criando um aplicativo web de vários locatários que usa Olá Microsoft Graph tooaccess Exchange, entre outros serviços.  Um cliente empresarial que adota esse aplicativo define uma política no SharePoint Online.  Quando o aplicativo da web de saudação solicita um token do MS Graph, uma política em qualquer Microsoft Service é aplicada (especificamente serviços que podem ser acessados por meio do gráfico).  Esse usuário final é solicitado a executar a MFA. No caso de Olá, usuários finais de saudação é assinado com tokens válidos, um desafio"declarações" é retornado toohello web app.  
* Você está criando um aplicativo nativo que usa uma saudação de tooaccess do serviço de camada intermediária Microsoft Graph.  Um cliente empresarial na empresa hello usando este aplicativo aplica-se um tooExchange política Online.  Quando um usuário final faz logon, o aplicativo nativo Olá solicitações de camada intermediária do acesso toohello e envia o token de saudação.  camada intermediária Olá executa em nome de fluxo toorequest acesso toohello MS Graph.  Neste ponto, um desafio"declarações" é apresentado a camada intermediária toohello. camada intermediária Olá envia Olá desafio toohello back aplicativo nativo, que deve toocomply com a política de acesso condicional hello.

### <a name="complying-with-a-conditional-access-policy"></a>Estabelecendo conformidade com uma política de acesso condicional

Para várias topologias de aplicativo diferente, uma política de acesso condicional é avaliada quando a sessão de saudação for estabelecida.  Como uma política de acesso condicional funciona com granularidade de saudação de aplicativos e serviços, no qual ele é chamado de ponto de saudação depende intensamente no cenário de saudação estiver tentando tooaccomplish.

Quando o aplicativo tenta tooaccess um serviço com uma política de acesso condicional, ele pode encontrar um desafio de acesso condicional.  Esse desafio é codificado em Olá `claims` parâmetro que vem em uma resposta do AD do Azure ou Olá Microsoft Graph.  Veja um exemplo desse parâmetro de desafio: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Os desenvolvedores podem assumir esse desafio e acrescentá-lo para um novo tooAzure de solicitação AD.  Passar esse estado solicita saudação do usuário final tooperform toocomply de necessária qualquer ação com a política de acesso condicional hello. Nos seguintes cenários de hello, detalhes específicos do erro hello e como tooextract Olá parâmetro são explicados. 

## <a name="scenarios"></a>Cenários

### <a name="prerequisites"></a>Pré-requisitos

O acesso condicional do Azure AD é um recurso incluído no [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Você pode aprender mais sobre licenciamento requisitos Olá [relatório de uso não licenciado](../active-directory-conditional-access-unlicensed-usage-report.md).  Os desenvolvedores podem ingressar Olá [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), que inclui toohello uma assinatura gratuita que inclui o Azure AD Premium Enterprise Mobility Suite.

### <a name="considerations-for-specific-scenarios"></a>Considerações para cenários específicos

Olá, somente as informações a seguir se aplica a esses cenários de acesso condicional:

* Aplicativos que estão acessando Olá Microsoft Graph
* Aplicativos de execução de fluxo de saudação em nome de
* Aplicativos acessando vários serviços/recursos
* Aplicativos de única página usando ADAL.js

Em Olá seções a seguir, vamos comum cenários nos quais são mais complexos.  núcleo de saudação princípio operacional é acesso condicional políticas são avaliadas em tempo de Olá Olá token é solicitado para o serviço de saudação que tem uma política de acesso condicional aplicada, a menos que ele está sendo acessado por meio de saudação do Microsoft Graph.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Cenário: Aplicativo acessando Olá Microsoft Graph

Nesse cenário, vamos percorrer caso hello quando um aplicativo web solicita acesso toohello Microsoft Graph. política de acesso condicional Olá nesse caso pode ser atribuída tooSharePoint, Exchange ou outro serviço que é acessado como uma carga de trabalho por meio de saudação do Microsoft Graph.  Neste exemplo, vamos supor que haja uma política de acesso condicional no Sharepoint Online.

![Acessando o diagrama de fluxo do Microsoft Graph saudação do aplicativo](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

aplicativo Hello primeiro solicita autorização toohello Microsoft Graph que requer acesso a uma carga de trabalho downstream sem acesso condicional.  solicitação de saudação terá êxito sem invocar qualquer política e aplicativo hello recebe tokens do Microsoft Graph.  Neste ponto, aplicativo hello pode usar o token de acesso Olá em uma solicitação de portador para ponto de extremidade de saudação solicitado. Agora, Olá aplicativo precisa tooaccess um ponto de extremidade do Sharepoint Online da Microsoft Graph, por exemplo:`https://graph.microsoft.com/v1.0/me/mySite`

aplicativo Hello já tem um token válido para Olá Microsoft Graph, para executar nova solicitação de saudação sem ser emitido um novo token. Esta solicitação falhará e um desafio de declarações é emitido a partir do Microsoft Graph na forma de saudação de um HTTP 403 Proibido com um ```WWW-Authenticate``` desafio.
Aqui está um exemplo de resposta de saudação: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Olá declarações desafio está dentro de saudação ```WWW-Authenticate``` cabeçalho, que pode ser analisado tooextract Olá declarações parâmetro para a próxima solicitação de saudação.  Quando estiver anexado toohello nova solicitação, AD do Azure sabe política de acesso condicional tooevaluate hello quando entrar no usuário hello e aplicativo hello agora está em conformidade com a política de acesso condicional hello.  Ponto de extremidade toohello de solicitação de saudação do Sharepoint Online de repetição é bem-sucedida.

Para obter exemplos de código que demonstram como toohandle Olá declarações desafio, consulte toohello [exemplo de código de área de trabalho do .NET](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) ADAL .NET ou Olá [em nome de código de exemplo](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) para .NET ADAL.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Cenário: Aplicativo executar o fluxo de saudação em nome de

Nesse cenário, vemos caso Olá no qual um aplicativo nativo chama uma API da serviços web.  Por sua vez, esse serviço faz [hello "em nome de" fluxo](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall um serviço de downstream.  Em nosso caso, estamos aplicou nosso serviço downstream do acesso condicional política toohello (Web API 2) e estiver usando um aplicativo nativo em vez de um aplicativo de servidor/daemon. 

![Olá em nome de diagrama de fluxo de execução do aplicativo](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

solicitação de token inicial Olá para API Web 1 não solicita informações do usuário final Olá para autenticação multifator como API Web 1 não pode atingir sempre Olá API de downstream.  Depois que a API Web 1 tenta toorequest um usuário de token em nome de saudação para API Web 2, falha na solicitação de saudação como usuário Olá não foi assinada com autenticação multifator.

O Azure AD retorna uma resposta HTTP com alguns dados interessantes: 

> [!NOTE]
> Neste exemplo é uma descrição de erro de autenticação multifator, mas não há uma ampla gama de `interaction_required` acesso possíveis de tooconditional pertencem.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Em nossa API Web 1, podemos captura erro Olá `error=interaction_required`e enviar Olá back `claims` aplicativo de área de trabalho de toohello de desafio.  Nesse ponto, pode fazer um novo aplicativo de área de trabalho Olá `acquireToken()` chamar e acrescentar Olá `claims`desafio como um parâmetro de cadeia de caracteres de consulta adicional.  Essa nova solicitação requer autenticação de multifator Olá usuário toodo e, em seguida, enviar esse novo token back tooWeb API 1 e a saudação completa em nome de fluxo.

tootry esse cenário, consulte nosso [exemplo de código do .NET](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Ele demonstra como toopass Olá desafio de declarações do aplicativo nativo do API Web 1 toohello e construir uma nova solicitação de dentro do aplicativo de cliente hello. 

### <a name="scenario-app-accessing-multiple-services"></a>Cenário: aplicativo acessando vários serviços

Nesse cenário, vemos caso Olá em que um aplicativo web acessa dois serviços um dos quais tem uma política de acesso condicional atribuída.  Dependendo de sua lógica de aplicativo, pode existir um caminho no qual seu aplicativo não exigir acesso tooboth web services.  Nesse cenário, em que você solicitar um token de ordem de saudação desempenha um papel importante na experiência do usuário final de saudação.

Vamos supor que temos o serviço Web A e B, e o serviço Web B tem nossa política de acesso condicional aplicada.  Durante a saudação inicial interativa de solicitações de autenticação requer o consentimento para ambos os serviços, a política de acesso condicional de saudação não é necessário em todos os casos.  Se o aplicativo hello solicita um token para o serviço web B, diretiva Olá é invocada, e as solicitações subsequentes de serviço da web A também será bem-sucedida da seguinte maneira.

![Diagrama do fluxo de aplicativo acessando vários serviços](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

Como alternativa, se o aplicativo hello inicialmente solicita um token para um de serviço da web, usuários finais de saudação não invocar política de acesso condicional hello.  Isso permite que o desenvolvedor do aplicativo hello experiência do toocontrol saudação do usuário final e não forçar toobe de política de acesso condicional Olá invocado em todos os casos. Olá difícil ocorre se o aplicativo hello subsequentemente solicita um token para o serviço web B. Neste ponto, usuários finais de saudação precisa toocomply com a política de acesso condicional hello.  Quando o aplicativo hello tenta muito`acquireToken`, ele pode gerar hello (ilustrado no diagrama a seguir de saudação) de erro a seguir: 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![Aplicativo acessando vários serviços que solicitam um novo token](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Se o aplicativo hello está usando a biblioteca ADAL hello, um token de saudação tooacquire falha será sempre repetido interativamente.  Quando essa solicitação interativa ocorre, usuários finais de saudação tem Olá oportunidade toocomply com acesso condicional hello.  Isso é verdadeiro, a menos que seja de solicitação de saudação um `AcquireTokenSilentAsync` ou `PromptBehavior.Never` caso em que o aplicativo hello precisa tooperform interativo ```AcquireToken``` toogive Olá uso final Olá oportunidade toocomply com a política de saudação de solicitação. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Cenário: SPA (Aplicativo de Única Página) usando ADAL.js

Nesse cenário, percorremos caso hello quando temos um aplicativo de página única (SPA), usando o ADAL.js toocall um acesso condicional protegidos API da web.  Essa é uma arquitetura simple, mas tem algumas nuances que precisam toobe levado em consideração ao desenvolver uma solução alternativa para o acesso condicional.

No ADAL.js, há algumas funções que obtêm tokens: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)` e `acquireTokenRedirect(…)`. 

* `login()` obtém um token de ID por meio de uma solicitação de entrada interativa, mas não obtém tokens de acesso para qualquer serviço (incluindo uma API Web protegida por acesso condicional).  
* `acquireToken(…)`pode ser usado toosilently obter um token de acesso que significa que ele não mostrar interface do usuário em nenhuma circunstância.  
* `acquireTokenPopup(…)`e `acquireTokenRedirect(…)` são ambos usados toointeractively solicitar um token para um recurso que significa que eles sempre mostrarem a entrada da interface do usuário.

Quando um aplicativo precisa ter um toocall de token de acesso uma API da Web, ele tenta uma `acquireToken(…)`.  Se a sessão token Olá expirou ou é necessário toocomply com uma política de acesso condicional, Olá *acquireToken* função falhar e Olá aplicativo usa `acquireTokenPopup()` ou `acquireTokenRedirect()`.

![Diagrama do fluxo de aplicativo de única página usando ADAL](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Vamos examinar um exemplo com nosso cenário de acesso condicional.  usuário final de saudação apenas descarregou no site hello e não tem uma sessão.  Executamos uma chamada `login()`, obtemos um token de ID sem autenticação multifator.  Em seguida, o usuário de saudação atinge um botão que requer Olá aplicativo toorequest dados de uma API da web.  Olá aplicativo tenta toodo um `acquireToken()` chamada mas falha porque o usuário Olá não realizou ainda a autenticação multifator e precisa toocomply com a política de acesso condicional hello.

AD do Azure envia back Olá resposta HTTP a seguir: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

Nosso aplicativo precisa Olá toocatch `error=interaction_required`.  Olá aplicativo pode usar o `acquireTokenPopup()` ou `acquireTokenRedirect()` Olá no mesmo recurso.  usuário de saudação é forçado toodo uma autenticação multifator. Depois que o usuário Olá conclui a autenticação multifator hello, aplicativo hello é emitido uma nova recurso do token de acesso para Olá solicitado.

tootry esse cenário, consulte nosso [em nome de código de exemplo do SPA JS](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Este exemplo de código usa a política de acesso condicional hello e você registrou anteriormente com um toodemonstrate JS SPA neste cenário de API da web. Ele mostra como declarações de saudação do identificador tooproperly desafiam e obtém um token de acesso que pode ser usado para a API da Web. Como alternativa, Olá de check-out geral [Angular.js exemplo de código](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) para obter orientação sobre um SPA Angular


## <a name="see-also"></a>Consulte também

* toolearn mais sobre os recursos de hello, consulte [acesso condicional no AD do Azure](../active-directory-conditional-access.md).
* Para obter mais exemplos de código do Azure AD, confira o [repositório Github de exemplos de código](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Para obter mais informações sobre Olá documentação de referência de saudação do SDK do ADAL e acesso, consulte [guia biblioteca](active-directory-authentication-libraries.md).
* toolearn mais sobre cenários multilocatário, consulte [como toosign em usuários usando Olá multilocatário padrão](active-directory-devhowto-multi-tenant-overview.md).
