---
title: "arquitetura de saudação aaaReview para tooAzure de replicação (sem o System Center VMM) do Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada ao replicar tooAzure de VMs Hyper-V (sem VMM) local com o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: ec148e87ab2fa17485001ee447ad9f9bf795840e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooazure"></a>Etapa 1: Revisar arquitetura Olá para tooAzure de replicação do Hyper-V


Este artigo descreve os componentes de saudação e processos envolvidos ao replicar máquinas virtuais Hyper-V (que não são gerenciados pelo System Center VMM), local tooAzure usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Lançar os comentários na parte inferior deste artigo ou de saudação do hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componentes de arquitetura

Há vários componentes envolvidos ao replicar tooAzure de VMs Hyper-V sem o VMM.

**Componente** | **Localidade** | **Detalhes**
--- | --- | ---
**As tabelas** | No Azure, você precisa de uma conta do Microsoft Azure, uma conta de armazenamento do Azure e uma rede do Azure. | Dados replicados são armazenados na conta de armazenamento hello e VMs do Azure são criadas com dados replicado de saudação quando ocorrer failover do seu site local.<br/><br/> Olá VMs do Azure conectar toohello rede virtual do Azure quando eles são criados.
**Hyper-V** | Hosts e clusters Hyper-V são reunidos em sites do Hyper-V. Olá provedor Azure Site Recovery e serviços de recuperação é instalado em cada host Hyper-V. | Olá provedor coordena a replicação com o Site Recovery pela Olá internet. Agente de serviços de recuperação de saudação lida com a replicação de dados.<br/><br/> Comunicações de saudação provedor e agente de saudação são seguro e criptografado. Os dados replicados no armazenamento do Azure também são criptografados.
**VMs Hyper-V** | Você precisa de uma ou mais VMs em execução no servidor de host Hyper-V. | Não é necessário nada tooexplicitly instalado nas VMs.

Saiba mais sobre os pré-requisitos de implantação de saudação e requisitos para cada um desses componentes de saudação [matriz de suporte](site-recovery-support-matrix-to-azure.md).

**Figura 1: Replicação de tooAzure do site de Hyper-V**

![Componentes](./media/hyper-v-site-walkthrough-architecture/arch-onprem-azure-hypervsite.png)


## <a name="replication-process"></a>Processo de replicação

**Figura 2: Processo de replicação e a recuperação para tooAzure de replicação do Hyper-V**

![fluxo de trabalho](./media/hyper-v-site-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Habilitar proteção

1. Depois de habilitar a proteção para uma VM Hyper-V, em Olá portal do Azure ou no local, Olá **Habilitar proteção** inicia.
2. Olá trabalho verifica máquina hello está em conformidade com os pré-requisitos, antes de chamar hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset a replicação com configurações de saudação configurado.
3. trabalho Olá inicia a replicação inicial invocando Olá [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) método tooinitialize uma replicação completa de VM e tooAzure de discos virtuais da VM de saudação do envio.
4. Você pode monitorar o trabalho Olá Olá **trabalhos** guia.
 
### <a name="replicate-hello-initial-data"></a>Replicar dados de saudação inicial

1. Um [Instantâneo da VM do Hyper-V](https://technet.microsoft.com/library/dd560637.aspx) é tirado quando a replicação inicial é disparada.
2. Discos rígidos virtuais são replicadas uma até que são todos os tooAzure copiado. Ele pode demorar um pouco, dependendo da saudação tamanho da VM e largura de banda de rede. toooptimize o uso da rede, consulte [como toomanage local tooAzure uso de largura de banda de rede de proteção](https://support.microsoft.com/kb/3056159).
3. Se ocorrerem alterações de disco enquanto a replicação inicial está em andamento, Olá rastreador de replicação de réplica do Hyper-V rastreia as alterações como Logs de replicação do Hyper-V (. hrl). Esses arquivos estão localizados em Olá mesma pasta que os discos de saudação. Cada disco tem um arquivo. hrl associado que será enviado toosecondary armazenamento.
4. arquivos de log e de instantâneo de saudação consumam recursos de disco enquanto a replicação inicial está em andamento.
5. Quando a replicação inicial Olá for concluído, o instantâneo de VM Olá é excluído. As alterações de disco delta no log de saudação são sincronizados e mesclada toohello pai disco.


### <a name="finalize-protection"></a>Finalizar proteção

1. Após a replicação inicial hello, hello **finalizar proteção na máquina virtual de saudação** trabalho configura rede e outras configurações depois da replicação, para que a máquina virtual hello está protegida.
2. Se você estiver replicando tooAzure, você pode precisar de configurações de Olá tootweak para a máquina virtual de saudação para que ele está pronto para failover. Neste ponto, você pode executar um toocheck de failover de teste que tudo está funcionando conforme o esperado.

### <a name="replicate-hello-delta"></a>Replicação delta Olá

1. Após a replicação inicial hello, sincronização delta começa, de acordo com as configurações de replicação.
2. Olá rastreador de replicação de réplica do Hyper-V controla Olá alterações tooa do disco rígido virtual como arquivos. hrl. Cada disco configurado para a replicação tem um arquivo .hrl associado. Esse log é enviado a conta de armazenamento do cliente toohello após a conclusão da replicação inicial. Quando um log está em trânsito tooAzure, as alterações de saudação no disco principal Olá são rastreadas em outro arquivo de log, em Olá mesmo diretório.
3. Durante a replicação inicial e delta, você pode monitorar Olá VM em Olá exibição VM. [Saiba mais](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Sincronizar a replicação

1. Se a replicação delta falhar, e uma replicação completa for dispendiosa em termos de largura de banda ou tempo, a VM fica marcada para ressincronização. Por exemplo, se hello. hrl arquivos cheguem ao 50% do tamanho do disco hello, em seguida, hello VM será marcada para ressincronização.
2.  A ressincronização minimiza a quantidade de saudação dos dados enviados Calculando somas de verificação de máquinas de virtuais de origem e destino hello e enviar somente dados de delta hello. A ressincronização usa um algoritmo de agrupamento de bloco fixo em que os arquivos de origem e destino são divididos em partes fixas. Somas de verificação para cada bloco são geradas e, em seguida, em comparação com toodetermine que bloqueia o hello origem necessidade toobe toohello aplicada destino.
3. Após a conclusão da ressincronização, a replicação delta normal deverá ser retomada. Por padrão, a ressincronização é agendado toorun automaticamente fora do expediente, mas você pode ressincronizar uma máquina virtual manualmente. Por exemplo, se ocorrer uma interrupção da rede ou outra interrupção qualquer, você poderá retomar a ressincronização. toodo isso, selecione Olá VM no portal de hello > **ressincronizar**.

    ![Ressincronização manual](./media/hyper-v-site-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a>Lógica de repetição

Se um erro de replicação ocorrer, haverá uma repetição interna. Ela pode ser classificada em duas categorias:

**Categoria** | **Detalhes**
--- | ---
**Erros não recuperáveis** | Nenhuma nova tentativa é feita. O status da VM será **Crítico** e há necessidade de intervenção do administrador. Exemplos desses erros: dividido cadeia VHD; Estado inválido para a réplica Olá VM; Erros de autenticação de rede: erros de autorização. VM não encontrou erros (para servidores do Hyper-V autônomo)
**Erros recuperáveis** | Novas tentativas ocorrem a cada intervalo de replicação, usando uma retirada exponencial que aumenta o intervalo de repetição de saudação do início de saudação da primeira tentativa hello, 1, 2, 4, 8 e 10 minutos. Se o erro persistir, repita a operação a cada 30 minutos. Os exemplos incluem: erros da rede; erros de pouco espaço em disco; condições de memória insuficiente |



## <a name="failover-and-failback-process"></a>Processo de failover e failback

1. Você pode executar um planejado ou não planejado [failover](site-recovery-failover.md) de tooAzure de VMs Hyper-V local. Se você executar um failover planejado, máquinas virtuais de origem são encerrados tooensure sem perda de dados.
2. Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) tooorchestrate failover de várias máquinas.
4. Depois de executar failover hello, deve ser capaz de toosee Olá criado VMs de réplica no Azure. Você pode atribuir um toohello de endereço IP público VM se necessário.
5. Em seguida, confirmar Olá failover toostart acessando a carga de trabalho de saudação da réplica Olá VM do Azure.
6. Quando o site primário local estiver disponível novamente, você poderá executar o [failback](site-recovery-failback-from-azure-to-hyper-v.md). Disparar um failover planejado de um site primário toohello do Azure. Para um failover planejado, que você pode selecione toofailback toohello mesmo VM ou tooan um local alternativo e sincronizar alterações entre o Azure e no local, tooensure sem perda de dados. Quando as VMs são criadas no local, você confirmar failover de saudação.




## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 2: examinar os pré-requisitos de implantação de saudação](hyper-v-site-walkthrough-prerequisites.md)
