---
title: aaaManage Cache Redis do Azure usando a CLI do Azure | Microsoft Docs
description: "Saiba como tooinstall Olá CLI do Azure em qualquer plataforma, como toouse-tooconnect tooyour conta do Azure e como toocreate e gerenciar um cache Redis da saudação CLI do Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Como toocreate e gerenciar o Cache Redis do Azure usando hello Azure Interface de linha de comando (CLI do Azure)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [CLI do Azure](cache-manage-cli.md)
>
>

Olá CLI do Azure é uma ótima maneira toomanage sua infraestrutura do Azure de qualquer plataforma. Este artigo mostra como toocreate e gerenciar suas instâncias de Cache Redis do Azure usando Olá CLI do Azure.

> [!NOTE]
> Este artigo se aplica a versão anterior do tooa da CLI do Azure. Para scripts de exemplo 2.0 do CLI do Azure mais recentes hello, consulte [exemplos de cache Redis do Azure CLI](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toocreate e gerenciar instâncias de Cache Redis do Azure usando a CLI do Azure, você deve concluir Olá etapas a seguir.

* Você deve ter uma conta do Azure. Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
* [Instalar Olá CLI do Azure](../cli-install-nodejs.md).
* Conecte-se a instalação da CLI do Azure com uma conta do Azure pessoal ou com um trabalho ou escola conta do Azure e fazer logon em Olá CLI do Azure usando Olá `azure login` comando. toounderstand Olá diferenças e escolher, consulte [conectar tooan assinatura do Azure do hello Azure Interface de linha de comando (CLI do Azure)](../xplat-cli-connect.md).
* Antes de executar qualquer um dos comandos a seguir de saudação, comutador hello CLI do Azure no modo do Gerenciador de recursos executando Olá `azure config mode arm` comando. Para obter mais informações, consulte [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Propriedades do Cache Redis
propriedades seguintes Hello são usadas ao criar e atualizar instâncias de Cache Redis.

| Propriedade | Switch | Descrição |
| --- | --- | --- |
| name |-n, --name |Nome da saudação Cache Redis. |
| grupo de recursos |-g, --resource-group |Nome da saudação grupo de recursos. |
| location |-l, --location |Cache de toocreate local. |
| tamanho |-z, --size |Tamanho do Cache Redis da saudação. Valores válidos: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| sku |-x, --sku |SKU Redis. Deve ser um destes: [Básico, Standard, Premium] |
| EnableNonSslPort |-e, --enable-non-ssl-port |Propriedade EnableNonSslPort de saudação Cache Redis. Adicione esse sinalizador se você quiser tooenable Olá não SSL porta para o cache |
| Configuração do Redis |-c, --redis-configuration |Configuração do Redis. Insira uma cadeia de caracteres JSON formatada de valores e chaves de configuração aqui. Format:"{"":"","":""}" |
| Configuração do Redis |-f, --redis-configuration-file |Configuração do Redis. Insira o caminho de saudação de um arquivo que contém as chaves de configuração e os valores aqui. Formato de entrada do arquivo hello: {"": "","": ""} |
| Contagem de Fragmento |-r, --shard-count |Número de fragmentos toocreate em um Cache de Cluster Premium com o cluster. |
| Rede Virtual |-v, --virtual-network |Quando seu cache em uma rede virtual de hospedagem Especifica Olá exata ARM ID de recurso Olá Olá de toodeploy de rede virtual redis cache no. Exemplo de formato: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| tipo de chave |-t, --key-type |Tipo de chave toorenew. Valores válidos: [Primary, Secondary] |
| StaticIP |-p, --static-ip <static-ip> |Ao hospedar o cache em uma rede virtual, especifica um endereço IP exclusivo na sub-rede Olá para o cache de saudação. Se não for fornecido, um é escolhido para você de sub-rede hello. |
| Sub-rede |t, --subnet <subnet> |Ao hospedar o cache em uma rede virtual, especifica o nome de saudação de sub-rede de saudação no cache de saudação que toodeploy. |
| VirtualNetwork |-v, --virtual-network <rede virtual> |Quando seu cache em uma rede virtual de hospedagem Especifica Olá exata ARM ID de recurso Olá Olá de toodeploy de rede virtual redis cache no. Exemplo de formato: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Assinatura |-s, --subscription |Identificador de assinatura de saudação. |

## <a name="see-all-redis-cache-commands"></a>Ver todos os comandos do Cache Redis
toosee todos os comandos de Redis Cache e seus parâmetros, use Olá `azure rediscache -h` comando.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Criar um Cache Redis
toocreate um Cache Redis, use Olá comando a seguir:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Para obter mais informações sobre esse comando, execute Olá `azure rediscache create -h` comando.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Excluir um Cache Redis existente
toodelete um Cache Redis, use Olá comando a seguir:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Para obter mais informações sobre esse comando, execute Olá `azure rediscache delete -h` comando.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Listar todos os Caches Redis em sua Assinatura ou Grupo de Recursos
toolist todos os Caches Redis dentro de sua assinatura ou grupo de recursos, use Olá seguinte comando:

    azure rediscache list [options]

Para obter mais informações sobre esse comando, execute Olá `azure rediscache list -h` comando.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Mostrar as propriedades de um Cache Redis existente
tooshow propriedades de um Cache Redis existente, use Olá comando a seguir:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Para obter mais informações sobre esse comando, execute Olá `azure rediscache show -h` comando.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Alterar as configurações de um Cache Redis existente
toochange configurações de um Cache Redis existente, use Olá comando a seguir:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Para obter mais informações sobre esse comando, execute Olá `azure rediscache set -h` comando.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Renovar a chave de autenticação Olá para um Cache existente Redis
chave de autenticação toorenew Olá para um Redis Cache existente, use Olá comando a seguir:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Especifique `Primary` ou `Secondary` como `key-type`.

Para obter mais informações sobre esse comando, execute Olá `azure rediscache renew-key -h` comando.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Listar as chaves Primária e Secundária de um Cache Redis existente
as chaves primária e secundária toolist de um Cache Redis existente, use Olá comando a seguir:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Para obter mais informações sobre esse comando, execute Olá `azure rediscache list-keys -h` comando.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
