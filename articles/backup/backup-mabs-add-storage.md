---
title: aaaUse modernos o armazenamento de Backup com o servidor de Backup do Azure v2 | Microsoft Docs
description: "Saiba mais sobre os novos recursos Olá no servidor de Backup do Azure v2. Este artigo descreve como tooupgrade a instalação do servidor de Backup."
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Adicionar armazenamento tooAzure v2 do servidor de Backup

Servidor de Backup do Azure v2 vem com o System Center 2016 Data Protection Manager armazenamento de backup moderno. O armazenamento de Backup moderno oferece economia de armazenamento de 50%, backups de armazenamento três vezes mais rápido e mais eficiente. Ele também oferece o armazenamento com reconhecimento de carga de trabalho. 

> [!NOTE]
> toouse modernos o armazenamento de Backup, você deve executar v2 do servidor de Backup no Windows Server 2016. Se você executar o servidor de Backup v2 em uma versão anterior do Windows Server, servidor de Backup do Azure não poderá tirar proveito do armazenamento de Backup moderno. Em vez disso, ele protegerá as cargas de trabalho, como ocorre com o servidor de Backup v1. Para obter mais informações, consulte a versão do servidor de Backup Olá [matriz proteção](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volumes no servidor de Backup v2

Servidor de Backup v2 aceita volumes de armazenamento. Quando você adicionar um volume, o servidor de Backup formata Olá volume tooResilient arquivo ReFS (sistema), que exige o armazenamento de Backup modernos. tooadd um volume e tooexpand-lo mais tarde se necessário, sugerimos que você use esse fluxo de trabalho:

1.  Configure o servidor Backup v2 em uma máquina virtual.
2.  Crie um volume em um disco virtual em um pool de armazenamento:
    1.  Adicionar um pool de armazenamento do disco tooa e criar um disco virtual com o layout simples.
    2.  Adicionar discos adicionais e expandir disco virtual hello.
    3.  Crie volumes no disco virtual hello.
3.  Adicione Olá volumes tooBackup Server.
4.  Configure o armazenamento com reconhecimento de carga de trabalho.

## <a name="create-a-volume-for-modern-backup-storage"></a>Crie um volume para armazenamento de Backup moderno

Usar um Servidor de Backup v2 com volumes como armazenamento de disco pode ajudá-lo a manter o controle sobre o armazenamento. Um volume pode ser um único disco. No entanto, se você quiser tooextend armazenamento Olá futuros, crie um volume fora de um disco criado usando espaços de armazenamento. Isso pode ajudar se você quiser tooexpand volume de saudação para armazenamento de backup. Esta seção oferece as práticas recomendadas para a criação de um volume com esta instalação.

1. No Gerenciador do Servidor, selecione **Arquivo e Serviços de Armazenamento** > **Volumes** > **Pools de armazenamento**. Em **DISCOS FÍSICOS**, selecione **novo Pool de armazenamento**. 

    ![Crie um novo pool de armazenamento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. Em Olá **tarefas** caixa de lista suspensa, selecione **novo disco Virtual**.

    ![Adicione um disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Selecione o pool de armazenamento hello e, em seguida, selecione **adicionar disco físico**.

    ![Adicione um disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Selecione o disco físico hello e, em seguida, selecione **Expandir Disco Virtual**.

    ![Expandir disco virtual Olá](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Selecione o disco virtual hello e, em seguida, selecione **Novo Volume**.

    ![Criar um novo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. Em Olá **Selecionar servidor de saudação e disco** caixa de diálogo, o servidor de saudação selecione e o novo disco de saudação. Em seguida, selecione **Avançar**.

    ![Selecione o disco e o servidor de saudação](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Adicione o armazenamento de disco do servidor de tooBackup volumes

tooadd tooBackup um volume no servidor, em Olá **gerenciamento** , examinar novamente armazenamento hello e, em seguida, selecione **adicionar**. É exibida uma lista de todos os Olá volumes disponíveis toobe adicionado para o armazenamento de servidor de Backup. Depois de volumes disponíveis são adicionados toohello lista dos volumes selecionados, você pode fornecer toohelp um nome amigável que você gerenciá-los. tooformat tooReFS esses volumes para fazer Backup do servidor possa usar os benefícios de saudação do armazenamento de Backup moderna, selecione **Okey**.

![Adicione Volumes disponíveis](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Configure o armazenamento com reconhecimento de carga de trabalho

Com o armazenamento com reconhecimento de carga de trabalho, você pode selecionar os volumes de saudação que armazenam preferencialmente determinados tipos de cargas de trabalho. Por exemplo, você pode definir volumes caros que dão suporte a um grande número de operações de entrada/saída por segundo (IOPS) toostore somente Olá cargas de trabalho que exigem backups frequentes, de alto volume. Um exemplo é o SQL Server com logs de transação. Outras cargas de trabalho de backup com menos frequência, como VMs, podem fazer backup de volumes toolow custo.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Você pode configurar o armazenamento com reconhecimento de carga de trabalho usando o cmdlet do PowerShell Olá Update-DPMDiskStorage, que atualiza as propriedades de saudação de um volume no pool de armazenamento de saudação em um servidor do Data Protection Manager.

Sintaxe:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Olá seguinte captura de tela mostra Olá atualização DPMDiskStorage cmdlet na janela do PowerShell hello.

![Olá DPMDiskStorage de atualização de comando na janela do PowerShell Olá](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

Olá alterações usando o PowerShell são refletidas no hello Console do administrador do servidor de Backup.

![Discos e volumes no hello Console do administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Próximas etapas
Depois de instalar o servidor de Backup, saiba como tooprepare seu servidor, ou começar a proteger uma carga de trabalho.

- [Preparar as cargas de trabalho do Servidor de Backup](backup-azure-microsoft-azure-backup.md)
- [Usar o servidor de Backup tooback um servidor VMware](backup-azure-backup-server-vmware.md)
- [Usar o servidor de Backup tooback o SQL Server](backup-azure-sql-mabs.md)

