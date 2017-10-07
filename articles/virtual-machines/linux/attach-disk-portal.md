---
title: aaaAttach um disco de dados tooa VM do Linux | Microsoft Docs
description: "Como tooa de disco de dados novos ou existentes tooattach VM do Linux no hello usando o portal do Azure Olá modelo de implantação do Gerenciador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Como tooattach dados de um disco tooa VM do Linux no hello portal do Azure
Este artigo mostra como tooattach novo e existente discos tooa máquina de virtual do Linux por meio de saudação portal do Azure. Você também pode [anexar tooa um disco de dados VM do Windows no portal do Azure de saudação](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Você pode escolher toouse qualquer um dos discos do Azure gerenciados ou não gerenciados discos. Discos gerenciados são tratados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los. Discos não gerenciados exigem uma conta de armazenamento e têm algumas [cotas e limites que se aplicam](../../azure-subscription-service-limits.md#storage-limits). Para saber mais sobre Azure Managed Disks, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).

Antes de anexar discos tooyour VM, examine essas dicas:

* tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* toouse armazenamento Premium, você precisa de uma máquina virtual da série DS ou série GS. Você pode usar discos Premium e Standard com essas máquinas virtuais. O armazenamento Premium está disponível em determinadas regiões. Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Discos anexados toovirtual máquinas são, na verdade, os arquivos. vhd armazenados no Azure. Para obter detalhes, confira [Sobre discos e VHDs para máquinas virtuais](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Localizar a máquina virtual de saudação
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **máquinas virtuais**.
3. Selecione máquina virtual de Olá Olá lista.
4. toohello Virtual máquinas folha, **Essentials**, clique em **discos**.
   
    ![Abrir configurações de disco](./media/attach-disk-portal/find-disk-settings.png)

Continue seguindo as instruções para anexar um [disco gerenciado](#use-azure-managed-disks) ou um [disco não gerenciado](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Usar o Azure Managed Disks

### <a name="attach-a-new-disk"></a>Anexar um novo disco

1. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
2. Clique o menu suspenso de saudação para **nome** e selecione **criar disco**:

    ![Criar disco gerenciado do Azure](./media/attach-disk-portal/create-new-md.png)

3. Insira um nome para o disco gerenciado. Examine as configurações padrão de saudação, atualizar conforme necessário e, em seguida, clique em **criar**.
   
   ![Analisar configurações de disco](./media/attach-disk-portal/create-new-md-settings.png)

4. Clique em **salvar** toocreate Olá gerenciados em disco e a atualização de configuração da VM hello:

   ![Salvar novo Azure Managed Disk](./media/attach-disk-portal/confirm-create-new-md.png)

5. Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**. Como discos gerenciados são um recurso de nível superior, o disco de saudação aparece na raiz de Olá Olá do grupo de recursos:

   ![Azure Managed Disk no grupo de recursos](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Anexar um disco existente
1. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
2. Clique o menu suspenso de saudação para **nome** tooview uma lista de existentes gerenciadas discos acessíveis tooyour assinatura do Azure. Selecione Olá gerenciado tooattach de disco:

   ![Anexar um Azure Managed Disk existente](./media/attach-disk-portal/select-existing-md.png)

3. Clique em **salvar** tooattach Olá existente gerenciados em disco e a atualização de configuração da VM hello:
   
   ![Salvar atualizações do Azure Managed Disk](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Após anexa Azure hello disco toohello VM, ela é listada em configurações de disco da máquina de virtual Olá em **discos de dados**.

## <a name="use-unmanaged-disks"></a>Usar discos não gerenciados

### <a name="attach-a-new-disk"></a>Anexar um novo disco

1. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
2. Examine as configurações padrão de saudação, atualizar conforme necessário e, em seguida, clique em **Okey**.
   
   ![Analisar configurações de disco](./media/attach-disk-portal/attach-new.png)
3. Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.

### <a name="attach-an-existing-disk"></a>Anexar um disco existente
1. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
2. Em **Anexar disco existente**, clique em **Arquivo VHD**.
   
   ![Anexar disco existente](./media/attach-disk-portal/attach-existing.png)
3. Em **contas de armazenamento**, selecione conta hello e contêiner que contém o arquivo. vhd de saudação.
   
   ![Localização do VHD](./media/attach-disk-portal/find-storage-container.png)
4. Selecione o arquivo. vhd de saudação.
5. Em **anexar o disco existente**, arquivo hello você selecionou é listado em **arquivo VHD**. Clique em **OK**.
6. Após anexa Azure hello disco toohello VM, ela é listada em configurações de disco da máquina de virtual Olá em **discos de dados**.


## <a name="next-steps"></a>Próximas etapas
Depois de saudação disco for adicionado, será necessário tooprepare-lo para uso. Para obter mais informações, veja [Como: inicializar um novo disco de dados no Linux](add-disk.md).
