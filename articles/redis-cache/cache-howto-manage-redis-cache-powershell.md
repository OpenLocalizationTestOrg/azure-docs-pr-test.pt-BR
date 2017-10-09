---
title: aaaManage Cache Redis do Azure com o Azure PowerShell | Microsoft Docs
description: Saiba como tooperform de tarefas administrativas para o Cache Redis do Azure usando o PowerShell do Azure.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Gerenciar o Cache Redis do Azure com o PowerShell do Azure
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [CLI do Azure](cache-manage-cli.md)
> 
> 

Este tópico mostra como tooperform comuns tarefas como criar, atualizar e dimensione suas instâncias de Cache Redis do Azure, como chaves de acesso tooregenerate e como tooview informações sobre seus caches. Para obter uma lista completa de cmdlets do PowerShell do Cache Redis do Azure, confira [Cmdlets do Cache Redis do Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Para obter mais informações sobre o modelo de implantação clássico hello, consulte [do Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Pré-requisitos
Se você já instalou o Azure PowerShell, você deve ter o Azure PowerShell versão 1.0.0 ou posterior. Você pode verificar a versão de saudação do PowerShell do Azure que você instalou com este comando no prompt de comando do PowerShell do Azure hello.

    Get-Module azure | format-table version


Primeiro, você deve efetuar login tooAzure com este comando.

    Login-AzureRmAccount

Especifique o endereço de email de saudação de sua conta do Azure e sua senha na caixa de diálogo Olá entrar no Microsoft Azure.

Em seguida, se você tiver várias assinaturas do Azure, será necessário tooset sua assinatura do Azure. toosee uma lista de suas assinaturas atuais, execute este comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

assinatura toospecify Olá executar Olá comando a seguir. Olá exemplo a seguir, nome de assinatura Olá é `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Antes de usar o Windows PowerShell com o Gerenciador de recursos do Azure, você precisa seguir hello:

* Windows PowerShell, versão 3.0 ou 4.0. versão de saudação do toofind do Windows PowerShell, digite:`$PSVersionTable` e verifique se o valor de saudação do `PSVersion` é 3.0 ou 4.0. tooinstall uma versão compatível, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget ajuda detalhada para qualquer cmdlet, que consulte neste tutorial, use Olá o cmdlet Get-Help.

    Get-Help <cmdlet-name> -Detailed

Por exemplo, tooget ajuda Olá `New-AzureRmRedisCache` cmdlet, digite:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Como tooconnect tooother nuvens
Por saudação padrão do Azure é ambiente `AzureCloud`, que representa Olá instância global em nuvem do Azure. tooconnect tooa instância diferente, use Olá `Add-AzureRmAccount` com hello `-Environment` ou -`EnvironmentName` opção de linha de comando com o ambiente desejado hello ou nome do ambiente.

lista de saudação toosee ambientes disponíveis, execute Olá `Get-AzureRmEnvironment` cmdlet.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello nuvem do Azure Government
tooconnect toohello nuvem do governo do Azure, use um dos Olá comandos a seguir.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

ou o

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate um cache no hello Azure governamental nuvem, use um dos seguintes locais de saudação.

* Gov. dos EUA – Virgínia
* Gov. dos EUA – Iowa

Para obter mais informações sobre hello Azure governamental nuvem, consulte [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) e [guia do desenvolvedor do Microsoft Azure Government](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello nuvem do Azure na China
tooconnect toohello nuvem do Azure na China, use um dos comandos a seguir de saudação.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

ou o

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate um cache na nuvem do Azure na China, usar um dos seguintes locais de saudação do hello.

* Leste da China
* Norte da China

Para obter mais informações sobre Olá nuvem do Azure na China, consulte [AzureChinaCloud para o Azure operado pela 21Vianet na China](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Azure Alemanha
tooconnect tooMicrosoft Azure Alemanha, use um dos comandos a seguir de saudação.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


ou o

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate um cache no Microsoft Azure Alemanha, use um dos seguintes locais de saudação.

* Alemanha Central
* Nordeste da Alemanha

Para obter mais informações sobre o Microsoft Azure Alemanha, consulte [Microsoft Azure Alemanha](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Propriedades usadas para o PowerShell do Cache Redis do Azure
Olá, a tabela a seguir contém as propriedades e descrições dos parâmetros usados ao criar e gerenciar suas instâncias de Cache Redis do Azure usando o PowerShell do Azure.

| Parâmetro | Descrição | Padrão |
| --- | --- | --- |
| Nome |Nome do cache de saudação | |
| Local |Local do cache de saudação | |
| ResourceGroupName |Nome do grupo de recursos no qual cache de saudação toocreate | |
| Tamanho |tamanho de saudação do cache de saudação. Os valores válidos são: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2.5 GB, 6 GB, 13 GB, 26 GB, 53 GB |1 GB |
| ShardCount |número de saudação de fragmentos toocreate ao criar um cache premium com cluster habilitado. Os valores válidos são: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Especifica a saudação SKU do cache de saudação. Os valores válidos são: Básico, Standard e Premium |Standard |
| RedisConfiguration |Especifica as definições de configuração do Redis. Para obter detalhes sobre cada configuração, consulte o seguinte Olá [RedisConfiguration propriedades](#redisconfiguration-properties) tabela. | |
| EnableNonSslPort |Indica se a porta do hello não SSL está habilitada. |Falso |
| MaxMemoryPolicy |Esse parâmetro foi desaprovado - use RedisConfiguration em vez disso. | |
| StaticIP |Ao hospedar o cache em uma rede virtual, especifica um endereço IP exclusivo na sub-rede Olá para o cache de saudação. Se não for fornecido, um é escolhido para você de sub-rede hello. | |
| Sub-rede |Ao hospedar o cache em uma rede virtual, especifica o nome de saudação de sub-rede de saudação no cache de saudação que toodeploy. | |
| VirtualNetwork |Quando hospedando o seu cache em uma rede virtual, especifica a ID de recurso de saudação do hello rede virtual no qual cache de saudação toodeploy. | |
| KeyType |Especifica qual chave de acesso tooregenerate durante a renovação de chaves de acesso. Os valores válidos são: Primary, Secondary | |

### <a name="redisconfiguration-properties"></a>propriedades RedisConfiguration
| Propriedade | Descrição | Tipos de preço |
| --- | --- | --- |
| rdb-backup-enabled |Se [persistência de dados Redis](cache-how-to-premium-persistence.md) está habilitada |Somente Premium |
| rdb-storage-connection-string |Olá conta de armazenamento de toohello de cadeia de caracteres de conexão para [Redis a persistência de dados](cache-how-to-premium-persistence.md) |Somente Premium |
| rdb-backup-frequency |Olá frequência de backup [Redis a persistência de dados](cache-how-to-premium-persistence.md) |Somente Premium |
| maxmemory-reserved |Configura Olá [memória reservada](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para processos não armazenados em cache |Standard e Premium |
| maxmemory-policy |Configura Olá [política de remoção](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para o cache de saudação |Todos os tipos de preço |
| notify-keyspace-events |Configura [notificações keyspace](cache-configure.md#keyspace-notifications-advanced-settings) |Standard e Premium |
| hash-max-ziplist-entries |Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos |Standard e Premium |
| hash-max-ziplist-value |Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos |Standard e Premium |
| set-max-intset-entries |Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos |Standard e Premium |
| zset-max-ziplist-entries |Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos |Standard e Premium |
| zset-max-ziplist-value |Configura [otimização de memória](http://redis.io/topics/memory-optimization) para tipos de dados de agregação pequenos |Standard e Premium |
| databases |Configura o número de saudação de bancos de dados. Essa propriedade pode ser configurada apenas na criação do cache. |Standard e Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate um Cache Redis
Novas instâncias de Cache Redis do Azure são criadas usando Olá [AzureRmRedisCache novo](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

> [!IMPORTANT]
> Olá primeira vez que você criar um cache Redis em uma assinatura usando Olá portal do Azure, portal Olá registra Olá `Microsoft.Cache` namespace para essa assinatura. Se você tentar toocreate Olá primeiro Redis cache em uma assinatura usando o PowerShell, você deve primeiro registrar esse namespace usando Olá comando; a seguir Caso contrário, cmdlets, como `New-AzureRmRedisCache` e `Get-AzureRmRedisCache` falhar.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

toosee uma lista de parâmetros disponíveis e suas descrições para `New-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate um cache com os parâmetros padrão, execute Olá comando a seguir.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, e `Location` são parâmetros obrigatórios, mas o restante da saudação são opcional e têm valores padrão. Executar o comando anterior Olá cria uma instância de padrão SKU Azure Redis Cache com o nome especificado do hello, o local e o grupo de recursos, que é de 1 GB de tamanho com a porta não SSL de saudação desabilitado.

toocreate um cache premium, especifique um tamanho de P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), ou P4 (53 GB - 530 GB). tooenable clustering, especifique uma contagem de fragmento usando Olá `ShardCount` parâmetro. Olá exemplo a seguir cria um cache premium de P1 com 3 fragmentos. Um cache premium de P1 é de 6 GB de tamanho, e como especificamos três fragmentos Olá tamanho total de 18 GB (3 x 6 GB).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

valores de toospecify para hello `RedisConfiguration` parâmetro, coloque valores hello dentro `{}` como chave/valor como pares `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Olá, exemplo a seguir cria um cache padrão de 1 GB com `allkeys-random` notificações keyspace e política maxmemory configuradas com `KEA`. Para obter mais informações, consulte [Notificações de keyspace (configurações avançadas)](cache-configure.md#keyspace-notifications-advanced-settings) e [Políticas de memória](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>bancos de dados do hello tooconfigure configuração durante a criação do cache
Olá `databases` configuração pode ser definida apenas durante a criação do cache. Olá, exemplo a seguir cria um premium P3 (26 GB) de cache com 48 bancos de dados usando Olá [AzureRmRedisCache novo](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Para obter mais informações sobre Olá `databases` propriedade, consulte [configuração do servidor padrão do Azure Redis Cache](cache-configure.md#default-redis-server-configuration). Para obter mais informações sobre como criar um cache usando Olá [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, consulte Olá anterior [toocreate um Cache Redis](#to-create-a-redis-cache) seção.

## <a name="tooupdate-a-redis-cache"></a>tooupdate um cache Redis
Instâncias de Cache Redis do Azure são atualizadas usando Olá [AzureRmRedisCache conjunto](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.

toosee uma lista de parâmetros disponíveis e suas descrições para `Set-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Olá `Set-AzureRmRedisCache` cmdlet pode ser usado tooupdate propriedades como `Size`, `Sku`, `EnableNonSslPort`e hello `RedisConfiguration` valores. 

Olá seguinte comando atualizações Olá política máxmemória Olá Redis Cache nomeado myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale um cache Redis
`Set-AzureRmRedisCache`pode ser usado tooscale uma instância de cache Redis do Azure ao hello `Size`, `Sku`, ou `ShardCount` propriedades são modificadas. 

> [!NOTE]
> Dimensionar um cache usando o PowerShell é o assunto toohello mesmos limites e diretrizes como dimensionar um cache de Olá portal do Azure. Você pode dimensionar tooa diferente preços com hello restrições a seguir.
> 
> * Não é possível redimensionar de um maior preço camada tooa menor preço.
> * Você não pode ser dimensionada de um **Premium** cache para baixo tooa **padrão** ou um **básica** cache.
> * Você não pode ser dimensionada de um **padrão** cache para baixo tooa **básica** cache.
> * Pode ser dimensionada de um **básica** cache tooa **padrão** cache, mas você não pode alterar o tamanho de saudação em Olá simultaneamente. Se você precisar de um tamanho diferente, você pode fazer um tamanho de toohello desejado escala operação subsequente.
> * Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache. Deve ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em uma escala subsequentes operação.
> * Não é possível redimensionar de um tamanho maior para baixo toohello **C0 (250 MB)** tamanho.
> 
> Para obter mais informações, consulte [como tooScale Cache Redis do Azure](cache-how-to-scale.md).
> 
> 

Olá exemplo a seguir mostra como tooscale um cache nomeado `myCache` tooa 2,5 GB cache. Observe que esse comando funciona para um cache Básico ou Standard.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Depois que esse comando for emitido, o status de saudação do cache de saudação é retornado (semelhante toocalling `Get-AzureRmRedisCache`). Observe que Olá `ProvisioningState` é `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Quando a operação de dimensionamento de saudação for concluída, Olá `ProvisioningState` muda muito`Succeeded`. Se você precisar toomake uma operação de dimensionamento subsequente, como a alteração de tooStandard básica e, em seguida, alterando o tamanho de saudação, você deve aguardar até que a operação anterior de saudação é concluída ou você receberá uma erro semelhante toohello a seguir.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>tooget informações sobre um cache Redis
Você pode recuperar informações sobre um cache usando Olá [AzureRmRedisCache Get](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.

toosee uma lista de parâmetros disponíveis e suas descrições para `Get-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooreturn informações sobre todos os caches na assinatura atual do hello, execute `Get-AzureRmRedisCache` sem parâmetros.

    Get-AzureRmRedisCache

tooreturn informações sobre todos os caches em um grupo de recursos específico, execute `Get-AzureRmRedisCache` com hello `ResourceGroupName` parâmetro.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

tooreturn informações sobre um cache específico, execute `Get-AzureRmRedisCache` com hello `Name` parâmetro que contém o nome de saudação do cache hello e hello `ResourceGroupName` parâmetro com o grupo de recursos de saudação que contém esse cache.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>chaves de acesso de saudação tooretrieve para um cache Redis
chaves de acesso tooretrieve Olá para seu cache, você pode usar o hello [AzureRmRedisCacheKey Get](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.

toosee uma lista de parâmetros disponíveis e suas descrições para `Get-AzureRmRedisCacheKey`, execute hello seguinte comando.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Olá tooretrieve chaves para seu cache, chamada hello `Get-AzureRmRedisCacheKey` cmdlet e passar no nome de saudação do cache Olá nome saudação do grupo de recursos que contém o cache de saudação.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>tooregenerate chaves de acesso para seu cache Redis
chaves de acesso tooregenerate Olá para seu cache, você pode usar o hello [AzureRmRedisCacheKey novo](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.

toosee uma lista de parâmetros disponíveis e suas descrições para `New-AzureRmRedisCacheKey`, execute hello seguinte comando.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

chave de primária ou secundária de saudação de tooregenerate para seu cache, chamada hello `New-AzureRmRedisCacheKey` cmdlet e passe Olá name, grupo de recursos e especifique o `Primary` ou `Secondary` para Olá `KeyType` parâmetro. Em Olá exemplo a seguir, chave de acesso secundária Olá para um cache for regenerado.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete um cache Redis
toodelete um cache Redis, use Olá [AzureRmRedisCache remover](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.

toosee uma lista de parâmetros disponíveis e suas descrições para `Remove-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Em Olá exemplo a seguir, Olá cache chamado `myCache` é removido.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport um cache Redis
Você pode importar dados em uma instância de Cache Redis do Azure usando Olá `Import-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> A opção Importar/Exportar está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) . Para saber mais sobre Importar/Exportar, confira [Importar e Exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).
> 
> 

toosee uma lista de parâmetros disponíveis e suas descrições para `Import-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Olá comando a seguir importa dados de blob de saudação especificado pelo uri SAS Olá em Cache Redis do Azure.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport um cache Redis
Você pode exportar dados de uma instância de Cache Redis do Azure usando Olá `Export-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> A opção Importar/Exportar está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) . Para saber mais sobre Importar/Exportar, confira [Importar e Exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).
> 
> 

toosee uma lista de parâmetros disponíveis e suas descrições para `Export-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Olá comando a seguir exporta dados de uma instância de Cache Redis do Azure no contêiner de saudação especificado pelo uri SAS hello.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot um cache Redis
Você pode reinicializar a instância de Cache Redis do Azure usando Olá `Reset-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> A reinicialização está disponível somente para caches do [tipo Premium](cache-premium-tier-intro.md) . Para saber mais sobre a reinicialização de seu cache, confira [Administração de cache - reinicializar](cache-administration.md#reboot).
> 
> 

toosee uma lista de parâmetros disponíveis e suas descrições para `Reset-AzureRmRedisCache`, execute hello seguinte comando.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


comando a seguir Hello reinicializa ambos os nós de saudação especificado cache.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como usar o Windows PowerShell com o Azure, consulte Olá recursos a seguir:

* [Documentação de cmdlet do Cache Redis do Azure no MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Cmdlets do Gerenciador de recursos do Azure](http://go.microsoft.com/fwlink/?LinkID=394765): Saiba mais sobre toouse Olá cmdlets no módulo do Azure Resource Manager hello.
* [Usando o recurso de grupos de toomanage os recursos do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Saiba como toocreate e gerenciar grupos de recursos da saudação portal do Azure.
* [Blog do Azure](http://blogs.msdn.com/windowsazure): obtenha informações sobre os novos recursos no Azure.
* [Blog do Windows PowerShell](http://blogs.msdn.com/powershell): obtenha informações sobre os novos recursos do Windows PowerShell.
* [Blog "Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): obter reais dicas e truques de saudação da comunidade do Windows PowerShell.

