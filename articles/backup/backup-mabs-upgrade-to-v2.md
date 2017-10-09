---
title: aaaInstall v2 do servidor de Backup do Azure | Microsoft Docs
description: "O Servidor de Backup do Azure v2 oferece recursos aprimorados de backup para proteção de VMs, arquivos e pastas, cargas de trabalho e muito mais. Saiba como tooinstall ou atualização tooAzure v2 do servidor de Backup."
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
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Instalar o Servidor de Backup do Azure v2

Servidor de Backup do Azure ajuda a proteger suas máquinas virtuais (VMs), cargas de trabalho, arquivos e pastas e muito mais. O Servidor de Backup do Azure v2 se baseia no Servidor de Backup do Azure v1 e oferece novos recursos que não estão disponíveis em v1. Para obter uma comparação de recursos entre v1 e v2, consulte [Matriz de proteção do Servidor de Backup do Azure](backup-mabs-protection-matrix.md). 

recursos adicionais de saudação no servidor de Backup v2 são uma atualização do servidor de Backup v1. No entanto, o Servidor de Backup v1 não é um pré-requisito para instalar o Servidor de Backup v2. Se você quiser tooupgrade do servidor de Backup v1 tooBackup v2 do servidor, instale v2 do servidor de Backup no servidor de proteção do servidor de Backup de saudação. As suas configurações do Servidor de Backup existentes permanecem intactas.

Você pode instalar o Servidor de Backup v2 no Windows Server 2012 R2 ou Windows Server 2016. tootake proveito dos novos recursos, como System Center 2016 Data Protection Manager moderno Backup armazenamento, você deve instalar o servidor de Backup v2 no Windows Server 2016. Antes de você atualizar a instalação de tooor v2 do servidor de Backup, leia sobre Olá [os pré-requisitos de instalação](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Servidor de Backup do Azure tem Olá mesmo código de base como o System Center Data Protection Manager. Backup v1 do servidor é o equivalente tooData Protection Manager 2012 R2 e v2 do servidor de Backup é equivalente tooData Protection Manager 2016. Este artigo ocasionalmente faz referência a documentação do Data Protection Manager hello.
>
>

## <a name="upgrade-backup-server-toov2"></a>Atualizar o servidor de Backup toov2
tooupgrade do servidor de Backup v1 tooBackup v2 do servidor, verifique se a instalação tem atualizações Olá necessários:

- [Atualizar os agentes de proteção Olá](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) em Olá servidores protegidos.
- Atualize o Windows Server 2012 R2 tooWindows Server 2016.
- Atualização do administrador remoto do Servidor de Backup do Azure em todos os servidores de produção.
- Certifique-se de que os backups são definidos toocontinue sem reiniciar o servidor de produção.


### <a name="upgrade-steps-for-backup-server-v2"></a>Etapas de atualização para o Servidor de Backup v2

1. Em Olá Centro de Download, [baixar o instalador de atualização Olá](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Depois de extrair o Assistente de instalação de saudação, certifique-se de que **executar setup.exe** está selecionado e, em seguida, selecione **concluir**.

  ![Instalador de instalação - Execute a instalação](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. No Assistente do servidor de Backup do Microsoft Azure hello, em **instalar**, selecione **Microsoft Azure Backup Server**.

  ![Instalador de instalação - Selecione instalação](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. Em Olá **bem-vindo** página, examine os avisos de saudação e, em seguida, selecione **próximo**.

  ![Instalador de instalação - Página Inicial](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. Assistente de instalação Olá executa verificações de pré-requisitos toomake-se de que atualiza seu ambiente. Em Olá **Prerequisite Checks** página, selecione **verificar**.

  ![Instalador de instalação - página Verificações de Pré-requisitos](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. Verificações de pré-requisitos de saudação deve passar em seu ambiente. Se seu ambiente não passarem na verificação de hello, observe Olá problemas e corrigi-los. Em seguida, selecione **Verificar Novamente**. Depois de passar verificações de pré-requisitos hello, selecione **próximo**.

  ![Instalador de instalação - Botão Verificar Novamente](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. Em Olá **configurações do SQL** página, selecione a opção de saudação relevantes para sua instalação do SQL e, em seguida, selecione **verificar e instalar**.

  ![Instalador de instalação - Página Configurações do SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  verificações de saudação podem levar alguns minutos. Quando as verificações de saudação são terminar, selecione **próximo**.

  ![Instalador de instalação - botão de Instalação e Verificação de Configurações do SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. Em Olá **configurações de instalação** página, que qualquer local de toohello alterações em que o servidor de Backup está instalado, ou toohello local de rascunho. Selecione **Avançar**.

  ![Instalador de instalação - página de Configurações de Instalação](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. Assistente de instalação Olá toofinish, selecione **concluir**.

  ![Instalador de instalação - Concluir](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Adicionar armazenamento para Armazenamento de Backup moderno

eficiência de armazenamento de backup tooimprove, v2 do servidor de Backup adiciona suporte para volumes. Como o Servidor de Backup v1, o Servidor de Backup v2 oferece suporte a discos.

### <a name="add-volumes-and-disks"></a>Adicionar discos e volumes
Se você executar v2 do servidor de Backup no Windows Server 2016, você pode usar dados de backup de toostore de volumes. Os volumes oferecem economia de armazenamento e backups mais rápidos. Como os volumes são tooBackup novo servidor, você deve adicioná-los. 

Quando você adiciona um servidor de tooBackup de volume, você pode dar volume Olá um nome amigável. Clique em Olá **nome amigável** coluna de volume Olá você deseja tooname. Você pode alterar o nome hello mais tarde, se necessário. Você também pode usar o PowerShell tooadd ou alterar nomes amigáveis para volumes.

tooadd um volume no hello Console do administrador:

1. No hello Console de administrador do servidor de Backup do Azure, selecione **gerenciamento** > **armazenamento em disco** > **adicionar**.

    ![Assistente de adicionar o armazenamento de disco Olá aberto](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Isso abre o Assistente de adicionar o armazenamento de disco de saudação.

2. Em Olá **adicionar armazenamento em disco** página Olá **volumes disponíveis** caixa, selecione um volume e, em seguida, selecione **adicionar**.
3. Em Olá **selecionado volumes** caixa, digite um nome amigável para o volume de saudação e, em seguida, selecione **Okey**.

      ![Assistente para Adicionar Armazenamento em Disco - Adicionar volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Se você quiser tooadd um disco, disco Olá deve pertencer tooa grupo de proteção que tem armazenamento legado. Esses discos podem ser usados apenas para esses grupos de proteção. Se o servidor de Backup não tem fontes que têm proteção herdada, disco Olá não está listado.

  Para obter mais informações sobre como adicionar discos, consulte [adicionando discos tooincrease herdados armazenamento](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). Você não pode dar um nome amigável para um disco.


### <a name="assign-workloads-toovolumes"></a>Atribuir toovolumes de cargas de trabalho

No servidor de Backup, você especificar que cargas de trabalho recebem toowhich volumes. Por exemplo, você pode definir volumes caros que dão suporte a um grande número de operações de entrada/saída por segundo (IOPS) toostore somente as cargas de trabalho que exigem backups frequentes, de alto volume. Um exemplo é o SQL Server com logs de transação.

#### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Propriedades de saudação tooupdate de um volume no pool de armazenamento Olá no servidor de Backup, use o cmdlet do PowerShell de saudação DPMDiskStorage de atualização.

Sintaxe:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

Todas as alterações feitas por meio do PowerShell são refletidas na saudação da interface do usuário.


## <a name="protect-data-sources"></a>Proteger fontes de dados
toobegin proteção fontes de dados, crie um grupo de proteção. Olá seguindo as etapas realce as alterações ou adições toohello assistente New Protection Group.

toocreate um grupo de proteção:

1. No hello Console do administrador do servidor de Backup, selecione **proteção**.

2. Na faixa de opções de ferramenta hello, selecione **novo**.

    Isso abre o Assistente para criar novo grupo de proteção de saudação.

  ![Assistente para Criar Novo Grupo de Proteção](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. Em Olá **bem-vindo** página, selecione **próximo**.
4. Em Olá **Selecionar tipo de grupo de proteção** , selecione o tipo de saudação do grupo de proteção, você deseja toocreate e, em seguida, selecione **próximo**.

  ![Selecionar a página do Tipo de Grupo de Proteção](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. Em Olá **selecionar membros do grupo** página Olá **membros disponíveis** painel, membros de saudação com proteção agentes estão listados. Neste exemplo, selecione o volume D:\ e E:\ e adicioná-las toohello **membros selecionados** painel. Selecione **Avançar**.

  ![Selecionar a página Membros do Grupo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. Em Olá **Selecionar método de proteção de dados** , insira um **nome do grupo de proteção**, selecione o método de proteção hello e, em seguida, selecione **próximo**. Se desejar que a proteção de curto prazo, você deve selecionar Olá **disco** método de backup.

  ![Selecionar a página Método de Proteção de Dados](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. Em Olá **especificar objetivos de curto prazo** página Detalhes Olá selecione **período de retenção** e **frequência de sincronização**. Em seguida, selecione **Avançar**. Opcionalmente, o agendamento de saudação toochange para quando os pontos de recuperação são feitos, selecione **modificar**.

  ![Especificar a página Objetivos de Curto Prazo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. Em Olá **rever alocação do disco armazenamento** página, examine os detalhes sobre as fontes de dados de saudação selecionado, tamanho e valores para Olá espaço toobe provisionado e Olá volume de armazenamento de destino.

  ![Página Examinar Alocação de Armazenamento de Disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Volumes de armazenamento são baseados na alocação de volume de carga de trabalho de saudação (definida usando o PowerShell) e Olá armazenamento disponível. Você pode alterar os volumes de armazenamento Olá selecionando outros volumes no menu suspenso de saudação. Se você alterar o valor Olá **armazenamento de destino**, Olá valor para **armazenamento em disco disponível** alterado dinamicamente valores de tooreflect em **espaço livre** e **Pela espaço**.

  Se as fontes de dados de saudação o crescimento como planejado, Olá valor Olá **espaço pela** coluna em **armazenamento em disco disponível** reflete a quantidade de saudação de armazenamento adicional é necessário. Use este plano de toohelp valor suas necessidades de armazenamento de backups suaves. Não se o valor de saudação for zero, há nenhum problema potencial com o armazenamento em um futuro próximo Olá. Se o valor de saudação é um número diferente de zero, você não tem armazenamento suficiente alocado (com base em sua proteção hello e política de tamanho dos dados de seus membros protegidos).

  ![Armazenamento em disco subalocado](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   toofinish criar Assistente de saudação completa, grupo de proteção.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Migrar armazenamento legado tooModern o armazenamento de Backup
Depois de atualizar instalação tooor v2 do servidor de Backup e atualização Olá tooWindows de sistema operacional Server 2016, atualize seu grupos de proteção toouse modernos o armazenamento de Backup. Por padrão, os grupos de proteção não são alterados. Eles continuam toofunction como eles foram configurados inicialmente. 

Atualizar grupos de proteção toouse modernos o armazenamento de Backup é opcional. grupo de proteção do tooupdate Olá, interrompa a proteção de todas as fontes de dados usando Olá manter opção dados. Em seguida, adicione Olá dados fontes tooa novo grupo de proteção.

1. No Console do administrador do hello, selecione Olá **proteção** recurso. Em Olá **membro do grupo de proteção** lista, membro hello e, em seguida, selecione **parar proteção do membro**.

  ![Interromper a proteção de membro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. Em Olá **remover do grupo** caixa de diálogo, examine Olá usado espaço em disco e Olá espaço livre para o pool de armazenamento hello. padrão de saudação é tooleave pontos de recuperação Olá no disco hello e permitir que eles tooexpire por sua política de retenção associado. Clique em **OK**.

  Se quiser que o pool do tooimmediately Olá retorno usado em disco espaço toohello livre de armazenamento, selecione Olá **excluir réplica no disco** dados backup da caixa de seleção toodelete saudação (e pontos de recuperação) associado a esse membro.

  ![Remover da caixa de diálogo Grupo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Crie um grupo de proteção que usa o Armazenamento de Backup Moderno. Inclua fontes de dados de Saudação desprotegida.


## <a name="add-disks-tooincrease-legacy-storage"></a>Adicionar discos tooincrease herdados armazenamento

Se você deseja que o armazenamento de toouse herdados com o servidor de Backup, talvez seja necessário armazenamento herdados do tooincrease tooadd discos. 

armazenamento em disco tooadd:

1. No Console do administrador do hello, selecione **gerenciamento** > **armazenamento em disco** > **adicionar**.

    ![Adicionar caixa de diálogo de Armazenamento em Disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. Em Olá **adicionar armazenamento em disco** caixa de diálogo, selecione **adicionar discos**.

5. Na lista de saudação de discos disponíveis, selecione discos Olá deseja tooadd, selecione **adicionar**e, em seguida, selecione **Okey**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Atualizar o agente de proteção Olá Data Protection Manager

Servidor de backup usa o agente de proteção do System Center Data Protection Manager Olá para atualizações. Se você estiver atualizando um agente de proteção não está conectado toohello rede, você não pode usar o hello Data Protection Manager Administrator Console toocomplete uma atualização de agente conectado. Você deve atualizar o agente de proteção de saudação em um ambiente de domínio não ativo. Até que o computador do cliente de saudação é rede toohello conectado, Olá que Data Protection Manager Administrator Console mostra essa atualização de agente de proteção hello está pendente.

Olá seções a seguir descrevem como tooupdate agentes de proteção para computadores cliente que estão conectados e os computadores cliente que não estão conectados.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Atualizar um agente de proteção de um computador cliente conectado

1. No hello Console do administrador do servidor de Backup, selecione **gerenciamento** > **agentes**.

2. No painel de exibição de hello, selecione os computadores cliente Olá para o qual você deseja que o agente de proteção de saudação tooupdate.

  > [!NOTE]
  > Olá **atualizações de agente** coluna indica quando uma atualização do agente de proteção está disponível para cada computador protegido. Em Olá **ações** painel, Olá **atualização** ação está disponível somente quando um computador protegido está selecionado e as atualizações estão disponíveis.
  >
  >

3. tooinstall atualizado agentes de proteção em computadores Olá selecionado, Olá **ações** painel, selecione **atualização**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Atualizar um agente de proteção em um computador cliente que não está conectado

1. No hello Console do administrador do servidor de Backup, selecione **gerenciamento** > **agentes**.

2. No painel de exibição de hello, selecione os computadores cliente Olá para o qual você deseja que o agente de proteção de saudação tooupdate.

  > [!NOTE]
   > Olá **atualizações de agente** coluna indica quando uma atualização do agente de proteção está disponível para cada computador protegido. Em Olá **ações** painel, Olá **atualização** ação não está disponível quando um computador protegido está selecionado, a menos que as atualizações estão disponíveis.
  >
  >

3. tooinstall atualizado agentes de proteção nos computadores de saudação selecionada, selecionados **atualização**.

4. Para um computador cliente que não está conectado rede toohello, até que o computador Olá é rede toohello conectado, Olá **Status do agente** coluna mostra um status de **atualização pendente**.

  Depois que um computador cliente estiver conectado toohello rede, Olá **atualizações de agente** coluna para o computador de cliente Olá mostra um status de **atualização**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Mover herdado de grupos de proteção de uma versão antiga e sincronização Olá nova versão com o Azure

Depois que o servidor de Backup do Azure e hello SO são atualizadas, você está pronto tooprotect novas fontes de dados usando o armazenamento de Backup modernos. No entanto já protegido fontes de dados continuará toobe protegido na Olá herdado de maneira que estavam no servidor de Backup do Azure, mas todas as novas proteções usará o armazenamento de Backup modernos.

Etapas a seguir são toomigrate fontes de dados do modo herdado proteção tooModern de armazenamento de backup.

• Adicione Olá novo volume toohello DPM pool de armazenamento e atribuir marcas de fonte de dados e nomes amigáveis, se desejado.
• Para cada fonte de dados que está no modo herdado, interrompa a proteção de fontes de dados hello e "Reter dados protegidos".  Isso permitirá a recuperação de pontos de recuperação antigos após a migração.

• Criar um novo grupo de proteção e selecione Olá fontes de dados que são armazenado usando o novo formato de toobe.
• O DPM fará uma cópia da réplica Olá herdados do armazenamento de backup em Olá volume de armazenamento de Backup modernos localmente.
Observação: Isso será visto como um trabalho de operação pós-recuperação • Todos os novos pontos de sincronização e de recuperação serão então armazenados no armazenamento de backup moderno.
• Pontos de recuperação antigos serão removidos de limite expirar e, eventualmente, libere espaço em disco hello.
• Depois que todos os volumes de saudação herdados são excluídos do armazenamento antigo hello, disco Olá pode ser removido do sistema de backup e hello do Azure.
• Fazer um backup de hello Azure DPMDB.

Parte 2:-itens importantes > novo servidor de saudação precisará toobe mesmo nome como servidor de Backup do Azure original hello. Não é possível alterar o nome de saudação do servidor de backup do Azure nova Olá se você deseja que o pool de armazenamento antigo toouse e pontos de recuperação de tooretain DPMDB - deve ter backup do DPMDB, pois ele será necessário toobe restaurado

1) Desligamento Olá servidor de backup do Azure original ou tirá-lo durante a transmissão hello.
2) Redefina conta da máquina Olá no active directory.
3) Instale o Server 2016 no novo computador e nome-Olá o mesmo nome de máquina de servidor de Backup do Azure original hello.
4) Unir Olá domínio
5) Instalar o servidor de Backup do Azure V2 (mover discos do pool de armazenamento do DPM do servidor antigo e importar)
6) Restaurar Olá DPMDB retirado do final da parte 2
7) Anexe armazenamento Olá da saudação original backup toohello novo servidor.
8) Na restauração do SQL Olá DPMDB
9) Na linha de comando de administrador no novo tooMicrosoft de cd do servidor do Azure Backup instalar local e a pasta bin

Exemplo de caminho: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
backup tooAzure execute DPMSYNC-SYNC

10) Execute o DPMSYNC-SYNC Observação Se você tiver adicionado um novo pool de armazenamento do DPM toohello discos em vez de mover Olá antigas, execute DPMSYNC - Reallocatereplica

## <a name="new-powershell-cmdlets-in-v2"></a>Novo cmdlets do PowerShell em v2

Quando você instala o Servidor de Backup do Azure v2, dois novos cmdlets estão disponíveis: 
* [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Próximas etapas

Saiba como tooprepare seu servidor ou começar a proteger uma carga de trabalho:
- [Preparar as cargas de trabalho do Servidor de Backup](backup-azure-microsoft-azure-backup.md)
- [Usar o servidor de Backup tooback um servidor VMware](backup-azure-backup-server-vmware.md)
- [Usar o servidor de Backup tooback o SQL Server](backup-azure-sql-mabs.md)
- [Usar o Armazenamento de Backup Moderno com o Servidor de Backup](backup-mabs-add-storage.md)

