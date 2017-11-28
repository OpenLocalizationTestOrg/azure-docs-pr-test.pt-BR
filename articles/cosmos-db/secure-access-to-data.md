---
title: aaaLearn como toosecure acessar toodata no banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre os conceitos do controle de acesso no Azure Cosmos DB, incluindo chaves mestras, chaves somente leitura, usuários e permissões."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="d9a3d-103">Proteção de dados do access tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d9a3d-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="d9a3d-104">Este artigo fornece uma visão geral de proteção de acesso toodata armazenado em [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="d9a3d-105">Banco de dados do Azure Cosmos usa dois tipos de chaves tooauthenticate usuários e fornecer acesso tooits dados e recursos.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="d9a3d-106">Tipo de chave</span><span class="sxs-lookup"><span data-stu-id="d9a3d-106">Key type</span></span>|<span data-ttu-id="d9a3d-107">Recursos</span><span class="sxs-lookup"><span data-stu-id="d9a3d-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="d9a3d-108">Chaves mestras</span><span class="sxs-lookup"><span data-stu-id="d9a3d-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="d9a3d-109">Usadas para os recursos administrativos: contas de bancos de dados, bancos de dados, usuários e permissões</span><span class="sxs-lookup"><span data-stu-id="d9a3d-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="d9a3d-110">Tokens de recurso</span><span class="sxs-lookup"><span data-stu-id="d9a3d-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="d9a3d-111">Usados para recursos do aplicativo: coleções, documentos, anexos, procedimentos armazenados, gatilhos e UDFs</span><span class="sxs-lookup"><span data-stu-id="d9a3d-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="d9a3d-112">Chaves mestras</span><span class="sxs-lookup"><span data-stu-id="d9a3d-112">Master keys</span></span> 

<span data-ttu-id="d9a3d-113">Chaves mestras forneça acesso toohello todos os recursos administrativos do hello para Olá banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="d9a3d-114">Chaves mestras:</span><span class="sxs-lookup"><span data-stu-id="d9a3d-114">Master keys:</span></span>  
- <span data-ttu-id="d9a3d-115">Forneça acesso tooaccounts, bancos de dados, os usuários e permissões.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="d9a3d-116">Não pode ser usado tooprovide acesso granular toocollections e documentos.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="d9a3d-117">São criados durante a criação de saudação de uma conta.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="d9a3d-118">Podem ser geradas novamente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="d9a3d-119">Cada conta é formada por duas Chaves mestras: uma chave primária e uma chave secundária.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="d9a3d-120">Olá finalidade chaves duplas é para que você pode gerar novamente ou reverter chaves, fornecendo dados e a conta de acesso contínuo a tooyour.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="d9a3d-121">Em adição toohello duas chaves de mestre para conta de banco de dados do Cosmos hello, há duas chaves somente leitura.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="d9a3d-122">Essas chaves somente leitura apenas permitem operações de leitura na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="d9a3d-123">Chaves somente leitura não fornecem acesso a recursos de permissões tooread.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="d9a3d-124">Primária, secundária somente leitura e chaves mestras de leitura / gravação podem ser recuperadas e regeneradas usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="d9a3d-125">Para obter instruções, veja [Exibir, copiar e gerar novamente as chaves de acesso](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Controle de acesso (IAM) no portal do Azure - demonstrando a segurança de banco de dados NoSQL de saudação](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="d9a3d-127">processo de saudação de girar a chave mestra é simple.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="d9a3d-128">Navegue toohello tooretrieve portal do Azure a chave secundária, em seguida, substituir a chave primária com a chave secundária em seu aplicativo e girar a chave primária Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Rotação da chave mestra no portal do Azure - demonstrando a segurança de banco de dados NoSQL de saudação](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="d9a3d-130">Código de exemplo toouse uma chave mestra</span><span class="sxs-lookup"><span data-stu-id="d9a3d-130">Code sample toouse a master key</span></span>

<span data-ttu-id="d9a3d-131">Olá exemplo de código a seguir ilustra como toouse um banco de dados do Cosmos uma DocumentClient tooinstantiate de ponto de extremidade e a chave mestra da conta e criar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a><span data-ttu-id="d9a3d-132">Tokens de recurso</span><span class="sxs-lookup"><span data-stu-id="d9a3d-132">Resource tokens</span></span>

<span data-ttu-id="d9a3d-133">Tokens de recurso fornecem acesso a recursos do aplicativo toohello dentro de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="d9a3d-134">Tokens de recurso:</span><span class="sxs-lookup"><span data-stu-id="d9a3d-134">Resource tokens:</span></span>
- <span data-ttu-id="d9a3d-135">Forneça acesso toospecific coleções, as chaves de partição, documentos, anexos, procedimentos armazenados, gatilhos e UDFs.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="d9a3d-136">São criados quando um [usuário](#users) é concedida [permissões](#permissions) tooa determinado recurso.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="d9a3d-137">São recriados quando um recurso de permissão recebe uma ação de uma chamada POST, GET ou PUT.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="d9a3d-138">Use um token de recurso de hash construído especificamente para o usuário hello, recursos e permissão.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="d9a3d-139">São associados a um período de validade personalizável.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="d9a3d-140">período de tempo válido saudação padrão é uma hora.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="d9a3d-141">Vida útil do token, no entanto, pode ser especificado explicitamente, o máximo de tooa de cinco horas.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="d9a3d-142">Forneça uma segurança toogiving alternativo Olá mestre chave.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="d9a3d-143">Habilite clientes tooread, gravação e exclusão de recursos na conta de banco de dados do Cosmos Olá toohello permissões que lhe foi concedidos de acordo com.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="d9a3d-144">Você pode usar um token de recursos (ao criar usuários de banco de dados do Cosmos e permissões) quando você quiser tooprovide tooresources de acesso no seu banco de dados do Cosmos conta cliente tooa não pode ser confiável com a chave mestra de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="d9a3d-145">Tokens de recurso do cosmos DB fornecem uma alternativa segura que permite que clientes tooread, gravação e exclusão recursos em sua conta de banco de dados do Cosmos permissões toohello que você concedeu de acordo com e sem necessidade de qualquer um mestre ou chave somente de leitura.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="d9a3d-146">Este é um padrão de design típico no qual os tokens de recurso podem ser solicitados, gerados e entregue tooclients:</span><span class="sxs-lookup"><span data-stu-id="d9a3d-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="d9a3d-147">Um serviço de camada intermediária é configurado tooserve fotos do usuário de tooshare um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="d9a3d-148">serviço de camada intermediária Olá possui a chave mestra de saudação do hello conta de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="d9a3d-149">aplicativo de fotos Hello está instalado em dispositivos móveis do usuário final.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="d9a3d-150">Em logon, o aplicativo de fotos Olá estabelece identidade de saudação do usuário de saudação com o serviço de camada intermediária Olá.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="d9a3d-151">Esse mecanismo de estabelecimento de identidade é puramente toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="d9a3d-152">Após o estabelecimento de identidade Olá, solicitações de serviço de nível intermediário de saudação permissões com base na identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="d9a3d-153">serviço de camada intermediária Olá envia um aplicativo de telefone do recurso token toohello voltar.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="d9a3d-154">aplicativo de telefone Olá pode continuar toouse Olá recurso token toodirectly acessar banco de dados do Cosmos os recursos com permissões de saudação definidas pelo token de recurso Olá e para o intervalo de saudação permitido pelo token de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="d9a3d-155">Quando o token de recurso Olá expira, as solicitações subsequentes recebem uma exceção de 401 não autorizado.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="d9a3d-156">Neste ponto, aplicativo de telefone Olá restabelece identidade hello e solicita um novo token de recurso.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Fluxo de trabalho dos tokens de recurso do Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="d9a3d-158">Gerenciamento e geração de token de recurso é tratado por bibliotecas de cliente Cosmos DB nativo Olá; No entanto, se você usar o REST, você precisa construir cabeçalhos de solicitação/autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="d9a3d-159">Para obter mais informações sobre a criação de cabeçalhos de autenticação para REST, consulte [controle de acesso nos recursos de banco de dados do Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) ou hello [código-fonte para nossos SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="d9a3d-160">Para um exemplo de um serviço de camada intermediária usados toogenerate ou agente de tokens de recurso, consulte Olá [ResourceTokenBroker aplicativo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="d9a3d-161">Usuários</span><span class="sxs-lookup"><span data-stu-id="d9a3d-161">Users</span></span>
<span data-ttu-id="d9a3d-162">Os usuários do Cosmos DB são associados a um banco de dados do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="d9a3d-163">Cada banco de dados pode conter nenhum ou mais usuários do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="d9a3d-164">Olá mostra exemplo de código a seguir como toocreate um recurso de usuário de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="d9a3d-165">Cada usuário de banco de dados do Cosmos tem uma propriedade PermissionsLink que pode ser usado tooretrieve Olá lista de [permissões](#permissions) associado Olá usuário.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="d9a3d-166">Permissões</span><span class="sxs-lookup"><span data-stu-id="d9a3d-166">Permissions</span></span>
<span data-ttu-id="d9a3d-167">Um recurso de permissão do Cosmos DB é associado a um usuário do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="d9a3d-168">Cada usuário pode conter nenhuma ou mais permissões do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="d9a3d-169">Um recurso de permissão fornece o token de segurança do acesso tooa que Olá necessidades dos usuários durante a tentativa de tooaccess um recurso de aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="d9a3d-170">Há dois níveis de acesso disponíveis que podem ser fornecidos por um recurso de permissão:</span><span class="sxs-lookup"><span data-stu-id="d9a3d-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="d9a3d-171">All: usuário Olá tem permissão total em recurso hello.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="d9a3d-172">Leitura: usuário Olá somente pode ler o conteúdo de saudação do recurso de saudação mas não é possível executar a gravação, atualização ou operações de exclusão no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="d9a3d-173">Em ordem toorun Cosmos DB procedimentos armazenados Olá usuário deve ter Olá todas as permissões na coleção de saudação no qual Olá procedimento armazenado será executado.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="d9a3d-174">Permissão de toocreate de exemplo de código</span><span class="sxs-lookup"><span data-stu-id="d9a3d-174">Code sample toocreate permission</span></span>

<span data-ttu-id="d9a3d-175">Olá exemplo de código a seguir mostra como toocreate um recurso de permissão de leitura Olá token de recurso do recurso de permissão hello e associar permissões Olá Olá [usuário](#users) criado acima.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

<span data-ttu-id="d9a3d-176">Se você tiver especificado que uma chave de partição para o seu conjunto, em seguida, permissão Olá para recursos de coleção, documentos e anexos também deve incluir Olá ResourcePartitionKey em adição toohello ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="d9a3d-177">Permissões de tooread de exemplo de código do usuário</span><span class="sxs-lookup"><span data-stu-id="d9a3d-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="d9a3d-178">tooeasily obter todos os recursos de permissão associados a um usuário específico, Cosmos DB disponibiliza uma permissão de feed para cada objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="d9a3d-179">Olá trecho de código a seguir mostra como a permissão de saudação tooretrieve associado Olá usuário criado acima, construir uma lista de permissão e criar uma instância de um novo DocumentClient em nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9a3d-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a><span data-ttu-id="d9a3d-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9a3d-180">Next steps</span></span>
* <span data-ttu-id="d9a3d-181">toolearn mais sobre a segurança de banco de dados do banco de dados do Cosmos, consulte [Cosmos DB: segurança de banco de dados](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="d9a3d-182">toolearn sobre o gerenciamento de chaves mestres e somente leitura, consulte [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="d9a3d-183">toolearn como tokens de autorização do banco de dados do Azure Cosmos tooconstruct, consulte [controle de acesso nos recursos de banco de dados do Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="d9a3d-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
