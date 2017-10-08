---
title: "aaaWhat é o Backup do Azure? | Microsoft Docs"
description: "Use tooback de Backup do Azure e restaurar dados e cargas de trabalho de máquinas virtuais do Azure, estações de trabalho do Windows, servidores do System Center DPM e servidores do Windows."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup e restauração; serviços de recuperação; soluções de backup"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Visão geral dos recursos de saudação do Backup do Azure
O Backup do Azure é hello Azure serviço você pode usar tooback (ou proteger) e restaurar dados de saudação nuvem da Microsoft. Ele substitui a solução de backup local ou externa existente por uma solução confiável, segura e econômica baseada em nuvem. O Backup do Azure oferece vários componentes que você baixar e implanta no computador apropriado do hello, servidor, ou na nuvem hello. componente de saudação ou agente, que você implantar depende o que você deseja tooprotect. Todos os componentes de Backup do Azure (não importa se você estiver protegendo dados locais ou na nuvem Olá) podem ser usado tooback o Cofre de serviços de recuperação de tooa de dados no Azure. Consulte Olá [tabela de componentes de Backup do Azure](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (posteriormente neste artigo) para obter informações sobre quais dados específicos do componente toouse tooprotect, aplicativos ou cargas de trabalho.

[Assista a uma visão geral em vídeo do Backup do Azure](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Por que usar o Backup do Azure?
Soluções tradicionais de backup evoluíram nuvem de saudação tootreat como um ponto de extremidade, ou o destino de armazenamento estático, semelhantes toodisks ou fita. Enquanto essa abordagem é simple, ele é limitado e não aproveita ao máximo de uma plataforma de nuvem subjacente, que converte tooan solução ineficiente caro. Outras soluções são caras porque você acabará pagar por tipo errado de saudação do armazenamento ou de armazenamento que não é necessário. Outras soluções geralmente são ineficientes porque eles não oferecem tipo hello ou a quantidade de armazenamento que você precisa ou tarefas administrativas exigem muito tempo. O Backup do Azure, por sua vez, oferece estes benefícios principais:

**Gerenciamento de armazenamento automático** - ambientes híbridos geralmente requerem armazenamento heterogêneo - alguns locais e algumas Olá nuvem. Com o Backup do Azure, não há nenhum custo para o uso de dispositivos de armazenamento local. O Backup do Azure aloca e gerencia automaticamente o armazenamento de backup, com um modelo de pagamento conforme o uso. Pagamento como você-uso significa que você só paga pelo armazenamento Olá consumidos. Para obter mais informações, consulte Olá [Azure preços artigo](https://azure.microsoft.com/pricing/details/backup).

**Dimensionamento ilimitado** - Backup do Azure usa Olá subjacente de energia e a escala ilimitada de saudação do Azure na nuvem toodeliver alta disponibilidade - com nenhuma manutenção ou sobrecarga de monitoramento. Você pode configurar informações de tooprovide alertas sobre eventos, mas tooworry sobre alta disponibilidade não é necessário para seus dados na nuvem hello.

**Várias opções de armazenamento** -um aspecto de alta disponibilidade é a replicação de armazenamento. O Backup do Azure oferece dois tipos de replicação: [armazenamento com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) e [armazenamento com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage). Escolha a opção de armazenamento de backup de saudação com base na necessidade de:

* Armazenamento localmente redundante (LRS) replica seus dados três vezes (ele cria três cópias de seus dados) em um datacenter emparelhado a saudação mesma região. O LRS é uma opção de baixo custo para proteger seus dados contra falhas de hardware local.

* Armazenamento com redundância geográfica (GRS) replica região secundária seus dados tooa (centenas de milhas fora do local principal de Olá Olá dos dados de origem). O GRS é mais caro do que o LRS, mas fornece um nível mais alto de durabilidade para seus dados, mesmo se houver uma interrupção regional.

**Transferência de dados ilimitado** - Backup do Azure não limitar a quantidade de saudação de entrada ou saídos você de transferência de dados. O Backup do Azure também não cobra por dados Olá que são transferidos. No entanto, se você usar Olá importação/exportação do Azure serviço tooimport grandes quantidades de dados, há um custo associado a dados de entrada. Para obter mais informações sobre esse custo, confira o [Fluxo de trabalho de backup offline no Backup do Azure](backup-azure-backup-import-export.md). Dados de saída refere-se toodata transferido de um cofre de serviços de recuperação durante uma operação de restauração.

**Criptografia de dados** -permite a criptografia de dados para transmissão segura e o armazenamento de seus dados na nuvem pública hello. Armazenar senha de criptografia Olá localmente, e nunca são transmitido ou armazenado no Azure. Se for necessário toorestore qualquer dos dados Olá, somente você tem a senha de criptografia ou chave.

**Backup consistente com o aplicativo** -se fazer backup de um servidor de arquivos, a máquina virtual ou o banco de dados SQL, você precisa de tooknow que um ponto de recuperação tem todos os necessários a cópia de backup dados toorestore Olá. O Backup do Azure fornece backups consistentes com aplicativos, o que garante correções adicionais não são necessários toorestore Olá dados. Restaurar dados consistentes do aplicativo reduz o tempo de restauração hello, permitindo que você tooquickly tooa retorno estado de execução.

**Retenção de longo prazo** -em vez de troca de cópias de backup de disco tootape e movendo Olá fita tooan local externo, você pode usar o Azure para retenção de curto e longo prazo. Azure não limita o comprimento de saudação de dados permanecem em um cofre de Backup ou recuperação de serviços de tempo. Você pode manter dados em um cofre para como desejar. O Backup do Azure tem um limite de pontos de recuperação 9999 por instância protegidos. Consulte Olá [Backup e retenção](backup-introduction-to-azure-backup.md#backup-and-retention) seção neste artigo para obter uma explicação de como esse limite pode impactar a suas necessidades de backup.  

## <a name="which-azure-backup-components-should-i-use"></a>Quais componentes do Backup do Azure devo usar?
Se você não tiver certeza de qual componente de Backup do Azure funciona para suas necessidades, consulte Olá para obter informações sobre o que você pode proteger com cada componente a tabela a seguir. Olá portal do Azure fornece um assistente, o que é criado no portal de hello, tooguide escolhendo Olá toodownload de componente e implantar. Assistente Hello, que faz parte da criação de Cofre de serviços de recuperação de hello, o guiará pelas etapas Olá para selecionar uma meta de backup e escolhendo tooprotect de dados ou aplicativo hello.

| Componente | Benefícios | limites | O que é protegido? | Onde os backups são armazenados? |
| --- | --- | --- | --- | --- |
| Agente de Backup do Azure (MARS) |<li>Fazer backup de arquivos e pastas no sistema operacional Windows físico ou virtual (as máquinas virtuais podem ser locais ou estar no Azure)<li>Nenhum servidor de backup separado necessário. |<li>Fazer backup 3 vezes por dia <li>Não reconhece aplicativos; arquivo, pasta e restauração em nível de volume somente, <li>  Não há suporte para Linux. |<li>Arquivos, <li>Pastas |Cofre dos Serviços de Recuperação |
| System Center DPM |<li>Instantâneos com reconhecimento de aplicativo (VSS)<li>Total flexibilidade para quando tootake backups<li>Granularidade da recuperação (tudo)<li>Pode usar cofre dos Serviços de Recuperação<li>Suporte para Linux no Hyper-V e VMs VMware <li>Backup e restauração das VMs VMware usando o DPM 2012 R2 |Não é possível fazer o backup da carga de trabalho do Oracle.|<li>Arquivos, <li>Pastas,<li> Volumes, <li>VMs,<li> Aplicativos,<li> Cargas de trabalho |<li>Cofre dos Serviços de Recuperação,<li> Disco conectado localmente,<li>  Fita (somente local) |
| Servidor de Backup do Azure |<li>Instantâneos com reconhecimento de aplicativo (VSS)<li>Total flexibilidade para quando tootake backups<li>Granularidade da recuperação (tudo)<li>Pode usar cofre dos Serviços de Recuperação<li>Suporte para Linux no Hyper-V e VMs VMware<li>Fazer backup e restaurar VMs VMware <li>Não exige uma licença do System Center |<li>Não é possível fazer o backup da carga de trabalho do Oracle.<li>Sempre requer assinatura do Azure ao vivo<li>Não há suporte para backup em fita |<li>Arquivos, <li>Pastas,<li> Volumes, <li>VMs,<li> Aplicativos,<li> Cargas de trabalho |<li>Cofre dos Serviços de Recuperação,<li> Disco conectado localmente |
| Backup de VM IaaS do Azure |<li>Backups nativos para Windows/Linux<li>Sem necessidade de instalação de agente específico<li>Backup em nível de malha sem a necessidade de uma infraestrutura de backup |<li>Fazer backup de máquinas virtuais uma vez por dia <li>Restaurar máquinas virtuais somente no nível do disco<li>Não pode fazer backup no local |<li>VMs, <li>Todos os discos (usando o PowerShell) |<p>Cofre dos Serviços de Recuperação</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Quais são os cenários de implantação Olá para cada componente?
| Componente | Pode ser implantado no Azure? | Pode ser implantado localmente? | Armazenamento de destino com suporte |
| --- | --- | --- | --- |
| Agente de Backup do Azure (MARS) |<p>**Sim**</p> <p>Agente de Backup do Azure Olá pode ser implantado em qualquer VM do Windows Server que é executado no Azure.</p> |<p>**Sim**</p> <p>Agente de Backup Olá pode ser implantado em qualquer máquina virtual do Windows Server ou o computador físico.</p> |<p>Cofre dos Serviços de Recuperação</p> |
| System Center DPM |<p>**Sim**</p><p>Saiba mais sobre [como tooprotect cargas de trabalho no Azure usando o System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Sim**</p> <p>Saiba mais sobre [como tooprotect cargas de trabalho e máquinas virtuais no seu datacenter](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Disco conectado localmente,</p> <p>Cofre dos Serviços de Recuperação,</p> <p>fita (somente local)</p> |
| Servidor de Backup do Azure |<p>**Sim**</p><p>Saiba mais sobre [como tooprotect cargas de trabalho no Azure usando o Azure Backup Server](backup-azure-microsoft-azure-backup.md).</p> |<p>**Sim**</p> <p>Saiba mais sobre [como tooprotect cargas de trabalho no Azure usando o Azure Backup Server](backup-azure-microsoft-azure-backup.md).</p> |<p>Disco conectado localmente,</p> <p>Cofre dos Serviços de Recuperação</p> |
| Backup de VM IaaS do Azure |<p>**Sim**</p><p>Parte da malha do Azure</p><p>Especializado para [backup de máquinas virtuais IaaS (infraestrutura do Azure como serviço)](backup-azure-vms-introduction.md).</p> |<p>**Não**</p> <p>Use o System Center DPM tooback backup de máquinas virtuais em seu data center.</p> |<p>Cofre dos Serviços de Recuperação</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Quais aplicativos e cargas de trabalho podem passar por backup?
Olá, a tabela a seguir fornece uma matriz de dados de saudação e cargas de trabalho que podem ser protegidas usando o Backup do Azure. a coluna de solução de Backup do Azure Olá tem documentação de implantação de toohello links para a solução. Cada componente do Backup do Azure pode ser implantado em um ambiente de modelo de implantação Clássico (implantação do Service Manager) ou do Gerenciador de Recursos.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Dados ou carga de trabalho | Ambiente de origem | Solução de Backup do Azure |
| --- | --- | --- |
| Arquivos e pastas |Windows Server |<p>[Agente do Backup do Azure](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| Arquivos e pastas |Computador com Windows |<p>[Agente do Backup do Azure](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| Máquina virtual do Hyper-V (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| Máquina virtual do Hyper-V (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de Backup do Azure Olá)</p> <p>[Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de Backup do Azure Olá)</p> |
| VMs IaaS do Azure (Windows) |em execução no Azure |[Backup do Azure (extensão VM)](backup-azure-vms-introduction.md) |
| VMs IaaS do Azure (Linux) |em execução no Azure |[Backup do Azure (extensão VM)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Suporte para Linux
Olá tabela a seguir mostra os componentes de Backup do Azure Olá têm suporte para Linux.  

| Componente | Suporte para Linux (endossado pelo Azure) |
| --- | --- |
| Agente de Backup do Azure (MARS) |Não (somente agente baseado no Windows) |
| System Center DPM |<li> Backup consistente de arquivos das VMs Convidadas Linux no Hyper-V e VMWare<br/> <li> Restauração da VM do Hyper-V e VMs Convidadas Linux do VMWare </br> </br>  *Backup consistente com o arquivo indisponível para a VM do Azure* <br/> |
| Servidor de Backup do Azure |<li>Backup consistente de arquivos das VMs Convidadas Linux no Hyper-V e VMWare<br/> <li> Restauração da VM do Hyper-V e VMs Convidadas Linux do VMWare </br></br> *Backup consistente com o arquivo indisponível para a VM do Azure*  |
| Backup de VM IaaS do Azure |Backup consistente de aplicativos usando uma [estrutura pré e pós-script](backup-azure-linux-app-consistent.md)<br/> [Recuperação granular de arquivos](backup-azure-restore-files-from-vm.md)<br/> [Restaurar todos os discos da VM](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [Restauração da VM](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Usando máquinas virtuais de Armazenamento Premium com o Backup do Azure
O Backup do Azure protege VMs de Armazenamento Premium. Armazenamento Premium do Azure é a unidade de estado sólido (SSD)-com base em cargas de trabalho do armazenamento projetado toosupport com alto e/S. O Armazenamento Premium é uma opção interessante para cargas de trabalho de máquina virtual (VM). Para obter mais informações sobre o armazenamento Premium, consulte o artigo Olá [armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquina Virtual do Azure](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Backup de VMs de Armazenamento Premium
Enquanto o backup de máquinas virtuais de armazenamento Premium, o serviço de Backup Olá cria um local de preparo temporário, denominada "AzureBackup-", na conta de armazenamento Premium Olá. tamanho de saudação do hello local de preparo é toohello igual tamanho do instantâneo de ponto de recuperação de saudação. Certifique-se de saudação conta de armazenamento Premium tem espaço livre suficiente tooaccommodate Olá temporário local de preparo. Para obter mais informações, consulte o artigo Olá [limitações de armazenamento premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Quando termina o trabalho de backup hello, Olá local de preparo é excluído. Olá preço de armazenamento usada para o local de preparo de saudação é consistente com todos os [preços de armazenamento Premium](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Não modifique nem editar Olá local de preparo.
>
>

### <a name="restore-premium-storage-vms"></a>Restaurar VMs de Armazenamento Premium
Máquinas virtuais de armazenamento Premium pode ser restaurado tooeither armazenamento Premium ou toonormal armazenamento. Restaurar tooPremium voltar uma máquina virtual de armazenamento Premium recuperação ponto de armazenamento é o processo típico de saudação da restauração. No entanto, pode ser econômico toorestore um armazenamento de toostandard de ponto de recuperação de VM de armazenamento Premium. Esse tipo de restauração pode ser usado se você precisar de um subconjunto de arquivos do hello VM.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Uso de VMs de disco gerenciado no Backup do Azure
O Backup do Azure protege VMs de disco gerenciado. Os discos gerenciados liberam você do gerenciamento de contas de armazenamento de máquinas virtuais e simplificam muito o provisionamento de VM.

### <a name="back-up-managed-disk-vms"></a>Fazer backup de VMs de disco gerenciado
O backup de VMs em discos gerenciados não é diferente de fazer backup de VMs do Resource Manager. Olá portal do Azure, você pode configurar o trabalho de backup Olá diretamente da saudação exibição de máquina Virtual ou de serviços de recuperação de saudação cofre exibição. Você pode fazer backup de VMs em discos gerenciados por meio de coleções de RestorePoint criadas com base em discos gerenciados. O Backup do Azure também oferece suporte ao backup de VMs de disco gerenciado criptografadas usando o ADE (Azure Disk Encryption).

### <a name="restore-managed-disk-vms"></a>Restaurar máquinas virtuais de disco gerenciado
O Backup do Azure permite que você toorestore uma VM completa com discos gerenciados ou restauração gerenciados conta de armazenamento tooa discos. O Azure gerencia discos Olá gerenciado durante o processo de restauração hello. Você (Olá cliente) gerencia conta de armazenamento de saudação criada como parte do processo de restauração de saudação. Quando a restauração gerenciado VMs criptografadas, hello chaves e segredos da VM devem existir na operação de restauração Olá Cofre de chaves toostarting anterior Olá.

## <a name="what-are-hello-features-of-each-backup-component"></a>Quais são os recursos de saudação de cada componente de Backup?
Olá seções a seguir fornece as tabelas que resumem disponibilidade hello ou o suporte de vários recursos em cada componente de Backup do Azure. Consulte informações Olá cada tabela para obter suporte adicional ou detalhes a seguir.

### <a name="storage"></a>Armazenamento
| Recurso | Agente de Backup do Azure | System Center DPM | Servidor de Backup do Azure | Backup de VM IaaS do Azure |
| --- | --- | --- | --- | --- |
| Cofre dos Serviços de Recuperação |![Sim][green] |![Sim][green] |![Sim][green] |![Sim][green] |
| Armazenamento em disco | |![Sim][green] |![Sim][green] | |
| Armazenamento em fita | |![Sim][green] | | |
| Compactação <br/>(no cofre dos Serviços de Recuperação) |![Sim][green] |![Sim][green] |![Sim][green] | |
| Backup incremental |![Sim][green] |![Sim][green] |![Sim][green] |![Sim][green] |
| Eliminação de duplicação de disco | |![Parcialmente][yellow] |![Parcialmente][yellow] | | |

![chave de tabela](./media/backup-introduction-to-azure-backup/table-key.png)

Olá Cofre de serviços de recuperação é o destino de armazenamento preferido de saudação em todos os componentes. System Center DPM e o servidor de Backup do Azure também fornecem Olá opção toohave uma cópia local do disco. No entanto, somente o System Center DPM fornece o dispositivo de armazenamento Olá opção toowrite dados tooa fita.

#### <a name="compression"></a>Compactação
Os backups são compactados tooreduce Olá necessária de espaço de armazenamento. único componente do Hello que não usam a compactação é a extensão VM de saudação. cópias de extensão VM Olá todos os dados de backup de sua conta de armazenamento toohello dos serviços de recuperação cofre em Olá mesma região. Nenhuma compactação é usada durante a transferência de dados de saudação. Transferência de dados de saudação sem compactação ligeiramente inflação do armazenamento Olá usado. No entanto, armazenar dados de saudação sem compactação permite a restauração mais rápida, se você precisar desse ponto de recuperação.


#### <a name="disk-deduplication"></a>Eliminação de duplicação de disco
Você poderá tirar proveito da eliminação de duplicação quando implantar o System Center DPM ou Servidor de Backup do Azure [em uma máquina virtual Hyper-V](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server executa a eliminação de duplicação de dados (em nível de host Olá) nos discos de rígidos virtuais (VHDs) que estão anexados toohello VM como armazenamento de backup.

> [!NOTE]
> A eliminação de duplicação não está disponível no Azure para nenhum dos componentes do Backup. Quando o System Center DPM e o servidor de Backup são implantados no Azure, os discos de armazenamento Olá anexado toohello que VM não pode ser com eliminação de duplicação.
>
>

### <a name="incremental-backup-explained"></a>Backup incremental explicado
Cada componente de Backup do Azure oferece suporte a backup incremental, independentemente do armazenamento de destino da saudação (disco, fita, o Cofre de serviços de recuperação). Backup incremental garante que os backups sejam armazenamento e tempo eficiente, transferindo somente as alterações feitas desde o último backup de saudação.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Comparando o backup Completo, Diferencial e Incremental

O consumo de armazenamento, o RTO (objetivo do tempo de recuperação) e o consumo de rede variam para cada tipo de método de backup. tookeep Olá backup custo total de propriedade (TCO) para baixo, você precisa toounderstand como solução de backup melhor toochoose hello. Olá a imagem a seguir compara o Backup completo, o Backup diferencial e o Backup Incremental. Na imagem hello, fonte de dados A é composta de armazenamento 10 bloqueia A1-A10, que é feito backup mensal. Blocos A2, A3, A4 e A9 alterar Olá primeiro mês e bloqueiam alterações A5 Olá próximo mês.

![imagem mostrando comparações entre os métodos de backup](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Com **Backup completo**, cada cópia de backup contém Olá toda fonte de dados. O backup completo consome uma grande quantidade de largura de banda e armazenamento de rede a cada vez que uma cópia de backup é transferida.

**Backup diferencial** armazena somente Olá blocos que foram alteradas desde Olá backup inicial completo, que resulta em uma quantidade menor de consumo de armazenamento e rede. Os backups diferenciais não mantém cópias redundantes dos dados inalterados. No entanto, como blocos de dados Olá permanecem inalterados entre os backups subsequentes são transferidos e armazenados, backups diferenciais são ineficientes. Na saudação segundo mês, os blocos alterados A2, A3, A4 e A9 são feitos backup. Em Olá terceiro mês, esses mesmos blocos de backup novamente, junto com os blocos alterados A5. Olá os blocos alterado continuar toobe realizado até o próximo backup completo de saudação acontece.

**Backup incremental** atinge a alta eficiência de armazenamento e rede armazenando somente blocos Olá dos dados alterados desde o backup anterior de saudação. Com o backup incremental, haja necessidade tootake backups regulares de completo. Exemplo hello, depois Olá backup completo é feito com hello primeiro mês, os blocos alterados A2, A3, A4 e A9 são marcados como alterado em transferidas para Olá segundo mês. No hello terceiro mês, apenas alterado bloco A5 está marcada e transferidos. A movimentação de menor quantidade de dados economiza recursos de armazenamento e de rede, o que reduz o TCO.   

### <a name="security"></a>Segurança
| Recurso | Agente de Backup do Azure | System Center DPM | Servidor de Backup do Azure | Backup de VM IaaS do Azure |
| --- | --- | --- | --- | --- |
| Segurança de rede<br/> (tooAzure) |![Sim][green] |![Sim][green] |![Sim][green] |![Parcialmente][yellow] |
| Segurança de dados<br/> (no Azure) |![Sim][green] |![Sim][green] |![Sim][green] |![Parcialmente][yellow] |

![chave de tabela](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Segurança de rede
Todo o tráfego de backup de seu toohello servidores que Cofre de serviços de recuperação é criptografado usando avançada 256 padrão de criptografia. dados de backup Olá são enviados por um link HTTPS seguro. dados de backup Olá também são armazenados no cofre de serviços de recuperação de saudação em formato criptografado. Somente você, Olá cliente do Azure, tenha Olá frase secreta toounlock esses dados. Microsoft não pode descriptografar dados de backup Olá a qualquer momento.

> [!WARNING]
> Depois de estabelecer o Cofre de serviços de recuperação Olá, somente você tenha de chave de criptografia de toohello de acesso. A Microsoft nunca mantém uma cópia de sua chave de criptografia e não tem acesso toohello chave. Se a chave de saudação é colocado incorretamente, Microsoft não é possível recuperar dados de backup hello.
>
>

#### <a name="data-security"></a>Segurança de dados
Fazendo backup de máquinas virtuais do Azure requer a configuração de criptografia *em* máquina virtual de saudação. Use o BitLocker em máquinas virtuais do Windows e **dm-crypt** em máquinas virtuais Linux. O Backup do Azure não criptografa automaticamente dados de backup provenientes desse caminho.

### <a name="network"></a>Rede
| Recurso | Agente de Backup do Azure | System Center DPM | Servidor de Backup do Azure | Backup de VM IaaS do Azure |
| --- | --- | --- | --- | --- |
| Compactação de rede <br/>(muito**server backup**) | |![Sim][green] |![Sim][green] | |
| Compactação de rede <br/>(muito**Cofre de serviços de recuperação**) |![Sim][green] |![Sim][green] |![Sim][green] | |
| Protocolo de rede <br/>(muito**server backup**) | |TCP |TCP | |
| Protocolo de rede <br/>(muito**Cofre de serviços de recuperação**) |HTTPS |HTTPS |HTTPS |HTTPS |

![chave de tabela](./media/backup-introduction-to-azure-backup/table-key-2.png)

Olá extensão da VM (em Olá IaaS VM) lê Olá dados diretamente de saudação conta de armazenamento do Azure pela rede de armazenamento Olá, portanto, não é necessário toocompress esse tráfego.

Se você usar um servidor do System Center DPM ou servidor de Backup do Azure como um servidor de backup secundário, compacte dados de saudação do servidor de backup Olá servidor primário toohello. A compactação de dados antes de fazer o backup tooDPM ou servidor de Backup do Azure, economiza largura de banda.

#### <a name="network-throttling"></a>Limitação de rede
Agente de Backup do Azure Olá oferece a limitação de rede, que permite a você toocontrol como largura de banda de rede é usada durante a transferência de dados. A limitação pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de internet. Transferência de limitação para dados aplica tooback backup e atividades de restauração.

## <a name="backup-and-retention"></a>Backup e retenção

O Backup do Azure tem um limite de 9999 pontos de recuperação, também conhecido como cópias de backup ou instantâneos, por *instância protegida*. Uma instância protegida é um computador, servidor (físico ou virtual) ou carga de trabalho configurada tooback backup tooAzure de dados. Para obter mais informações, consulte a seção hello, [o que é uma instância protegida](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Uma instância está protegida depois que uma cópia de backup de dados foi salva. cópia de backup de saudação de dados é a proteção de saudação. Se os dados de origem de saudação foram perdidos ou corrompido, cópia de backup Olá pode restaurar dados de origem de saudação. Olá tabela a seguir mostra frequência de backup máximo Olá para cada componente. A configuração de política de backup determina a rapidez de consumir pontos de recuperação de saudação. Por exemplo, se você criar um ponto de recuperação por dia, poderá depois retê-los por 27 anos antes de executá-los. Se você colocar um ponto de recuperação mensais, você pode manter os pontos de recuperação por 833 anos antes de expirar. saudação de serviço de Backup não define um limite de tempo de validade em um ponto de recuperação.

|  | Agente de Backup do Azure | System Center DPM | Servidor de Backup do Azure | Backup de VM IaaS do Azure |
| --- | --- | --- | --- | --- |
| Frequência de backup<br/> (serviços de tooRecovery cofre) |Três backups por dia |Dois backups por dia |Dois backups por dia |Um backup por dia |
| Frequência de backup<br/> (toodisk) |Não aplicável |<li>A cada 15 minutos para o SQL Server <li>A cada hora para outras cargas de trabalho |<li>A cada 15 minutos para o SQL Server <li>A cada hora para outras cargas de trabalho</p> |Não aplicável |
| Opções de retenção |Diária, semanal, mensal, anual |Diária, semanal, mensal, anual |Diária, semanal, mensal, anual |Diária, semanal, mensal, anual |
| Pontos de recuperação máximos por instância protegida |9999|9999|9999|9999|
| Período de retenção máximo |Depende da frequência de backup |Depende da frequência de backup |Depende da frequência de backup |Depende da frequência de backup |
| Pontos de recuperação no disco local |Não aplicável |<li>64 para Servidores de Arquivos,<li>448 para Servidores de Aplicativos |<li>64 para Servidores de Arquivos,<li>448 para Servidores de Aplicativos |Não aplicável |
| Pontos de recuperação em fita |Não aplicável |Ilimitado |Não aplicável |Não aplicável |

## <a name="what-is-a-protected-instance"></a>O que é uma instância protegida
Uma instância protegida é um computador com Windows tooa referência genérica, um servidor (físico ou virtual) ou banco de dados SQL que tenha sido configurado tooback backup tooAzure. Uma instância está protegida quando você configurar uma política de backup para o computador hello, servidor ou banco de dados e cria uma cópia de backup de dados de saudação. Subsequentes cópias dos dados de backup Olá para aquela instância protegida (que são chamados de pontos de recuperação), aumente a quantidade de saudação de armazenamento consumido. Você pode criar pontos de recuperação de too9999 para uma instância protegida. Se você excluir um ponto de recuperação de armazenamento, ele não contam para o total de ponto de recuperação 9999 Olá.
Alguns exemplos comuns de instâncias protegidas são máquinas virtuais, servidores de aplicativos, bancos de dados e computadores pessoais com o sistema de operacional do Windows hello. Por exemplo:

* Uma máquina virtual executando Olá malha de hipervisor Hyper-V ou IaaS do Azure. Olá sistemas de operacionais de convidados para a máquina virtual de saudação pode ser Windows Server ou Linux.
* Um servidor de aplicativos: servidor de aplicativos Olá pode ser um computador físico ou virtual executando o Windows Server e cargas de trabalho com dados que precisam toobe backup. Cargas de trabalho comuns são Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server e função de servidor de arquivos Olá no Windows Server. tooback essas cargas de trabalho, você precisará System Center Data Protection Manager (DPM) ou o servidor de Backup do Azure.
* Um computador pessoal, estação de trabalho ou laptop executando o sistema de operacional do Windows hello.


## <a name="what-is-a-recovery-services-vault"></a>O que é um cofre dos Serviços de Recuperação?
Um cofre de serviços de recuperação é que uma entidade de armazenamento online no Azure usada toohold dados como cópias de backup, os pontos de recuperação e as políticas de backup. Você pode usar os dados de backup de toohold de cofres de serviços de recuperação para estações de trabalho e servidores de serviços e locais do Azure. Os cofres de serviços de recuperação tornam fácil tooorganize os dados de backup, minimizando a sobrecarga de gerenciamento. Você pode criar quantos cofres dos Serviços de Recuperação desejar dentro de uma assinatura.

Cofres de backup, que são baseados no Gerenciador de serviço do Azure, foram a primeira versão saudação do cofre hello. Cofres dos serviços de recuperação, o que adicionam recursos de modelo do Azure Resource Manager hello, são a segunda versão saudação do cofre hello. Consulte Olá [artigo de visão geral do Cofre de serviços de recuperação](backup-azure-recovery-services-vault-overview.md) para obter uma descrição completa das diferenças de recurso hello. Você não pode mais criar use Olá portal toocreate cofres de Backup, mas ainda há suporte para os cofres de Backup.

> [!IMPORTANT]
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> **15 de outubro de 2017**, não será capaz de toouse PowerShell toocreate os cofres de Backup. <br/> **Em 1º de novembro de 2017**:
>- Nenhum Cofre de Backup restante será automaticamente atualizado tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Qual a diferença entre o Backup do Azure e o Azure Site Recovery?
O Backup do Azure e o Azure Site Recovery são relacionados, pois ambos são serviços de backup de dados e podem restaurar esses dados. No entanto, esses serviços têm finalidades diferentes para permitir a continuidade dos negócios e a recuperação de desastres no seu negócio. Use tooprotect Azure Backup e restaurar dados em um nível mais granular. Por exemplo, se uma apresentação em um laptop se tornou corrompida, você usaria apresentação de saudação do toorestore de Backup do Azure. Se você quisesse tooreplicate Olá dados de configuração e em uma máquina virtual em outro datacenter, use o Azure Site Recovery.

O Backup do Azure protege dados locais e na nuvem hello. O Azure Site Recovery coordena a replicação, o failover e o failback de servidores físicos e máquinas virtuais. Ambos os serviços são importantes, como sua solução de recuperação de desastres precisa tookeep seus dados seguros e recuperáveis (Backup) *e* manter suas cargas de trabalho disponíveis (recuperação de Site) quando ocorrem falhas.

Olá conceitos a seguir pode ajudá-lo a tomar decisões importantes em torno de backup e recuperação de desastres.

| Conceito | Detalhes | Backup | DR (Recuperação de desastre) |
| --- | --- | --- | --- |
| RPO (Objetivo de Ponto de Recuperação) |quantidade de saudação de perda de dados aceitável se precisar de uma recuperação toobe feito. |Há uma grande variação do RPO aceitável entre as soluções de backup. Os backups de máquina virtual geralmente têm um RPO de um dia, enquanto os backups de banco de dados têm RPOs de até 15 minutos. |Soluções de recuperação de desastre têm RPOs baixos. Olá DR cópia pode estar atrás por alguns segundos ou alguns minutos. |
| RTO (Objetivo de Tempo de Recuperação) |quantidade de saudação de tempo que demora toocomplete uma restauração ou recuperação. |Devido a saudação RPO maior, quantidade de saudação de dados que precisa de uma solução de backup tooprocess é geralmente muito maior, o que leva RTOs toolonger. Por exemplo, pode levar dias toorestore dados de fitas, dependendo da saudação tempo tootransport fita de saudação de um local externo. |Soluções de recuperação de desastres tem RTOs menores porque eles estão mais em sincronia com a origem de saudação. Menos alterações necessário toobe processado. |
| Retenção |Quanto tempo os dados precisam toobe armazenado |Para cenários que exigem recuperação operacional (dados corrompidos, exclusão acidental de arquivos, falhas no sistema operacional), os dados de backup normalmente são retidos por 30 dias ou menos.<br>Do ponto de vista de conformidade, os dados talvez precisem toobe armazenado por meses ou mesmo anos. Nesses casos, os dados de backup são ideais para arquivamento. |Recuperação de desastres precisa apenas dados de recuperação operacional, que geralmente leva apenas algumas horas ou tooa dia. Devido a captura de dados refinada Olá usada em soluções de recuperação de desastres, não é recomendável usar dados de recuperação de desastres para retenção de longo prazo. |

## <a name="next-steps"></a>Próximas etapas
Use um dos Olá seguintes tutoriais para instruções detalhadas passo a passo, para proteger dados no Windows Server, ou proteger uma máquina virtual (VM) no Azure:

* [Fazer backup de arquivos e pastas](backup-try-azure-backup-in-10-mins.md)
* [Fazer backup de máquinas virtuais do Azure](backup-azure-vms-first-look-arm.md)

Para obter detalhes sobre como proteger outras cargas de trabalho, experimente um dos seguintes artigos:

* [Fazer backup do seu servidor Windows](backup-configure-vault.md)
* [Fazer backup de cargas de trabalho do aplicativo](backup-azure-microsoft-azure-backup.md)
* [Backup de VM IaaS do Azure](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
