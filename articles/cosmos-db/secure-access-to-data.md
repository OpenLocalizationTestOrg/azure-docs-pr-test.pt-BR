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
# <a name="securing-access-tooazure-cosmos-db-data"></a>Proteção de dados do access tooAzure Cosmos DB
Este artigo fornece uma visão geral de proteção de acesso toodata armazenado em [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).

Banco de dados do Azure Cosmos usa dois tipos de chaves tooauthenticate usuários e fornecer acesso tooits dados e recursos. 

|Tipo de chave|Recursos|
|---|---|
|[Chaves mestras](#master-keys) |Usadas para os recursos administrativos: contas de bancos de dados, bancos de dados, usuários e permissões|
|[Tokens de recurso](#resource-tokens)|Usados para recursos do aplicativo: coleções, documentos, anexos, procedimentos armazenados, gatilhos e UDFs|

<a id="master-keys"></a>

## <a name="master-keys"></a>Chaves mestras 

Chaves mestras forneça acesso toohello todos os recursos administrativos do hello para Olá banco de dados. Chaves mestras:  
- Forneça acesso tooaccounts, bancos de dados, os usuários e permissões. 
- Não pode ser usado tooprovide acesso granular toocollections e documentos.
- São criados durante a criação de saudação de uma conta.
- Podem ser geradas novamente a qualquer momento.

Cada conta é formada por duas Chaves mestras: uma chave primária e uma chave secundária. Olá finalidade chaves duplas é para que você pode gerar novamente ou reverter chaves, fornecendo dados e a conta de acesso contínuo a tooyour. 

Em adição toohello duas chaves de mestre para conta de banco de dados do Cosmos hello, há duas chaves somente leitura. Essas chaves somente leitura apenas permitem operações de leitura na conta de saudação. Chaves somente leitura não fornecem acesso a recursos de permissões tooread.

Primária, secundária somente leitura e chaves mestras de leitura / gravação podem ser recuperadas e regeneradas usando Olá portal do Azure. Para obter instruções, veja [Exibir, copiar e gerar novamente as chaves de acesso](manage-account.md#keys).

![Controle de acesso (IAM) no portal do Azure - demonstrando a segurança de banco de dados NoSQL de saudação](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

processo de saudação de girar a chave mestra é simple. Navegue toohello tooretrieve portal do Azure a chave secundária, em seguida, substituir a chave primária com a chave secundária em seu aplicativo e girar a chave primária Olá Olá portal do Azure.

![Rotação da chave mestra no portal do Azure - demonstrando a segurança de banco de dados NoSQL de saudação](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Código de exemplo toouse uma chave mestra

Olá exemplo de código a seguir ilustra como toouse um banco de dados do Cosmos uma DocumentClient tooinstantiate de ponto de extremidade e a chave mestra da conta e criar um banco de dados. 

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

## <a name="resource-tokens"></a>Tokens de recurso

Tokens de recurso fornecem acesso a recursos do aplicativo toohello dentro de um banco de dados. Tokens de recurso:
- Forneça acesso toospecific coleções, as chaves de partição, documentos, anexos, procedimentos armazenados, gatilhos e UDFs.
- São criados quando um [usuário](#users) é concedida [permissões](#permissions) tooa determinado recurso.
- São recriados quando um recurso de permissão recebe uma ação de uma chamada POST, GET ou PUT.
- Use um token de recurso de hash construído especificamente para o usuário hello, recursos e permissão.
- São associados a um período de validade personalizável. período de tempo válido saudação padrão é uma hora. Vida útil do token, no entanto, pode ser especificado explicitamente, o máximo de tooa de cinco horas.
- Forneça uma segurança toogiving alternativo Olá mestre chave. 
- Habilite clientes tooread, gravação e exclusão de recursos na conta de banco de dados do Cosmos Olá toohello permissões que lhe foi concedidos de acordo com.

Você pode usar um token de recursos (ao criar usuários de banco de dados do Cosmos e permissões) quando você quiser tooprovide tooresources de acesso no seu banco de dados do Cosmos conta cliente tooa não pode ser confiável com a chave mestra de saudação.  

Tokens de recurso do cosmos DB fornecem uma alternativa segura que permite que clientes tooread, gravação e exclusão recursos em sua conta de banco de dados do Cosmos permissões toohello que você concedeu de acordo com e sem necessidade de qualquer um mestre ou chave somente de leitura.

Este é um padrão de design típico no qual os tokens de recurso podem ser solicitados, gerados e entregue tooclients:

1. Um serviço de camada intermediária é configurado tooserve fotos do usuário de tooshare um aplicativo móvel. 
2. serviço de camada intermediária Olá possui a chave mestra de saudação do hello conta de banco de dados do Cosmos.
3. aplicativo de fotos Hello está instalado em dispositivos móveis do usuário final. 
4. Em logon, o aplicativo de fotos Olá estabelece identidade de saudação do usuário de saudação com o serviço de camada intermediária Olá. Esse mecanismo de estabelecimento de identidade é puramente toohello aplicativo.
5. Após o estabelecimento de identidade Olá, solicitações de serviço de nível intermediário de saudação permissões com base na identidade de saudação.
6. serviço de camada intermediária Olá envia um aplicativo de telefone do recurso token toohello voltar.
7. aplicativo de telefone Olá pode continuar toouse Olá recurso token toodirectly acessar banco de dados do Cosmos os recursos com permissões de saudação definidas pelo token de recurso Olá e para o intervalo de saudação permitido pelo token de recurso de saudação. 
8. Quando o token de recurso Olá expira, as solicitações subsequentes recebem uma exceção de 401 não autorizado.  Neste ponto, aplicativo de telefone Olá restabelece identidade hello e solicita um novo token de recurso.

    ![Fluxo de trabalho dos tokens de recurso do Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

Gerenciamento e geração de token de recurso é tratado por bibliotecas de cliente Cosmos DB nativo Olá; No entanto, se você usar o REST, você precisa construir cabeçalhos de solicitação/autenticação hello. Para obter mais informações sobre a criação de cabeçalhos de autenticação para REST, consulte [controle de acesso nos recursos de banco de dados do Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) ou hello [código-fonte para nossos SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Para um exemplo de um serviço de camada intermediária usados toogenerate ou agente de tokens de recurso, consulte Olá [ResourceTokenBroker aplicativo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Usuários
Os usuários do Cosmos DB são associados a um banco de dados do Cosmos DB.  Cada banco de dados pode conter nenhum ou mais usuários do Cosmos DB.  Olá mostra exemplo de código a seguir como toocreate um recurso de usuário de banco de dados do Cosmos.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Cada usuário de banco de dados do Cosmos tem uma propriedade PermissionsLink que pode ser usado tooretrieve Olá lista de [permissões](#permissions) associado Olá usuário.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Permissões
Um recurso de permissão do Cosmos DB é associado a um usuário do Cosmos DB.  Cada usuário pode conter nenhuma ou mais permissões do Cosmos DB.  Um recurso de permissão fornece o token de segurança do acesso tooa que Olá necessidades dos usuários durante a tentativa de tooaccess um recurso de aplicativo específico.
Há dois níveis de acesso disponíveis que podem ser fornecidos por um recurso de permissão:

* All: usuário Olá tem permissão total em recurso hello.
* Leitura: usuário Olá somente pode ler o conteúdo de saudação do recurso de saudação mas não é possível executar a gravação, atualização ou operações de exclusão no recurso de saudação.

> [!NOTE]
> Em ordem toorun Cosmos DB procedimentos armazenados Olá usuário deve ter Olá todas as permissões na coleção de saudação no qual Olá procedimento armazenado será executado.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Permissão de toocreate de exemplo de código

Olá exemplo de código a seguir mostra como toocreate um recurso de permissão de leitura Olá token de recurso do recurso de permissão hello e associar permissões Olá Olá [usuário](#users) criado acima.

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

Se você tiver especificado que uma chave de partição para o seu conjunto, em seguida, permissão Olá para recursos de coleção, documentos e anexos também deve incluir Olá ResourcePartitionKey em adição toohello ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Permissões de tooread de exemplo de código do usuário

tooeasily obter todos os recursos de permissão associados a um usuário específico, Cosmos DB disponibiliza uma permissão de feed para cada objeto de usuário.  Olá trecho de código a seguir mostra como a permissão de saudação tooretrieve associado Olá usuário criado acima, construir uma lista de permissão e criar uma instância de um novo DocumentClient em nome de usuário de saudação.

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

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a segurança de banco de dados do banco de dados do Cosmos, consulte [Cosmos DB: segurança de banco de dados](database-security.md).
* toolearn sobre o gerenciamento de chaves mestres e somente leitura, consulte [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md#keys).
* toolearn como tokens de autorização do banco de dados do Azure Cosmos tooconstruct, consulte [controle de acesso nos recursos de banco de dados do Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
