---
title: aaaManage DNS zonas no DNS do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando a CLI do Azure 2.0. Este artigo mostra como tooupdate, excluir e criar zonas DNS no DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Como toomanage zonas de DNS no DNS do Azure usando Olá 2.0 do CLI do Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI 1.0 do Azure](dns-operations-dnszones-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-dnszones-cli.md)


Este guia mostra como toomanage suas zonas DNS usando Olá multiplataforma CLI do Azure, que está disponível para Windows, Mac e Linux. Você também pode gerenciar as zonas DNS usando [Azure PowerShell](dns-operations-dnszones.md) ou Olá portal do Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

* [1.0 de CLI do Azure](dns-operations-dnszones-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.
* [2.0 do CLI do Azure](dns-operations-dnszones-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.

## <a name="introduction"></a>Introdução

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Configurar a CLI do Azure 2.0 para DNS do Azure

### <a name="before-you-begin"></a>Antes de começar

Verifique se você tem Olá itens a seguir antes de começar a configuração.

* Uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).

* Instale a versão mais recente Olá de saudação 2.0 do CLI do Azure, disponível para Windows, Linux ou Mac. Mais informações estão disponíveis em [instalação hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Entrar tooyour conta do Azure

Abra uma janela do console e autentique com suas credenciais. Para obter mais informações, consulte o Log em tooAzure de saudação CLI do Azure

```
az login
```

### <a name="select-hello-subscription"></a>Selecione a assinatura de saudação

Verificar as assinaturas de saudação para conta de saudação.

```
az account list
```

Escolha qual toouse suas assinaturas do Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Isso é usado como o local padrão de saudação para recursos desse grupo de recursos. No entanto, como todos os recursos DNS são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto no DNS do Azure.

Você pode ignorar esta etapa se está usando um grupo de recursos existente.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Obtendo ajuda

Todos os comandos de CLI 2.0 relacionadas tooAzure DNS iniciam com `az network dns`. A Ajuda está disponível para cada comando usando Olá `--help` opção (forma abreviada `-h`).  Por exemplo:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada usando Olá `az network dns zone create` comando. Para obter ajuda, consulte `az network dns zone create -h`.

Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate uma zona DNS com marcas

Olá exemplo a seguir mostra como toocreate um DNS da zona com dois [do Azure Resource Manager marcas](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*, usando Olá `--tags` parâmetro (forma abreviada `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Obter uma zona DNS

tooretrieve uma zona DNS, use `az network dns zone show`. Para obter ajuda, consulte `az network dns zone show --help`.

Olá, exemplo a seguir retorna zona do DNS Olá *contoso.com* e seus dados associados do grupo de recursos *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

saudação de exemplo a seguir é a resposta de saudação.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Observe que registros DNS não são retornados por `az network dns zone show`. registros DNS toolist, use `az network dns record-set list`.


## <a name="list-dns-zones"></a>Listar as zonas DNS

zonas DNS tooenumerate, use `az network dns zone list`. Para obter ajuda, consulte `az network dns zone list --help`.

Grupo de recursos de saudação especificando lista apenas as zonas no grupo de recursos de saudação:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Grupo de recursos de saudação omitindo lista todas as zonas na assinatura hello:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Atualizar uma zona DNS

Alterações tooa recurso de zona do DNS pode ser feito usando `az network dns zone update`. Para obter ajuda, consulte `az network dns zone update --help`.

Este comando não atualizar conjuntos de registros de DNS hello dentro da zona de saudação (consulte [como registros DNS tooManage](dns-operations-recordsets-cli.md)). É tooupdate usadas somente propriedades do próprio recurso de zona hello. Essas propriedades são atualmente limitado toohello [do Azure Resource Manager 'tags'](dns-zones-records.md#tags) para o recurso de zona hello.

Olá exemplo a seguir mostra como tooupdate Olá marcas em uma zona DNS. marcas existentes Hello serão substituídas por Olá valor especificado.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Excluir uma zona DNS

As zonas DNS podem ser excluídas por meio do `az network dns zone delete`. Para obter ajuda, consulte `az network dns zone delete --help`.

> [!NOTE]
> Excluir uma zona DNS também exclui todos os registros DNS na zona de saudação. Essa operação não pode ser desfeita. Se a zona DNS de saudação está em uso, serviços usando zona Olá falhará quando Olá zona é excluída.
>
>tooprotect contra a exclusão acidental de zona, consulte [como tooprotect DNS zonas e os registros](dns-protect-zones-recordsets.md).

Esse comando solicita uma confirmação. Olá opcional `--yes` suprime esse prompt.

Olá exemplo a seguir mostra como toodelete Olá zona *contoso.com* do grupo de recursos *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[gerenciar conjuntos de registros e registros](dns-getstarted-create-recordset-cli.md) na zona DNS.

Saiba como muito[delegar tooAzure seu domínio DNS](dns-domain-delegation.md).

