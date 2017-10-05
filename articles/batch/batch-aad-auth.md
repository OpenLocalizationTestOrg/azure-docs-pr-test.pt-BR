---
title: "Usar o Azure Active Directory para autenticar as soluções do serviço do Lote do Azure | Microsoft Docs"
description: "O Lote dá suporte ao Azure AD para autenticação por meio do serviço do Lote."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Autenticar soluções do serviço do Lote no Active Directory

O Lote do Azure dá suporte à autenticação com o [Azure AD][aad_about] (Azure Active Directory). O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft. O Azure em si usa o Azure AD para autenticar seus clientes, administradores de serviços e usuários organizacionais.

Ao usar a autenticação do Azure AD com o Lote do Azure, você pode fazer a autenticação usando uma destas duas maneiras:

- Usando a **autenticação integrada** para autenticar um usuário que está interagindo com o aplicativo. Um aplicativo que usa a autenticação integrada coleta as credenciais do usuário e usa essas credenciais para autenticar o acesso aos recursos do Lote.
- Usando uma **entidade de serviço** para autenticar um aplicativo autônomo. Uma entidade de serviço define a política e as permissões de um aplicativo, a fim de representar o aplicativo ao acessar recursos em tempo de execução.

Para saber mais sobre o Azure AD, veja a [documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Autenticação e modo de alocação de pool

Ao criar uma conta do Lote, você poderá especificar o local ao qual os pools criados para essa conta devem ser alocados. Você pode optar por alocar pools na assinatura padrão do serviço do Lote ou em uma assinatura de usuário. Sua escolha afeta como você autentica o acesso aos recursos nessa conta.

- **Assinatura do serviço do Lote**. Por padrão, os pools de lote são alocados em uma assinatura de serviço de lote. Se você escolher essa opção, poderá autenticar o acesso aos recursos nessa conta com uma [Chave Compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou com o Azure AD.
- **Assinatura de usuário.** Você pode optar por alocar pools do Lote em uma assinatura de usuário especificada. Se você escolher essa opção, deverá autenticar no Azure AD.

## <a name="endpoints-for-authentication"></a>Pontos de extremidade para autenticação

Para autenticar aplicativos do Lote no Azure AD, você precisa incluir alguns pontos de extremidade conhecidos no código.

### <a name="azure-ad-endpoint"></a>Ponto de extremidade do Azure AD

O ponto de extremidade de autoridade base do Azure AD é:

`https://login.microsoftonline.com/`

Para autenticar no Azure AD, use esse ponto de extremidade junto com a ID do locatário (ID do diretório). A ID do locatário identifica o locatário do Azure AD a ser usado para autenticação. Para recuperar a ID do locatário, siga as etapas descritas em [Obter a ID do locatário para o Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> O ponto de extremidade específico ao locatário é necessário quando você realiza uma autenticação usando uma entidade de serviço. 
> 
> O ponto de extremidade específico ao locatário é opcional, mas recomendado, quando você realiza uma autenticação usando a autenticação integrada. No entanto, você também pode usar o ponto de extremidade comum do Azure AD. O ponto de extremidade comum fornece uma interface genérica de coleta de credenciais quando um locatário específico não é fornecido. O ponto de extremidade comum é `https://login.microsoftonline.com/common`.
>
>

Para obter mais informações sobre pontos de extremidade do Azure AD, consulte [Cenários de autenticação do Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Ponto de extremidade de recursos do Lote

Use o **ponto de extremidade de recursos do Lote do Azure** para adquirir um token para autenticar solicitações no serviço do Lote:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Registrar seu aplicativo em um locatário

A primeira etapa do uso do Azure AD para realizar a autenticação é registrar seu aplicativo em um locatário do Azure AD. O registro do aplicativo permite que você chame a [ADAL][aad_adal] (Biblioteca de Autenticação do Active Directory) do Azure por meio do código. A ADAL fornece uma API para realizar a autenticação no Azure AD por meio do aplicativo. O registro do aplicativo é necessário se você pretende usar a autenticação integrada ou uma entidade de serviço.

Ao registrar o aplicativo, você fornece informações sobre ele ao Azure AD. Em seguida, o Azure AD fornece uma ID de aplicativo que você usa para associar seu aplicativo ao Azure AD em tempo de execução. Para saber mais sobre a ID do aplicativo, veja [Objetos de aplicativo e de entidade de serviço no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

Para registrar o aplicativo Lote, siga as etapas da seção [Adicionar um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) em [Integração de aplicativos com o Azure Active Directory][aad_integrate]. Se você registrar o aplicativo como um Aplicativo Nativo, poderá especificar qualquer URI válido para o **URI de Redirecionamento**. Ele não precisa ser um ponto de extremidade real.

Depois de registrar o aplicativo, você verá a ID do aplicativo:

![Registrar seu aplicativo Lote no Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Para obter mais informações sobre como registrar um aplicativo no Azure AD, consulte [Cenários de autenticação do Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-the-tenant-id-for-your-active-directory"></a>Obter a ID do locatário para o Active Directory

A ID do locatário identifica o locatário do Azure AD que fornece serviços de autenticação para o aplicativo. Para obter a ID de locatário, siga estas etapas:

1. No portal do Azure, selecione seu Active Directory.
2. Clique em **Propriedades**.
3. Copie o valor do GUID fornecido para a ID do diretório. Esse valor também é chamado de ID do locatário.

![Copiar a ID do diretório](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Usar a autenticação integrada

Para autenticar com a autenticação integrada, você precisa conceder as permissões do aplicativo para se conectar à API do serviço do Lote. Esta etapa permite que o aplicativo autentique chamadas à API do serviço do Lote no Azure AD.

Depois de [registrar o aplicativo](#register-your-application-with-an-azure-ad-tenant), siga estas etapas no portal do Azure para conceder a ele o acesso ao serviço do Lote:

1. No painel de navegação esquerdo do portal do Azure, escolha **Mais Serviços** e clique em **Registros de Aplicativo**.
2. Pesquise pelo nome do seu aplicativo na lista de registros do aplicativo:

    ![Procure o nome do aplicativo](./media/batch-aad-auth/search-app-registration.png)

3. Abra a folha **Configurações** de seu aplicativo. Na seção **Acesso à API**, selecione **Permissões necessárias**.
4. No **permissões necessárias** folha, clique o **adicionar** botão.
5. Na etapa 1, pesquise a API de Lote. Procure cada uma dessas cadeias de caracteres até encontrar a API:
    1. **MicrosoftAzureBatch**.
    2. **Lote do Microsoft Azure**. Os locatários mais recentes do Azure AD podem usar esse nome.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** é a ID para a API do Lote. 
6. Depois de encontrar a API de Lote, selecione-a e clique no botão **Selecionar**.
6. Na etapa 2, selecione a caixa de seleção Avançar ao **acesso serviço do Azure Batch** e clique no **selecione** botão.
7. Clique no botão **Concluído**.

A folha **Permissões Necessárias** agora mostra que o aplicativo do Azure AD tem acesso à ADAL e à API do serviço do Lote. As permissões são concedidas à ADAL automaticamente quando você registra seu aplicativo no Azure AD pela primeira vez.

![Conceder permissões de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Usar uma entidade de serviço 

Para autenticar um aplicativo que é executado de forma autônoma, use uma entidade de serviço. Depois de registrar o aplicativo, siga estas etapas no portal do Azure para configurar uma entidade de serviço:

1. Solicitar uma chave secreta para o aplicativo.
2. Atribuir uma função RBAC ao aplicativo.

### <a name="request-a-secret-key-for-your-application"></a>Solicitar uma chave secreta para o aplicativo

Quando o aplicativo é autenticado com uma entidade de serviço, ele envia a ID do aplicativo e uma chave secreta para o Azure AD. Você precisará criar e copiar a chave secreta a ser usada do código.

Siga estas etapas no portal do Azure:

1. No painel de navegação esquerdo do portal do Azure, escolha **Mais Serviços** e clique em **Registros de Aplicativo**.
2. Pesquise o nome do aplicativo na lista de registros de aplicativo.
3. Exibição de **configurações** folha. Na seção **Acesso à API**, selecione **Chaves**.
4. Para criar uma chave, insira uma descrição para a chave. Em seguida, selecione uma duração para a chave de um ou dois anos. 
5. Clique no botão **Salvar** para criar e exibir a chave. Copie o valor da chave para um local seguro, pois você não poderá acessá-lo novamente depois de sair da folha. 

    ![Criar uma chave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a>Atribuir uma função RBAC ao aplicativo

Para autenticar com uma entidade de serviço, você precisa atribuir uma função RBAC ao aplicativo. Siga estas etapas:

1. No portal do Azure, navegue para a conta do Lote usada pelo aplicativo.
2. Na folha **Configurações** da conta do Lote, selecione **Controle de Acesso (IAM)**.
3. Clique no botão **Adicionar** . 
4. Na lista suspensa **Função**, escolha a função _Colaborador_ ou _Leitor_ para o aplicativo. Para obter mais informações sobre essas funções, consulte [Introdução ao Controle de Acesso Baseado em Função no portal do Azure](../active-directory/role-based-access-control-what-is.md).  
5. No campo **Selecionar**, insira o nome de seu aplicativo. Selecione o aplicativo na lista e clique em **Salvar**.

O aplicativo agora deverá ser exibido nas configurações de controle de acesso com uma função RBAC atribuída. 

![Atribuir uma função RBAC ao aplicativo](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a>Obter a ID do locatário para o Azure Active Directory

A ID do locatário identifica o locatário do Azure AD que fornece serviços de autenticação para o aplicativo. Para obter a ID de locatário, siga estas etapas:

1. No portal do Azure, selecione seu Active Directory.
2. Clique em **Propriedades**.
3. Copie o valor do GUID fornecido para a ID do diretório. Esse valor também é chamado de ID do locatário.

![Copiar a ID do diretório](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Exemplos de código

Os exemplos de código desta seção mostram como realizar a autenticação com o Azure AD usando a autenticação integrada e com uma entidade de serviço. Esses exemplos de código usam o .NET, mas os conceitos são semelhantes para outras linguagens.

> [!NOTE]
> Um token de autenticação do AD do Azure expirará após uma hora. Ao usar uma vida útil longa **BatchClient** de objeto, é recomendável que você recuperar um token da ADAL em cada solicitação para garantir que você sempre tenha um token válido. 
>
>
> Para fazer isso no .NET, escrever um método que recupera o token do AD do Azure e passar esse método para um **BatchTokenCredentials** objeto como um delegado. O método de representante é chamado em cada solicitação para o serviço de lote para garantir que um token válido seja fornecido. Por padrão ADAL armazena em cache os tokens, para que um novo token é recuperado do AD do Azure somente quando necessário. Para saber mais sobre tokens no AD do Azure, veja [Cenários de autenticação do AD do Azure][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Exemplo de código: Usando a autenticação integrada do Azure AD com o .NET do Lote

Para autenticar com a autenticação integrada por meio do .NET do Lote, referencie o pacote [.NET do Lote do Azure](https://www.nuget.org/packages/Azure.Batch/) e o pacote [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).

Inclua as seguintes intruções `using` no seu código:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Referencie o ponto de extremidade do Azure AD no código, incluindo a ID do locatário. Para recuperar a ID do locatário, siga as etapas descritas em [Obter a ID do locatário para o Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Referencie o ponto de extremidade de recursos do serviço do Lote:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Referencie a conta do Lote:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Especifique a ID do aplicativo (ID do cliente) para seu aplicativo. A ID do aplicativo está disponível no registro de aplicativo no portal do Azure:

```csharp
private const string ClientId = "<application-id>";
```

Também copie o URI que você especificou durante o processo de registro de redirecionamento. O URI de redirecionamento especificado no código deve corresponder ao URI de redirecionamento que você forneceu quando registrou o aplicativo:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Escreva um método de retorno de chamada para adquirir o token de autenticação do AD do Azure. O método de retorno de chamada **GetAuthenticationTokenAsync** mostrado aqui chama a ADAL para autenticar um usuário que está interagindo com o aplicativo. O método **AcquireTokenAsync** fornecido pela ADAL solicita ao usuário suas credenciais e o aplicativo continua depois que o usuário fornece essas credenciais (a menos que ele já tenha as credenciais armazenadas em cache):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Construa um objeto **BatchTokenCredentials** que use o delegado como um parâmetro. Use essas credenciais para abrir um objeto **BatchClient**. Você pode usar esse objeto **BatchClient** para as próximas operações no serviço do Lote:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Exemplo de código: Usando uma entidade de serviço do Azure AD com o .NET do Lote

Para autenticar com uma entidade de serviço por meio do .NET do Lote, referencie o pacote [.NET do Lote do Azure](https://www.nuget.org/packages/Azure.Batch/) e o pacote [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).

Inclua as seguintes intruções `using` no seu código:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Referencie o ponto de extremidade do Azure AD no código, incluindo a ID do locatário. Ao usar uma entidade de serviço, você deve fornecer um ponto de extremidade específico ao locatário. Para recuperar a ID do locatário, siga as etapas descritas em [Obter a ID do locatário para o Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Referencie o ponto de extremidade de recursos do serviço do Lote:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Referencie a conta do Lote:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Especifique a ID do aplicativo (ID do cliente) para seu aplicativo. A ID do aplicativo está disponível no registro de aplicativo no portal do Azure:

```csharp
private const string ClientId = "<application-id>";
```

Especifique a chave secreta que você copiou do portal do Azure:

```csharp
private const string ClientKey = "<secret-key>";
```

Escreva um método de retorno de chamada para adquirir o token de autenticação do AD do Azure. O método de retorno de chamada **GetAuthenticationTokenAsync** mostrado aqui chama a ADAL para a autenticação autônoma:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Construa um objeto **BatchTokenCredentials** que use o delegado como um parâmetro. Use essas credenciais para abrir um objeto **BatchClient**. Depois, você pode usar esse objeto **BatchClient** para as próximas operações no serviço do Lote:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Azure AD, veja a [documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Exemplos mais detalhados que mostram como usar o ADAL estão disponíveis na biblioteca [Amostras de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).

Para saber mais sobre entidades de serviço, consulte [Objetos de aplicativo e de entidade de serviço no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). Para criar uma entidade de serviço usando o portal do Azure, consulte [Usar o portal para criar um aplicativo e uma entidade de serviço do Active Directory que pode acessar recursos](../resource-group-create-service-principal-portal.md). Você também pode criar uma entidade de serviço com o PowerShell ou a CLI do Azure. 

Para autenticar aplicativos do Gerenciamento de Lotes usando o Azure AD, consulte [Autenticar soluções do Gerenciamento de Lotes de com o Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"
[azure_portal]: http://portal.azure.com
