---
title: Usar armazenamento de Backup moderno com Servidor de Backup do Azure v2 | Microsoft Docs
description: "Saiba mais sobre os novos recursos no Servidor de Backup do Azure v2. Este artigo descreve como atualizar sua instalação do servidor de Backup."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a>Adicionar armazenamento ao Servidor de Backup do Azure v2

Servidor de Backup do Azure v2 vem com o System Center 2016 Data Protection Manager armazenamento de backup moderno. O armazenamento de Backup moderno oferece economia de armazenamento de 50%, backups de armazenamento três vezes mais rápido e mais eficiente. Ele também oferece o armazenamento com reconhecimento de carga de trabalho. 

> [!NOTE]
> Para usar o armazenamento de Backup modernos, você deve executar servidor de Backup v2 no Windows Server 2016. Se você executar o servidor de Backup v2 em uma versão anterior do Windows Server, servidor de Backup do Azure não poderá tirar proveito do armazenamento de Backup moderno. Em vez disso, ele protegerá as cargas de trabalho, como ocorre com o servidor de Backup v1. Para obter mais informações, consulte a versão do servidor de Backup [matriz proteção](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volumes no servidor de Backup v2

Servidor de Backup v2 aceita volumes de armazenamento. Quando você adiciona um volume, o servidor de Backup formata o volume para o sistema de arquivos resiliente (ReFS), que exige o armazenamento de Backup modernos. Para adicionar um volume e expandi-lo mais tarde, se você precisar, sugerimos que você use esse fluxo de trabalho:

1.  Configure o servidor Backup v2 em uma máquina virtual.
2.  Crie um volume em um disco virtual em um pool de armazenamento:
    1.  Adicione um disco para um pool de armazenamento e crie um disco virtual com o layout simples.
    2.  Adicione quaisquer discos adicionais e estenda o disco virtual.
    3.  Crie volumes no disco virtual.
3.  Adicione volumes ao servidor de Backup.
4.  Configure o armazenamento com reconhecimento de carga de trabalho.

## <a name="create-a-volume-for-modern-backup-storage"></a>Crie um volume para armazenamento de Backup moderno

Usar um Servidor de Backup v2 com volumes como armazenamento de disco pode ajudá-lo a manter o controle sobre o armazenamento. Um volume pode ser um único disco. No entanto, se você quiser estender o armazenamento no futuro, crie um volume fora de um disco criado usando espaços de armazenamento. Isso pode ajudar se você quiser expandir o volume de armazenamento de backup. Esta seção oferece as práticas recomendadas para a criação de um volume com esta instalação.

1. No Gerenciador do Servidor, selecione **Arquivo e Serviços de Armazenamento** > **Volumes** > **Pools de armazenamento**. Em **DISCOS FÍSICOS**, selecione **novo Pool de armazenamento**. 

    ![Crie um novo pool de armazenamento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. Em **TAREFAS** caixa suspensa, selecione **novo Disco Virtual**.

    ![Adicione um disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Selecione o pool de armazenamento e, em seguida, selecione **Adicionar Disco Físico**.

    ![Adicione um disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Selecione o disco físico e, em seguida, selecione **Expandir Disco Virtual**.

    ![Estender o disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Selecione o disco virtual e, em seguida, selecione **Novo Volume**.

    ![Criar um novo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. No diálogo **Selecione o servidor e disco**, selecione o servidor e o novo disco. Em seguida, selecione **Avançar**.

    ![Selecione o servidor e disco](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a>Adicione volumes de armazenamento do servidor de Backup em disco

Para adicionar um volume ao servidor de Backup, no painel **Gerenciamento**, examinar novamente o armazenamento e, em seguida, selecione **Adicionar**. É exibida uma lista de todos os volumes disponíveis para serem adicionados para o armazenamento de servidor de Backup. Depois dos volumes disponíveis serem adicionados à lista de volumes selecionados, você pode dar-lhes um nome amigável para te ajudar a gerenciá-los. Para formatar esses volumes para ReFS para que o servidor de Backup possa usar os benefícios do armazenamento de Backup moderna, selecione **Ok**.

![Adicione Volumes disponíveis](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Configure o armazenamento com reconhecimento de carga de trabalho

Com o armazenamento com reconhecimento de carga de trabalho, você pode selecionar os volumes que armazenam preferencialmente determinados tipos de cargas de trabalho. Por exemplo, você pode definir volumes caros que dão suporte a um grande número de operações de entrada/saída por segundo (IOPS) para armazenar apenas as cargas de trabalho que exigem backups frequentes de alto volume. Um exemplo é o SQL Server com logs de transação. Outras cargas de trabalho de backup com menos frequência, como VMs, podem ser feitas o backup de volumes de baixo custo.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Você pode configurar o armazenamento com reconhecimento de carga de trabalho usando o cmdlet do PowerShell Update-DPMDiskStorage, que atualiza as propriedades de um volume no pool de armazenamento em um servidor do Data Protection Manager.

Sintaxe:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
A captura de tela a seguir mostra o cmdlet Update-DPMDiskStorage na janela do PowerShell.

![O comando Update-DPMDiskStorage na janela do PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

As alterações feitas por meio do PowerShell são refletidas no Console do administrador do servidor de Backup.

![Discos e volumes no Console do administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Próximas etapas
Depois de instalar o Servidor de Backup, saiba como preparar seu servidor, ou começar a proteger uma carga de trabalho.

- [Preparar as cargas de trabalho do Servidor de Backup](backup-azure-microsoft-azure-backup.md)
- [Usar o Servidor de Backup para fazer backup de um Servidor do VMware](backup-azure-backup-server-vmware.md)
- [Usar o Servidor de Backup para fazer backup de um SQL Server](backup-azure-sql-mabs.md)

