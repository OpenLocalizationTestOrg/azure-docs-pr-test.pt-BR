---
title: um gerenciado do Azure do disco para fazer backup de aaaCopy | Microsoft Docs
description: "Saiba como toocreate uma cópia de um toouse de disco gerenciado do Azure para fazer backup ou solução de problemas de disco emite."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Criar uma cópia de um VHD armazenado como um Disco Gerenciado do Azure usando instantâneos gerenciados
Tirar um instantâneo de um disco de gerenciado para backup ou criar um disco gerenciado de instantâneo hello e anexá-lo tooa tootroubleshoot de máquina virtual de teste. Um Instantâneo Gerenciado é uma cópia pontual completa de um Disco Gerenciado da VM. Ele cria uma cópia somente leitura do seu VHD e, por padrão, a armazena como um Disco Gerenciado Standard. 

Para saber mais sobre preços, confira [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Use o hello Azure tootake de 2.0 do CLI do Azure do portal ou hello um instantâneo de saudação disco gerenciado.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Usar o Azure CLI 2.0 tootake um instantâneo

> [!NOTE] 
> Olá exemplo a seguir requer hello Azure CLI 2.0 instalado e registrado na sua conta do Azure.

Olá etapas a seguir mostram como tooobtain e tirar um instantâneo de um sistema operacional gerenciado disco usando Olá `az snapshot create` com hello `--source-disk` parâmetro. Olá exemplo a seguir supõe que haja uma VM chamada `myVM` criado com um disco de sistema operacional gerenciado no hello `myResourceGroup` grupo de recursos.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

saída de Hello deve ser algo como:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Use tootake portal do Azure um instantâneo 

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Iniciando no hello superior esquerdo, clique em **novo** e procure **instantâneo**.
3. Na folha de instantâneo hello, clique em **criar**.
4. Insira um **nome** para instantâneo de saudação.
5. Selecione uma existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo. 
6. Selecione um Local do datacenter do Azure.  
7. Para **disco de origem**, selecione Olá toosnapshot de disco gerenciado.
8. Selecione Olá **tipo de conta** instantâneo de saudação do toouse toostore. É recomendável **Standard_LRS**, a menos que você precise dele armazenado em um disco de alto desempenho.
9. Clique em **Criar**.

Se você planejar toouse Olá instantâneo toocreate um disco gerenciado e anexá-lo uma VM que precisa toobe alto desempenho, use o parâmetro hello `--sku Premium_LRS` com hello `az snapshot create` comando. Isso cria o instantâneo Olá para que ela é armazenada como um disco de gerenciado para Premium. Os Discos Gerenciados Premium têm melhor desempenho porque são SSDs (unidades de estado sólido), mas são mais caros que os HDDs (discos rígidos) Standard.


