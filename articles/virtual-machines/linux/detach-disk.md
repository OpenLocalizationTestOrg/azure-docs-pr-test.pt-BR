---
title: aaaDetach um disco de dados de uma VM do Linux - Azure | Microsoft Docs
description: "Saiba toodetach um disco de dados de uma máquina virtual no Azure usando a CLI 2.0 ou hello portal do Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Como toodetach dados de um disco de uma máquina virtual Linux

Quando você não precisa mais um disco de dados é anexado tooa VM, você pode facilmente desanexá-lo. Isso remove o disco de saudação da máquina virtual de hello, mas não o remove do armazenamento. 

> [!WARNING]
> Se você desanexar um disco, ele não será excluído automaticamente. Se você se inscreveu tooPremium armazenamento, você continuará tooincur encargos de armazenamento de disco de saudação. Para obter mais informações, consulte muito[preços e faturamento ao usar o armazenamento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma máquina virtual ou outro.  

## <a name="detach-a-data-disk-using-cli-20"></a>Desanexar um disco de dados usando a CLI 2.0

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.


## <a name="detach-a-data-disk-using-hello-portal"></a>Desanexar um disco de dados usando o portal de saudação
1. No hub de portal hello, selecione **máquinas virtuais**.
2. Selecionar máquina virtual Olá que tenha Olá disco de dados que deseja toodetach e clique **parar** toodeallocate Olá VM.
3. Na folha de máquina virtual hello, selecione **discos**.
4. Na parte superior de saudação do hello **discos** folha, selecione **editar**.
5. Em Olá **discos** folha, toohello à direita saudação do disco de dados que deseja toodetach, clique em Olá ![imagem do botão desanexar](./media/detach-disk/detach.png) desanexar botão.
5. Depois que o disco Olá foi removido, clique em Salvar na parte superior de saudação da folha de saudação.
6. Na folha de máquina virtual de saudação, clique em **visão geral** e, em seguida, clique em Olá **iniciar** botão na parte superior de saudação do hello toorestart da folha Olá VM.

disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.








## <a name="next-steps"></a>Próximas etapas
Se desejar que o disco de dados tooreuse hello, você pode simplesmente [anexá-lo tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

