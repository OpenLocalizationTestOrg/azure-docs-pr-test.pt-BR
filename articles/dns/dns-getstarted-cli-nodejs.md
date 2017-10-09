---
title: aaaGet iniciado com o DNS do Azure usando o Azure CLI 1.0 | Microsoft Docs
description: "Saiba como toocreate um DNS zona e registro de DNS do Azure. Isso é um guia passo a passo toocreate e gerenciar sua primeira zona DNS e o registro usando Olá 1.0 da CLI do Azure."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a>Introdução ao DNS do Azure usando a CLI do Azure 1.0

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI 1.0 do Azure](dns-getstarted-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-getstarted-cli.md)

Este artigo orienta Olá etapas toocreate sua primeira zona DNS e o registro usando Olá plataforma cruzada do Azure CLI 1.0, que está disponível para Windows, Mac e Linux. Você também pode executar essas etapas usando Olá portal do Azure ou o Azure PowerShell.

Uma zona DNS é usado toohost Olá registros DNS para um domínio específico. toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio. Cada registro DNS para seu domínio é criado dentro dessa zona DNS. Finalmente, toopublish o DNS da zona toohello da Internet, você precisa de servidores de nome de saudação tooconfigure para domínio de saudação. Cada uma dessas etapas é descrita abaixo.

Essas instruções presumem que você já instalado e conectado tooAzure CLI 1.0. Para obter ajuda, consulte [como toomanage DNS zonas usando o Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Antes de criar a zona DNS de saudação, um grupo de recursos é criado toocontain Olá DNS zona. Veja a seguir de Olá comando hello.

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada usando Olá `azure network dns zone create` comando. toosee ajuda para este comando, digite `azure network dns zone create -h`.

Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*. Use toocreate de exemplo hello uma zona DNS, substituindo valores de saudação para seu próprio.

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a>Criar um registro DNS

toocreate um registro DNS, use Olá `azure network dns record-set add-record` comando. Para obter ajuda, consulte `azure network dns record-set add-record -h`.

Olá exemplo a seguir cria um registro com o nome relativo do hello "www" hello "contoso.com", no grupo de recursos "MyResourceGroup" de zona de DNS. nome totalmente qualificado de saudação do conjunto de registros de saudação é "www.contoso.com". tipo de registro de saudação é "A", com o endereço IP "1.2.3.4" e um TTL padrão de 3600 segundos (1 hora) é usado.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

Para outros tipos de registro, para conjuntos de registros com mais de um registro para valores alternativos de TTL e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).


## <a name="view-records"></a>Exibir registros

registros DNS Olá toolist na zona, use:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a>Atualizar servidores de nome

Quando estiver satisfeito de que a zona DNS e registros de tem sido instalados corretamente, você precisa tooconfigure seu nome de domínio toouse servidores de nome DNS do Azure hello. Isso permite que outros usuários no hello Internet toofind seus registros DNS.

servidores de nome de saudação para sua zona são fornecidos por Olá `azure network dns zone show` comando:

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

Esses servidores de nome devem ser configurados com o registrador de nome de domínio hello (onde você adquiriu o nome de domínio Olá). Seu registrador oferecerá Olá opção tooset os servidores de nome Olá para o domínio de saudação. Para obter mais informações, consulte [delegar tooAzure seu domínio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Excluir todos os recursos
 
toodelete todos os recursos criados neste artigo, Olá take etapa a seguir:

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o DNS do Azure, consulte [visão geral do DNS do Azure](dns-overview.md).

toolearn mais sobre o gerenciamento de zonas DNS no DNS do Azure, consulte [zonas DNS gerenciar no DNS do Azure usando o Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

toolearn mais sobre o gerenciamento de registros DNS no DNS do Azure, consulte [registros de DNS de gerenciar e registro define no DNS do Azure usando o Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).

