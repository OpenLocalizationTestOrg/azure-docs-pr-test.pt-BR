---
title: aaaManage DNS zonas no DNS do Azure - 1.0 da CLI do Azure | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando a CLI do Azure 1.0. Este artigo mostra como tooupdate, excluir e criar zonas DNS no DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Como toomanage zonas de DNS no DNS do Azure usando Olá 1.0 da CLI do Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI 1.0 do Azure](dns-operations-dnszones-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-dnszones-cli.md)

Este guia mostra como toomanage suas zonas DNS usando Olá multiplataforma CLI do Azure 1.0, que está disponível para Windows, Mac e Linux. Você também pode gerenciar as zonas DNS usando [Azure PowerShell](dns-operations-dnszones.md) ou Olá portal do Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

* [1.0 de CLI do Azure](dns-operations-dnszones-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.
* [2.0 do CLI do Azure](dns-operations-dnszones-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.

## <a name="introduction"></a>Introdução

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Obtendo ajuda

Todos os comandos de CLI 1.0 relacionadas tooAzure DNS iniciam com `azure network dns`. A Ajuda está disponível para cada comando usando Olá `--help` opção (forma abreviada `-h`).  Por exemplo:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada usando Olá `azure network dns zone create` comando. Para obter ajuda, consulte `azure network dns zone create -h`.

Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate uma zona DNS com marcas

Olá exemplo a seguir mostra como toocreate um DNS da zona com dois [do Azure Resource Manager marcas](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*, usando Olá `--tags` parâmetro (forma abreviada `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Obter uma zona DNS

tooretrieve uma zona DNS, use `azure network dns zone show`. Para obter ajuda, consulte `azure network dns zone show -h`.

Olá, exemplo a seguir retorna zona do DNS Olá *contoso.com* e seus dados associados do grupo de recursos *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

saudação de exemplo a seguir é a resposta de saudação.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Observe que registros DNS não são retornados por `azure network dns zone show`. registros DNS toolist, use `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Listar as zonas DNS

zonas DNS tooenumerate, use `azure network dns zone list`. Para obter ajuda, consulte `azure network dns zone list -h`.

Grupo de recursos de saudação especificando lista apenas as zonas no grupo de recursos de saudação:

```azurecli
azure network dns zone list MyResourceGroup
```

Grupo de recursos de saudação omitindo lista todas as zonas na assinatura hello:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Atualizar uma zona DNS

Alterações tooa recurso de zona do DNS pode ser feito usando `azure network dns zone set`. Para obter ajuda, consulte `azure network dns zone set -h`.

Este comando não atualizar conjuntos de registros de DNS hello dentro da zona de saudação (consulte [como registros DNS tooManage](dns-operations-recordsets-cli-nodejs.md)). É tooupdate usadas somente propriedades do próprio recurso de zona hello. Essas propriedades são atualmente limitado toohello [do Azure Resource Manager 'tags'](dns-zones-records.md#tags) para o recurso de zona hello.

Olá exemplo a seguir mostra como tooupdate Olá marcas em uma zona DNS. marcas existentes Hello serão substituídas por Olá valor especificado.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Excluir uma zona DNS

As zonas DNS podem ser excluídas por meio do `azure network dns zone delete`. Para obter ajuda, consulte `azure network dns zone delete -h`.

> [!NOTE]
> Excluir uma zona DNS também exclui todos os registros DNS na zona de saudação. Essa operação não pode ser desfeita. Se a zona DNS de saudação está em uso, serviços usando zona Olá falhará quando Olá zona é excluída.
>
>tooprotect contra a exclusão acidental de zona, consulte [como tooprotect DNS zonas e os registros](dns-protect-zones-recordsets.md).

Esse comando solicita uma confirmação. Olá opcional `--quiet` alternar (forma abreviada `-q`) suprime esse prompt.

Olá exemplo a seguir mostra como toodelete Olá zona *contoso.com* do grupo de recursos *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[gerenciar conjuntos de registros e registros](dns-getstarted-create-recordset-cli-nodejs.md) na zona DNS.

Saiba como muito[delegar tooAzure seu domínio DNS](dns-domain-delegation.md).

