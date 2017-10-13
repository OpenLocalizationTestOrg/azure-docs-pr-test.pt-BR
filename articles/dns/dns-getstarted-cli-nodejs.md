---
title: "Introdução ao DNS do Azure usando a CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como criar uma zona e registro DNS no DNS do Azure. Este é uma guia passo a passo para criar e gerenciar sua primeira zona e registro DNS usando a CLI do Azure 1.0."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a>Introdução ao DNS do Azure usando a CLI do Azure 1.0

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI 1.0 do Azure](dns-getstarted-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-getstarted-cli.md)

Este artigo explica as etapas de criação de sua primeira zona e registro DNS usando a CLI do Azure 1.0 entre plataformas, que está disponível para Windows, Mac e Linux. Você também pode executar essas etapas usando o Portal do Azure ou o Azure PowerShell.

Uma zona DNS é usada para hospedar os registros DNS para um domínio específico. Para iniciar a hospedagem do seu domínio no DNS do Azure, você precisará criar uma zona DNS para esse nome de domínio. Cada registro DNS para seu domínio é criado dentro dessa zona DNS. Por fim, para publicar sua zona DNS na Internet, você precisa configurar os servidores de nome para o domínio. Cada uma dessas etapas é descrita abaixo.

Essas instruções pressupõem que você já instalou e entrou na CLI do Azure 1.0. Para obter ajuda, confira [Como gerenciar as zonas DNS usando a CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md).

## <a name="create-the-resource-group"></a>Criar o grupo de recursos

Antes de criar a zona DNS, um grupo de recursos é criado para conter a zona DNS. O código a seguir mostra o comando.

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada usando o comando `azure network dns zone create` . Para ver a ajuda desse comando, digite `azure network dns zone create -h`.

O exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos chamado *MyResourceGroup*. Use o exemplo para criar uma zona DNS, substituindo os valores pelos seus próprios.

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a>Criar um registro DNS

Para criar um registro DNS, use o comando `azure network dns record-set add-record`. Para obter ajuda, consulte `azure network dns record-set add-record -h`.

O exemplo a seguir cria um registro com o nome relativo "www" na Zona DNS "contoso.com", no grupo de recursos "MyResourceGroup". O nome totalmente qualificado do conjunto de registros é “www.contoso.com”. O tipo de registro é "A", com o endereço IP "1.2.3.4", e um TTL padrão de 3600 segundos (1 hora) é usado.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

Para outros tipos de registros, para conjuntos de registros com mais de um registro, para valores de TTL alternativos e para modificar registros existentes, consulte [Gerenciar registros DNS e conjuntos de registros usando a CLI do Azure 1.0](dns-operations-recordsets-cli-nodejs.md).


## <a name="view-records"></a>Exibir registros

Para listar os registros DNS em sua zona, use:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a>Atualizar servidores de nome

Quando você estiver satisfeito com a configuração de sua zona e registros DNS, configure seu nome de domínio para usar os servidores de nome DNS do Azure. Isso permite que outros usuários na Internet encontrem os registros DNS.

Os servidores de nomes de sua zona são fornecidos pelo comando `azure network dns zone show`:

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

Esses servidores de nome devem ser configurados com o registrador de nome de domínio (onde você adquiriu o nome de domínio). Seu registrador oferecerá a opção de configurar os servidores de nome do domínio. Para saber mais, confira [Delegar um domínio ao DNS do Azure](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Excluir todos os recursos
 
Para excluir todos os recursos criados neste artigo, execute as seguintes etapas:

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o DNS do Azure, veja [Visão geral do DNS do Azure](dns-overview.md).

Para saber mais sobre como gerenciar as zonas DNS no DNS do Azure, veja [Gerenciar zonas DNS no DNS do Azure usando a CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md).

Para saber mais sobre como gerenciar os registros DNS no DNS do Azure, veja [Gerenciar registros DNS e conjuntos de registros no DNS do Azure usando a CLI do Azure 1.0](dns-operations-recordsets-cli-nodejs.md).

