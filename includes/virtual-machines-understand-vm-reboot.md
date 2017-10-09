Máquinas virtuais (VMs) do Azure às vezes pode reinicializar sem motivo aparente, sem evidência de seu tendo iniciou Olá operação de reinicialização. Este artigo lista os eventos que podem causar tooreboot VMs e fornecem informações sobre como tooavoid inesperado reinicializar problemas ou reduzir o impacto de saudação desses problemas e as ações de saudação.

## <a name="configure-hello-vms-for-high-availability"></a>Configurar VMs Olá para alta disponibilidade
saudação de melhor forma tooprotect um aplicativo que está em execução no Azure em relação a VM reinicia e tempo de inatividade é tooconfigure Olá máquinas virtuais para alta disponibilidade.

tooprovide este nível de aplicativo de tooyour de redundância, é recomendável agrupar duas ou mais VMs em um conjunto de disponibilidade. Essa configuração garante que, durante a um evento de manutenção planejada ou não planejada, pelo menos uma VM está disponível e atende 99,95 por cento de Olá [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Para obter mais informações sobre conjuntos de disponibilidade, consulte Olá artigos a seguir:

- [Gerenciar a disponibilidade de saudação de VMs](../articles/virtual-machines/windows/manage-availability.md)
- [Configurar a disponibilidade das VMs](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Informações do Resource Health 
Integridade de recursos do Azure é um serviço que expõe a integridade de saudação de recursos do Azure individuais e fornece orientação acionável para solução de problemas. Em um ambiente de nuvem em que não é possível toodirectly os servidores de acesso ou elementos de infraestrutura, o meta Olá da integridade de recurso é tooreduce Olá tempo gasto na solução de problemas. Em particular, o objetivo de saudação é tempo de saudação tooreduce gasto determinando se raiz de saudação do problema Olá está no aplicativo hello, ou em um evento de saudação plataforma Windows Azure. Para saber mais, confira [Compreender e usar o Resource Health](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Ações e eventos que podem causar Olá tooreboot VM

### <a name="planned-maintenance"></a>Manutenção planejada
Microsoft Azure executa periodicamente atualizações em segurança da infraestrutura de host Olá subjacente VMs, desempenho e confiabilidade de Olá Olá mundo tooimprove. Muitas dessas atualizações, incluindo atualizações com preservação de memória, são realizadas sem nenhum impacto sobre as VMs ou os serviços de nuvem.

No entanto, algumas atualizações requerem uma reinicialização. Nesses casos, o hello VMs são desligadas enquanto estamos patch infraestrutura hello e Olá VMs são reiniciadas.

toounderstand qual a manutenção planejada do Azure e como ele pode afetar a disponibilidade de saudação de suas VMs do Linux, consulte os artigos de saudação listados aqui. artigos de saudação fornecem informações detalhadas sobre o processo de manutenção planejada do Azure hello e como tooschedule planejado manutenção toofurther reduzem o impacto de saudação.

- [Manutenção planejada para VMs no Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Como tooschedule manutenção planejada em VMs do Azure](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Atualizações que preservam a memória   
Para essa classe de atualizações no Microsoft Azure, os usuários não têm impacto em suas VMs em execução. Muitas dessas atualizações são toocomponents ou serviços que podem ser atualizados sem interferir Olá instância em execução. Alguns são as atualizações de infraestrutura de plataforma no sistema operacional do host Olá que podem ser aplicadas sem a reinicialização do hello VMs.

Essas atualizações com preservação de memória são realizadas com a tecnologia que permite a migração ao vivo local. Quando ele está sendo atualizado, Olá VM é colocada em uma *pausado* estado. Esse estado preserva memória Olá na RAM enquanto Olá sistema operacional do host subjacente recebe patches e atualizações necessárias hello. Olá VM é reiniciada dentro de 30 segundos de em pausa. Depois de Olá que VM é reiniciada, seu relógio será sincronizado automaticamente.

Devido ao período de pequena pausa Olá, implantação de atualizações por meio desse mecanismo consideravelmente reduz o impacto de saudação em Olá VMs. No entanto, nem todas as atualizações podem ser implantadas dessa maneira. 

Atualizações de múltiplas instâncias (para VMs em um conjunto de disponibilidade) são aplicadas em um domínio de atualização por vez.

> [!NOTE]
> As máquinas Linux que têm versões antigas do kernel são afetadas por um pânico de kernel durante esse método de atualização. tooavoid esse problema, a atualização tookernel versão 3.10.0-327.10.1 ou posterior. Para saber mais, confira [Uma VM Linux do Azure em um kernel com base em 3.10 sofre pane após uma atualização de nó host](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Ações de reinicialização ou desligamento iniciado pelo usuário
 
Se você executar uma reinicialização do hello portal do Azure, PowerShell do Azure, interface de linha de comando ou redefinição de API, você encontrará evento Olá Olá [o Log de atividades do Azure](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Se você executar a ação de saudação do sistema operacional da VM hello, você pode encontrar o evento Olá nos logs de sistema hello.

Outros cenários que causam geralmente Olá VM tooreboot incluem várias ações de alteração de configuração. Normalmente, você verá uma mensagem de aviso que indica que a execução de uma determinada ação resultará em uma reinicialização do hello VM. Exemplos incluem quaisquer operações de redimensionamento da VM, alterando Olá senha de conta administrativa hello e a configuração de um endereço IP estático.

### <a name="azure-security-center-and-windows-update"></a>Central de Segurança do Azure e Windows Update
A Central de Segurança do Azure monitora diariamente VMs Windows e Linux para saber se faltam atualizações do sistema operacional. A Central de Segurança recupera uma lista de atualizações críticas e de segurança disponíveis no Windows Update ou no WSUS (Windows Server Update Services), dependendo de qual serviço está configurado em uma VM do Windows. Também verifica se há atualizações mais recentes de saudação para sistemas Linux. Se faltar uma atualização do sistema em sua VM, a Central de Segurança recomendará que você aplique as atualizações do sistema. aplicativo Hello dessas atualizações do sistema é controlado por meio de saudação Central de segurança no hello portal do Azure. Depois de aplicar algumas atualizações, pode ser necessário reiniciar algumas VMs. Para saber mais, confira [Aplicar atualizações do sistema na Central de Segurança do Azure](../articles/security-center/security-center-apply-system-updates.md).

Assim como os servidores locais, Azure não enviar atualizações do Windows Update tooWindows VMs do Azure, porque essas máquinas estão pretendido toobe gerenciada por seus usuários. No entanto, você está incentivados tooleave Olá Windows Update configuração automática habilitada. Instalação automática de atualizações do Windows Update também pode causar reinicializações toooccur após a aplicação de atualizações de saudação. Para saber mais, confira [Perguntas frequentes sobre o Windows Update](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Outras situações afetar a disponibilidade de saudação da VM
Há outros casos em que Azure ativamente pode suspender o uso de saudação de uma VM. Você receberá notificações por email antes que essa ação é realizada, assim você terá uma chance tooresolve Olá problemas subjacentes. Violações de segurança e expiração de saudação de métodos de pagamento são exemplos de problemas que afetam a disponibilidade da VM.

### <a name="host-server-faults"></a>Falhas do servidor host 
Olá VM é hospedado em um servidor físico que está em execução dentro de um datacenter do Azure. Olá servidor físico executa um agente chamado hello agente de Host em adição tooa alguns outros componentes do Azure. Quando esses componentes de software do Azure no servidor físico Olá param de responder, sistema de monitoramento de saudação dispara uma reinicialização Olá host tooattempt de recuperação do servidor. Olá VM é geralmente disponível novamente dentro de cinco minutos e continua toolive Olá mesmo host como anteriormente.

Falhas de servidor são geralmente causadas por falha de hardware, como falha de saudação de um disco rígido ou unidade de estado sólido. Azure continuamente monitora essas ocorrências, identifica bugs subjacente hello e distribui atualizações após a redução de saudação foi implementada e testada.

Como algumas falhas de servidor de host podem ser toothat específicas de servidor, uma situação de reinicialização VM repetida pode ser melhorada reimplantando manualmente o servidor de host de tooanother Olá VM. Essa operação pode ser acionada usando Olá **reimplantar** opção na página de detalhes de saudação do hello VM ou interrompendo e reiniciando Olá VM em Olá portal do Azure.

### <a name="auto-recovery"></a>Recuperação automática
Se o servidor de host de saudação não pode reinicializar por qualquer motivo, Olá plataforma Windows Azure inicia um servidor de host com defeito recuperação automática ação tootake Olá fora de rotação para obter mais informações. 

Todas as máquinas virtuais no host são automaticamente realocados tooa servidor de host diferente e íntegro. O processo é concluído normalmente em 15 minutos. toolearn mais sobre o processo de recuperação automática hello, consulte [recuperação automática de VMs](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Manutenção não planejada
Em raras ocasiões, Olá a equipe de operações do Azure pode precisar tooperform tooensure de atividades de manutenção Olá integridade geral dos Olá plataforma Windows Azure. Esse comportamento pode afetar a disponibilidade VM e geralmente resulta em Olá mesma ação de recuperação automática, conforme descrito anteriormente.  

Maintenances não planejados incluem o seguinte hello:

- Desfragmentação de nó urgente
- Atualizações de comutador de rede urgentes

### <a name="vm-crashes"></a>Falhas de VM
Máquinas virtuais podem ser reiniciado devido a problemas na Olá própria máquina virtual. carga de trabalho de saudação ou função que está sendo executado no hello VM pode acionar uma verificação de bug no sistema de operacional convidado hello. Para ajudar a determinar o motivo Olá falha hello, exibir logs do sistema e o aplicativo hello para VMs do Windows e Olá logs seriais para VMs do Linux.

### <a name="storage-related-forced-shutdowns"></a>Desligamentos forçados relacionados ao armazenamento
Máquinas virtuais no Azure dependem de discos virtuais para o sistema operacional e o armazenamento de dados que está hospedado em Olá infraestrutura de armazenamento do Azure. Sempre que a disponibilidade de saudação ou conectividade entre hello VM e discos virtuais Olá associado é afetada por mais de 120 segundos, Olá plataforma Windows Azure executa um desligamento forçado do hello VMs tooavoid dados corrompidos. Olá VMs são ativadas automaticamente novamente depois que a conectividade de armazenamento foi restaurada. 

Olá durante desligamento Olá pode demorar mais de cinco minutos, mas pode ser significativamente maior. a seguir Olá é um dos casos específicos de saudação associado desligamentos forçados relacionados ao armazenamento: 

**Ultrapassando limites de E/S**

Máquinas virtuais podem temporariamente desligar quando solicitações de e/s são limitadas consistentemente porque o volume Olá de operações de e/s por segundo (IOPS) excede os limites de hello e/s de disco de saudação. (Armazenamento de disco padrão é limitado IOPS too500.) toomitigate esse problema, use a distribuição de disco ou espaço de armazenamento hello dentro Olá convidado VM, dependendo da carga de trabalho de saudação. Para obter detalhes, consulte [Configurando VMs do Azure para otimizar o desempenho de armazenamento](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Limites de IOPS maiores estão disponíveis por meio do armazenamento do Azure Premium com backup too80, IOPS, 000. Para obter mais informações, consulte [Armazenamento Premium de alto desempenho](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Outros incidentes
Em raras circunstâncias, um problema mais amplo pode afetar vários servidores em um data center do Azure. Se esse problema ocorrer, Olá, equipe do Azure envia email assinaturas toohello afetado de notificações. Você pode verificar Olá [painel de integridade do serviço Azure](https://azure.microsoft.com/status/) e Olá portal do Azure para status de saudação de interrupções em andamento e incidentes passados.
