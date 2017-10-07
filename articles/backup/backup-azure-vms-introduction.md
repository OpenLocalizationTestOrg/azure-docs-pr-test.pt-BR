---
title: aaaPlanning sua infra-estrutura de backup de VM no Azure | Microsoft Docs
description: "Considerações importantes ao planejar tooback backup de máquinas virtuais no Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup de vms, backup de máquinas virtuais"
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Planejar sua infraestrutura de backup da VM no Azure
Este artigo fornece desempenho e recurso sugestões toohelp planejar sua infra-estrutura de backup de VM. Ele também define os aspectos fundamentais do serviço de Backup Olá; Esses aspectos podem ser essenciais para determinar sua arquitetura, planejamento de capacidade e agendamento. Se você tiver [preparar o ambiente](backup-azure-vms-prepare.md), planejamento é a próxima etapa de saudação antes de começar a [tooback máquinas virtuais](backup-azure-vms.md). Se você precisar de mais informações sobre máquinas virtuais do Azure, consulte Olá [documentação de máquinas virtuais](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>Como o Azure faz backup de máquinas virtuais?
Quando Olá serviço Backup do Azure inicia um trabalho de backup no tempo de saudação agendado, ela aciona Olá extensão backup tootake um instantâneo point-in-time. saudação de serviço de Backup do Azure usa Olá _VMSnapshot_ extensão no Windows e hello _VMSnapshotLinux_ extensão no Linux. extensão de saudação é instalado durante o primeiro backup VM hello. extensão de saudação tooinstall, Olá VM deve estar em execução. Se hello VM não está em execução, Olá serviço de Backup tira um instantâneo de saudação armazenamento subjacente (já que nenhum aplicativo grava ocorre durante a saudação que VM estiver parada).

Ao tirar um instantâneo de máquinas virtuais do Windows, o serviço de Backup Olá coordena com hello Volume Shadow Copy Service (VSS) tooget um instantâneo consistente dos discos da máquina de virtual hello. Se você estiver fazendo backup de máquinas virtuais do Linux, você pode escrever a consistência de tooensure seus próprios scripts personalizados quando tirar um instantâneo VM. Detalhes sobre como invocar esses scripts são fornecidos posteriormente neste artigo.

Depois de saudação serviço Backup do Azure usa instantâneo hello, dados saudação são toohello transferidos cofre. toomaximize eficiência, o serviço de saudação identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior de saudação hello.

![Arquitetura de backup de máquinas virtuais do Azure](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Quando a transferência de dados de saudação for concluída, Olá é removido e um ponto de recuperação é criado.

> [!NOTE]
> 1. Durante o processo de backup hello, Backup do Azure não inclui Olá temporário em disco anexado toohello VM. Para obter mais informações, consulte o blog de saudação em [armazenamento temporário](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Desde o Backup do Azure usa um instantâneo do nível de armazenamento e transferências que toovault de instantâneo, não altere chaves de conta de armazenamento Olá até a conclusão do trabalho de backup hello.
> 3. Para VMs premium, podemos copiar conta de toostorage Olá instantâneo. Trata-se de que o serviço de Backup do Azure obtém IOPS suficientes para a transferência de dados toovault de toomake. Essa cópia adicional de armazenamento é cobrada de acordo com a saudação tamanho alocado de VM. 
>

### <a name="data-consistency"></a>Consistência de dados
Fazendo backup e restaurando dados críticos de negócios é complicada pelo fato de saudação que dados corporativos críticos devem ser feitos enquanto os aplicativos de saudação que produzem Olá dados estão em execução. tooaddress essa, Backup do Azure suporta os backups consistentes com aplicativos para Windows e VMs do Linux
#### <a name="windows-vm"></a>VM Windows
O Backup do Azure realiza backups completos de VSS em VMs do Windows (leia mais sobre [backup completo de VSS](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). backups de cópia VSS tooenable, Olá conjunto de toobe de necessidades de chave do registro a seguir em Olá VM.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>VMs Linux
O Backup do Azure fornece uma estrutura de script. consistência do aplicativo tooensure ao fazer backup de máquinas virtuais Linux, criar personalizados scripts de pré e pós-que controlam o fluxo de trabalho de backup hello e ambiente. O Backup do Azure invoca pré-script Olá antes de tirar instantâneo VM hello e invoca pós-script Olá, após a conclusão do trabalho de instantâneo VM hello. Para obter mais detalhes, consulte [Backup de VM Linux consistente com o aplicativo usando pré-script e pós-script](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> O Backup do Azure apenas invoca Olá gravados pelo cliente pré e pós-scripts. Se o pré-script de Olá e pós-scripts executar com êxito, o Backup do Azure marca Olá ponto de recuperação como aplicativo consistente. No entanto, o cliente Olá é basicamente responsável pelos consistência do aplicativo hello ao usar scripts personalizados.
>


Esta tabela explica os tipos de saudação de consistência e hello condições que ocorrem em durante o backup de VM do Azure e os procedimentos de restauração.

| Consistência | Baseado em VSS | Explicação e detalhes |
| --- | --- | --- |
| Consistência de aplicativo |Sim para Windows|A consistência do aplicativo é ideal para cargas de trabalho, pois garante que:<ol><li> Olá VM *é inicializado*. <li>Não há *corrupção*. <li>*Não há perda de dados*.<li> dados saudação são aplicativo toohello consistente que usa dados hello, envolvendo o aplicativo hello no tempo de saudação do backup – usando o script VSS ou pré/pós.</ol> <li>*Máquinas virtuais do Windows*-cargas de trabalho Microsoft mais tem gravadores VSS que realizam ações específicas da carga de trabalho relacionados toodata consistência. Por exemplo, Microsoft SQL Server tem um gravador VSS que garante que o arquivo de log de transações do hello gravações toohello e banco de dados de saudação são feitas corretamente. Para backups de VM do Windows Azure, toocreate um ponto de recuperação consistentes com aplicativos, extensão de backup Olá deve invocar o fluxo de trabalho do hello VSS e concluí-la antes de tirar instantâneo VM hello. Para hello Azure VM instantâneo toobe precisa, gravadores VSS de saudação de todos os aplicativos de máquina virtual do Azure devem concluir também. (Aprenda Olá [Noções básicas do VSS](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) e aprofundar nos detalhes de saudação do [como ele funciona](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Máquinas virtuais de Linux*-os clientes podem executar [consistência do aplicativo personalizado tooensure script de pré e pós-](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Consistência do sistema de arquivos |Sim - para computadores baseados em Windows |Há dois cenários em que o ponto de recuperação Olá pode ser *no sistema de arquivos consistente*:<ul><li>Backups de VMs Linux no Azure, sem pré-script/pós-script ou se o pré-script/pós-script falhou. <li>Falha do VSS durante o backup de VMs Windows no Azure.</li></ul> Em ambos os casos esses Olá melhor que pode ser feito é tooensure que: <ol><li> Olá VM *é inicializado*. <li>Não há *corrupção*.<li>*Não há perda de dados*.</ol> Aplicativos precisam tooimplement seu próprios "corrigir o" mecanismo em dados Olá restaurado. |
| Consistência de falhas |Não |Essa situação é máquina virtual de tooa equivalente com "Falha" (por meio de um software ou hardware Redefinir). Consistência de falha normalmente acontece quando Olá máquina virtual do Azure está desligado no momento de saudação do backup. Um ponto de recuperação consistente não fornece nenhuma garantia de consistência de saudação dos dados de saudação na mídia de armazenamento hello – da perspectiva de saudação do sistema operacional de saudação ou aplicativo hello. Somente os dados Olá que já existe no disco Olá no momento de saudação do backup são capturados e backup. <br/> <br/> Embora não haja nenhuma garantia, geralmente, Olá a inicialização do sistema operacional, seguida de verificação de disco procedimento, como chkdsk, toofix quaisquer erros de corrupção. Todos os dados na memória ou gravações não foram transferidos toohello disco serão perdidas. aplicativo Hello geralmente segue com seu próprio mecanismo de verificação, no caso de reversão de dados precisa toobe feito. <br><br>Por exemplo, se o log de transações Olá tem entradas que não estão presentes no banco de dados hello, em seguida, software de banco de dados de saudação faz uma reversão até que dados saudação são consistentes. Quando dados são distribuídos entre vários discos virtuais (como volumes estendidos), um ponto de recuperação consistente não fornece nenhuma garantia de correção de saudação de dados de saudação. |

## <a name="performance-and-resource-utilization"></a>Desempenho e utilização de recursos
Assim como o software de backup que é implantado localmente, você deve se planejar em termos das necessidades de utilização de recursos e capacidade ao fazer o backup de VMs no Azure. Olá [limites de armazenamento do Azure](../azure-subscription-service-limits.md#storage-limits) definir como toostructure VM implantações tooget máximo desempenho com mínimo impacto toorunning cargas de trabalho.

Preste atenção toohello que limita o armazenamento do Azure a seguir ao planejar o desempenho de backup:

* Egresso máximo por conta de armazenamento
* Taxa de solicitação total por conta de armazenamento

### <a name="storage-account-limits"></a>Limites da conta de armazenamento
Dados de backup copiados de uma conta de armazenamento, adiciona toohello operações de entrada/saída por segundo (IOPS) e métricas de saída (ou a taxa de transferência) Olá da conta de armazenamento. AT Olá mesmo tempo máquinas virtuais também estão consumindo IOPS e taxa de transferência. meta de saudação é tooensure Backup e tráfego de máquina virtual não excedam os limites da conta de armazenamento.

### <a name="number-of-disks"></a>Número de discos
o processo de backup Olá tenta toocomplete um trabalho de backup mais rápido possível. Dessa forma, ele consome o mínimo de recursos possível. No entanto, todas as operações de e/s são limitadas por Olá *meta de produtividade para Blob único*, que tem um limite de 60 MB por segundo. Em uma tentativa de toomaximize sua velocidade, o processo de backup Olá tenta tooback a cada um dos discos da VM Olá *em paralelo*. Se uma VM tiver quatro discos, o serviço de saudação tenta tooback backup de todos os quatro discos em paralelo. Olá **número de discos** está sendo feito, é o fator mais importante Olá para determinar o tráfego de backup de conta de armazenamento.

### <a name="backup-schedule"></a>Agendamento de backup
Um fator adicional que afeta o desempenho é hello **agendamento de backup**. Se você configurar políticas de saudação para todas as máquinas virtuais são feitas no hello mesmo tempo, você tiver agendado uma retenção de tráfego. o processo de backup Olá tentativas tooback backup de todos os discos em paralelo. tooreduce Olá tráfego de backup de uma conta de armazenamento, faça backup diferentes VMs em um horário diferente do hello, sem sobreposição.

## <a name="capacity-planning"></a>Planejamento da capacidade
Reunindo fatores anteriores Olá, é necessário tooplan Olá necessidades de uso de conta de armazenamento. Baixar Olá [planilha de planejamento de capacidade de backup VM](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) toosee impacto de saudação do disco e opções de agendamento de backup.

### <a name="backup-throughput"></a>Taxa de transferência de backup
Para cada disco que está sendo feito, Backup do Azure lê blocos Olá no disco hello e armazena apenas Olá dados alterados (backup incremental). Olá tabela a seguir mostra valores de taxa de transferência de serviço de Backup médios de saudação. Usando Olá dados a seguir, você pode estimar a quantidade de saudação de tempo necessário tooback backup de um disco de um determinado tamanho.

| Operação de backup | Melhor taxa de transferência possível |
| --- | --- |
| Backup inicial |160 Mbps |
| Backup incremental (DR) |640 Mbps  <br><br> Descartes de taxa de transferência significativamente se Olá alterado dados (que precisa toobe backup) é espalhada disco hello.|

## <a name="total-vm-backup-time"></a>Tempo total de backup da VM
Enquanto a maior parte do tempo de backup de saudação é gasto ler e copiar dados, outras operações contribuem toohello tooback de tempo total necessário a uma máquina virtual:

* Tempo necessário muito[instalar ou atualizar a extensão de backup Olá](backup-azure-vms.md).
* Hora do instantâneo, que é Olá tempo tootrigger um instantâneo. Os instantâneos são disparados toohello fechar agendado tempo de backup.
* Tempo de espera da fila. Desde que o serviço de Backup hello está processando os backups de vários clientes, copiando dados de backup do backup do instantâneo toohello ou serviços de recuperação cofre não seja iniciada imediatamente. Em períodos de pico de carga, espera Olá pode ampliar o tooeight horas devido toohello número de backups que estão sendo processados. No entanto, o tempo total de backup de VM Olá é menor que 24 horas para políticas de backup diárias.
* Tempo de transferência de dados, tempo necessário para backup toocompute Olá incremental alterações de backup anterior de serviço e transferir o armazenamento de toovault essas alterações.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>Por que eu estou observando tempos de backup mais longos (mais de 12 horas)?
Backup consiste em duas fases: criação de instantâneos e transferindo Olá instantâneos toohello cofre. otimiza o Hello serviço de Backup de armazenamento. Ao transferir Olá instantâneo dados tooa cofre, o serviço de Olá transfere apenas as alterações incrementais do instantâneo anterior hello.  alterações incrementais de saudação de toodetermine, o serviço Olá computa a soma de verificação de saudação de blocos de saudação. Se um bloco for alterado, bloco de saudação é identificado como um toobe bloco enviado toohello cofre. Detalhada do serviço de saudação adicional em cada um dos Olá identificados blocos, procurando oportunidades toominimize Olá dados tootransfer. Depois de avaliar todos os blocos alterados, o serviço de Olá mescla alterações hello e envia toohello cofre. Em alguns aplicativos herdados, gravações pequenas e fragmentadas não são ideais para armazenamento. Se o instantâneo Olá contém muitas gravações pequenas, fragmentadas, serviço Olá gasta mais tempo de processamento de dados Olá gravados por aplicativos de saudação. Olá recomendado gravar bloco de aplicativo do Azure, para aplicativos em execução dentro de saudação VM, é um mínimo de 8 KB. Se o aplicativo usar um bloco inferior a 8 KB, o desempenho do backup será afetado. Para obter ajuda com o ajuste de desempenho do backup tooimprove seu aplicativo, consulte [ajuste de aplicativos para o desempenho ideal com o armazenamento do Azure](../storage/common/storage-premium-storage-performance.md). Embora o artigo Olá no desempenho de backup usa exemplos de armazenamento Premium, diretrizes de saudação são aplicável para discos de armazenamento padrão.

## <a name="total-restore-time"></a>Tempo total de restauração
Uma operação de restauração consiste em duas tarefas principais sub: copiar dados da conta de armazenamento do cliente do hello cofre toohello escolhido e criação de máquina virtual de saudação. Copiando dados do cofre Olá depende de onde os backups de saudação são armazenados internamente no Azure, e onde a conta de armazenamento do cliente hello está armazenada. Tempo gasto toocopy dados depende de:
* Fila esperas - como processos de serviço Olá trabalhos de restauração de vários clientes da saudação mesmo tempo, a solicitações de restauração são colocados em uma fila.
* Cópia de dados de tempo - dados são copiados da conta de armazenamento Olá cofre toohello cliente. Restaurar tempo depende de IOPS e taxa de transferência do serviço de Backup do Azure obtém na conta de armazenamento do cliente de saudação selecionada. tooreduce Olá copiando a hora durante o processo de restauração hello, selecione uma conta de armazenamento não foi carregada com outras leituras e gravações de aplicativo.

## <a name="best-practices"></a>Práticas recomendadas
É recomendável seguir essas práticas ao configurar backups de máquinas virtuais:

* Não agende mais de 10 VMs clássicas de Olá mesmo nuvem tooback de serviço para cima em Olá simultaneamente. Se você quiser tooback várias máquinas virtuais do mesmo serviço de nuvem, balancear os horários de início de saudação por uma hora.
* Não agende mais de 40 tooback de VMs para cima em Olá simultaneamente.
* Agende os backups de VM fora do horário de pico. Olá essa forma serviço de Backup usa o IOPS para transferir dados do cofre toohello de conta de armazenamento do hello cliente.
* Certifique-se de que uma política seja aplicada às VMs distribuídas entre diferentes contas de armazenamento. Sugerimos que não mais do que 20 discos total de uma única conta de armazenamento protegida pelo Olá mesmo agendamento de backup. Se você tiver mais de 20 discos em uma conta de armazenamento, distribuir as VMs em várias tooget de políticas Olá IOPS necessários durante a fase de transferência Olá Olá do processo de backup.
* Não restaure uma VM em execução na conta de armazenamento de toosame de armazenamento Premium. Se o processo de operação de restauração Olá coincide com a operação de backup hello, ele reduz Olá IOPS disponível para backup.
* Para backup de VM Premium, certifique-se de que a conta de armazenamento que hospeda os discos premium tem pelo menos 50% de espaço livre para preparar instantâneo de um backup bem-sucedido. 
* Verifique se essa versão do python em VMs do Linux habilitado para backup é 2.7

## <a name="data-encryption"></a>Criptografia de dados
O Backup do Azure não criptografa os dados como parte do processo de backup hello. No entanto, você pode criptografar os dados dentro de saudação VM e faça backup Olá dados protegidos diretamente (Leia mais sobre [backup de dados criptografados](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Calcular o custo de saudação de instâncias protegidas
Máquinas virtuais do Azure que são feitas por meio do Backup do Azure são sujeitas muito[preços do Azure Backup](https://azure.microsoft.com/pricing/details/backup/). Olá cálculo protegido instâncias baseia-se a saudação *real* tamanho da máquina virtual de saudação, que é a soma de saudação de todos os dados de saudação na máquina virtual de hello – excluindo hello "disco de recurso".

Os preços para fazer backup de máquinas virtuais é *não* com base no tamanho de saudação máximo com suporte para cada máquina virtual do disco anexado toohello de dados. Preços baseia-se em dados reais de saudação armazenados no disco de dados hello. Da mesma forma, conta de armazenamento de backup Olá baseia-se na quantidade de saudação de dados que são armazenados no Backup do Azure, que é a soma de saudação dos dados reais de saudação em cada ponto de recuperação.

Por exemplo, considere uma máquina virtual de tamanho A2 Standard que tem dois discos de dados adicionais com um tamanho máximo de 1 TB cada. Olá tabela a seguir fornece os dados reais Olá armazenados em cada um desses discos:

| Tipo de disco | Tamanho máx. | Dados reais presentes |
| --- | --- | --- |
| Disco do sistema operacional |1023 GB |17 GB |
| Disco local/disco de recursos |135 GB |5 GB (não incluído no backup) |
| Disco de dados 1 |1023 GB |30 GB |
| Disco de dados 2 |1023 GB |0 GB |

Olá *real* tamanho da máquina virtual de saudação nesse caso é 17 GB + 30 GB + 0 GB = 47 GB. Esse tamanho de instância protegida (47 GB) se torna a base de saudação para cobrança mensal hello. Como Olá quantidade de dados na máquina virtual de saudação cresce, tamanho de instância protegida Olá usado adequadamente para alterações na cobrança.

Cobrança não inicia até que o backup bem-sucedido do primeiro Olá for concluída. Neste ponto, cobrança Olá para armazenamento e instâncias protegido começa. Cobrança continuará desde que haja *quaisquer dados armazenados em um cofre de backup* para a máquina virtual de saudação. Se você interromper a proteção na máquina virtual de hello, mas os dados de backup de máquina virtual existem em um cofre, a cobrança continuará.

Para uma máquina virtual especificada para apenas se Olá proteção foi parada de cobrança *e* todos os dados de backup é excluído. Quando a proteção for interrompido e não há nenhum trabalho de backup ativo, tamanho de saudação do último backup VM bem-sucedido Olá torna-se o tamanho de instância protegida Olá usado para cobrança mensal hello.

## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Próximas etapas
* [Backup de máquinas virtuais](backup-azure-vms.md)
* [Gerenciar o backup de máquinas virtuais](backup-azure-manage-vms.md)
* [Restaurar máquinas virtuais](backup-azure-restore-vms.md)
* [Solucionar problemas de backup da VM](backup-azure-vms-troubleshoot.md)
