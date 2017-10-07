---
title: 'Backup do Azure: Recuperar arquivos e pastas de um backup de VM do Azure | Microsoft Docs'
description: "Recuperar arquivos de um ponto de recuperação de uma máquina virtual do Azure"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "recuperação a nível de item; recuperação de arquivos de backup da VM do Azure; restaurar arquivos de uma VM do Azure"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Recuperar arquivos de um backup de máquina virtual do Azure

O backup do Azure fornece Olá recurso toorestore [VMs do Azure e discos](./backup-azure-arm-restore-vms.md) de backups de máquina virtual do Azure. Este artigo explica como você pode recuperar itens, como arquivos e pastas, de um backup de VM do Azure.

> [!Note]
> Este recurso está disponível para máquinas virtuais do Azure implantados usando o modelo do Gerenciador de recursos de saudação e protegido tooa Cofre de serviços de recuperação.
> Não há suporte para a recuperação de arquivos de um backup criptografado de VM.
>

## <a name="mount-hello-volume-and-copy-files"></a>Montar o volume e copiar arquivos de saudação

1. O logon no hello [portal do Azure](http://portal.Azure.com). Localize o Cofre de serviços de recuperação relevante hello e fazer backup do item Olá necessário.

2. Na folha de Item de Backup hello, clique em **recuperação de arquivos**

    ![Abra o item de backup do cofre de Serviços de Recuperação](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Olá **recuperação de arquivo** folha é aberta.

    ![Folha de recuperação de arquivo](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. De saudação **Selecionar ponto de recuperação** menu suspenso, o ponto de recuperação Olá select que contém arquivos de saudação desejado. Por padrão, o último ponto de recuperação Olá já está selecionado.

4. Clique em **executável baixar** (para VM do Windows Azure) ou **baixar Script** (para VM do Azure Linux) software de saudação toodownload que você usará toocopy arquivos de ponto de recuperação de saudação.

  executável/script Hello cria uma conexão entre o computador local hello e hello especificado ponto de recuperação.

5. Você precisa de um script executável Olá baixado senha toorun. Você pode copiar senha de saudação do portal hello usando Olá cópia botão ao lado de senha Olá gerado

    ![Senha gerada](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. No computador de saudação onde deseja toorecover Olá arquivos, execute o executável/script hello. Execute o script com credenciais de administrador. Se você executar o script hello em um computador com acesso restrito, certifique-se de que há acesso a:

    - download.microsoft.com
    - Pontos de extremidade do Azure usados para backups de VM do Azure
    - porta de saída 3260

   Para o Linux, script hello exige componentes 'open-iscsi' e 'lshw' ponto de recuperação de toohello tooconnect. Se aqueles não existe no computador de saudação em que é executado, ele solicita para componentes relevantes da permissão tooinstall hello e instala-os mediante consentimento.
   
   Digite a senha de saudação copiada do portal de saudação quando solicitado. Depois que a senha válida Olá é inserida scripts Olá conecta toohello ponto de recuperação.
      
    ![Folha de recuperação de arquivo](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Você pode executar o script hello em qualquer computador que tenha o sistema operacional de saudação mesmo (ou compatíveis) como Olá backup VM. Consulte Olá [tabela de sistema operacional compatível](backup-azure-restore-files-from-vm.md#compatible-os) para sistemas operacionais compatíveis. Se Olá protegido virtual do Azure usa máquina que arrays(for Linux VMs) LVM/RAID ou espaços de armazenamento do Windows (para VMs do Windows Azure), e você não pode executar Olá executável/script hello mesma máquina virtual. Em vez disso, execute-o em qualquer outra máquina com um sistema operacional compatível.

### <a name="compatible-os"></a>Sistema operacional compatível

#### <a name="for-windows"></a>Para Windows

Olá a seguinte tabela mostra Olá compatibilidade entre os sistemas operacionais de servidor e o computador. Ao recuperar arquivos, você não pode restaurar arquivos entre sistemas operacionais incompatíveis.

|Sistema operacional de servidor | Sistema operacional de cliente compatível  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Para Linux

No Linux, o requisito fundamental Olá é que Olá sistema operacional da máquina de saudação onde é executado o script hello deve dar suporte a saudação de sistema de arquivos de saudação arquivos presentes no hello backup VM do Linux. Ao selecionar um script da máquina toorun hello, verifique se que ele tem versões compatíveis de sistema operacional e Olá Olá conforme mencionado na tabela de saudação abaixo.

|Sistema operacional Linux | Versões  |
| --------------- | ---- |
| Ubuntu | 12.04 e acima |
| CentOS | 6.5 e acima  |
| RHEL | 6.7 e acima |
| Debian | 7 e acima |
| Oracle Linux | 6.4 e acima |

Olá script também requer python e bash tooexecute de componentes e se conectar com segurança toohello ponto de recuperação.

|Componente | Versão  |
| --------------- | ---- |
| bash | 4 e acima |
| python | 2.6.6 e acima  |


### <a name="identifying-volumes"></a>Identificação de Volumes

#### <a name="for-windows"></a>Para Windows

Quando você executa exectuable hello, o sistema de operacional de Olá monta volumes novo hello e atribui letras de unidade. Você pode usar o Windows Explorer ou do Explorador de arquivos toobrowse essas unidades. Olá letras de unidade atribuídas toohello volumes podem não ser Olá letras mesmo como hello máquina virtual original, no entanto, Olá nome do volume é preservada. Por exemplo, se hello volume na máquina virtual original de saudação foi "disco de dados (e:\)", que o volume pode ser conectado como "disco de dados ('Qualquer letra de unidade disponível':\) no computador local hello. Procure por meio de todos os volumes mencionados na saída do script hello até encontrar a pasta/arquivos.  
       
   ![Folha de recuperação de arquivo](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Para Linux

No Linux, volumes Olá Olá do ponto de recuperação são montados toohello pasta onde o script hello é executado. Olá anexar discos, volumes e montagem correspondente Olá caminhos são mostrados adequadamente. Esses caminhos de montagem são visíveis toousers ter acesso ao nível raiz. Navegar pelos volumes Olá mencionados na saída do script hello.

  ![Folha Recuperação de Arquivo do Linux](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Fechando a conexão de saudação

Depois de identificar arquivos hello e copiá-los tooa local de armazenamento local, remover ou desmontar unidades adicionais hello. toounmount Olá unidades, Olá **a recuperação de arquivos** folha em Olá portal do Azure, clique em **desmontar discos**.

![Desmontar discos](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Quando discos Olá tiverem sido desmontados, você receberá uma mensagem informando que ela foi bem-sucedida. Ele pode levar alguns minutos para Olá toorefresh de conexão para que você possa remover discos hello.

No Linux, após o ponto de recuperação Olá conexão toohello for rompido, Olá SO não remove caminhos de montagem correspondente Olá automaticamente. Eles existem como volumes "órfãos" e são visíveis, mas gera um erro quando você arquivos Olá acesso/gravação. Eles podem ser removidos manualmente. script Hello, quando executado, identifica esses volumes existentes de pontos de recuperação anterior e limpa mediante consentimento.

## <a name="special-configurations"></a>Configurações especiais

### <a name="dynamic-disks"></a>Discos Dinâmicos

Se Olá VM do Azure que foi feito o backup tem volumes que abrangem vários discos (volumes estendidos e distribuídos) e/ou tolerância volumes (volumes espelhados e RAID-5) em discos dinâmicos, você não pode executar o script executável Olá Olá mesma VM. Em vez disso, execute o script executável hello em qualquer outro computador com um sistema operacional compatível.

### <a name="windows-storage-spaces"></a>Espaços de Armazenamento do Windows

Espaços de armazenamento do Windows é uma tecnologia no armazenamento do Windows que permite que você toovirtualize armazenamento. Com espaços de armazenamento do Windows, você pode agrupar os discos de padrão industrial nos pools de armazenamento e, em seguida, criar discos virtuais, chamados de espaços de armazenamento do espaço disponível de saudação desses pools de armazenamento.

Se Olá VM do Azure que foi feito o backup usa espaços de armazenamento do Windows, em seguida, você não pode executar o script executável Olá Olá mesma VM. Em vez disso, execute o script executável hello em qualquer outro computador com um sistema operacional compatível.

### <a name="lvmraid-arrays"></a>Matrizes LVM/RAID

No Linux, o Gerenciador de volumes lógicos (LVM) e/ou software matrizes RAID são volumes lógicos usados toomanage através de vários discos. Se Olá backup VM Linux usa LVM e/ou matrizes RAID, você não pode executar o script hello em hello mesma VM. Em vez disso, execute o script hello em qualquer outro computador com sistema operacional compatível e que oferece suporte ao sistema de arquivos de backup de VM de hello.

saída do script Hello exibe hello LVM e/ou discos de matrizes RAID e volumes de saudação com tipo de partição Olá conforme mostrado abaixo

   ![Folha Saída de LVM do Linux](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Olá seguir comandos precisa toobe executar por Olá usuário toobring essas partições online. 

**Para partições LVM**

```
$ pvs <volume name as shown above in hello script output> 
```
Lista nomes de grupo de volume Olá em um volume físico.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Isso lista todos os volumes lógicos, os nomes e os seus caminhos em um grupo de volumes.

```
$ mount <LV path> </mountpath>
```
caminho de toohello toomount Olá volumes lógicos de sua escolha.


**Para Matrizes RAID**

```
$ mdadm –detail –scan
```
Isso exibe detalhes sobre todos os discos raid. disco RAID relevante Hello será exibido como`/dev/mdm/<RAID array name in hello backed up VM>`

Use o comando de montagem de saudação se o disco RAID Olá tem volumes físicos.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Se esse disco RAID tiver outro LVM definida siga Olá mesmo procedimento, conforme descrito acima para partições LVM com o nome do volume Olá sendo Olá nome de disco RAID

## <a name="troubleshooting"></a>Solucionar problemas

Se você tiver problemas durante a recuperação de arquivos de máquinas virtuais de saudação, verifique Olá tabela para obter informações adicionais a seguir.

| Mensagem de erro/Cenário | Causas prováveis | Ação recomendada |
| ------------------------ | -------------- | ------------------ |
| Saída de exe: *exceção conectando toohello destino* |Script não é capaz de tooaccess ponto de recuperação de saudação | Verifique se o computador Olá atende aos requisitos de acesso de saudação mencionados acima|  
|   Saída de exe: *destino Olá já foi registrado por meio de uma sessão ISCSI.* |   script Hello já foi executado no hello mesmas unidades de máquina e hello foram anexadas |   volumes de saudação do ponto de recuperação Olá já foram anexados. NÃO pode ser montados com hello mesmo de letras de unidade Olá VM original. Navegar por todos os volumes de saudação disponíveis no Explorador de arquivos Olá para o arquivo |
| Saída de exe: *esse script é inválido porque discos Olá tem sido desmontados por meio de limite de RH 12 Olá portal/excedido. Baixe um novo script do portal de saudação.* |    discos Olá tem sido desmontados de portal hello ou limite de RH 12 Olá excedido |  Esse exe é inválido e não pode ser executado. Se você quiser tooaccess Olá arquivos essa recuperação point-in-time, visite o portal de saudação para um novo. exe|
| Na máquina de saudação onde Olá exe é executado: novos volumes de saudação não são desmontados depois Olá desmontagem botão é clicado |    Iniciador ISCSI Olá na máquina de saudação não esteja respondendo/atualizar o seu destino de toohello de conexão e manter o cache de saudação |    Aguarde alguns minutos depois Olá desmontagem botão é pressionado. Se novos volumes de saudação não ainda são desmontados, procure por meio de todos os volumes de saudação. Isso força Olá iniciador toorefresh Olá conexão Olá volume e é desmontado com uma mensagem de erro que Olá disco não está disponível|
| Saída de exe: Script é executado com êxito, mas "Novos volumes anexados" não são exibidos na saída do script hello |   Esse é um problema temporário   | volumes Olá seriam foram já anexados. Abra o Explorer toobrowse. Se você estiver usando Olá mesmo computador para executar scripts sempre, considere Reiniciar computador hello e Olá lista deve ser exibida nas execuções de exe subsequentes hello. |
| Específicas do Linux: não é possível tooview Olá desejado volumes | Olá sistema operacional da máquina de saudação onde o script hello é executado pode não reconhecer Olá o sistema de arquivos subjacente de saudação backup de VM | Verifique se o ponto de recuperação de saudação é falha consistente ou consistentes de arquivos. Se o script em outro computador cujo sistema operacional reconhece Olá Olá consistente, execute do arquivo de backup do sistema de arquivos da VM |
| Específicas do Windows: não é possível tooview Olá desejado volumes | discos Olá podem ter sido anexados, mas não foram configurados volumes Olá | Na tela de gerenciamento de disco hello, identificar o ponto de recuperação de toohello relacionados de discos adicionais de saudação. Se qualquer um desses discos estiverem offline no estado tente torná-los online clicando em disco hello e clique em 'Online'|
