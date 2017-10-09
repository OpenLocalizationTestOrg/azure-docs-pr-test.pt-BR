---
title: Perguntas frequentes sobre o Backup de aaaAzure | Microsoft Docs
description: "Respostas a perguntas toocommon sobre: recursos de Backup do Azure, incluindo serviços de recuperação cofres, o que pode fazer backup, como ele funciona, criptografia e limites. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup e recuperação de desastre; serviço de backup"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Perguntas sobre Olá serviço Backup do Azure
Este artigo possui respostas toocommon perguntas toohelp componentes de Backup do Azure Olá você compreender rapidamente. Em algumas das respostas hello, há artigos de toohello links com informações abrangentes. Você pode fazer perguntas sobre Backup do Azure clicando em **comentários** (toohello direito). Os comentários aparecem na parte inferior da saudação deste artigo. Uma conta de Livefyre é toocomment necessária. Você também pode postar perguntas sobre Olá serviço Backup do Azure no hello [Fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

tooquickly verificação Olá seções deste artigo, use toohello direita Olá links em **neste artigo**.


## <a name="recovery-services-vault"></a>Cofre dos serviços de recuperação

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Há nenhum limite no número de saudação de cofres que podem ser criadas em cada assinatura do Azure? <br/>
Sim. A partir de setembro de 2016, você pode criar 25 Serviços de Recuperação ou cofres de backup por assinatura. Você pode criar os serviços de recuperação de too25 cofres, por região com suporte de Backup do Azure por assinatura. Se você precisar de cofres adicionais, crie outra assinatura.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Há limites no número de saudação de servidores/máquinas que podem ser registrados em relação a cada cofre? <br/>
Sim, você pode registrar as máquinas too50 por cofre. Para máquinas virtuais do Azure IaaS, Olá limite é de 200 máquinas virtuais por cofre. Se você precisar de mais máquinas tooregister, crie outro cofre.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Se a minha organização tiver um cofre, como posso isolar dados de um servidor de outro servidor ao restaurar os dados?<br/>
Todos os servidores que estão registrado toohello mesmo cofre poderão recuperar Olá dados submetidos a backup por outros servidores *Olá que usam a mesma senha*. Se você tiver servidores dados cujos backup você deseja tooisolate de outros servidores na sua organização, use uma senha designada para esses servidores. Por exemplo, os servidores de recursos humanos podem usar uma senha de criptografia, os servidores de contabilidade podem usar outra senha e os outros servidores de armazenamento podem usar uma terceira senha.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Posso "migrar" meus dados de backup ou cofre entre assinaturas? <br/>
Não. cofre Olá é criado em um nível de assinatura e não pode ser reatribuída tooanother assinatura quando ela é criada.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Os cofres dos Serviços de Recuperação se baseiam no Resource Manager. Os cofres de Backup (modo clássico) ainda têm suporte? <br/>
Todos os cofres de Backup existentes no hello [portal clássico](https://manage.windowsazure.com) continuar toobe com suporte. No entanto, você não pode usar cofres de Backup novo Olá toodeploy portal clássico. Microsoft recomenda usar cofres dos serviços de recuperação para todas as implantações porque aperfeiçoamentos futuros aplicam tooRecovery cofres de serviços, apenas. Se você tentar toocreate um cofre de Backup no portal clássico do hello, você será redirecionado toohello [portal do Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Posso migrar um cofre de serviços de recuperação de tooa de Cofre de Backup? <br/>
Infelizmente não, você não pode migrar conteúdo de saudação de um tooa de Cofre de Backup que Cofre de serviços de recuperação. Estamos trabalhando na adição dessa funcionalidade, mas ela não está disponível atualmente.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Fiz backup de minhas VMs clássicas em um cofre de Backup. É possível migrar Minhas VMs de modo do Gerenciador de tooResource de modo clássico e protegê-los em um cofre de serviços de recuperação?
Pontos de recuperação clássicos VM em um cofre de backup não migrar automaticamente tooa Cofre de serviços de recuperação quando você move Olá VM de tooResource clássico modo do Gerenciador. Siga estas etapas tootransfer seus backups VM:

1. No cofre de Backup hello, acesse toohello **itens protegidos** guia e selecione Olá VM. Clique em [Parar Proteção](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deixe a opção *Excluir dados de backup associados***desmarcada**.
2. Exclua a extensão de backup/instantâneo de saudação da saudação VM.
3. Migre máquina virtual de saudação do modo do Gerenciador de tooResource de modo clássico. Certifique-se de informações de rede e armazenamento de saudação máquina de virtual toohello correspondente também é migrado tooResource Manager modo.
4. Criar um cofre de serviços de recuperação e configurar backup em Olá migrados máquina virtual usando **Backup** ação na parte superior do painel do cofre. Para obter informações detalhadas sobre como fazer backup dos serviços de recuperação de tooa VM cofre, consulte o artigo hello, [proteger máquinas virtuais do Azure com um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Agente de Backup do Azure
Há uma lista detalhada de perguntas nas [Perguntas Frequentes sobre o backup da pasta de arquivos do Azure](backup-azure-file-folder-backup-faq.md)

## <a name="azure-vm-backup"></a>Backup da VM do Azure
Há uma lista detalhada de perguntas nas [Perguntas Frequentes sobre o backup da VM do Azure](backup-azure-vm-backup-faq.md)

## <a name="back-up-vmware-servers"></a>Fazer backup dos servidores VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>Posso fazer backup de tooAzure de servidores do VMware vCenter?

Sim. Você pode usar o Azure Backup Server tooback o VMware vCenter e ESXi tooAzure. Para obter informações sobre Olá suporte VMware versão, consulte o artigo Olá [matriz de proteção do Azure Backup Server](backup-mabs-protection-matrix.md). Para obter instruções passo a passo, consulte [tooback do servidor de Backup do Azure Use um servidor VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Servidor de Backup do Azure e System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Posso usar o servidor de Backup do Azure toocreate um backup Bare Metal BMR (recuperação) para um servidor físico? <br/>
Sim.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>Posso registrar meu cofres de toomultiple do servidor DPM? <br/>
Não. Um servidor DPM ou MABS pode ser registrado tooonly um cofre.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Há suporte para qual versão do System Center Data Protection Manager? <br/>
Recomendamos que você instale Olá [mais recente](http://aka.ms/azurebackup_agent) Azure Backup agent no rollup de atualização mais recente do hello (UR) para o System Center Data Protection Manager (DPM). A partir de agosto de 2016, 11 de Rollup de atualização é mais recente atualização do hello.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Instalei Azure Backup agent tooprotect Meus arquivos e pastas. Agora posso instalar o System Center DPM toowork com o Azure Backup agent tooprotect local cargas de trabalho de aplicativo VM tooAzure? <br/>
toouse Backup do Azure com System Center Data Protection Manager (DPM), instale o DPM primeiro e, em seguida, instale o agente de Backup do Azure. Instalação dos componentes de Backup do Azure Olá nesta ordem garante o agente de Backup do Azure Olá funciona com o DPM. Instalando agente de Backup do Azure Olá antes de instalar o DPM não é aconselhável ou suporte.


## <a name="how-azure-backup-works"></a>Como funciona o Backup do Azure
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Se eu cancelar um trabalho de backup depois de iniciada, é hello dados transferidos de backup excluídos? <br/>
Não. Todos os dados transferidos no cofre hello, antes do trabalho de backup Olá foi cancelado, permanece no cofre hello. Azure usa Backup toooccasionally de mecanismo um ponto de verificação adicionar dados de backup toohello pontos de verificação durante Olá backup. Porque há pontos de verificação nos dados de backup Olá, o processo de backup seguinte Olá pode validar a integridade de Olá dos arquivos de saudação. próximo trabalho de backup Hello serão toohello incremental feito anteriormente. Os backups incrementais transferem apenas dados novos ou alterados, que é igual a toobetter utilização de largura de banda.

Se você cancelar um trabalho de backup para uma VM do Azure, os dados transferidos serão ignorados. próximo trabalho de backup Olá transfere dados incrementais do último trabalho backup bem-sucedido hello.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Há algum limite de quando ou quantas vezes um backup pode ser agendado?<br/>
Sim. Você pode executar trabalhos de backup no Windows Server ou estações de trabalho do Windows se toothree vezes por dia. Você pode executar trabalhos de backup no System Center DPM backup tootwice por dia. Você pode executar um trabalho de backup para VMs IaaS uma vez por dia. Você pode usar o hello política de agendamento para toospecify de estação de trabalho do Windows ou Windows Server agendas diárias ou semanais. Usando o System Center DPM, especifique o agendamento diário, semanal, mensal e anual.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Por que é o tamanho Olá Olá dados transferidos toohello que Cofre de serviços de recuperação seja menor do que os dados de saudação feito?<br/>
 Todos os dados de saudação que são feitos o backup do Azure Backup Agent ou o SCDPM ou o servidor de Backup do Azure, são compactados e criptografados antes de serem transferidos. Depois que a criptografia e compactação de saudação é aplicado, dados Olá no cofre de backup Olá serão 30 a 40% menor.

## <a name="what-can-i-back-up"></a>Do que eu posso fazer backup
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Quais sistemas operacionais dão suporte ao Backup do Azure? <br/>
O Backup do Azure oferece suporte a saudação seguindo a lista de sistemas operacionais para o backup: arquivos e pastas e aplicativos de carga de trabalho protegidos usando o servidor de Backup do Azure e System Center Data Protection Manager (DPM).

| Sistema operacional | Plataforma | SKU |
|:--- | --- |:--- |
| Windows 8 e SPs mais recentes |64 bits |Enterprise, Pro |
| Windows 7 e SPs mais recentes |64 bits |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 e SPs mais recentes |64 bits |Enterprise, Pro |
| Windows 10 |64 bits |Enterprise, Pro, Home |
| Windows Server 2016 |64 bits |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 e SPs mais recentes |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 e SPs mais recentes |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 e SPs mais recentes |64 bits |Standard, Workgroup | 
| Windows Storage Server 2012 R2 e SPs mais recentes |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 e SPs mais recentes |64 bits |Standard, Workgroup |
| Windows Server 2012 R2 e SPs mais recentes |64 bits |Essential |
| Windows Server 2008 R2 SP1 |64 bits |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bits |Standard, Enterprise, Datacenter, Foundation |

**Para o backup de VM do Azure:**

* **Linux**: o Backup do Azure dá suporte a [uma lista de distribuições endossadas pelo Azure](../virtual-machines/linux/endorsed-distros.md) exceto o principal sistema operacional Linux.  Outros traga-seu-proprietário-distribuições do Linux também podem funcionar, contanto que o agente de VM hello está disponível na máquina virtual de saudação e suporte para Python existe.
* **Windows Server**: não há suporte para versões anteriores ao Windows Server 2008 R2.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Há um limite de tamanho de saudação de cada fonte de dados que está sendo feito? <br/>
Não há nenhum limite na quantidade de saudação de dados que você pode fazer backup tooa cofre. O Backup do Azure restringe o tamanho máximo de Olá Olá fonte de dados, no entanto, esses limites forem grandes. A partir de agosto de 2015, tamanho máximo de saudação para uma fonte de dados para sistemas operacionais de saudação com suporte é:

| S.Não | Sistema operacional | Tamanho máximo da fonte de dados |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 ou posterior |54.400 GB |
| 2 |Windows 8 ou superior |54.400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Olá, a tabela a seguir explica como cada tamanho de fonte de dados é determinado.

| Fonte de dados | Detalhes |
|:---:|:--- |
| Volume |quantidade de saudação de dados de backup do volume único de um computador cliente ou servidor |
| Máquina virtual do Hyper-V |Soma dos dados de todos os VHDs de saudação da máquina virtual de hello está sendo feito |
| Banco de dados do Microsoft SQL Server |O tamanho de um banco de dados SQL único do qual está sendo feito o backup |
| Microsoft SharePoint |Soma de saudação conteúdo e configuração de bancos de dados dentro de um farm do SharePoint que está sendo feito |
| Microsoft Exchange |Soma de todos os bancos de dados do Exchange em um servidor Exchange do qual está sendo feito o backup |
| Estado do Sistema/BMR |Cada cópia individual de BMR ou estado do sistema da máquina hello está sendo feito |

Para backup de VM do Azure, cada VM pode ter até too16 discos de dados com cada disco de dados sendo de tamanho de 1.023 GB ou menos. 

## <a name="retention-policy-and-recovery-points"></a>Política de retenção e pontos de recuperação
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Há uma diferença entre a política de retenção de saudação do DPM e o servidor/cliente do Windows (ou seja, no Windows Server sem o DPM)?<br/>
Não, o DPM e o Windows Server/cliente Windows têm políticas de retenção diárias, semanais, mensais e anuais.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Posso configurar minhas políticas de retenção de forma seletiva – ou seja, configurar semanal e diária, mas não anual e mensal?<br/>
Sim, Olá estrutura de retenção de Backup do Azure permite toohave total flexibilidade na definição de política de retenção de saudação de acordo com suas necessidades.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Posso “agendar um backup” às 18h e especificar “políticas de retenção” em um momento diferente?<br/>
Não. As políticas de retenção só podem ser aplicadas em pontos de backup. No Olá a imagem a seguir, a política de retenção de saudação é especificada para backups feitos em 12: 00 e 18: 00. <br/>

![Retenção e agendamento de Backup](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Se um backup é mantido por um longo tempo, é necessário toorecover de tempo mais um ponto de dados mais antigo? <br/>
Não – o tempo de saudação toorecover hello mais antigo ou Olá ponto mais recente é Olá mesmo. Cada ponto de recuperação se comporta como um ponto completo.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Se cada ponto de recuperação é como o ponto de dados completo, ele afeta a saudação total faturável de armazenamento de backup?<br/>
Os produtos típicos de ponto de retenção de longo prazo armazenam dados de backup como pontos completos. pontos completo Olá são um armazenamento *ineficiente* , mas são mais fáceis e mais rápido toorestore. Cópias incrementais são um armazenamento *eficiente* , mas exige que você toorestore uma cadeia de dados, o que afeta o tempo de recuperação. Azure Backup armazenamento arquitetura fornece Olá melhor dos dois mundos por armazenar dados para restauração rápida e incorrer em custos de armazenamento baixa ideal. Essa abordagem de armazenamento de dados garante que a largura de banda de entrada e saída seja usada com eficiência. Tanto a quantidade de saudação de tempo de armazenamento e hello dados toorecover Olá dados necessários, é mantido tooa mínimo. Saiba mais sobre como os [backups incrementais](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/) são eficientes.

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Há um limite no número de saudação de pontos de recuperação que podem ser criados?<br/>
Você pode criar pontos de recuperação too9999 por instância protegida. Uma instância protegida é um computador, servidor (físico ou virtual) ou carga de trabalho configurada tooback backup tooAzure de dados. Para obter mais informações, consulte explicações Olá [Backup e retenção](./backup-introduction-to-azure-backup.md#backup-and-retention), e [o que é uma instância protegida](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Como muitas recuperações pode executar nos dados Olá backup tooAzure?<br/>
Não há nenhum limite no número de saudação de recuperações de Backup do Azure.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Ao restaurar os dados, eu pago para tráfego de saída de saudação do Azure? <br/>
Não. A recuperação está livre e não será cobrado para tráfego de saída de hello.

## <a name="azure-backup-encryption"></a>Criptografia do Backup do Azure
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Olá dados enviados tooAzure criptografado? <br/>
Sim. Os dados são criptografados no computador de cliente/servidor/SCDPM local hello usando AES256 e dados de saudação são enviados por um link HTTPS seguro.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>É dados de backup Olá no Azure criptografado?<br/>
Sim. dados de saudação enviada tooAzure permanece criptografado (em repouso). Microsoft não descriptografa os dados de backup da saudação a qualquer momento. Ao fazer backup de uma VM do Azure, o Backup do Azure depende de criptografia da máquina virtual de saudação. Por exemplo, se sua VM é criptografada usando criptografia de disco do Azure, ou alguma outra tecnologia de criptografia, Backup do Azure usa esse toosecure criptografia seus dados.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>O que é o comprimento mínimo de saudação da chave de criptografia usado tooencrypt dados de backup? <br/>
chave de criptografia Olá deve ser pelo menos 16 caracteres, quando você estiver usando o agente de backup do Azure. Para VMs do Azure, não há nenhum toolength limite das chaves usadas pelo Azure KeyVault. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>O que acontece se eu enganos chave de criptografia de saudação? Posso recuperar dados de saudação (ou) pode Microsoft recuperar dados de saudação? <br/>
dados de backup tooencrypt usado chave Olá Olá estão presentes apenas em instalações de saudação do cliente. A Microsoft não mantém uma cópia no Azure e não tem nenhuma chave de acesso de toohello. Se o cliente Olá misplaces chave hello, Microsoft não é possível recuperar dados de backup hello.
