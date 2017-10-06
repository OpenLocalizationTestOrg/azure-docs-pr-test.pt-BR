---
title: "excluindo contas de armazenamento do Azure, contêineres ou VHDs em uma implantação clássica de aaaTroubleshoot | Microsoft Docs"
description: "Solucionar problemas ao excluir contas de armazenamento, contêineres ou VHDs do Azure em uma implantação clássica"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Solucionar problemas ao excluir contas de armazenamento, contêineres ou VHDs do Azure em uma implantação clássica
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Você poderá receber erros ao tentar conta de armazenamento do Azure toodelete hello, contêiner ou VHD no hello [portal do Azure](https://portal.azure.com/) ou hello [portal clássico do Azure](https://manage.windowsazure.com/). problemas de saudação podem ser causados por Olá circunstâncias a seguir:

* Quando você exclui uma VM, disco hello e VHD não são automaticamente excluídos. Que pode ser motivo Olá Falha na exclusão da conta de armazenamento. Nós não exclua o disco Olá para que você possa usar Olá disco toomount outra VM.
* Ainda há uma concessão em um blob de disco ou hello associada com o disco de saudação.
* Ainda há uma imagem de VM que está usando uma conta de armazenamento, contêiner ou blob.

Se o problema do Azure não é abordado neste artigo, visite Olá fóruns do Azure em [MSDN e Olá estouro de pilha](https://azure.microsoft.com/support/forums/). Você pode lançar seu problema nesses fóruns ou too@AzureSupport no Twitter. Além disso, você pode emitir uma solicitação de suporte do Azure, selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Sintomas
Olá seção a seguir lista os erros comuns que podem ser exibidas ao tentar contas de armazenamento do Azure toodelete hello, contêineres ou VHDs.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Cenário 1: Não é possível toodelete uma conta de armazenamento
Quando você navega toohello conta de armazenamento clássicas Olá [portal do Azure](https://portal.azure.com/) e selecione **excluir**, pode ser apresentada uma lista de objetos que estão impedindo a exclusão da conta de armazenamento hello:

  ![Imagem de erro ao excluir conta de armazenamento Olá](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Quando você navega a conta de armazenamento toohello Olá [portal clássico do Azure](https://manage.windowsazure.com/) e selecione **excluir**, você poderá ver um Olá os erros a seguir:

- *A conta de armazenamento StorageAccountName contém imagens de VM. Assegure-se de que essas imagens de VM sejam removidas antes de excluir essa conta de armazenamento.*

- *Falha na conta de armazenamento toodelete < vm-armazenamento-account-name >. Conta de armazenamento não é possível toodelete < vm-armazenamento-account-name >: ' < vm-armazenamento-account-name > de conta de armazenamento tem algumas imagens de ativas e/ou discos. Garanta que esses discos e/ou essas imagens sejam removidos antes de excluir essa conta de armazenamento.'*.

- *A conta de armazenamento <vm-storage-account-name> tem algumas imagens e/ou discos ativos, por exemplo, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Garanta que esses discos e/ou essas imagens sejam removidos antes de excluir essa conta de armazenamento.*

- *A conta de armazenamento <vm-storage-account-name> tem um contêiner com artefatos de imagens e/ou discos ativos. Certifique-se de que esses artefatos são removidos do repositório de imagens de saudação antes de excluir esta conta de armazenamento*.

- *A conta de armazenamento com falha no envio <vm-storage-account-name> tem um contêiner com artefatos de imagens e/ou discos ativos. Certifique-se de que esses artefatos são removidos do repositório de imagens de saudação antes de excluir esta conta de armazenamento. Quando você tentar toodelete uma conta de armazenamento e houver discos ainda estão ativos associados a ele, você verá uma mensagem indicando que há discos ativos que precisem toobe excluído*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Cenário 2: Não é possível toodelete um contêiner
Quando você tenta toodelete contêiner de armazenamento de saudação, você poderá ver Olá erro a seguir:

*Contêiner de armazenamento com falha toodelete <container name>. Erro: ' atualmente há uma concessão no contêiner de saudação e nenhuma ID de concessão foi especificada na solicitação Olá*.

Ou

*Olá seguintes discos da máquina virtual usa blobs nesse contêiner, portanto, Olá contêiner não pode ser excluído: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Cenário 3: Não é possível toodelete um VHD
Depois que você excluir uma máquina virtual e, em seguida, tente toodelete Olá blobs para Olá associados VHDs, você poderá receber a seguinte mensagem de saudação:

*Blob toodelete com falha ' caminho/XXXXXX-XXXXXX-os-1447379084699.vhd'. Erro: ' atualmente há uma concessão no blob hello e nenhuma ID de concessão foi especificada na solicitação de saudação.*

Ou

*Blob 'BlobName.vhd' está em uso como disco da máquina virtual 'VirtualMachineDiskName' blob Olá não pode ser excluído.*

## <a name="solution"></a>Solução
problemas mais comuns do tooresolve hello, tente Olá método a seguir:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>Etapa 1: Excluir todos os discos que estão impedindo a exclusão da conta de armazenamento hello, contêiner ou VHD
1. Alternar toohello [portal clássico do Azure](https://manage.windowsazure.com/).
2. Selecione **MÁQUINA VIRTUAL** > **DISCOS**.

    ![Imagem de discos em máquinas virtuais no portal clássico do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Localize discos Olá associados à conta de armazenamento hello, contêiner ou VHD que você deseja toodelete. Quando você verificar o local de saudação do disco hello, você encontrará Olá associados a conta de armazenamento, contêiner ou VHD.

    ![Imagem que mostra informações sobre o local para os discos no portal clássico do Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Exclua discos hello usando um dos métodos a seguir de saudação:

  - Se não houver nenhuma VM listadas no hello **conectado a** campo disco hello, você pode excluir disco Olá diretamente.

  - Se o disco de saudação é um disco de dados, siga estas etapas:

    1. Verifique o nome de saudação do hello VM Olá disco está anexado ao.
    2. Vá muito**máquinas virtuais** > **instâncias**e, em seguida, localize Olá VM.
    3. Certifique-se de que nada está usando ativamente disco hello.
    4. Selecione **desanexar disco** na parte inferior de saudação do disco de saudação do hello toodetach portal.
    5. Vá muito**máquinas virtuais** > **discos**e aguarde Olá **conectado a** tooturn de campo em branco. Isso indica que o disco Olá foi desanexado com êxito da saudação VM.
    6. Selecione **excluir** na parte inferior de saudação do **máquinas virtuais** > **discos** toodelete disco de saudação.

  - Se o disco Olá é um disco do sistema operacional (Olá **contém OS** campo tem um valor como Windows) e tooa anexado VMs, siga estas etapas toodelete Olá VM. não é possível desanexar o disco do sistema operacional Olá para que tenhamos concessão de saudação do toodelete Olá VM toorelease.

    1. Verifique o nome da máquina Virtual de Olá Olá A que disco de dados está anexado hello.  
    2. Vá muito**máquinas virtuais** > **instâncias**, e, em seguida, selecione Olá VM Olá disco está associada.
    3. Certifique-se de que nada está usando ativamente Olá de máquina virtual, e que você não precisa Olá máquina virtual.
    4. Selecione Olá VM Olá disco está anexado, em seguida, selecione **excluir** > **Delete Olá anexou discos**.
    5. Vá muito**máquinas virtuais** > **discos**e aguarde Olá toodisappear de disco.  Pode levar alguns minutos para que essa toooccur e página de saudação toorefresh talvez seja necessário.
    6. Se o disco de saudação não desaparecem, aguarde Olá **conectado a** tooturn de campo em branco. Isso indica que o disco Olá totalmente soltou de saudação VM.  Em seguida, selecione o disco hello e selecione **excluir** na parte inferior de saudação do disco de Olá Olá página toodelete.


   > [!NOTE]
   > Se um disco estiver anexado tooa VM, não será capaz de toodelete-lo. Discos são desconectados de uma VM excluída assincronamente. Pode levar alguns minutos após Olá VM seja excluído para tooclear esse campo para cima.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>Etapa 2: Excluir as imagens de VM que estão impedindo a exclusão da conta de armazenamento hello ou do contêiner
1. Alternar toohello [portal clássico do Azure](https://manage.windowsazure.com/).
2. Selecione **máquina VIRTUAL** > **imagens**e, em seguida, excluir imagens Olá associados à conta de armazenamento hello, contêiner ou VHD.

    Depois disso, tente conta de armazenamento toodelete hello, contêiner ou VHD novamente.

> [!WARNING]
> Ser tooback-se de que qualquer valor que você deseja toosave antes de excluir a conta de saudação. Quando você exclui um VHD, blob, tabela, fila ou arquivo, ele é permanentemente excluído. Certifique-se de que o recurso de saudação não está em uso.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>Sobre Olá status parado (desalocado)
Máquinas virtuais que foram criados no modelo de implantação clássico hello e que foram retidos terá Olá **parado (desalocado)** status em qualquer Olá [portal do Azure](https://portal.azure.com/) ou [portal clássico do Azure ](https://manage.windowsazure.com/).

**Portal Clássico do Azure**:

![Status Parado (Desalocado) para VMs no portal do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Portal do Azure**:

![Status Parado (desalocado) para VMs no portal clássico do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

Um status "Parada (desalocada)" libera recursos do computador hello, como saudação da CPU, memória e rede. No entanto, discos Hello, ainda são mantidos para que você pode rapidamente recriar Olá VM se necessário. Esses discos são criados sobre os VHDs cujos backups são feitos pelo armazenamento do Azure. conta de armazenamento Olá tem esses VHDs e discos de saudação têm concessões nesses VHDs.

## <a name="next-steps"></a>Próximas etapas
* [Excluir uma conta de armazenamento](storage-create-storage-account.md#delete-a-storage-account)
