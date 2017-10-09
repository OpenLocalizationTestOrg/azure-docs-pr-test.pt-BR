---
title: "Replicar máquinas virtuais do Azure entre regiões do Azure para necessidades de recuperação de desastres: tooAzure do Azure | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooreplicate Azure VMs entre regiões do Azure (Azure para Azure) com o serviço do Azure Site Recovery Olá para necessidades de recuperação de desastres."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Você pode replicar VMs do Azure entre regiões usando o Site Recovery

>[!NOTE]
>
> A replicação do Azure Site Recovery para as máquinas virtuais (VMs) do Azure está atualmente na versão prévia.

Este artigo descreve como tooreplicate VMs do Azure entre regiões do Azure usando Olá [recuperação de Site](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Recuperação de desastre no Azure

Recursos internos de infraestrutura do Azure contribuem tooa estratégia de disponibilidade robusta e flexível para cargas de trabalho que são executados em máquinas virtuais do Azure. No entanto, há muitos motivos para você usar tooplan para recuperação de desastres entre regiões do Azure por conta própria:

- Você precisa toomeet diretrizes de conformidade para cargas de trabalho que exigem uma estratégia de recuperação (BCDR) de desastres e continuidade dos negócios e aplicativos específicos.
- Você deseja Olá capacidade tooprotect e recupere máquinas virtuais do Azure com base em suas decisões de negócios e não apenas com base na funcionalidade do Azure embutida.
- É necessário tootest failover e recuperação de acordo com suas necessidades de negócios e de conformidade, sem afetar a produção.
- Você precisa toofail toohello região de recuperação em caso de saudação de um desastre e falha a região de origem original toohello back perfeitamente.

Usar o Site Recovery para a VM do Azure para o Azure replicação toohelp você fazer todas essas tarefas.


## <a name="why-use-site-recovery"></a>Por que usar a Recuperação de Site?      

Recuperação de site fornece uma maneira simples de tooreplicate VMs do Azure entre regiões:

- **Implantação automática**. Ao contrário de um modelo de replicação ativa, não é necessário para uma infraestrutura caro e complexo na região secundária hello. Quando você habilitar a replicação, recuperação de Site cria automaticamente recursos Olá necessários na região de destino hello, com base nas configurações de região de origem.
- **Controlar regiões**. Recuperação de Site, é possível replicar qualquer região tooany região dentro de um continente. Compare isso com o armazenamento com redundância geográfica com acesso de leitura, que replica de forma assíncrona entre apenas o padrão de [regiões emparelhadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions). Armazenamento com redundância geográfica com acesso de leitura fornece dados de toohello de acesso somente leitura na região de destino hello.
- **A replicação automatizada**. Recuperação de site fornece replicação contínua automatizada. Failover e failback podem ser disparados com um único clique.
- **RTO e RPO**. Recuperação de site aproveita hello Azure da infraestrutura de rede que conecta regiões tookeep RTO e RPO muito baixo.
- **Testando**. Você pode executar os exercícios de recuperação de desastres com failovers de teste sob demanda, conforme a necessidade, sem afetar a cargas de trabalho de produção ou de replicação contínua.
- **Planos de recuperação**. Você pode usar planos de recuperação tooorchestrate failover e failback de todo o aplicativo hello em execução em várias VMs. recurso de plano de recuperação de saudação tem integração avançada de primeira classe com runbooks de automação do Azure.


## <a name="deployment-summary"></a>Resumo da implantação

Aqui está um resumo do que você precisa tooset toodo a replicação de máquinas virtuais entre regiões do Azure:

1. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.
2. Habilite a replicação para Olá VMs do Azure.
3. Execute um toomake de failover de teste se tudo está funcionando conforme o esperado.

>[!IMPORTANT]
>
> Você pode verificar Olá [matriz de suporte para replicação de VM do Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Para obter informações sobre como tooconfigure Olá necessária conectividade de saída de rede para máquinas virtuais do Azure para replicação de recuperação de Site, consulte Olá [documento de diretrizes de rede](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Antes de começar

* Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de uma máquina virtual do Azure.
* Sua assinatura do Azure deve ser habilitado toocreate VMs no local de destino Olá que você deseja toouse como a região de recuperação de desastres de saudação. Contate o suporte tooenable Olá cota necessária.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> É recomendável que você crie Olá Cofre de serviços de recuperação no local de saudação onde você deseja que seu tooreplicate VMs. Por exemplo, se o local de destino é hello central nos, criar hello cofre no **centro dos EUA**.

## <a name="enable-replication"></a>Habilitar a replicação

Em **os cofres de serviços de recuperação**, clique em nome do cofre hello. No cofre hello, clique em Olá **+ replicar** botão.

### <a name="step-1-configure-hello-source"></a>Etapa 1. Configurar fonte Olá
1. Em **fonte**, selecione **Azure - VISUALIZAÇÃO**.
2. Em **local de origem**, selecione origem Olá região do Azure em que suas VMs estão sendo executados.
3. Modelo de implantação de saudação Select das suas máquinas virtuais: **Gerenciador de recursos de** ou **clássico**.
4. Selecione Olá **grupo de recursos de origem** para máquinas virtuais do Gerenciador de recursos ou **serviço de nuvem** para VMs clássicas.

    ![Configurar fonte Olá](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Etapa 2. Selecionar máquinas virtuais

* Selecione Olá VMs você deseja tooreplicate e, em seguida, clique em **Okey**.

    ![Selecione as máquinas virtuais](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Etapa 3. Configurar definições

1. padrão de saudação toooverride configurações de destino e especifique as configurações de saudação de sua escolha, clique em **personalizar**. Para obter mais informações, consulte [Personalizar recursos de destino](site-recovery-replicate-azure-to-azure.md##customize-target-resources).

    ![Configurar definições](./media/site-recovery-azure-to-azure/settings.png)


2. Por padrão, a recuperação de Site cria uma política de replicação que usa instantâneos consistentes com o aplicativo a cada 4 horas e retém pontos de recuperação por 24 horas. toocreate uma política com configurações diferentes, clique em **personalizar** Avançar muito**política de replicação**.

    ![Personalizar política](./media/site-recovery-azure-to-azure/customize-policy.png)

3. provisionar recursos de destino de saudação toostart, clique em **criar recursos de destino**. O provisionamento demora alguns minutos. Não feche a folha de saudação durante o provisionamento ou precisar de toostart.

4. replicação de tootrigger de saudação selecionada de VM, clique em **habilitar replicação**.

5. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**.

6. Em **configurações** > **itens replicados**, você pode exibir o status de saudação de VMs e Olá andamento da replicação inicial. Clique em Olá VM toodrill abaixo em suas configurações.

## <a name="run-a-test-failover"></a>Execute um teste de failover

Depois de configurar tudo, execute um toomake de failover de teste se que tudo está funcionando conforme o esperado:

1. toofail em um único computador, em **configurações** > **itens duplicados**, clique em Olá VM **+ Failover de teste** ícone.

2. Planejar toofail sobre a recuperação, em **configurações** > **planos de recuperação**, plano de saudação do botão direito do mouse **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md). 

3. Em **Failover de teste**, selecione toowhich de rede virtual do Azure de destino Olá VMs do Azure conectadas após o failover de saudação.

4. toostart Olá failover, clique em **Okey**. tootrack de andamento, clique em Olá VM tooopen suas propriedades. Ou você pode clicar em Olá **Failover de teste** trabalho em nome do cofre hello > **configurações** > **trabalhos** > **ostrabalhosderecuperaçãodeSite**.

5. Depois de saudação failover for concluído, réplica Olá máquina do Azure aparece no portal do Azure de saudação > **máquinas virtuais**. Certifique-se de que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.

6. Olá toodelete VMs que foram criados durante a saudação failover de teste, clique em **failover de teste de limpeza** em Olá replicadas item ou hello plano de recuperação. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. 

[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.


## <a name="next-steps"></a>Próximas etapas

Depois de testar a implantação de saudação:

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- Saiba mais sobre [usando planos de recuperação](site-recovery-create-recovery-plans.md) tooreduce RTO.
