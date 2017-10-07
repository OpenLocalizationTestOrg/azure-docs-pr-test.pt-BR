---
title: "B2C de diretório ativo do Azure: Saudação de uso API do Graph | Microsoft Docs"
description: "Como toocall hello Graph API para um locatário B2C usando um processo de saudação de tooautomate de identidade de aplicativo."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>B2C do AD do Azure: Use Olá API do Graph
Locatários do Active Directory (AD do Azure) B2C do Azure tendem toobe muito grande. Isso significa que muitas tarefas comuns de gerenciamento de locatário necessário toobe executada de forma programática. O principal exemplo é o gerenciamento de usuário. Talvez seja necessário toomigrate um locatário de B2C tooa do repositório do usuário existente. Você pode desejar toohost registro de usuário em sua página e criar contas de usuário no diretório do Azure AD B2C em segundo plano da saudação. Esses tipos de tarefas exigem Olá capacidade toocreate, ler, atualizar e excluir contas de usuário. Você pode fazer essas tarefas usando hello Azure AD Graph API.

Para B2C locatários, há dois modos principais de se comunicar com hello API do Graph.

* Para tarefas interativas, executar uma vez, você deve agir como uma conta de administrador no locatário de B2C hello quando você executa tarefas de saudação. Esse modo requer toosign um administrador com credenciais antes que o administrador pode executar qualquer toohello chamadas API do Graph.
* Para tarefas automatizadas, contínuas, você deve usar algum tipo de conta de serviço que você fornecer com tarefas de gerenciamento de tooperform Olá os privilégios necessários. No AD do Azure, você pode fazer isso por registrar um aplicativo e autenticação tooAzure AD. Isso é feito usando um **ID do aplicativo** que usa Olá [as credenciais do cliente OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). Nesse caso, aplicativo hello atua como em si, não como um usuário, Olá toocall API do Graph.

Neste artigo, discutiremos como tooperform Olá caso de uso automatizada. toodemonstrate, criaremos um .NET 4.5 `B2CGraphClient` que executa o usuário criar, ler, atualizar e excluir operações (CRUD). cliente Olá terá uma interface de linha de comando do Windows (CLI) que permite que você tooinvoke vários métodos. No entanto, o código de saudação é gravado toobehave de maneira interativa, automatizada.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obter um locatário do Azure AD B2C
Antes de criar aplicativos ou usuários, ou interagir com o Azure AD em todos os, será necessário um locatário Azure AD B2C e uma conta de administrador global no locatário hello. Se você ainda não tiver um locatário, confira a [introdução ao Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Registrar seu aplicativo em seu locatário
Depois que você tiver um locatário B2C, você precisa tooregister seu aplicativo por meio de saudação [Portal do Azure](https://portal.azure.com).

> [!IMPORTANT]
> toouse Olá Graph API com seu locatário B2C, você precisará tooregister um aplicativo dedicado usando Olá genérico *registros do aplicativo* folha em Olá Portal do Azure, **não** do Azure AD B2C  *Aplicativos* folha. Não é possível reutilizar Olá já existente B2C aplicativos que você registrou no saudação do Azure AD B2C *aplicativos* folha.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do Azure AD B2C selecionando sua conta no canto superior direito de saudação da página de saudação.
3. No painel de navegação esquerdo hello, escolha **mais serviços**, clique em **registros do aplicativo**e clique em **adicionar**.
4. Siga os prompts de saudação e criar um novo aplicativo. 
    1. Selecione **aplicativo Web / API** como Olá tipo de aplicativo.    
    2. Forneça **qualquer URI de redirecionamento** (por exemplo, https://B2CGraphAPI), pois isso não é relevante para este exemplo.  
5. Olá aplicativo serão agora aparecem na lista de saudação de aplicativos, clique nela Olá tooobtain **ID do aplicativo** (também conhecido como ID do cliente). Copie-a, pois precisará dela em uma seção posterior.
6. Na folha de configurações de saudação, clique em **chaves** e adicione uma nova chave (também conhecido como o segredo do cliente). Copie-a também para uso em uma seção posterior.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Configurar as permissões de criação, leitura e atualização para seu aplicativo
Agora você precisa tooconfigure seu tooget aplicativo que todos Olá necessário toocreate permissões, ler, atualizar e excluir usuários.

1. Continuar em Olá folha de registros do aplicativo do portal do Azure, selecione seu aplicativo.
2. Na folha de configurações de saudação, clique em **as permissões necessárias**.
3. Na folha de permissões necessárias de saudação, clique em **Windows Azure Active Directory**.
4. Na folha de habilitar o acesso de saudação, selecione Olá **ler e gravar dados de diretório** permissão de **permissões de aplicativo** e clique em **salvar**.
5. Por fim, na folha de permissões necessárias hello, clique em Olá **conceder permissões** botão.

Agora você tem um aplicativo que tem permissão a usuários toocreate, leitura e atualização do seu locatário B2C.

## <a name="configure-delete-permissions-for-your-application"></a>Configurar permissões de exclusão para seu aplicativo
Atualmente, Olá *ler e gravar dados de diretório* permissão **não** incluem hello capacidade toodo qualquer exclusão como excluir usuários. Se você quiser toogive os usuários do aplicativo hello capacidade toodelete, você precisará toodo estas etapas adicionais que envolvem o PowerShell, caso contrário, você pode ignorar toohello próxima seção.

Primeiro, baixe e instale Olá [assistente Microsoft Online Services entrar](http://go.microsoft.com/fwlink/?LinkID=286152). Baixe e instale Olá [módulo do Active Directory do Azure de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

Depois de instalar o módulo do PowerShell hello, abra o PowerShell e conecte-se tooyour B2C locatário. Depois de executar `Get-Credential`, você será solicitado um nome de usuário e senha, insira Olá nome de usuário e senha da sua conta de administrador de inquilinos B2C.

> [!IMPORTANT]
> Você precisa de conta de administrador do locatário toouse um B2C é **local** toohello B2C locatário. Essas contas têm esta aparência: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Agora, vamos usar Olá **ID do aplicativo** no script hello abaixo tooassign Olá Olá usuário conta administrador função de aplicativo que permitirá que ele toodelete usuários. Essas funções têm identificadores conhecidos, para que você só precisa toodo é de entrada seu **ID do aplicativo** no script de saudação abaixo.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

Seu aplicativo agora também tem permissões toodelete os usuários do seu locatário B2C.

## <a name="download-configure-and-build-hello-sample-code"></a>Baixar, configurar e compilar o código de exemplo hello
Primeiro, baixe o código de exemplo hello e executá-lo. Em seguida, faremos uma análise mais detalhada.  Você pode [baixar o código de exemplo hello como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). Você também pode cloná-lo em um diretório de sua escolha:

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Olá abrir `B2CGraphClient\B2CGraphClient.sln` solução do Visual Studio no Visual Studio. Em Olá `B2CGraphClient` projeto, o arquivo hello abrir `App.config`. Substitua três configurações de aplicativo hello com seus próprios valores:

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Em seguida, clique duas vezes em Olá `B2CGraphClient` exemplo hello de solução e recompilação. Se tiver êxito, agora deverá você ter um arquivo executável `B2C.exe` localizado em `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Criar operações CRUD de usuário usando Olá API do Graph
Olá toouse B2CGraphClient, abra um `cmd` Windows command prompt e altere seu diretório toohello `Debug` directory. Em seguida, execute Olá `B2C Help` comando.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Isso exibirá uma breve descrição de cada comando. Cada vez que você chamar um desses comandos, `B2CGraphClient` faz uma solicitação toohello API do Azure AD Graph.

### <a name="get-an-access-token"></a>Obter um token de acesso
Qualquer solicitação toohello Graph API requer um token de acesso para autenticação. `B2CGraphClient`usa Olá código-fonte aberto biblioteca de autenticação do Active Directory (ADAL) toohelp adquirir tokens de acesso. A ADAL facilita a aquisição de tokens, fornecendo uma API simples e cuidando de alguns detalhes importantes, como armazenar em cache os tokens de acesso. Você não tem toouse tooget ADAL tokens, embora. Você também pode obter tokens ao criar solicitações HTTP.

> [!NOTE]
> Este exemplo de código usa ADAL v2 na ordem toocommunicate com hello API do Graph.  Você deve usar o ADAL v2 ou v3 em ordem tooget os tokens de acesso que podem ser usados com hello Azure AD Graph API.
> 
> 

Quando `B2CGraphClient` é executado, ele cria uma instância de saudação `B2CGraphClient` classe. construtor Olá para esta classe define uma estrutura de autenticação de ADAL:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Vamos usar Olá `B2C Get-User` comando como um exemplo. Quando `B2C Get-User` for chamado sem qualquer entradas adicionais, Olá CLI chamadas Olá `B2CGraphClient.GetAllUsers(...)` método. Este método chama `B2CGraphClient.SendGraphGetRequest(...)`, que envia um toohello de solicitação HTTP GET API do Graph. Antes de `B2CGraphClient.SendGraphGetRequest(...)` envia Olá solicitação GET, ele primeiro obtém um token de acesso usando a ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

Você pode obter um acesso de token para Olá API do Graph por chamada hello ADAL `AuthenticationContext.AcquireToken(...)` método. ADAL, em seguida, retorna um `access_token` que representa a identidade do aplicativo hello.

### <a name="read-users"></a>Ler usuários
Quando você deseja tooget uma lista de usuários ou obter um usuário específico do hello API do Graph, você pode enviar um HTTP `GET` solicitação toohello `/users` ponto de extremidade. Uma solicitação para todos os usuários de saudação em um locatário tem esta aparência:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee essa solicitação, execute:

 ```
 > B2C Get-User
 ```

Há dois toonote de coisas importantes:

* Olá token de acesso adquirido por meio do ADAL é adicionado toohello `Authorization` cabeçalho usando Olá `Bearer` esquema.
* Para locatários B2C, você deve usar o parâmetro de consulta Olá `api-version=1.6`.

Ambos esses detalhes são tratados no hello `B2CGraphClient.SendGraphGetRequest(...)` método:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Criar contas de usuário consumidor
Ao criar contas de usuário em seu locatário B2C, você pode enviar um HTTP `POST` solicitação toohello `/users` ponto de extremidade:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

A maioria dessas propriedades nesta solicitação é usuários do consumidor toocreate necessária. toolearn mais, clique em [aqui](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Observe que Olá `//` comentários foram incluídos para fins ilustrativos. Não os inclua em uma solicitação real.

solicitação toosee hello, execute um dos Olá comandos a seguir:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Olá `Create-User` comando usa um arquivo. JSON como um parâmetro de entrada. Ele contém uma representação JSON de um objeto de usuário. Há dois arquivos. JSON de exemplo no código de exemplo hello: `usertemplate-email.json` e `usertemplate-username.json`. Você pode modificar esses arquivos toosuit suas necessidades. Além disso, toohello necessários campos acima, vários campos opcionais que você pode usar são incluídos nesses arquivos. Obter detalhes sobre os campos opcionais Olá podem ser encontrados no Olá [referência de entidade de API do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

Você pode ver como a solicitação POST Olá é construída no `B2CGraphClient.SendGraphPostRequest(...)`.

* Anexa um toohello de token de acesso `Authorization` cabeçalho de solicitação de saudação.
* Ela define `api-version=1.6`.
* Objeto de usuário do JSON Olá estão incluídos no corpo de saudação da solicitação de saudação.

> [!NOTE]
> Se Olá contas que você deseja toomigrate de um repositório de usuário existente tem a menor força da senha de saudação [força da senha forte imposta pelo Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), você pode desabilitar o requisito de senha forte hello usando Olá `DisableStrongPassword`valor Olá `passwordPolicies` propriedade. Por exemplo, você pode modificar Olá criar solicitação de usuário fornecidas acima da seguinte maneira: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Atualizar contas de usuário consumidor
Quando você atualiza os objetos de usuário, o processo de saudação é semelhante toohello utiliza objetos de usuário toocreate. Mas esse processo usa Olá HTTP `PATCH` método:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Tente tooupdate um usuário, atualizando os arquivos JSON com novos dados. Você pode usar `B2CGraphClient` toorun um destes comandos:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Inspecionar Olá `B2CGraphClient.SendGraphPatchRequest(...)` método para obter detalhes sobre como toosend esta solicitação.

### <a name="search-users"></a>Pesquisar usuários
É possível pesquisar usuários em seu locatário B2C de duas maneiras. Um, usando a ID de objeto ou a dois, usando o identificador de entrada do usuário de saudação do usuário hello (ou seja, Olá `signInNames` propriedade).

Execute um dos Olá toosearch de comandos para um usuário específico a seguir:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Aqui estão alguns exemplos:

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Excluir usuários
processo de saudação à exclusão de um usuário é simples. Olá Use HTTP `DELETE` método e construir URL Olá Olá corrigir ID de objeto:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee por exemplo, insira esta solicitação de exclusão Olá comando e o modo de exibição que é impressa toohello console:

```
> B2C Delete-User <object-id-of-user>
```

Inspecionar Olá `B2CGraphClient.SendGraphDeleteRequest(...)` método para obter detalhes sobre como toosend esta solicitação.

Você pode executar muitas outras ações com hello Azure AD Graph API no gerenciamento de toouser de adição. A [Referência da API do Graph do Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) fornece detalhes de cada ação, bem como solicitações de exemplo.

## <a name="use-custom-attributes"></a>Usar atributos personalizados
A maioria dos aplicativos de consumidor necessário toostore algum tipo de informações de perfil de usuário personalizada. Uma forma que você pode fazer isso é toodefine um atributo personalizado no seu locatário B2C. Em seguida, você pode tratar Olá esse atributo mesma maneira que você trate qualquer outra propriedade em um objeto de usuário. Você pode atualizar o atributo hello, atributo de Olá exclusão, consulta pelo atributo Olá, enviar atributo hello como uma declaração em tokens de entrada e muito mais.

toodefine um atributo personalizado no seu locatário B2C, consulte Olá [referência de atributo personalizado B2C](active-directory-b2c-reference-custom-attr.md).

Você pode exibir hello atributos personalizados definidos no seu locatário B2C usando `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

saída de Hello dessas funções revela detalhes de saudação de cada atributo personalizado, como:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

Você pode usar o hello nome completo, como `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, como uma propriedade em seus objetos de usuário.  Atualizar o arquivo. JSON com hello nova propriedade e um valor para a propriedade hello e, em seguida, execute:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Usando `B2CGraphClient`, você terá um aplicativo de serviço que pode gerenciar os usuários de locatário B2C de forma programática. `B2CGraphClient`usa seu próprio toohello de tooauthenticate de identidade de aplicativo do Azure AD Graph API. Ele também adquire tokens usando um segredo do cliente. Ao incorporar essa funcionalidade a seu aplicativo, lembre-se de alguns pontos importantes para aplicativos B2C:

* É necessário toogrant Olá aplicativo hello permissões adequadas no locatário hello.
* Por enquanto, você precisa de tokens de acesso de tooget toouse ADAL (não MSAL). (Você também pode enviar mensagens de protocolo diretamente, sem usar uma biblioteca.)
* Quando você chama hello Graph API, use `api-version=1.6`.
* Quando você cria e atualiza usuários consumidores, algumas propriedades são obrigatórias, conforme descrito acima.

Se você tiver perguntas ou solicitações de ações que você gostaria que tooperform usando Olá API do Graph em seu locatário B2C, deixe um comentário sobre este artigo ou um problema de arquivos no repositório de exemplo de código Olá GitHub.

