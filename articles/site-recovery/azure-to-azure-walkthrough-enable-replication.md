---
title: "a replicação para máquinas virtuais do Azure tooanother região do Azure com o Azure Site Recovery aaaEnable | Microsoft Docs"
description: "Resume as etapas de saudação precisar tooenable replicação tooanother região do Azure para máquinas virtuais do Azure, usando o serviço do Azure Site Recovery Olá"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Etapa 5: habilitar replicação para VMs do Azure


Depois de configurar um [Cofre de serviços de recuperação](azure-to-azure-walkthrough-vault.md), use a replicação de tooenable de artigo de máquinas virtuais (VMs) tooanother região do Azure, com [do Azure Site Recovery](site-recovery-overview.md). replicação tooenable, você definir as configurações de origem e de destino, verifique se a política de replicação hello e selecione VMs que você deseja tooreplicate.

- Quando você terminar de artigo hello, suas VMs do Azure deve estar replicando toohello região secundária do Azure.
- Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Atualmente, a replicação de VM do Azure está em versão prévia.


## <a name="select-hello-source"></a>Selecione a fonte de saudação 

1. Cofres de serviços de recuperação, clique em nome do cofre hello > **+ replicar**.
2. Em **fonte**, selecione **Azure - VISUALIZAÇÃO**.
2. Em **local de origem**, selecione origem Olá região do Azure em que suas VMs estão sendo executados.
3. Selecione Olá **modelo de implantação de máquina virtual do Azure** para VMs: **Gerenciador de recursos de** ou **clássico**.
4. Selecione Olá **grupo de recursos de origem** para VMs do Gerenciador de recursos, ou **serviço de nuvem** para VMs clássicas.
5. Clique em **Okey** toosave configurações de saudação.

    ![Configurar fonte Olá](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Selecione Olá VMs

Recuperação de site recupera uma lista de saudação que VMs associadas com assinatura hello e serviço de nuvem/grupo de recursos.

1. Em **máquinas virtuais**, selecione VMs Olá deseja tooreplicate.
2. Clique em **OK**.

    ![Selecione as máquinas virtuais](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Configurar definições

Recuperação de site fornece configurações padrão para a região de destino da saudação (com base nas configurações de região de origem de saudação) e a política de replicação hello:

   - **Local de destino**: região de destino Olá desejar toouse para recuperação de desastres. É recomendável que o local de destino Olá corresponde ao local de Olá do Cofre de recuperação de Site hello.
   - **Grupo de recursos de destino**: toowhich do grupo de recursos VMs do Azure na região de destino Olá pertencerão após o failover. Por padrão, a recuperação de Site cria um novo grupo de recursos na região de destino Olá com um sufixo "asr". 
   - **Rede virtual de destino**: rede Olá em qual VMs do Azure no hello região de destino serão localizado após o failover. Por padrão, a recuperação de Site cria uma nova rede virtual (e sub-redes) na região de destino Olá com um sufixo "asr". Esta rede é mapeada tooyour rede de origem. Observe que você pode atribuir um endereço IP específico após o failover de uma máquina virtual, se você precisar tooretain Olá mesmo endereço IP em locais de origem e destino hello. 
   - **Contas de armazenamento de cache**: recuperação de Site usa uma conta de armazenamento na região de origem de saudação. Alterações nas máquinas virtuais de origem são enviadas toothis conta, antes do local de destino do toohello de replicação. 
   - **Contas de armazenamento de destino**: por padrão, a recuperação de Site cria uma nova conta de armazenamento na região de destino hello, origem de saudação toomirror conta de armazenamento da VM.
   -  **Conjuntos de disponibilidade de destino**: por padrão, a recuperação de Site cria uma novo conjunto de disponibilidade no região de destino hello, com o sufixo de "asr" hello. 
   - **Nome da política de replicação**: nome da política.
   - **Retenção de ponto de recuperação**: por padrão, o Site Recovery mantém os pontos de recuperação por 24 horas. É possível configurar um valor entre 1 e 72 horas.
   - **Frequência de instantâneo consistente com o aplicativo**: por padrão, o Site Recovery obtém um instantâneo consistente com o aplicativo a cada 4 horas. É possível configurar qualquer valor entre 1 e 12 horas. Os dados são replicados continuamente:
    - Os pontos de recuperação consistentes com falha mantêm uma ordem de gravação de dados consistente quando criados. Esse tipo de ponto de recuperação é geralmente suficiente se seu aplicativo é projetado toorecover em caso de falha sem inconsistências de dados
    - Os pontos de recuperação consistentes com falha são gerados a cada poucos minutos. Usando essas toofail de pontos de recuperação sobre e recuperar suas VMs fornece um ponto de RPO (objetivo recuperação) na ordem de saudação de minutos.
    - Pontos de recuperação consistentes com o aplicativo (na consistência de ordem de toowrite adição) Verifique se os aplicativos em execução concluir todas as operações e liberar buffers toodisk (pausas de aplicativo). É recomendável utilizar esses pontos de recuperação para aplicativos de banco de dados, como SQL Server, Oracle e Exchange.
        
    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Modificar configurações

Se você quiser toomodify configurações de política de replicação e de destino, Olá a seguir:

1. tooview ou modificar as configurações de destino, clique em **configurações**.
2. configurações de destino do toooverride saudação padrão, clique em **personalizar**. É possível especificar um grupo de recursos de destino, uma rede virtual, um conjunto de disponibilidade e uma conta de armazenamento de destino. Você só pode adicionar conjuntos de disponibilidade se as VMs são parte de um conjunto na região de origem de saudação.

    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. configurações de replicação de toooverride para pontos de recuperação e instantâneos consistentes com o aplicativo, clique em **personalizar** Avançar muito**política de replicação**.
 
    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. provisionar recursos de destino de saudação toostart, clique em **criar recursos de destino**. O provisionamento demora alguns minutos. Não feche a folha de saudação durante o provisionamento, ou você terá toostart sobre.




## <a name="enable-replication"></a>Habilitar a replicação

1. Em **Configurações**, clique em **Habilitar replicação**. Isso permite que a replicação inicial da saudação VMs que você selecionou. Status de replicação inicial pode levar algum tempo toorefresh. Clique em **atualização** status mais recente do tooget hello.

2. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**.

3. Em **configurações** > **itens replicados**, você pode exibir o status de saudação de VMs e Olá andamento da replicação inicial. Clique em Olá VM toodrill abaixo em suas configurações.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 6: executar um failover de teste](azure-to-azure-walkthrough-test-failover.md)
