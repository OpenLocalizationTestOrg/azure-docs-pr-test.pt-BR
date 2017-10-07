---
title: "soluções de serviço de lote do Azure do aaaUse Active Directory do Azure tooauthenticate | Microsoft Docs"
description: "Lote dá suporte ao AD do Azure para autenticação do serviço de lote de saudação."
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
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Autenticar soluções do serviço do Lote no Active Directory

O Lote do Azure dá suporte à autenticação com o [Azure AD][aad_about] (Azure Active Directory). O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft. Azure próprio usa tooauthenticate do AD do Azure, seus clientes, os administradores de serviços e usuários organizacionais.

Ao usar a autenticação do Azure AD com o Lote do Azure, você pode fazer a autenticação usando uma destas duas maneiras:

- Usando **autenticação integrada** tooauthenticate um usuário que está interagindo com o aplicativo hello. Um aplicativo usando a autenticação integrada reúne as credenciais do usuário e usa essas credenciais tooauthenticate acessar tooBatch os recursos.
- Usando um **entidade de serviço** tooauthenticate um aplicativo autônomo. Uma entidade de serviço define permissões para um aplicativo e política de saudação no aplicativo de saudação do pedido toorepresent ao acessar recursos em tempo de execução.

toolearn mais sobre o AD do Azure, consulte Olá [documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Autenticação e modo de alocação de pool

Ao criar uma conta do Lote, você poderá especificar o local ao qual os pools criados para essa conta devem ser alocados. Você pode escolher pools tooallocate na assinatura do serviço de lote saudação padrão ou em uma assinatura do usuário. Sua escolha afeta como autenticar o acesso tooresources nessa conta.

- **Assinatura do serviço do Lote**. Por padrão, os pools de lote são alocados em uma assinatura de serviço de lote. Se você escolher essa opção, você pode autenticar acesso tooresources nessa conta com [chave compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou com o AD do Azure.
- **Assinatura de usuário.** Você pode escolher tooallocate pools de lote em uma assinatura de usuário que você especificar. Se você escolher essa opção, deverá autenticar no Azure AD.

## <a name="endpoints-for-authentication"></a>Pontos de extremidade para autenticação

aplicativos de lote tooauthenticate com o AD do Azure, você precisa tooinclude alguns pontos de extremidade conhecidos no seu código.

### <a name="azure-ad-endpoint"></a>Ponto de extremidade do Azure AD

Olá base é o ponto de extremidade do AD do Azure autoridade:

`https://login.microsoftonline.com/`

tooauthenticate com o AD do Azure, você usar esse ponto de extremidade junto com a ID de locatário hello (ID de diretório). ID de locatário Olá identifica Olá toouse de locatário do AD do Azure para autenticação. tooretrieve Olá ID de locatário, siga etapas Olá descritas em [obter ID de locatário Olá para Active Directory do Azure](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> o ponto de extremidade do Hello específico de locatário é necessário quando você autenticar usando uma entidade de serviço. 
> 
> ponto de extremidade de locatário específico de saudação é opcional quando você autenticar usando a autenticação integrada, mas recomendada. No entanto, você também pode usar o ponto de extremidade comum Olá AD do Azure. ponto de extremidade comum Olá fornece uma credencial genérica coleta interface quando um locatário específico não é fornecido. ponto de extremidade comum Olá é `https://login.microsoftonline.com/common`.
>
>

Para obter mais informações sobre pontos de extremidade do Azure AD, consulte [Cenários de autenticação do Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Ponto de extremidade de recursos do Lote

Saudação de uso **ponto de extremidade de recursos do Azure Batch** tooacquire um token para autenticar solicitações de serviço de lote toohello:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Registrar seu aplicativo em um locatário

a primeira etapa Hello usando tooauthenticate do AD do Azure está registrando seu aplicativo em um locatário do AD do Azure. Registrar seu aplicativo permite que você toocall hello Azure [biblioteca de autenticação do Active Directory] [ aad_adal] (ADAL) no seu código. Olá ADAL fornece uma API para autenticar com o AD do Azure do seu aplicativo. Registrar seu aplicativo é necessária se você planejar a autenticação integrada toouse ou uma entidade de serviço.

Quando você registra seu aplicativo, você fornece informações sobre seu aplicativo tooAzure AD. Em seguida, o AD do Azure fornece uma ID de aplicativo que você use tooassociate seu aplicativo com o AD do Azure em tempo de execução. toolearn mais informações sobre a ID do aplicativo hello, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister seu aplicativo de lote, siga etapas Olá Olá [adicionar um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) seção [integrando aplicativos com o Active Directory do Azure][aad_integrate]. Se você registrar seu aplicativo como um aplicativo nativo, você pode especificar qualquer URI válido para Olá **URI de redirecionamento**. Ele não precisa toobe um ponto de extremidade real.

Depois que você já registrou seu aplicativo, você verá a ID do aplicativo hello:

![Registrar seu aplicativo Lote no Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Para obter mais informações sobre como registrar um aplicativo no Azure AD, consulte [Cenários de autenticação do Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Obter ID de locatário de saudação do seu Active Directory

ID de locatário Olá identifica Olá locatário do AD Azure que fornece serviços de autenticação tooyour de aplicativo. tooget Olá ID de locatário, siga estas etapas:

1. No portal do Azure de Olá, selecione seu Active Directory.
2. Clique em **Propriedades**.
3. Copiar o valor GUID Olá fornecido para a ID de diretório hello. Esse valor também é chamado de ID de locatário hello.

![Copiar a ID de diretório Olá](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Usar a autenticação integrada

tooauthenticate com a autenticação integrada, é necessário toogrant toohello de tooconnect de permissões seu aplicativo API do serviço de lote. Esta etapa permite que a sua API de serviço do aplicativo tooauthenticate chamadas toohello em lotes com o Azure AD.

Depois que você [registrou seu aplicativo](#register-your-application-with-an-azure-ad-tenant), siga estas etapas no hello toogrant portal do Azure que acessar o serviço de lote toohello:

1. No painel de navegação do lado esquerdo de saudação do Olá portal do Azure, escolha **mais serviços**, clique em **registros do aplicativo**.
2. Pesquisar por nome de saudação do seu aplicativo na lista de saudação de registros do aplicativo:

    ![Procure o nome do aplicativo](./media/batch-aad-auth/search-app-registration.png)

3. Olá abrir **configurações** folha para seu aplicativo. Em Olá **acesso à API** seção, selecione **as permissões necessárias**.
4. Em Olá **as permissões necessárias** folha, clique em Olá **adicionar** botão.
5. Na etapa 1, procure Olá API de lote. Pesquisar para cada uma dessas cadeias de caracteres até encontrar hello API:
    1. **MicrosoftAzureBatch**.
    2. **Lote do Microsoft Azure**. Os locatários mais recentes do Azure AD podem usar esse nome.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** é identificação Olá Olá API de lote. 
6. Depois de encontrar hello API de lote, selecione-o e clique Olá **selecione** botão.
6. Na etapa 2, selecione Olá caixa de seleção próxima muito**serviço de lote do Azure acesso** e clique em Olá **selecione** botão.
7. Clique em Olá **feito** botão.

Olá **permissões necessárias** folha agora mostra que o aplicativo do AD do Azure tem acesso tooboth ADAL e Olá API do serviço de lote. As permissões são concedidas tooADAL automaticamente quando você primeiro registra seu aplicativo com o Azure AD.

![Conceder permissões de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Usar uma entidade de serviço 

tooauthenticate um aplicativo executado autônomo, você usa uma entidade de serviço. Depois que você já registrou seu aplicativo, siga estas etapas no hello tooconfigure portal do Azure uma entidade de serviço:

1. Solicitar uma chave secreta para o aplicativo.
2. Atribua um aplicativo de tooyour função RBAC.

### <a name="request-a-secret-key-for-your-application"></a>Solicitar uma chave secreta para o aplicativo

Quando seu aplicativo é autenticado com uma entidade de serviço, ele envia Olá ID do aplicativo e um tooAzure chave secreta AD. Você precisa toocreate e copiar toouse chave secreta de saudação do seu código.

Siga estas etapas no hello portal do Azure:

1. No painel de navegação do lado esquerdo de saudação do Olá portal do Azure, escolha **mais serviços**, clique em **registros do aplicativo**.
2. Pesquisar por nome de saudação do seu aplicativo na lista de saudação de registros do aplicativo.
3. Saudação de exibição **configurações** folha. Em Olá **acesso à API** seção, selecione **chaves**.
4. toocreate uma chave, insira uma descrição para a chave de saudação. Em seguida, selecione uma duração para a chave de saudação de um ou dois anos. 
5. Clique em Olá **salvar** botão toocreate e exibir chave hello. Copiar local seguro do tooa do valor de chave de hello, pois não será capaz de tooaccess-lo novamente depois que você deixe folha hello. 

    ![Criar uma chave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Atribuir um aplicativo de tooyour função RBAC

tooauthenticate com uma entidade de serviço, você precisa tooassign um aplicativo de tooyour função RBAC. Siga estas etapas:

1. No portal do Azure de Olá, navegue toohello conta do lote usada pelo seu aplicativo.
2. Em Olá **configurações** folha para a conta de lote hello, selecione **controle de acesso (IAM)**.
3. Clique em Olá **adicionar** botão. 
4. De saudação **função** lista suspensa, escolha a saudação _Colaborador_ ou _leitor_ função para seu aplicativo. Para obter mais informações sobre essas funções, consulte [Introdução ao controle de acesso baseado em função no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).  
5. Em Olá **selecione** , digite o nome de saudação do seu aplicativo. Selecione o aplicativo hello lista e, em seguida, clique em **salvar**.

O aplicativo agora deverá ser exibido nas configurações de controle de acesso com uma função RBAC atribuída. 

![Atribuir um aplicativo de tooyour função RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Obter ID de locatário Olá para Active Directory do Azure

ID de locatário Olá identifica Olá locatário do AD Azure que fornece serviços de autenticação tooyour de aplicativo. tooget Olá ID de locatário, siga estas etapas:

1. No portal do Azure de Olá, selecione seu Active Directory.
2. Clique em **Propriedades**.
3. Copiar o valor GUID Olá fornecido para a ID de diretório hello. Esse valor também é chamado de ID de locatário hello.

![Copiar a ID de diretório Olá](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Exemplos de código

exemplos de código de saudação nesta seção mostram como tooauthenticate com o AD do Azure usando a autenticação integrada e com uma entidade de serviço. Esses exemplos de código usam o .NET, mas os conceitos de saudação são semelhantes para outros idiomas.

> [!NOTE]
> Um token de autenticação do AD do Azure expirará após uma hora. Ao usar uma vida útil longa **BatchClient** do objeto, é recomendável que você recuperar um token de ADAL em cada solicitação tooensure sempre ter um token válido. 
>
>
> tooachieve isso no .NET, escrever um método que recupera Olá token do AD do Azure e passa esse método tooa **BatchTokenCredentials** objeto como um representante. método de representante Hello é chamado em cada solicitação toohello lote serviço tooensure que é fornecido um token válido. Por padrão ADAL armazena em cache os tokens, para que um novo token é recuperado do AD do Azure somente quando necessário. Para saber mais sobre tokens no AD do Azure, veja [Cenários de autenticação do AD do Azure][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Exemplo de código: Usando a autenticação integrada do Azure AD com o .NET do Lote

tooauthenticate com a autenticação integrada do .NET em lotes, Olá referência [do Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pacote e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacote.

Incluir o seguinte Olá `using` no seu código:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Saudação de referência ponto de extremidade do AD do Azure no seu código, incluindo Olá locatário ID. tooretrieve Olá ID de locatário, siga etapas Olá descritas em [obter ID de locatário Olá para Active Directory do Azure](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Referência de ponto de extremidade recurso serviço de lote de hello:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Referencie a conta do Lote:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Especifique a ID de aplicativo de saudação (ID do cliente) para seu aplicativo. ID do aplicativo Hello está disponível em seu registro de aplicativo no portal do Azure de saudação:

```csharp
private const string ClientId = "<application-id>";
```

Também copie o URI que você especificou durante o processo de registro de saudação de redirecionamento de saudação. Olá URI especificado em seu código deve coincidir com a URI que você forneceu ao registrar o aplicativo hello de redirecionamento de saudação de redirecionamento:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Grave um token de autenticação do retorno de chamada método tooacquire saudação do AD do Azure. Olá **GetAuthenticationTokenAsync** tooauthenticate ADAL as chamadas método de retorno de chamada mostrado aqui um usuário que está interagindo com o aplicativo hello. Olá **AcquireTokenAsync** método fornecido por ADAL prompts Olá suas credenciais do usuário e o aplicativo hello continua uma vez usuário Olá fornecerá a eles (a menos que ele já tem em cache as credenciais):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Construir um **BatchTokenCredentials** objeto que usa Olá delegado como um parâmetro. Use essas credenciais tooopen um **BatchClient** objeto. Você pode usá-lo **BatchClient** objeto para operações subsequentes em relação a saudação serviço de lote:

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

tooauthenticate com uma entidade de serviço do .NET em lotes, Olá referência [do Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pacote e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacote.

Incluir o seguinte Olá `using` no seu código:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Saudação de referência ponto de extremidade do AD do Azure no seu código, incluindo Olá locatário ID. Ao usar uma entidade de serviço, você deve fornecer um ponto de extremidade específico ao locatário. tooretrieve Olá ID de locatário, siga etapas Olá descritas em [obter ID de locatário Olá para Active Directory do Azure](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Referência de ponto de extremidade recurso serviço de lote de hello:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Referencie a conta do Lote:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Especifique a ID de aplicativo de saudação (ID do cliente) para seu aplicativo. ID do aplicativo Hello está disponível em seu registro de aplicativo no portal do Azure de saudação:

```csharp
private const string ClientId = "<application-id>";
```

Especifique a chave de segredo Olá que você copiou da saudação portal do Azure:

```csharp
private const string ClientKey = "<secret-key>";
```

Grave um token de autenticação do retorno de chamada método tooacquire saudação do AD do Azure. Olá **GetAuthenticationTokenAsync** método de retorno de chamada mostrado aqui chamadas de ADAL para autenticação autônoma:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Construir um **BatchTokenCredentials** objeto que usa Olá delegado como um parâmetro. Use essas credenciais tooopen um **BatchClient** objeto. Você pode usá-lo, em seguida, **BatchClient** objeto para operações subsequentes em relação a saudação serviço de lote:

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

toolearn mais sobre o AD do Azure, consulte Olá [documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/). Os exemplos mais detalhados mostrando como toouse ADAL estão disponíveis no hello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.

toolearn mais informações sobre entidades de serviço, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). toocreate uma entidade de serviço usando hello Azure portal, consulte [usar o aplicativo do portal toocreate do Active Directory e a entidade de serviço que pode acessar recursos](../resource-group-create-service-principal-portal.md). Você também pode criar uma entidade de serviço com o PowerShell ou a CLI do Azure. 

aplicativos de gerenciamento de lote de tooauthenticate usando o AD do Azure, consulte [soluções de gerenciamento de lote de autenticar com o Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"
[azure_portal]: http://portal.azure.com
