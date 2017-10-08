---
title: "aaaAzure Cosmos DB automação - gerenciamento com o Powershell | Microsoft Docs"
description: Use o Azure PowerShell para gerenciar suas contas do Azure Cosmos DB.
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Criar uma conta do Azure Cosmos DB usando o PowerShell

Olá, guia a seguir descreve comandos tooautomate do gerenciamento de suas contas de banco de dados do banco de dados do Azure Cosmos usando o Powershell do Azure. Ele também inclui chaves de conta toomanage comandos e prioridades de failover em [contas de banco de dados de várias regiões][scaling-globally]. Atualize sua conta de banco de dados permite que você toomodify políticas de consistência e adicionar ou remover regiões. Para o gerenciamento de plataforma cruzada de sua conta do Azure Cosmos DB, você pode usar [CLI do Azure](cli-samples.md), Olá [API de REST do provedor de recursos][rp-rest-api], ou hello [Azure Portal](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Introdução

Siga as instruções de saudação em [como tooinstall e configurar o Azure PowerShell] [ powershell-install-configure] tooinstall e efetuar login no tooyour do Azure Resource Manager conta no Powershell.

### <a name="notes"></a>Observações

* Se você desejar Olá tooexecute comandos a seguir sem a necessidade de confirmação do usuário, acrescentar Olá `-Force` sinalizador toohello comando.
* Saudação de todos os comandos a seguir são síncronas.

## <a id="create-documentdb-account-powershell"></a> Criar uma conta do Azure Cosmos DB

Este comando permite que você toocreate uma conta de banco de dados do banco de dados do Azure Cosmos. Configure sua nova conta de banco de dados como região única ou [várias regiões][scaling-globally] com uma [política de consistência](consistency-levels.md) determinada.

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nome de local de saudação do hello região da conta de banco de dados de saudação de gravação. Esse local é necessário toohave um valor de prioridade de failover de 0. Deve haver exatamente uma região de gravação por conta do banco de dados.
* `<read-region-location>`nome de local de saudação do hello ler região da conta de banco de dados de saudação. Esse local é necessário toohave um valor de prioridade de failover de maior que 0. Pode haver mais de uma região de leitura por conta do banco de dados.
* `<ip-range-filter>`Especifica o conjunto de saudação de endereços IP ou intervalos de endereços IP no toobe de formulário CIDR incluído como Olá permitido a lista de IPs de cliente para uma conta de banco de dados especificado. Os intervalos/endereços IP devem ser separados por vírgula e não devem conter espaços. Para obter mais informações, consulte [Suporte ao firewall do Azure Cosmos DB](firewall-support.md)
* `<default-consistency-level>`nível de consistência de padrão de saudação do hello Azure Cosmos DB conta. Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).
* `<max-interval>`Quando usado com consistência envelhecimento limitado, esse valor representa a quantidade de tempo de saudação de desatualização associada (em segundos) tolerada. O intervalo aceito para este valor é de 1 a 100.
* `<max-staleness-prefix>`Quando usado com consistência envelhecimento limitado, esse valor representa o número de saudação de solicitações obsoletos tolerado. O intervalo aceito para este valor é de 1 a 2,147,483,647.
* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<resource-group-location>`local de saudação do hello conta de banco de dados do novo banco de dados do Azure Cosmos do grupo de recursos do Azure toowhich Olá pertence.
* `<database-account-name>`nome de saudação da conta de banco de dados do hello Azure Cosmos DB toobe criado. Ele só pode usar letras minúsculas, números, hello '-' caracteres e deve ser entre 3 e 50 caracteres.

Exemplo: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Observações
* Olá exemplo anterior cria uma conta de banco de dados com duas regiões. Também é possível toocreate uma conta de banco de dados com uma região (que é designada como a região de gravação da saudação e ter um valor de prioridade de failover de 0) ou mais de duas regiões. Para saber mais, veja [Contas de banco de dados com várias regiões][scaling-globally].
* locais de saudação devem ser regiões em que o banco de dados do Azure Cosmos está disponível. lista atual de saudação de regiões é fornecida em Olá [página regiões do Azure](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a> Atualizar uma conta de banco de dados do DocumentDB

Este comando permite que você tooupdate propriedades da conta de banco de dados de banco de dados do Azure Cosmos. Isso inclui locais hello e política de consistência Olá qual conta de banco de dados Olá existe no.

> [!NOTE]
> Este comando permite que você tooadd e remover regiões, mas não permite toomodify prioridades de failover. toomodify prioridades de failover, consulte [abaixo](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nome de local de saudação do hello região da conta de banco de dados de saudação de gravação. Esse local é necessário toohave um valor de prioridade de failover de 0. Deve haver exatamente uma região de gravação por conta do banco de dados.
* `<read-region-location>`nome de local de saudação do hello ler região da conta de banco de dados de saudação. Esse local é necessário toohave um valor de prioridade de failover de maior que 0. Pode haver mais de uma região de leitura por conta do banco de dados.
* `<default-consistency-level>`nível de consistência de padrão de saudação do hello Azure Cosmos DB conta. Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).
* `<ip-range-filter>`Especifica o conjunto de saudação de endereços IP ou intervalos de endereços IP no toobe de formulário CIDR incluído como Olá permitido a lista de IPs de cliente para uma conta de banco de dados especificado. Os intervalos/endereços IP devem ser separados por vírgula e não devem conter espaços. Para obter mais informações, consulte [Suporte ao firewall do Azure Cosmos DB](firewall-support.md)
* `<max-interval>`Quando usado com consistência envelhecimento limitado, esse valor representa a quantidade de tempo de saudação de desatualização associada (em segundos) tolerada. O intervalo aceito para este valor é de 1 a 100.
* `<max-staleness-prefix>`Quando usado com consistência envelhecimento limitado, esse valor representa o número de saudação de solicitações obsoletos tolerado. O intervalo aceito para este valor é de 1 a 2,147,483,647.
* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<resource-group-location>`local de saudação do hello conta de banco de dados do novo banco de dados do Azure Cosmos do grupo de recursos do Azure toowhich Olá pertence.
* `<database-account-name>`nome de saudação da conta de banco de dados do hello Azure Cosmos DB toobe atualizado.

Exemplo: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> Excluir uma conta de banco de dados do DocumentDB

Este comando permite que você toodelete uma conta de banco de dados existente do banco de dados do Azure Cosmos.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<database-account-name>`nome de saudação da conta de banco de dados do hello Azure Cosmos DB toobe excluído.

Exemplo:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a>Obter propriedades de uma conta de banco de dados do DocumentDB

Este comando permite que você tooget propriedades de saudação de uma conta de banco de dados existente do banco de dados do Azure Cosmos.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<database-account-name>`nome de saudação do hello conta de banco de dados do banco de dados do Azure Cosmos.

Exemplo:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> Atualizar as marcações de uma conta de banco de dados do Azure Cosmos DB

Olá exemplo a seguir descreve como tooset [marcas de recurso do Azure] [ azure-resource-tags] para seu banco de dados do Azure Cosmos conta banco de dados.

> [!NOTE]
> Este comando pode ser combinado com hello criar ou atualizar comandos acrescentando Olá `-Tags` sinalizador com parâmetro correspondente hello.

Exemplo:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> Listar chaves da conta

Quando você cria uma conta de banco de dados do Azure Cosmos, o serviço de hello gera duas chaves de acesso principal que podem ser usadas para autenticação quando hello Azure Cosmos DB conta é acessada. Fornecendo duas chaves de acesso, o banco de dados do Azure Cosmos permite chaves de saudação tooregenerate com tooyour sem interrupção conta de banco de dados do Azure Cosmos. Também estão disponíveis chaves somente leitura para autenticação de operações somente leitura. Há duas chaves de leitura/gravação (primária e secundária) e duas chaves somente leitura (primária e secundária).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<database-account-name>`nome de saudação do hello conta de banco de dados do banco de dados do Azure Cosmos.

Exemplo:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> Listar Cadeias de Conexão

Para contas do MongoDB, Olá tooconnect de cadeia de caracteres de conexão, que sua conta de banco de dados do MongoDB aplicativo toohello pode ser recuperada usando o comando a seguir de saudação.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<database-account-name>`nome de saudação do hello conta de banco de dados do banco de dados do Azure Cosmos.

Exemplo:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> Recuperar a chave da conta

Você deve alterar a conta de banco de dados do Azure Cosmos Olá acesso chaves tooyour periodicamente toohelp manter suas conexões mais segura. Duas chaves de acesso atribuídas tooenable você toomaintain conexões toohello conta de banco de dados do Azure Cosmos usando uma chave de acesso enquanto você regenera Olá outra chave de acesso.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<database-account-name>`nome de saudação do hello conta de banco de dados do banco de dados do Azure Cosmos.
* `<key-kind>`Um dos Olá quatro tipos de chaves: ["Principal" | " Secundário "|" PrimaryReadonly "|" SecondaryReadonly"] que deseja tooregenerate.

Exemplo:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> Modificar a Prioridade de Failover de uma Conta de Banco de Dados do Azure Cosmos DB

Para contas de banco de dados de várias regiões, você pode alterar a prioridade de failover de saudação da saudação várias regiões que Olá conta de banco de dados do banco de dados do Azure Cosmos existe no. Para obter mais informações sobre failover em sua conta de banco de dados do Azure Cosmos DB, consulte [Distribuir dados globalmente com o Azure Cosmos DB][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`nome de local de saudação do hello região da conta de banco de dados de saudação de gravação. Esse local é necessário toohave um valor de prioridade de failover de 0. Deve haver exatamente uma região de gravação por conta do banco de dados.
* `<read-region-location>`nome de local de saudação do hello ler região da conta de banco de dados de saudação. Esse local é necessário toohave um valor de prioridade de failover de maior que 0. Pode haver mais de uma região de leitura por conta do banco de dados.
* `<resource-group-name>`nome de saudação do hello [o grupo de recursos do Azure] [ azure-resource-groups] conta toowhich Olá novo banco de dados do Azure Cosmos banco de dados pertence.
* `<database-account-name>`nome de saudação do hello conta de banco de dados do banco de dados do Azure Cosmos.

Exemplo:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Próximas etapas

* tooconnect usando .NET, consulte [conectar e consultar com .NET](create-documentdb-dotnet.md).
* tooconnect usando .NET Core, consulte [conectar e consultar com .NET Core](create-documentdb-dotnet-core.md).
* tooconnect usando Node. js, consulte [conectar e consultar com Node. js e um aplicativo do MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
