---
title: "aaaHow funciona Hyper-V replicação tooAzure na recuperação de Site? | Microsoft Docs"
description: "Este artigo fornece uma visão geral do funcionamento da replicação do Hyper-V no Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Como funciona o tooAzure de replicação do Hyper-V?

Leia esta arquitetura de saudação do artigo toounderstand e fluxos de trabalho para tooAzure de replicação do Hyper-V usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Lançar os comentários na parte inferior deste artigo ou de saudação do hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Você pode replicar Olá tooAzure a seguir:
- **Hyper-V com o VMM**: as máquinas virtuais em hosts do Hyper-V local gerenciadas nas nuvens do System Center Virtual MAchine Manager (VMM). Os hosts podem estar executando qualquer [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Replique VMs Hyper-V executando qualquer sistema operacional convidado [com suporte do Hyper-V e do Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).
- **Hyper-V sem o VMM**: VMs locais localizadas nos hosts Hyper-V que não são gerenciadas em nuvens do VMM. Hosts podem executar qualquer um dos Olá [sistemas operacionais com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Replique VMs Hyper-V executando qualquer sistema operacional convidado [com suporte do Hyper-V e do Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="architectural-components"></a>Componentes de arquitetura

**Área** | **Componente** | **Detalhes**
--- | --- | ---
**As tabelas** | No Azure, você precisa de uma conta do Microsoft Azure, uma conta de armazenamento do Azure e uma rede do Azure. | O armazenamento e a rede podem ser contas baseadas no Gerenciador de Recursos ou clássicas.<br/><br/> Dados replicados são armazenados na conta de armazenamento hello e VMs do Azure são criadas com dados replicado de saudação quando ocorrer failover do seu site local.<br/><br/> Olá VMs do Azure conectar toohello rede virtual do Azure quando eles são criados.
**Servidor VMM** | Hosts Hyper-V localizados em nuvens do VMM | Se os hosts Hyper-V são gerenciadas em nuvens do VMM, registre o servidor do VMM Olá no Olá que Cofre de serviços de recuperação.<br/><br/> No servidor do VMM Olá você instala a replicação de tooorchestrate de provedor de recuperação de Site Olá com o Azure.<br/><br/> Você precisa lógicas e redes VM Configurar mapeamento de rede tooconfigure. Uma rede VM deve ser vinculado tooa rede lógica associada com a nuvem de saudação.
**Host Hyper-V** | Os servidores Hyper-V podem ser implantados com ou sem o servidor do VMM. | Se não houver nenhum servidor do VMM, Olá provedor de recuperação de Site está instalado em replicação de tooorchestrate Olá host com a recuperação de Site sobre Olá da internet. Se houver um servidor do VMM, Olá provedor está instalado nele e não no host de saudação.<br/><br/> Agente de serviços de recuperação de saudação é instalado na replicação de dados de toohandle Olá host.<br/><br/> Comunicações de saudação provedor e agente de saudação são seguro e criptografado. Os dados replicados no armazenamento do Azure também são criptografados.
**VMs Hyper-V** | Você precisa de uma ou mais VMs no servidor de host do Hyper-V hello. | Não é necessário nada tooexplicitly instalado em máquinas virtuais

## <a name="deployment-steps"></a>Etapas de implantação.

1. **Azure**: configurar Olá componentes do Azure. Recomendamos que você configure as contas de armazenamento e rede antes de começar a implantação da Recuperação de Site.
2. **Cofre**: crie um cofre de Serviços de Recuperação para o Site Recovery e defina configurações de cofre, inclusive as configurações de origem e destino, configuração de uma política de replicação e habilitando a replicação.
3. **Origem e destino**:
    - **Hosts do Hyper-V nas nuvens do VMM**: como parte da especificação de configurações de fonte, você pode baixar e instalar Olá provedor Azure Site Recovery no servidor do VMM hello e agente de serviços de recuperação do Azure de saudação em cada host Hyper-V. origem de saudação será servidor do VMM hello. destino de saudação é o Azure.
    - Hosts do Hyper-V sem o VMM: quando você especificar configurações de fonte, você baixar e instalar hello provedor e agente em cada host Hyper-V. Durante a implantação reunir hosts Olá em um site do Hyper-V e especifique este site como fonte de saudação. destino de saudação é o Azure.

    ![Replicação do Hyper-V/VMM tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![tooAzure de replicação de site do Hyper-V](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Política de replicação**: criar uma política de replicação para o site Olá Hyper-V ou de nuvem do VMM. política de saudação é tooall aplicada VMs localizadas em hosts na nuvem ou site hello.
5. **Habilitar replicação**: habilite a replicação para máquinas virtuais do Hyper-V. A replicação inicial ocorre de acordo com as configurações de política de replicação hello. As alterações de dados são rastreadas e a replicação de tooAzure de alterações delta começa após a conclusão da replicação inicial de saudação. As alterações acompanhadas para um item são mantidas em um arquivo .hrl.
6. **Failover de teste**: executar um toomake de failover de teste se tudo está funcionando conforme o esperado.

Saiba mais sobre a implantação:
- [Introdução ao Hyper-V VM replicação tooAzure - com o VMM](site-recovery-vmm-to-azure.md)
- [Introdução ao Hyper-V VM replicação tooAzure - do VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Fluxo de trabalho de replicação do Hyper-V

### <a name="enable-protection"></a>Habilitar proteção

1. Depois de habilitar a proteção para uma VM Hyper-V, em Olá portal do Azure ou no local, Olá **Habilitar proteção** inicia.
2. Olá trabalho verifica máquina hello está em conformidade com os pré-requisitos, antes de chamar hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset a replicação com configurações de saudação configurado.
3. trabalho Olá inicia a replicação inicial invocando Olá [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) método tooinitialize uma replicação completa de VM e tooAzure de discos virtuais da VM de saudação do envio.
4. Você pode monitorar o trabalho Olá Olá **trabalhos** guia.      ![Lista de trabalhos](media/site-recovery-hyper-v-azure-architecture/image1.png) ![Habilitar busca detalhada da proteção](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>Replicação inicial

1. Um [Instantâneo da VM do Hyper-V](https://technet.microsoft.com/library/dd560637.aspx) é tirado quando a replicação inicial é disparada.
2. Discos rígidos virtuais são replicadas uma até que são todos os tooAzure copiado. Ele pode demorar um pouco, dependendo da saudação tamanho da VM e largura de banda de rede. toooptimize o uso da rede, consulte [como toomanage local tooAzure uso de largura de banda de rede de proteção](https://support.microsoft.com/kb/3056159).
3. Se ocorrerem alterações de disco enquanto a replicação inicial está em andamento, Olá rastreador de replicação de réplica do Hyper-V rastreia as alterações como Logs de replicação do Hyper-V (. hrl). Esses arquivos estão localizados em Olá mesma pasta que os discos de saudação. Cada disco tem um arquivo. hrl associado que será enviado toosecondary armazenamento.
4. arquivos de log e de instantâneo de saudação consumam recursos de disco enquanto a replicação inicial está em andamento.
5. Quando a replicação inicial Olá for concluído, o instantâneo de VM Olá é excluído. As alterações de disco delta no log de saudação são sincronizados e mesclada toohello pai disco.


### <a name="finalize-protection"></a>Finalizar proteção

1. Após a replicação inicial hello, hello **finalizar proteção na máquina virtual de saudação** trabalho configura rede e outras configurações depois da replicação, para que a máquina virtual hello está protegida.
    ![Finalizar trabalho de proteção](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Se você estiver replicando tooAzure, você pode precisar de configurações de Olá tootweak para a máquina virtual de saudação para que ele está pronto para failover. Neste ponto, você pode executar um toocheck de failover de teste que tudo está funcionando conforme o esperado.

### <a name="delta-replication"></a>Replicação delta

1. Após a replicação inicial hello, sincronização delta começa, de acordo com as configurações de replicação.
2. Olá rastreador de replicação de réplica do Hyper-V controla Olá alterações tooa do disco rígido virtual como arquivos. hrl. Cada disco configurado para a replicação tem um arquivo .hrl associado. Esse log é enviado a conta de armazenamento do cliente toohello após a conclusão da replicação inicial. Quando um log está em trânsito tooAzure, as alterações de saudação no disco principal Olá são rastreadas em outro arquivo de log, em Olá mesmo diretório.
3. Durante a replicação inicial e delta, você pode monitorar Olá VM em Olá exibição VM. [Saiba mais](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>Sincronização de replicação

1. Se a replicação delta falhar, e uma replicação completa for dispendiosa em termos de largura de banda ou tempo, a VM fica marcada para ressincronização. Por exemplo, se hello. hrl arquivos cheguem ao 50% do tamanho do disco hello, em seguida, hello VM será marcada para ressincronização.
2.  A ressincronização minimiza a quantidade de saudação dos dados enviados Calculando somas de verificação de máquinas de virtuais de origem e destino hello e enviar somente dados de delta hello. A ressincronização usa um algoritmo de agrupamento de bloco fixo em que os arquivos de origem e destino são divididos em partes fixas. Somas de verificação para cada bloco são geradas e, em seguida, em comparação com toodetermine que bloqueia o hello origem necessidade toobe toohello aplicada destino.
3. Após a conclusão da ressincronização, a replicação delta normal deverá ser retomada. Por padrão, a ressincronização é agendado toorun automaticamente fora do expediente, mas você pode ressincronizar uma máquina virtual manualmente. Por exemplo, se ocorrer uma interrupção da rede ou outra interrupção qualquer, você poderá retomar a ressincronização. toodo isso, selecione Olá VM no portal de hello > **ressincronizar**.

    ![Ressincronização manual](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Novas tentativas

Se um erro de replicação ocorrer, haverá uma repetição interna. Ela pode ser classificada em duas categorias:

**Categoria** | **Detalhes**
--- | ---
**Erros não recuperáveis** | Nenhuma nova tentativa é feita. O status da VM será **Crítico** e há necessidade de intervenção do administrador. Exemplos desses erros: dividido cadeia VHD; Estado inválido para a réplica Olá VM; Erros de autenticação de rede: erros de autorização. VM não encontrou erros (para servidores do Hyper-V autônomo)
**Erros recuperáveis** | Novas tentativas ocorrem a cada intervalo de replicação, usando uma retirada exponencial que aumenta o intervalo de repetição de saudação do início de saudação da primeira tentativa hello, 1, 2, 4, 8 e 10 minutos. Se o erro persistir, repita a operação a cada 30 minutos. Os exemplos incluem: erros da rede; erros de pouco espaço em disco; condições de memória insuficiente |

## <a name="protection-and-recovery-lifecycle"></a>Proteção e ciclo de vida de recuperação

![fluxo de trabalho](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Próximas etapas

- [Verificar pré-requisitos da implantação](site-recovery-prereq.md)
- Solucionar problemas com:
    - [Monitorar e solucionar problemas de proteção](site-recovery-monitoring-and-troubleshooting.md)
    - [Ajuda do suporte da Microsoft](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [Erros comuns e resoluções](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
