---
title: "aaaAuthentication e autorização no serviço de aplicativo do Azure | Microsoft Docs"
description: "Referência conceitual e visão geral da saudação autenticação / autorização de recursos para o serviço de aplicativo do Azure"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Autenticação e autorização no Serviço de Aplicativo do Azure
## <a name="what-is-app-service-authentication--authorization"></a>O que é a Autenticação/Autorização do Serviço de Aplicativo?
Autenticação do serviço de aplicativo / autorização é um recurso que fornece uma maneira para toosign seu aplicativo em usuários para que você não tem o código de toochange no back-end de aplicativo hello. Ele fornece uma maneira fácil tooprotect seu aplicativo e o trabalho com dados por usuário.

O Serviço de Aplicativo usa uma identidade federada, na qual um provedor de identidade de terceiros armazena contas e autentica usuários. aplicativo Hello depende de informações de identidade do provedor Olá para que hello aplicativo não tiver toostore essas informações em si. Serviço de aplicativo oferece suporte a provedores de identidade cinco imediato saudação: Active Directory do Azure, Facebook, Google, Microsoft Account e Twitter. Seu aplicativo pode usar qualquer número desses tooprovide de provedores de identidade seus usuários com opções para como entrarem no. suporte interno a saudação tooexpand, você pode integrar outro provedor de identidade ou [sua própria solução de identidade personalizado][custom-auth].

Se você quiser tooget iniciado imediatamente, consulte um dos Olá tutoriais a seguir:

* [Adicionar aplicativo do iOS autenticação tooyour] [ iOS] (ou [Android], [Windows], [xamarin], [ Xamarin], [xamarin. Forms], ou [Cordova])
* [Autenticação de usuário para Aplicativos de API no Serviço de Aplicativo do Azure][apia-user]
* [Introdução ao Serviço de Aplicativo do Azure - Parte 2][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Como funciona a autenticação no Serviço de Aplicativo
Em ordem tooauthenticate usando um dos provedores de identidade Olá, é necessário primeiro tooknow de provedor de identidade tooconfigure Olá sobre seu aplicativo. provedor de identidade Hello, em seguida, fornecem IDs e segredos que você forneça tooApp serviço. Isso conclui a relação de confiança de saudação para que o serviço de aplicativo possa validar declarações de usuário, como tokens de autenticação, Olá do provedor de identidade.

toosign um usuário usando um desses provedores, o usuário de saudação deve ser redirecionado tooan ponto de extremidade que conecta os usuários para o provedor. Se os clientes estão usando um navegador da web, você pode ter o serviço de aplicativo direcionar automaticamente todos os usuários não autenticados toohello ponto de extremidade entra em usuários. Caso contrário, será necessário toodirect seus clientes muito`{your App Service base URL}/.auth/login/<provider>`, onde `<provider>` é uma saudação valores a seguir: aad, facebook, google, microsoft ou twitter. Os cenários móveis e de API serão explicados em seções posteriores deste artigo.

Os usuários que interagem com seu aplicativo por meio de um navegador da Web terão um cookie definido, para que possam permanecer autenticados conforme navegam no aplicativo. Para outros tipos de cliente, como o dispositivo móvel, um JSON web token (JWT), que deve ser apresentado no hello `X-ZUMO-AUTH` cabeçalho, será emitido toohello cliente. cliente de aplicativos móveis Olá SDKs tratará isso para você. Como alternativa, um token de acesso ou o token de identidade do Active Directory do Azure pode ser diretamente incluído em Olá `Authorization` cabeçalho como uma [token de portador](https://tools.ietf.org/html/rfc6750).

Serviço de aplicativo validará qualquer token que seu aplicativo emite tooauthenticate usuários ou cookie. toorestrict quem pode acessar seu aplicativo, consulte Olá [autorização](#authorization) seção mais adiante neste artigo.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Autenticação móvel com um SDK do provedor
Depois que tudo está configurado em Olá back-end, você pode modificar toosign clientes móveis com o serviço de aplicativo. Há duas abordagens aqui:

* Usar um SDK que um provedor de identidade fornecida publica tooestablish identidade e, em seguida, obtenha acesso tooApp serviço.
* Use uma única linha de código para que esse cliente de aplicativos móveis Olá SDK possa se conectar aos usuários.

> [!TIP]
> A maioria dos aplicativos deve usar um provedor SDK tooget uma experiência mais consistente quando os usuários entrarem, suporte de atualização de toouse e tooget outros benefícios que provedor Olá especifica.
> 
> 

Quando você usa um provedor de SDK, os usuários possam entrar experiência tooan que integra o mais próximo sistema de operacional Olá que o aplicativo hello está em execução. Isso também fornece um token do provedor e algumas informações de usuário no cliente hello, o que torna muito mais fácil gráfico de tooconsume APIs e personalizar a experiência do usuário hello. Ocasionalmente em blogs e fóruns, você verá esse Olá tooas chamado "fluxo de cliente" ou "fluxo direcionada pelo cliente" porque o código no cliente Olá entra em usuários e o código de cliente de saudação tem token de acesso do provedor de tooa.

Depois que um token do provedor é obtido, ela deve toobe enviado tooApp serviço para validação. Depois que o serviço de aplicativo valida o token hello, serviço de aplicativo cria um novo token de serviço de aplicativo que é retornado toohello cliente. SDK de cliente de aplicativos móveis Olá tem auxiliar métodos toomanage essa troca e anexar automaticamente Olá tooall token solicitações toohello aplicativo back-end. Os desenvolvedores também podem manter um token de referência do provedor toohello se eles assim escolhem.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Autenticação móvel sem um SDK do provedor
Se você não quiser tooset um provedor de SDK, você pode permitir recursos de aplicativos móveis saudação do serviço de aplicativo do Azure toosign para você. SDK de cliente de aplicativos móveis Olá abrirá um provedor de toohello de exibição da web de sua escolha e entrar no usuário de saudação. Ocasionalmente em blogs e fóruns, você verá esse tooas chamado hello "fluxo de servidor" ou "orientado para servidor de fluxo" como servidor Olá gerencia processo Olá que conecta os usuários e o SDK de cliente Olá nunca recebe o token de saudação do provedor.

Código toostart que deste fluxo está incluído no tutorial de autenticação Olá para cada plataforma. No final de saudação do fluxo de hello, SDK de cliente Olá tem um token de serviço de aplicativo e token Olá é anexado automaticamente tooall solicitações toohello aplicativo back-end.

### <a name="service-to-service-authentication"></a>Autenticação serviço a serviço
Embora você pode dar aos usuários acesso tooyour aplicativo, você pode também confiar toocall de outro aplicativo sua própria API. Por exemplo, você poderia ter um aplicativo Web chamando uma API em outro aplicativo Web. Nesse cenário, você pode usar as credenciais para uma conta de serviço em vez de credenciais de usuário tooget um token. Uma conta de serviço também é conhecida como *entidade de serviço* no jargão do Azure Active Directory, e a autenticação que usa essa conta também é chamada de cenário de serviço a serviço.

> [!IMPORTANT]
> Como os aplicativos móveis são executados em dispositivos do cliente, os aplicativos móveis *não* contam como aplicativos confiáveis e não devem usar um fluxo da entidade de serviço. Em vez disso, eles devem usar um fluxo de usuário detalhado anteriormente.
> 
> 

Para cenários de serviço a serviço, o Serviço de Aplicativo pode proteger seu aplicativo usando o Azure Active Directory. aplicativo de chamada Hello só precisa tooprovide um token de autorização principal de serviço do Active Directory do Azure que é obtido, fornecendo a ID de saudação do cliente e cliente secreto do Active Directory do Azure. Um exemplo desse cenário que usa a API do ASP.NET apps é explicado pelo tutorial hello, [autenticação principal do serviço para aplicativos de API][apia-service].

Se você quiser toouse toohandle de autenticação do serviço de aplicativo um cenário de serviços, você pode usar certificados de cliente ou a autenticação básica. Para obter informações sobre certificados de cliente no Azure, consulte [como tooConfigure autenticação mútua do TLS para aplicativos Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Para saber mais sobre a autenticação básica no ASP.NET, confira [Filtros de autenticação na API Web 2 ASP.NET](http://www.asp.net/web-api/overview/security/authentication-filters).

Autenticação de conta de serviço de um aplicativo do serviço de aplicativo lógica aplicativo tooan API é um caso especial que é detalhado no [usando sua API personalizada hospedado no serviço de aplicativo com aplicativos lógicos](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Como funciona a autorização no Serviço de Aplicativo
Você tem controle total sobre solicitações de saudação que pode acessar o aplicativo. Autenticação do serviço de aplicativo / autorização pode ser configurada com nenhum dos Olá comportamentos a seguir:

* Permitir que somente solicitações autenticadas tooreach seu aplicativo.
  
    Se um navegador recebe uma solicitação anônima, o serviço de aplicativo redirecionará página tooa para provedor de identidade Olá que você escolher para que os usuários possam entrar. Se a solicitação de saudação é proveniente de um dispositivo móvel, Olá retornou a resposta é um HTTP *401 não autorizado* resposta.
  
    Com essa opção, você não precisa toowrite qualquer código de autenticação em todos os em seu aplicativo. Se você precisar de autorização mais refinada, informações sobre o usuário Olá são código tooyour disponíveis.
* Permitir tooreach de todas as solicitações do aplicativo, mas validar solicitações autenticadas e passa informações de autenticação nos cabeçalhos de saudação HTTP.
  
    Essa opção adia o código do aplicativo de tooyour de decisões de autorização. Ele oferece mais flexibilidade no tratamento de solicitações anônimas, mas você tiver código toowrite.
* Permitir tooreach de todas as solicitações de seu aplicativo e não executar nenhuma ação nas informações de autenticação em solicitações de saudação.
  
    Nesse caso, Olá autenticação / autorização de recurso está desativado. tarefas de saudação de autenticação e autorização são totalmente o código do aplicativo de tooyour.

comportamentos anterior Olá são controlados pelo Olá **tootake de ação quando a solicitação não está autenticada** opção Olá portal do Azure. Se você escolher * * fazer login *nome do provedor* * *, todas as solicitações tem toobe autenticado. **Permitir solicitação (nenhuma ação)** adia o código de tooyour de decisão de autorização hello, mas ainda fornece informações de autenticação. Se você quiser toohave seu código lidar com tudo, você pode desabilitar Olá autenticação / recurso de autorização.

## <a name="working-with-user-identities-in-your-application"></a>Trabalhando com identidades de usuário em seu aplicativo
Serviço de aplicativo passa algum aplicativo de tooyour de informações do usuário usando cabeçalhos especiais. As solicitações externas proíbem esses cabeçalhos e só estarão presentes se definidas pela Autenticação/Autorização do Serviço de Aplicativo. Alguns cabeçalhos de exemplo incluem:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Código que está escrito em qualquer idioma ou a estrutura pode obter informações de saudação que ele precisa desses cabeçalhos. Para aplicativos ASP.NET 4.6, Olá **ClaimsPrincipal** é definido automaticamente com os valores apropriados hello.

Seu aplicativo também pode obter detalhes adicionais de usuário por meio de um HTTP GET em Olá `/.auth/me` ponto de extremidade de seu aplicativo. Um token válido que foi incluído na solicitação de saudação de retorno de uma carga JSON com detalhes sobre o provedor de saudação que está sendo usado, Olá token do provedor subjacente e algumas outras informações do usuário. o servidor de aplicativos móveis SDKs Hello fornecem métodos auxiliares toowork com esses dados. Para obter mais informações, consulte [como toouse Olá SDK do Azure Mobile aplicativos Node.js](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), e [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Documentação e recursos adicionais
### <a name="identity-providers"></a>Provedores de identidade
Olá seguintes tutoriais mostram como provedores de autenticação diferentes de toouse tooconfigure do serviço de aplicativo:

* [Como tooconfigure seu logon do aplicativo toouse Active Directory do Azure][AAD]
* [Como tooconfigure o logon do Facebook toouse aplicativo][Facebook]
* [Como tooconfigure o logon do Google toouse aplicativo][Google]
* [Como tooconfigure seu logon do aplicativo toouse Account da Microsoft][MSA]
* [Como tooconfigure o logon do Twitter toouse aplicativo][Twitter]

Se você quiser toouse um sistema de identidade que Olá aqueles fornecidos aqui, você também pode usar Olá [visualizar o suporte a autenticação personalizada no SDK do servidor do .NET de aplicativos móveis Olá][custom-auth], que pode ser usado em aplicativos da web, aplicativos móveis ou aplicativos de API.

### <a name="web-applications"></a>Aplicativos Web
Olá tutoriais a seguir mostra como tooadd tooa de autenticação de aplicativo web:

* [Introdução ao Serviço de Aplicativo do Azure - Parte 2][web-getstarted]

### <a name="mobile-applications"></a>Aplicativos móveis
Olá tutoriais a seguir mostra como clientes móveis de tooadd autenticação tooyour usando Olá orientado para servidor de fluxo:

* [Adicionar aplicativo do iOS tooyour autenticação][iOS]
* [Adicionar aplicativo do Android autenticação tooyour][Android]
* [Adicionar um aplicativo de Windows Authentication tooyour][Windows]
* [Adicionar autenticação tooyour xamarin aplicativo][xamarin]
* [Adicionar autenticação tooyour xamarin aplicativo][ Xamarin]
* [Adicionar autenticação tooyour xamarin. Forms aplicativo][xamarin. Forms]
* [Adicionar autenticação tooyour Cordova aplicativo][Cordova]

Use Olá recursos a seguir se quiser que o fluxo de cliente direcionado Olá toouse Active Directory do Azure:

* [Saudação de usar a biblioteca de autenticação do Active Directory para iOS][ADAL-iOS]
* [Usar Olá biblioteca de autenticação do Active Directory para Android][ADAL-Android]
* [Use Olá Active Directory autenticação Library para Windows e o Xamarin][ADAL-dotnet]

Use Olá recursos a seguir se quiser que o fluxo de cliente direcionado Olá toouse para o Facebook:

* [Use Olá Facebook SDK para iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Use Olá recursos a seguir se quiser que o fluxo de cliente direcionado Olá toouse do Twitter:

* [Usar o Twitter Fabric para iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Use Olá recursos a seguir se quiser que o fluxo de cliente direcionado Olá toouse para o Google:

* [Use Olá Google entrar SDK para iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>Aplicativos de API
Olá Mostrar tutoriais a seguir como tooprotect seus aplicativos de API:

* [Autenticação de usuário para Aplicativos de API no Serviço de Aplicativo do Azure][apia-user]
* [Autenticação de entidade de serviço para Aplicativos de API no Serviço de Aplicativo do Azure][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[xamarin]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[xamarin. Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
