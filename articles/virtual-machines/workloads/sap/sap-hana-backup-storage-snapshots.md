---
title: "backup do Azure do HANA aaaSAP com base em instantâneos de armazenamento | Microsoft Docs"
description: "Há duas possibilidades principais de backup para SAP HANA em máquinas virtuais do Azure, e este artigo aborda o backup do Azure do SAP HANA baseado em instantâneos de armazenamento"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Backup do SAP HANA com base em instantâneos de armazenamento

## <a name="introduction"></a>Introdução

Este artigo faz parte de uma série dividida em três partes com artigos relacionados ao backup do SAP HANA. [Guia de backup para o SAP HANA em máquinas virtuais Azure](sap-hana-backup-guide.md) fornece uma visão geral e informações sobre como começar, e [SAP HANA Azure Backup em nível de arquivo](sap-hana-backup-file-level.md) abrange Olá a opção de backup baseado em arquivo.

Ao usar um recurso de backup de VM para um sistema de demonstração de em um instância única, um considere fazer um backup VM em vez de gerenciar backups do HANA em Olá nível do sistema operacional. Uma alternativa é cópias de toocreate do tootake BLOBs do Azure instantâneos de discos virtuais individuais, que são anexados tooa VM e manter os arquivos de dados do HANA hello. Mas ponto crítico é a consistência do aplicativo quando criar um instantâneo de backup ou o disco VM enquanto Olá sistema está ligado e em execução. Consulte _consistência de dados SAP HANA ao armazenamento de instantâneos_ no artigo relacionado Olá [guia de Backup para o SAP HANA em máquinas virtuais Azure](sap-hana-backup-guide.md). O SAP HANA tem um recurso que oferece suporte a esses tipos de instantâneos de armazenamento.

## <a name="sap-hana-snapshots"></a>Instantâneos do SAP HANA

Há um recurso no SAP HANA que oferece suporte a tirar um instantâneo do armazenamento. No entanto, a partir de dezembro de 2016, há uma restrição sistemas toosingle contêiner. As configurações de contêiner multilocatário não dão suporte a esse tipo de instantâneo de banco de dados (veja [Criar um instantâneo de armazenamento (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).

Ele funciona da seguinte maneira:

- Preparar para um instantâneo de armazenamento iniciando o instantâneo do SAP HANA Olá
- Execute o instantâneo de armazenamento da saudação (BLOBs do Azure, instantâneo, por exemplo)
- Confirme o instantâneo do SAP HANA Olá

![Esta captura de tela mostra que um instantâneo de dados do SAP HANA pode ser criado por meio de uma instrução SQL](media/sap-hana-backup-storage-snapshots/image011.png)

Esta captura de tela mostra que um instantâneo de dados do SAP HANA pode ser criado por meio de uma instrução SQL.

![Olá, em seguida, de instantâneo também aparece no catálogo de backup de saudação do SAP HANA Studio](media/sap-hana-backup-storage-snapshots/image012.png)

Olá, em seguida, de instantâneo também aparece no catálogo de backup de saudação do SAP HANA Studio.

![No disco, instantâneo Olá aparece no diretório de dados do SAP HANA Olá](media/sap-hana-backup-storage-snapshots/image013.png)

No disco, instantâneo Olá aparece no diretório de dados do SAP HANA hello.

Um tem tooensure que também é a garantia de consistência do sistema de arquivo hello antes de executar o instantâneo de armazenamento Olá enquanto HANA SAP está no modo de preparação de instantâneo hello. Consulte _consistência de dados SAP HANA ao armazenamento de instantâneos_ no artigo relacionado Olá [guia de Backup para o SAP HANA em máquinas virtuais Azure](sap-hana-backup-guide.md).

Depois de instantâneo de armazenamento Olá, é instantâneo de SAP HANA Olá tooconfirm crítico. Há um toorun de instrução SQL correspondente: instantâneo de fechamento de dados de BACKUP (consulte [BACKUP de dados de instantâneo instrução CLOSE (Backup e recuperação)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Confirme o instantâneo do HANA hello. Vencimento muito&quot;Copy-on-Write,&quot; SAP HANA podem exigir espaço em disco adicional no instantâneo-modo de preparação e não é possível toostart novos backups até que o instantâneo do SAP HANA Olá for confirmado.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Backup da VM do HANA por meio do serviço de Backup do Azure

A partir de dezembro de 2016, o agente de backup de saudação do hello serviço Backup do Azure não está disponível para VMs do Linux. uso de toomake de backup do Azure no nível de arquivo/diretório hello, um copie tooa de arquivos de backup do SAP HANA VM do Windows e, em seguida, usar o agente de backup hello. Caso contrário, apenas um backup completo de VM do Linux é possível por meio do serviço de Backup do Azure hello. Consulte [visão geral da saudação recursos no Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) toofind mais.

Olá serviço Backup do Azure oferece uma opção tooback e restaurar uma máquina virtual. Para obter mais informações sobre esse serviço e como ele funciona podem ser encontradas no artigo de saudação [planejar sua infraestrutura de backup de VM no Azure](../../../backup/backup-azure-vms-introduction.md).

Há duas considerações importantes, de acordo com o artigo toothat:

_&quot;Para máquinas virtuais Linux, somente backups consistentes de arquivos são possíveis, como Linux não tem um tooVSS plataforma equivalente.&quot;_

_&quot;Os aplicativos precisam tooimplement seus próprios &quot;correção&quot; mecanismo Olá restaurado dados.&quot;_

Portanto, um tem toomake se que SAP HANA está em um estado consistente no disco quando Olá backup é iniciado. Consulte _instantâneos do SAP HANA_ descritos anteriormente Olá documento. Mas há um problema em potencial quando o SAP HANA permanece nesse modo de preparação de instantâneo. Veja [Criar um instantâneo de armazenamento (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) para saber mais.

O artigo declara:

_&quot;Ele é altamente recomendável tooconfirm ou abandonar um instantâneo de armazenamento mais rápido possível depois de ele ter sido criado. Enquanto o instantâneo de armazenamento hello está sendo preparado ou criado, Olá dados relevantes de instantâneo estão congelados. Enquanto dados relevantes de instantâneo Olá permanecem congelados, alterações ainda podem ser feitas no banco de dados de saudação. Essas alterações não causará Olá congelado toobe relevantes de instantâneo de dados alterado. Em vez disso, as alterações de saudação são gravadas toopositions na área de dados Olá separados do instantâneo de armazenamento hello. As alterações também são gravadas toohello log. No entanto, mais dados de instantâneo relevantes Olá Olá são mantidos congelados, Olá Olá mais volume de dados pode crescer.&quot;_

O Backup do Azure cuida da consistência do sistema de arquivo hello por meio de extensões de VM do Azure. Essas extensões não são autônomos disponíveis e funcionam somente em conjunto com o serviço de Backup do Azure. No entanto, ainda é um requisito toomanage uma consistência de aplicativo SAP HANA instantâneo tooguarantee.

O Backup do Azure tem duas fases principais:

- Tirar instantâneo
- Transferência de dados toovault

Uma pode confirmar o instantâneo do SAP HANA Olá após a conclusão da fase de serviço de Backup do Azure Olá de tirar um instantâneo. Pode levar vários toosee de minutos em Olá portal do Azure.

![Esta figura mostra a parte da lista de trabalhos de backup de saudação de um serviço de Backup do Azure](media/sap-hana-backup-storage-snapshots/image014.png)

Esta figura mostra a parte da lista de trabalho de backup de saudação de um serviço de Backup do Azure, que era usado tooback a VM de teste HANA hello.

![detalhes do trabalho Olá tooshow, clique em trabalho de backup Olá no hello portal do Azure](media/sap-hana-backup-storage-snapshots/image015.png)

detalhes do trabalho Olá tooshow, clique em trabalho de backup Olá no hello portal do Azure. Aqui, um pode ver Olá duas fases. Pode levar alguns minutos até que ela mostra a fase de instantâneo Olá como concluída. A maioria do tempo de saudação é gasto na fase de transferência de dados de saudação.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Automação de backups HANA VM por meio do serviço de Backup do Azure

Um pôde confirmar instantâneo do SAP HANA Olá manualmente depois que a fase de instantâneo do Azure Backup Olá for concluída, conforme descrito anteriormente, mas é útil tooconsider automação porque um administrador não pode monitorar a lista de trabalho de backup de saudação em Olá portal do Azure.

Aqui está uma explicação de como isso pode ser obtido por meio de cmdlets do Azure PowerShell.

![Um serviço de Backup do Azure foi criado com hello nome hana--Cofre de backup](media/sap-hana-backup-storage-snapshots/image016.png)

Um serviço de Backup do Azure foi criado com o nome da saudação &quot;hana-backup-cofre.&quot; Olá comando PS **AzureRmRecoveryServicesVault de Get-nome do Cofre de backup do hana** recupera Olá objeto correspondente. Esse objeto é usado tooset Olá backup contexto como mostrado na figura a seguir hello.

![É possível verificar Olá trabalho de backup em andamento](media/sap-hana-backup-storage-snapshots/image017.png)

Depois de contexto correto de saudação de configuração, um pode verificar Olá trabalho de backup está em andamento e, em seguida, procure os detalhes do trabalho. lista a subtarefa Olá mostra se fase de instantâneo de saudação do hello trabalho de backup do Azure já foi concluído:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Valor de saudação de pesquisa em um loop até que ele transforma tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Depois que os detalhes do trabalho Olá são armazenados em uma variável, é simplesmente PS sintaxe tooget toohello primeira entrada da matriz e recuperar o valor de status de saudação. script de automação de saudação toocomplete, sondagem Olá valor em um loop até que ele ativa muito&quot;concluída.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Restaurar a chave de licença do HANA e VM por meio do serviço de Backup do Azure

saudação de serviço de Backup do Azure é projetado toocreate uma nova VM durante a restauração. Não há nenhum plano à direita agora toodo um &quot;in-loco&quot; restauração de uma VM do Azure existente.

![Esta figura mostra a opção de restauração de saudação de saudação do serviço do Azure em Olá portal do Azure](media/sap-hana-backup-storage-snapshots/image019.png)

Esta figura mostra a opção de restauração de saudação de saudação do serviço do Azure em Olá portal do Azure. Você pode escolher entre criar uma máquina virtual durante a restauração ou restauração de discos de saudação. Depois de restaurar discos Olá, é necessário ainda toocreate uma nova VM sobre ele. Sempre que uma nova VM é criada em alterações de VM ID exclusivas hello Azure (consulte [acessando e usando o Azure VM ident](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Esta figura mostra a ID exclusiva de VM do Azure Olá antes e após a restauração de saudação por meio do serviço de Backup do Azure](media/sap-hana-backup-storage-snapshots/image020.png)

Esta figura mostra a ID exclusiva de VM do Azure Olá antes e após a restauração de saudação por meio do serviço de Backup do Azure. chave de hardware do SAP Hello, que é usado para licenciamento do SAP, está usando esta ID exclusiva de VM. Como consequência, uma nova licença SAP tem toobe instalado após uma restauração de VM.

Um novo recurso de Backup do Azure foi apresentado no modo de visualização durante a criação de saudação deste guia de backup. Ele permite que uma restauração de nível de arquivo com base no instantâneo VM Olá que foi feito para Olá VM backup. Isso evita a necessidade de saudação toodeploy uma nova VM e, portanto, permanece de VM ID exclusivo Olá Olá mesmo e nenhuma nova chave de licença do SAP HANA é necessária. Mais documentação sobre este recurso será fornecida depois que ele foi totalmente testado.

O Backup do Azure serão eventualmente permitir o backup de discos virtuais do Azure individuais, além de arquivos e diretórios de dentro de Olá VM. Uma grande vantagem do Backup do Azure é o gerenciamento de todos os backups de hello, salvando Prezado cliente tenha toodo-lo. Se uma restauração for necessária, o Backup do Azure selecionará Olá toouse de backup correto.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>Backup de VM do SAP HANA por meio de instantâneo de disco manual

Em vez de usar o serviço de Backup do Azure Olá, um pode configurar uma solução de backup individual por meio da criação de instantâneos de blob do Azure VHDs manualmente por meio do PowerShell. Consulte [usando instantâneos de blob com o PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) para obter uma descrição das etapas de saudação.

Ele oferece mais flexibilidade, mas não resolve problemas de saudação explicados anteriormente neste documento:

- Você ainda deve se certificar de que o SAP HANA está em um estado consistente
- disco do sistema operacional Olá não pode ser substituído, mesmo que exista Olá que VM é desalocada devido a um erro informando que uma concessão. Funciona somente após a exclusão Olá VM, que poderia levar tooa novo exclusivo ID da VM e hello necessidade tooinstall uma nova licença SAP.

![É possível toorestore somente Olá os discos de dados de uma VM do Azure](media/sap-hana-backup-storage-snapshots/image021.png)

É toorestore possíveis apenas discos de dados de saudação de uma VM do Azure, evitando o problema de saudação da obtenção de uma nova ID exclusiva da VM e, portanto, invalidados licença do SAP hello:

- Para teste hello, dois discos de dados do Azure foram anexado tooa VM e RAID de software foi definida na parte superior-los 
- Ele foi confirmado que o SAP HANA estava em um estado consistente pelo recurso de instantâneo do SAP HANA
- Congelamento do sistema de arquivos (consulte _consistência de dados SAP HANA ao armazenamento de instantâneos_ no artigo relacionado Olá [guia de Backup para o SAP HANA em máquinas virtuais Azure](sap-hana-backup-guide.md))
- Instantâneos de blob foram tirados de ambos os discos de dados
- Descongelar do sistema de arquivos
- Confirmação de instantâneo do SAP HANA
- desanexar de ambos os discos e discos de dados do toorestore hello, Olá VM foi desligado
- Depois de desanexar discos hello, foram substituídos com instantâneos de blob antiga Olá
- E discos virtuais Olá restaurado foram anexados novamente toohello VM
- Depois que o tempo de instantâneo de VM, tudo no software Olá RAID funcionou bem e foi redefinido blob toohello de saudação inicial
- HANA foi redefinido instantâneo do HANA toohello

Se foi possível tooshut para baixo do SAP HANA antes de instantâneos de blob hello, procedimento Olá seria menos complexo. Nesse caso, um pode ignorar o instantâneo do HANA hello e, se nada mais acontece no sistema hello, também ignorar congelamento de sistema de arquivo hello. Complexidade adicional é imagem hello quando é necessário toodo instantâneos enquanto tudo está online. Consulte _consistência de dados SAP HANA ao armazenamento de instantâneos_ no artigo relacionado Olá [guia de Backup para o SAP HANA em máquinas virtuais Azure](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Próximas etapas
* [Guia de backup do SAP HANA nas Máquinas Virtuais do Azure](sap-hana-backup-guide.md) fornece uma visão geral e informações sobre como começar.
* [Backup do HANA SAP com base no nível de arquivo](sap-hana-backup-file-level.md) abrange Olá a opção de backup baseado em arquivo.
* toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP no Azure (instâncias grandes), consulte [SAP HANA (instâncias grandes) alta disponibilidade e recuperação de desastres no Azure](hana-overview-high-availability-disaster-recovery.md).
