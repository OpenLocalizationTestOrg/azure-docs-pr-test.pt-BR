---
title: aaaAzure do Active Directory authentication e o Gerenciador de recursos | Microsoft Docs
description: Tooauthentication de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure e Active Directory do Azure para integrar um aplicativo com outras assinaturas do Azure.
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Usar assinaturas de tooaccess de API de autenticação do Gerenciador de recursos
## <a name="introduction"></a>Introdução
Se você for um desenvolvedor de software que precisa toocreate um aplicativo que gerencia os recursos do Azure do cliente, este tópico mostra como tooauthenticate com hello APIs do Gerenciador de recursos do Azure e obter acesso tooresources em outras assinaturas.

Seu aplicativo pode acessar Olá APIs do Gerenciador de recursos de duas maneiras:

1. **Acesso de aplicativo + usuário**: para aplicativos que acessam recursos em nome de um usuário conectado. Essa abordagem funciona para aplicativos, como aplicativos Web e ferramentas de linha de comando, que lidam apenas com "gerenciamento interativo" dos recursos do Azure.
2. **Acesso somente a aplicativos**: para aplicativos que executam serviços daemon e trabalhos agendados. identidade do aplicativo Hello recebe recursos de toohello acesso direto. Essa abordagem funciona para aplicativos que precisam tooAzure de acesso (autônomo) sem cabeçalho de longo prazo.

Este tópico fornece instruções passo a passo toocreate um aplicativo que utiliza esses dois métodos de autorização. Ele mostra como tooperform cada etapa com API REST ou c#. aplicativo ASP.NET MVC completo de saudação está disponível em [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>O aplicativo web de saudação não
Olá web app:

1. Conecta um usuário do Azure.
2. Solicita acesso usuário toogrant Olá web aplicativo tooResource Manager.
3. Obtém o token de acesso de usuário + aplicativo acessando o Resource Manager.
4. Usa toocall token (da etapa 3) o Gerenciador de recursos e a função de tooa principal de serviço do aplicativo de saudação atribuir na assinatura hello, que dá a assinatura toohello de acesso a longo prazo Olá aplicativo.
5. Obtém o token de acesso somente ao aplicativo.
6. Usa recursos de token (da etapa 5) toomanage na assinatura Olá por meio do Gerenciador de recursos.

Aqui está o fluxo de ponta a ponta de saudação do aplicativo da web hello.

![Fluxo de autenticação do Resource Manager](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Como um usuário forneça a id da assinatura Olá assinatura Olá deseja toouse:

![fornecer ID de assinatura](./media/resource-manager-api-authentication/sample-ux-1.png)

Selecione Olá toouse de conta para efetuar login.

![escolher conta](./media/resource-manager-api-authentication/sample-ux-2.png)

Forneça suas credenciais.

![fornecer credenciais](./media/resource-manager-api-authentication/sample-ux-3.png)

Conceda tooyour de acesso do aplicativo hello assinaturas do Azure:

![Conceder acesso](./media/resource-manager-api-authentication/sample-ux-4.png)

Gerencie as assinaturas conectadas:

![Conectar assinatura](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Registrar aplicativo
Antes de iniciar a codificação, registre o aplicativo Web com o Azure AD (Active Directory). o registro do aplicativo Hello cria uma identidade central para seu aplicativo no AD do Azure. Ela contém informações básicas sobre o seu aplicativo como ID do cliente OAuth, URLs de resposta e as credenciais que o aplicativo usa tooauthenticate e acesso a APIs do Gerenciador de recursos do Azure. o registro do aplicativo Hello também registra Olá várias permissões que seu aplicativo precisa ao acessar APIs Microsoft em nome de usuário de saudação.

Como o aplicativo acessa outra assinatura, você deve configurá-lo como um aplicativo multilocatário. validação de toopass, forneça um domínio associado com o Azure Active Directory. domínios de saudação toosee associados com o Active Directory do Azure, o log em toohello [portal clássico](https://manage.windowsazure.com). Selecione o Azure Active Directory e depois **Domínios**.

saudação de exemplo a seguir mostra como tooregister Olá aplicativo usando o PowerShell do Azure. Você deve ter Olá versão mais recente (agosto de 2016) do PowerShell do Azure para este comando toowork.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog em como Olá aplicativo do AD, é necessário senha e a id do aplicativo hello. toosee Olá id do aplicativo que é retornado pelo comando anterior hello, use:

    $app.ApplicationId

saudação de exemplo a seguir mostra como tooregister Olá aplicativo usando a CLI do Azure.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

resultados da saudação incluem hello AppId, que é necessário ao autenticar como aplicativo hello.

### <a name="optional-configuration---certificate-credential"></a>Configuração opcional - credenciais de certificado
O AD do Azure também oferece suporte a credenciais de certificado para aplicativos: criar um certificado autoassinado, mantenha a chave privada hello e adicionar o registro do aplicativo hello tooyour de chave pública do Azure AD. Para autenticação, o aplicativo envia tooAzure uma pequena carga AD assinado usando sua chave privada e o AD do Azure valida a assinatura de saudação usando a chave pública de saudação que você registrou.

Para obter informações sobre como criar um aplicativo do AD com um certificado, consulte [toocreate de usar o Azure PowerShell uma entidade de serviço recursos tooaccess](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) ou [toocreate CLI do Azure Use uma entidade de serviço tooaccess recursos](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Obter ID de locatário da ID de assinatura
toorequest um token que pode ser usado toocall Gerenciador de recursos, seu aplicativo precisa tooknow Olá locatário ID de locatário de saudação do AD do Azure que hospeda Olá assinatura do Azure. É bem provável que os usuários saibam as respectivas IDs de assinatura, mas talvez não saibam as IDs de seus locatários para o Azure Active Directory. tooget Olá id de locatário do usuário, peça ao usuário Olá Olá id da assinatura. Forneça essa id de assinatura ao enviar uma solicitação de assinatura de saudação:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

Falha na solicitação de saudação porque Olá usuário não foi conectado ainda, mas você pode recuperar a id de locatário de saudação da resposta de saudação. Essa exceção, recuperar id de locatário de saudação do valor de cabeçalho de resposta Olá para **WWW-Authenticate**. Consulte esta implementação em Olá [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) método.

## <a name="get-user--app-access-token"></a>Obter token de acesso ao aplicativo + usuário
Seu aplicativo redireciona Olá usuário tooAzure AD com um OAuth 2.0 autorizar solicitar - tooauthenticate Olá as credenciais de usuário e voltar a um código de autorização. Seu aplicativo usa tooget código de autorização Olá um token de acesso para o Gerenciador de recursos. Olá [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) método cria a solicitação de autorização de saudação.

Este tópico mostra o usuário de saudação do hello API REST solicitações tooauthenticate. Você também pode usar a autenticação do auxiliar bibliotecas tooperform em seu código. Para saber mais sobre essas bibliotecas, confira [Bibliotecas de autenticação do Azure Active Directory](../active-directory/active-directory-authentication-libraries.md). Para obter instruções sobre como integrar o gerenciamento de identidades em um aplicativo, confira [Guia do desenvolvedor do Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Solicitação de autorização (OAuth 2.0)
Emita um ponto de extremidade de autorização toohello AD do Azure abrir conectar/OAuth 2.0 autorizar solicitações de identificação:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

parâmetros de cadeia de caracteres de consulta de saudação que estão disponíveis para esta solicitação são descritos em Olá [solicitar um código de autorização](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) tópico.

Olá mostrado no exemplo a seguir como toorequest autorização do OAuth 2.0:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

O AD do Azure autentica o usuário hello e, se necessário, pede Olá usuário toogrant permissão toohello aplicativo. Ele retorna toohello código de autorização Olá URL de resposta do seu aplicativo. Dependendo da saudação solicitado response_mode, o envia de volta Olá dados na cadeia de caracteres de consulta ou como dados de postagem do AD do Azure.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Solicitação de autorização (Open ID Connect)
Se você não só deseja tooaccess Gerenciador de recursos do Azure em nome de usuário hello, mas também permite Olá usuário toosign no aplicativo tooyour usando sua conta do AD do Azure, execute um Open ID autorizar solicitação de conexão. Com o Open ID Connect, seu aplicativo também recebe um id_token do AD do Azure que seu aplicativo pode usar toosign usuário hello.

parâmetros de cadeia de caracteres de consulta de saudação que estão disponíveis para esta solicitação são descritos em Olá [Olá entrar a solicitação de envio](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) tópico.

Eis um exemplo de solicitação Open ID Connect:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

O AD do Azure autentica o usuário hello e, se necessário, pede Olá usuário toogrant permissão toohello aplicativo. Ele retorna toohello código de autorização Olá URL de resposta do seu aplicativo. Dependendo da saudação solicitado response_mode, o envia de volta Olá dados na cadeia de caracteres de consulta ou como dados de postagem do AD do Azure.

Eis um exemplo de resposta Open ID Connect:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Solicitação de token (Fluxo de concessão de código OAuth 2.0)
Agora que seu aplicativo tiver recebido o código de autorização de saudação do AD do Azure, é o token de acesso de saudação do tempo tooget para o Gerenciador de recursos do Azure.  Poste um solicitação Token do OAuth 2.0 código Grant toohello Token de AD do Azure ponto de extremidade:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

parâmetros de cadeia de caracteres de consulta de saudação que estão disponíveis para esta solicitação são descritos em Olá [usar código de autorização Olá](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) tópico.

saudação de exemplo a seguir mostra uma solicitação de token de concessão de código com credencial de senha:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Ao trabalhar com as credenciais de certificado, crie um JSON Web Token (JWT) e o sinal (RSA SHA256) usando Olá a chave privada da credencial de certificado do aplicativo. Olá tipos de declaração de token de saudação são mostrados na [declarações do token de JWT](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Para referência, consulte Olá [código de biblioteca de autenticação do Active Directory (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign de tokens JWT de asserção do cliente.

Consulte Olá [abrir conexão de ID especificação](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) para obter detalhes sobre autenticação de cliente.

saudação de exemplo a seguir mostra uma solicitação de token de concessão de código com credenciais de certificado:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Um exemplo de resposta de token de concessão de código:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Manipular resposta de token de concessão de código
Uma resposta bem-sucedida de token contém o token de acesso de saudação (usuário + aplicativo) para o Gerenciador de recursos do Azure. Seu aplicativo usa esse acesso token tooaccess Gerenciador de recursos em nome de usuário de saudação. tempo de vida de saudação de tokens de acesso emitido pelo AD do Azure é uma hora. É improvável que seu aplicativo da web precisa de token de acesso do toorenew hello (usuário + aplicativo). Se precisar de token de acesso do toorenew Olá, use o token de atualização de saudação que seu aplicativo recebe na resposta de token hello. Poste um solicitação de Token OAuth 2.0 toohello Token de AD do Azure ponto de extremidade:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Olá toouse parâmetros com a solicitação de atualização de saudação são descritos em [atualização token de acesso de saudação](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Olá exemplo a seguir mostra como o token de atualização toouse hello:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Embora os tokens de atualização podem ser usado tooget novos tokens de acesso para o Azure Resource Manager, eles não são adequados para acesso offline por seu aplicativo. tempo de vida de tokens de atualização Olá é limitado e tokens de atualização são usuário toohello associado. Se o usuário Olá deixa a organização hello, aplicativo hello usando o token de atualização Olá perde o acesso. Essa abordagem não é adequada para aplicativos que são usadas por equipes toomanage seus recursos do Azure.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Verifique se o usuário pode atribuir acesso toosubscription
Seu aplicativo agora tem um token tooaccess Gerenciador de recursos do Azure em nome de usuário de saudação. próxima etapa do Hello é tooconnect sua assinatura do aplicativo toohello. Depois de se conectar, seu aplicativo pode gerenciar as assinaturas mesmo quando o usuário Olá não estiver presente (acesso offline a longo prazo).

Para cada tooconnect de assinatura, chame Olá [permissões de lista do Gerenciador de recursos](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine se o usuário Olá tem direitos de gerenciamento de acesso para a assinatura de saudação.

Olá [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) método hello amostra de aplicativo do ASP.NET MVC implementa esta chamada.

Olá mostrado no exemplo a seguir como toorequest permissões de um usuário em uma assinatura. 83cfe939-2402-4581-b761-4f59b0a041e4 é a id de saudação de assinatura de saudação.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Um exemplo de permissões do usuário do hello resposta tooget na assinatura é:

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

permissões de saudação API retorna várias permissões. Cada permissão consiste em ações permitidas (actions) e ações não permitidas (notactions). Se uma ação está presente no hello permitido a lista de ações de permissão e não está presente na lista de notactions Olá dessa permissão, o usuário de saudação é permitido tooperform essa ação. **Microsoft.Authorization/RoleAssignments/Write** ação Olá que que concede acesso rights management. Seu aplicativo deve analisar Olá permissões resultado toolook uma correspondência de regex nessa cadeia de caracteres de ação em ações hello e notactions de cada permissão.

## <a name="get-app-only-access-token"></a>Obter token de acesso somente ao aplicativo
Agora, você sabe se o usuário Olá pode atribuir acesso toohello assinatura do Azure. Olá próximas etapas são:

1. Atribua Olá apropriado RBAC função tooyour identidade do aplicativo na assinatura de saudação.
2. Valide a atribuição de acesso de saudação consultando a permissão do aplicativo hello assinatura hello ou acessando o Gerenciador de recursos usando o token somente de aplicativo.
3. Conexão de registro Olá em sua estrutura de dados de aplicativos "assinaturas conectado" - persistência id Olá de assinatura de saudação.

Vamos analisar mais detalhadamente a primeira etapa de saudação. tooassign Olá apropriado RBAC função toohello identidade do aplicativo, você deve determinar:

* id de objeto de saudação da identidade do aplicativo no Active Directory do Azure do usuário Olá
* Olá identificador da função RBAC Olá que seu aplicativo requer assinatura Olá

Quando o aplicativo autentica um usuário em um Azure AD, ele cria um objeto de entidade de serviço para o aplicativo nesse Azure AD. O Azure permite RBAC funções toobe atribuído entidades tooservice aplicativos de toocorresponding toogrant acesso direto em recursos do Azure. Esta ação é exatamente o que desejamos toodo. Consulta hello Azure AD Graph API toodetermine Olá identificador da entidade de serviço de saudação do seu aplicativo no usuário conectado Olá 's AD do Azure.

Você só tem um token de acesso para o Gerenciador de recursos do Azure - você precisa de uma novo saudação de toocall token de acesso do Azure AD Graph API. Cada aplicativo no AD do Azure tem permissão tooquery seu próprio objeto de entidade de serviço, para que um token de acesso somente de aplicativo é suficiente.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Obter o token de acesso somente de aplicativo para a API do Azure AD Graph
tooauthenticate seu aplicativo e obter um token tooAzure AD Graph API, emitir um endpoint token tooAzure AD de solicitação de token OAuth 2.0 de concessão de credenciais de cliente fluxo (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/Token**).

Olá [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) método hello aplicativo de exemplo do ASP.net MVC obtém um aplicativo somente acesso de token para o uso da API do Graph hello biblioteca de autenticação do Active Directory para .NET.

parâmetros de cadeia de caracteres de consulta de saudação que estão disponíveis para esta solicitação são descritos em Olá [solicitar um Token de acesso](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) tópico.

Um exemplo de solicitação de token de concessão de credencial de cliente:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Um exemplo de resposta de token de concessão de credencial de cliente:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Obter a ID de objeto da entidade de serviço de aplicativo no Azure AD do usuário
Agora, use Olá Olá de tooquery de token de acesso somente de aplicativo [entidades de serviço do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) saudação do API toodetermine Id de objeto da entidade de serviço do aplicativo hello no diretório de saudação.

Olá [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) método hello aplicativo de exemplo do ASP.net MVC implementa esta chamada.

Olá mostrado no exemplo a seguir como toorequest entidade de serviço do aplicativo. a0448380-c346-4f9f-b897-c18733de9394 é a id de cliente de saudação do aplicativo hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Olá exemplo a seguir mostra uma resposta toohello solicitação de serviço do aplicativo principal

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Obter o identificador de função RBAC do Azure
tooassign Olá apropriado RBAC tooyour serviço de função principal, você deve determinar o identificador de saudação da função de RBAC do Azure de saudação.

função RBAC de direito Hello, para seu aplicativo:

* Se seu aplicativo monitora apenas assinatura hello, sem fazer alterações, ele requer somente permissões de leitura de assinatura de saudação. Atribuir Olá **leitor** função.
* Se seu aplicativo gerencia a assinatura do Azure hello, criação/modificação/exclusão de entidades, ele requer permissões de Colaborador hello.
  * toomanage um determinado tipo de recurso, atribuir funções de Colaborador de recursos específicos de saudação (colaborador da máquina Virtual, colaborador de rede Virtual, colaborador da conta de armazenamento, etc.)
  * toomanage qualquer tipo de recurso, atribuir Olá **Colaborador** função.

atribuição de função de saudação para seu aplicativo é toousers visível, para que selecionar Olá privilégio necessário pelo menos.

Chamar hello [definição de função do Gerenciador de recursos API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist todas as funções de RBAC do Azure e pesquisa, em seguida, itere Olá Olá de toofind do resultado desejado a definição de função por nome.

Olá [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) método hello amostra de aplicativo do ASP.net MVC implementa esta chamada.

solicitação a seguir Olá exemplo mostra como identificador de função tooget RBAC do Azure. 09cbd307-aa71-4aca-b346-5f253e6e3ebb é a id de saudação de assinatura de saudação.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

resposta de saudação está no hello formato a seguir:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Não é necessário toocall essa API em uma base contínua. Depois de determinar Olá GUID conhecida Olá da definição da função, você pode construir a id de definição de função hello como:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Aqui estão os guids de saudação bem conhecidos de funções internas usadas:

| Função | Guid |
| --- | --- |
| Leitor |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Colaborador |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Colaborador de Máquina Virtual |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Colaborador de Rede Virtual |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Colaborador da Conta de Armazenamento |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Colaborador do Site |de139f84-1756-47ae-9be6-808fbbe84772 |
| Colaborador do Plano de Web |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| Colaborador do SQL Server |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| Colaborador do banco de dados SQL |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>Atribuir RBAC função tooapplication
Você tem tudo o que precisa tooassign Olá apropriado RBAC função tooyour entidade de serviço usando Olá [Gerenciador de recursos de criar a atribuição de função](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Olá [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) método hello amostra de aplicativo do ASP.net MVC implementa esta chamada.

Um exemplo solicitação tooassign RBAC função tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

Na solicitação de Olá Olá valores a seguir é usado:

| Guid | Descrição |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |id de saudação de assinatura de saudação |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |id de objeto de saudação da entidade de serviço de saudação do aplicativo hello |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |id de saudação da função de leitor de saudação |
| 4f87261d-2816-465d-8311-70a27558df4c |um novo guid criado para a nova atribuição de função hello |

resposta de saudação está no hello formato a seguir:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Obter token de acesso somente de aplicativo para o Azure Resource Manager
toovalidate que o aplicativo tem acesso de saudação desejado na assinatura hello, executar uma tarefa de teste Olá assinatura usando um token somente de aplicativo.

tooget um token de acesso somente de aplicativo, siga as instruções da seção [obter token de acesso de somente de aplicativo do Azure AD Graph API](#app-azure-ad-graph), com um valor diferente para o parâmetro de recurso hello:

    https://management.core.windows.net/

Olá [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) método hello aplicativo de exemplo do ASP.NET MVC obtém um acesso somente de aplicativo token para usar o Gerenciador de recursos do Azure hello biblioteca de autenticação do Active Directory para .net.

#### <a name="get-applications-permissions-on-subscription"></a>Obter permissões do aplicativo na assinatura
toocheck que seu aplicativo tem Olá desejado de acesso em uma assinatura do Azure, você também pode chamar hello [permissões do Gerenciador de recursos](https://docs.microsoft.com/rest/api/authorization/permissions) API. Essa abordagem é toohow semelhante, você determinou se usuário Olá tem direitos de gerenciamento de acesso para a assinatura de saudação. No entanto, neste momento, chame hello permissões API com o token de acesso somente de aplicativo hello recebido na etapa anterior hello.

Olá [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) método hello amostra de aplicativo do ASP.NET MVC implementa esta chamada.

## <a name="manage-connected-subscriptions"></a>Gerenciar assinaturas conectadas
Quando a função apropriada de RBAC Olá é atribuída a entidade de serviço do aplicativo tooyour assinatura hello, seu aplicativo pode manter monitorar e gerenciar usando tokens de acesso somente de aplicativo para o Gerenciador de recursos do Azure.

Se um proprietário da assinatura remove a atribuição de função do aplicativo usando o portal clássico do hello ou ferramentas de linha de comando, o aplicativo é tooaccess não é mais possível essa assinatura. Nesse caso, você deve notificar o usuário Olá que conexão Olá com assinatura Olá foi danificada do aplicativo fora do hello e conceder a eles uma opção muito "reparar" conexão hello. "Reparar" seria simplesmente crie novamente a atribuição de função hello que foi excluída offline.

Assim como você ativou o aplicativo de tooyour hello usuário tooconnect assinaturas, você deve permitir assinaturas de toodisconnect usuário Olá muito. De um acesso gerenciamento ponto de Vista, desconecte significa remover a atribuição de função de saudação entidade de serviço do aplicativo hello tem assinatura hello. Opcionalmente, pode ser removido qualquer estado no aplicativo hello para assinatura Olá muito.
Somente os usuários com permissão de gerenciamento de acesso na assinatura de saudação são toodisconnect capaz de assinatura de saudação.

Olá [RevokeRoleFromServicePrincipalOnSubscription método](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) de saudação ASP.net MVC o aplicativo de exemplo implementa esta chamada.

Pronto! Agora os usuários podem agora se conectar e gerenciar suas assinaturas do Azure com seu aplicativo facilmente.
