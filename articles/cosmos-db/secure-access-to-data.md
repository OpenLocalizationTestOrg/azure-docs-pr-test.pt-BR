---
title: Saiba como proteger o acesso aos dados no Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="dad05-103">Protegendo o acesso aos dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="dad05-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="dad05-104">Este artigo fornece uma visão geral de como proteger o acesso aos dados armazenados no [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="dad05-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="dad05-105">O Azure Cosmos DB usa dois tipos de chaves para autenticar usuários e fornecer acesso aos seus dados e recursos.</span><span class="sxs-lookup"><span data-stu-id="dad05-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="dad05-106">Tipo de chave</span><span class="sxs-lookup"><span data-stu-id="dad05-106">Key type</span></span>|<span data-ttu-id="dad05-107">Recursos</span><span class="sxs-lookup"><span data-stu-id="dad05-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="dad05-108">Chaves mestras</span><span class="sxs-lookup"><span data-stu-id="dad05-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="dad05-109">Usadas para os recursos administrativos: contas de bancos de dados, bancos de dados, usuários e permissões</span><span class="sxs-lookup"><span data-stu-id="dad05-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="dad05-110">Tokens de recurso</span><span class="sxs-lookup"><span data-stu-id="dad05-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="dad05-111">Usados para recursos do aplicativo: coleções, documentos, anexos, procedimentos armazenados, gatilhos e UDFs</span><span class="sxs-lookup"><span data-stu-id="dad05-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="dad05-112">Chaves mestras</span><span class="sxs-lookup"><span data-stu-id="dad05-112">Master keys</span></span> 

<span data-ttu-id="dad05-113">As chaves mestras fornecem acesso a todos os recursos administrativos para a conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="dad05-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="dad05-114">Chaves mestras:</span><span class="sxs-lookup"><span data-stu-id="dad05-114">Master keys:</span></span>  
- <span data-ttu-id="dad05-115">Fornecem acesso a contas, a bancos de dados, a usuários e a permissões.</span><span class="sxs-lookup"><span data-stu-id="dad05-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="dad05-116">Não podem ser usadas para fornecer acesso granular a documentos e coleções.</span><span class="sxs-lookup"><span data-stu-id="dad05-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="dad05-117">São criadas durante a criação de uma conta.</span><span class="sxs-lookup"><span data-stu-id="dad05-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="dad05-118">Podem ser geradas novamente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="dad05-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="dad05-119">Cada conta é formada por duas Chaves mestras: uma chave primária e uma chave secundária.</span><span class="sxs-lookup"><span data-stu-id="dad05-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="dad05-120">A finalidade das chaves duplas é para que você possa gerar novamente, ou reverter as chaves, fornecendo acesso contínuo à sua conta e dados.</span><span class="sxs-lookup"><span data-stu-id="dad05-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="dad05-121">Além das duas chaves mestras da conta do Cosmos DB, há duas chaves somente leitura.</span><span class="sxs-lookup"><span data-stu-id="dad05-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="dad05-122">Essas chaves somente leitura só permitem operações de leitura na conta.</span><span class="sxs-lookup"><span data-stu-id="dad05-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="dad05-123">As chaves somente leitura não fornecem acesso a recursos com permissões de leitura.</span><span class="sxs-lookup"><span data-stu-id="dad05-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="dad05-124">As chaves mestras primária, secundária, somente leitura e de leitura-gravação podem ser recuperadas e geradas novamente usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dad05-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="dad05-125">Para obter instruções, veja [Exibir, copiar e gerar novamente as chaves de acesso](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="dad05-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Controle de acesso (IAM) no Portal do Azure - demonstrando a segurança do banco de dados NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="dad05-127">O processo de girar a chave mestra é simples.</span><span class="sxs-lookup"><span data-stu-id="dad05-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="dad05-128">Navegue até o Portal do Azure para recuperar a chave secundária, depois substitua a chave primária pela chave secundária em seu aplicativo e gire a chave primária no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dad05-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Rotação de chave mestra no Portal do Azure – demonstrando a segurança do banco de dados NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="dad05-130">Exemplo de código para uso de uma chave mestra</span><span class="sxs-lookup"><span data-stu-id="dad05-130">Code sample to use a master key</span></span>

<span data-ttu-id="dad05-131">O exemplo de código a seguir ilustra como usar o ponto de extremidade e a chave mestra de uma conta do Cosmos DB para criar uma instância de um DocumentClient e criar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="dad05-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="dad05-132">Tokens de recurso</span><span class="sxs-lookup"><span data-stu-id="dad05-132">Resource tokens</span></span>

<span data-ttu-id="dad05-133">Os tokens de recurso fornecem acesso aos recursos do aplicativo em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="dad05-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="dad05-134">Tokens de recurso:</span><span class="sxs-lookup"><span data-stu-id="dad05-134">Resource tokens:</span></span>
- <span data-ttu-id="dad05-135">Fornecem acesso a coleções, chaves de partição, documentos, anexos, procedimentos armazenados, gatilhos e UDFs específicos.</span><span class="sxs-lookup"><span data-stu-id="dad05-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="dad05-136">São criados quando um [usuário](#users) recebe [permissões](#permissions) para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="dad05-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="dad05-137">São recriados quando um recurso de permissão recebe uma ação de uma chamada POST, GET ou PUT.</span><span class="sxs-lookup"><span data-stu-id="dad05-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="dad05-138">Use um token de recurso de hash construído especificamente para o usuário, o recurso e a permissão.</span><span class="sxs-lookup"><span data-stu-id="dad05-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="dad05-139">São associados a um período de validade personalizável.</span><span class="sxs-lookup"><span data-stu-id="dad05-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="dad05-140">O intervalo de tempo válido padrão é de uma hora.</span><span class="sxs-lookup"><span data-stu-id="dad05-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="dad05-141">O tempo de vida do token, no entanto, pode ser especificado explicitamente, até o máximo de cinco horas.</span><span class="sxs-lookup"><span data-stu-id="dad05-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="dad05-142">Fornecem uma alternativa segura para o fornecimento da chave mestra.</span><span class="sxs-lookup"><span data-stu-id="dad05-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="dad05-143">Permitem aos clientes ler, gravar e excluir recursos da conta do Cosmos DB de acordo com as permissões que receberam.</span><span class="sxs-lookup"><span data-stu-id="dad05-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="dad05-144">Você pode usar um token de recurso (criando usuários e permissões do Cosmos DB) quando desejar fornecer acesso aos recursos de sua conta do Cosmos DB a um cliente que não é confiável para receber a chave mestra.</span><span class="sxs-lookup"><span data-stu-id="dad05-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="dad05-145">Os tokens de recurso do Cosmos DB fornecem uma alternativa segura que permite aos clientes ler, gravar e excluir recursos de sua conta do Cosmos DB de acordo com as permissões que você concedeu e sem a necessidade de uma chave mestra ou somente leitura.</span><span class="sxs-lookup"><span data-stu-id="dad05-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="dad05-146">Este é um padrão de design típico no qual tokens de recurso podem ser solicitados, gerados e fornecidos aos clientes:</span><span class="sxs-lookup"><span data-stu-id="dad05-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="dad05-147">Um serviço de camada intermediária é configurado para atender a um aplicativo móvel de compartilhamento de fotos do usuário.</span><span class="sxs-lookup"><span data-stu-id="dad05-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="dad05-148">O serviço de camada intermediária tem a chave mestra da conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dad05-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="dad05-149">O aplicativo de fotos é instalado em dispositivos móveis de usuários finais.</span><span class="sxs-lookup"><span data-stu-id="dad05-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="dad05-150">No logon, o aplicativo de fotos estabelece a identidade do usuário com o serviço de camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="dad05-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="dad05-151">Esse mecanismo de estabelecimento de identidade depende apenas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dad05-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="dad05-152">Depois que a identidade é estabelecida, o serviço de camada intermediária solicita permissões com base na identidade.</span><span class="sxs-lookup"><span data-stu-id="dad05-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="dad05-153">O serviço de camada intermediária envia um token de recurso de volta para o aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="dad05-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="dad05-154">O aplicativo de telefone pode continuar usando o token de recurso para acessar diretamente recursos do Cosmos DB com as permissões definidas pelo token de recurso e no intervalo permitido por ele.</span><span class="sxs-lookup"><span data-stu-id="dad05-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="dad05-155">Quando o token de recurso expira, as solicitações seguintes recebem uma exceção 401 de não autorizado.</span><span class="sxs-lookup"><span data-stu-id="dad05-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="dad05-156">Nesse ponto, o aplicativo móvel restabelece a identidade e solicita um novo token de recurso.</span><span class="sxs-lookup"><span data-stu-id="dad05-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Fluxo de trabalho dos tokens de recurso do Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="dad05-158">A geração e o gerenciamento do token de recurso são manipulados pelas bibliotecas de cliente nativas do Cosmos DB; no entanto, se você usar a REST, deverá construir os cabeçalhos de solicitação/autenticação.</span><span class="sxs-lookup"><span data-stu-id="dad05-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="dad05-159">Para obter mais informações sobre como criar cabeçalhos de autenticação para a REST, consulte [Controle de Acesso em recursos do Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) ou o [código-fonte de nossos SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="dad05-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="dad05-160">Para obter um exemplo de um serviço de camada intermediária usado para gerar, ou tokens de recurso do agente, confira o [aplicativo ResourceTokenBroker](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="dad05-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="dad05-161">Usuários</span><span class="sxs-lookup"><span data-stu-id="dad05-161">Users</span></span>
<span data-ttu-id="dad05-162">Os usuários do Cosmos DB são associados a um banco de dados do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dad05-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="dad05-163">Cada banco de dados pode conter nenhum ou mais usuários do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dad05-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="dad05-164">O exemplo de código a seguir mostra como criar um recurso de usuário do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dad05-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="dad05-165">Cada usuário do Cosmos DB tem uma propriedade PermissionsLink que pode ser usada para recuperar a lista de [permissões](#permissions) associadas ao usuário.</span><span class="sxs-lookup"><span data-stu-id="dad05-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="dad05-166">Permissões</span><span class="sxs-lookup"><span data-stu-id="dad05-166">Permissions</span></span>
<span data-ttu-id="dad05-167">Um recurso de permissão do Cosmos DB é associado a um usuário do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dad05-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="dad05-168">Cada usuário pode conter nenhuma ou mais permissões do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dad05-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="dad05-169">Um recurso de permissão fornece acesso a um token de segurança de que o usuário precisa ao tentar acessar um recurso de aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="dad05-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="dad05-170">Há dois níveis de acesso disponíveis que podem ser fornecidos por um recurso de permissão:</span><span class="sxs-lookup"><span data-stu-id="dad05-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="dad05-171">Tudo: o usuário tem permissão total com relação ao recurso.</span><span class="sxs-lookup"><span data-stu-id="dad05-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="dad05-172">Leitura: O usuário pode apenas ler o conteúdo do recurso, mas não pode executar operações de gravação, atualização ou exclusão no recurso.</span><span class="sxs-lookup"><span data-stu-id="dad05-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="dad05-173">Para executar os procedimentos armazenados do Cosmos DB, o usuário deve ter a permissão Tudo na coleção na qual o procedimento armazenado será executado.</span><span class="sxs-lookup"><span data-stu-id="dad05-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="dad05-174">Exemplo de código para criar permissão</span><span class="sxs-lookup"><span data-stu-id="dad05-174">Code sample to create permission</span></span>

<span data-ttu-id="dad05-175">O exemplo de código a seguir mostra como criar um recurso de permissão, ler o token de recurso do recurso de permissão e associar as permissões ao [usuário](#users) criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dad05-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="dad05-176">Se você tiver especificado uma chave de partição para sua coleção, depois a permissão para coleta, os recursos de documento e anexo também deverão incluir o ResourcePartitionKey além do ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="dad05-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="dad05-177">Exemplo de código para permissões de leitura para usuário</span><span class="sxs-lookup"><span data-stu-id="dad05-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="dad05-178">Para obter facilmente todos os recursos de permissão associados a determinado usuário, o Cosmos DB disponibiliza um feed de permissões para cada objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="dad05-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="dad05-179">O trecho de código a seguir mostra como recuperar a permissão associada ao usuário criado acima, construir uma lista de permissões e instanciar um novo DocumentClient em nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="dad05-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dad05-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dad05-180">Next steps</span></span>
* <span data-ttu-id="dad05-181">Para saber mais sobre a segurança do banco de dados do Cosmos DB, consulte [Cosmos DB: Segurança do banco de dados](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="dad05-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="dad05-182">Para saber mais sobre como gerenciar chaves mestras e chaves somente leitura, consulte [Como gerenciar uma conta do Azure Cosmos DB](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="dad05-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="dad05-183">Para saber como construir tokens de autorização do Azure Cosmos DB, consulte [Controle de Acesso em recursos do Azure Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="dad05-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
