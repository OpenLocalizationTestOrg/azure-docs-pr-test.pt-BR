---
title: aplicativos de aaaReplicate (tooAzure do Azure) | Microsoft Docs
description: "Este artigo descreve como tooset a replicação virtual máquinas em execução em uma região do Azure muito outra região no Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Replicar máquinas virtuais do Azure tooanother região do Azure



>[!NOTE]
>
> Atualmente, a replicação do Site Recovery para máquinas virtuais do Azure está em versão prévia.

Este artigo descreve como tooset a replicação virtual máquinas em execução em uma região do Azure tooanother região do Azure.

## <a name="prerequisites"></a>Pré-requisitos

* artigo de saudação pressupõe que você já sabe sobre o Cofre de serviços de recuperação e recuperação de Site. É necessário toohave pré 'Cofre de serviços de recuperação' criado.

    >[!NOTE]
    >
    > É recomendável criar hello 'Cofre de serviços de recuperação' no local de saudação onde você deseja que seu tooreplicate VMs. Por exemplo, se o local de destino é ‘Centro dos EUA’, crie o cofre no ‘Centro dos EUA’.

* Se você estiver usando regras de grupos de segurança de rede (NSG) ou conectividade de internet do firewall proxy toocontrol acesso toooutbound em Olá VMs do Azure, certifique-se de que Olá de lista branca você exigido URLs ou IPs. Consulte também[documento Guia de rede](./site-recovery-azure-to-azure-networking-guidance.md) para obter mais detalhes.

* Se você tiver um ExpressRoute ou uma conexão VPN entre locais e hello local no Azure de origem, execute [considerações de recuperação de Site para o Azure tooon local ExpressRoute / configuração de VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.

* Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de uma máquina virtual do Azure.

* Sua assinatura do Azure deve ser habilitado toocreate VMs no local de destino Olá deseja toouse região a recuperação de desastres. Você pode contatar o suporte tooenable Olá necessário cota.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Habilite a replicação do cofre Azure Site Recovery
Nesta ilustração, podemos replicará as VMs em execução no toohello de local do Azure Olá 'Ásia Oriental' local ' Sudeste da Ásia '. etapas de saudação são da seguinte maneira:

 Clique em **+ replicar** em replicação de tooenable Olá cofre para máquinas virtuais de saudação.

1. **Fonte:** refere-se o ponto de toohello de origem de máquinas de saudação que nesse caso é **Azure**.

2. **Local de origem:** é Olá região do Azure de onde você deseja tooprotect suas máquinas virtuais. Para nesta ilustração, o local de origem Olá será 'Ásia Oriental'

3. **Modelo de implantação:** refere-se o modelo de implantação do Azure toohello das máquinas de origem hello. Você pode selecionar qualquer clássico ou Gerenciador de recursos e computadores que pertencem a modelo específico toohello serão listados para a proteção na próxima etapa do hello.

      >[!NOTE]
      >
      > É possível replicar apenas uma máquina virtual clássica e recuperá-la como uma máquina virtual clássica. Não é possível recuperá-la como uma máquina de virtual do Resource Manager.

4. **Grupo de recursos:** -lo da saudação recurso grupo toowhich suas máquinas virtuais de origem pertence. Olá todas as VMs no grupo de recursos selecionado hello serão listados para a proteção na próxima etapa do hello.

    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

Em **máquinas virtuais > Selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em OK.
    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


Na seção de Configurações, você pode configurar as propriedades do site de destino

1. **Local de destino:** Olá local onde sua fonte de dados de máquina virtual serão replicados. Dependendo de seu local de máquinas selecionadas, a recuperação de Site fornecerá que Olá lista de regiões de destino adequado.

    > [!TIP]
    > Recomenda-se o local de destino tookeep mesmo a partir de sua recuperação o Cofre de serviços.

2. **Grupo de recursos de destino:** é Olá recurso grupo toowhich todas as suas máquinas virtuais replicadas pertencerá. Por padrão a ASR criará um novo grupo de recursos na região de destino Olá com nome com o sufixo "asr". No caso de grupo de recursos criado pelo ASR já existir, ela será reutilizada. Você também pode escolher toocustomize-lo, conforme mostrado na seção de saudação abaixo.    
3. **Rede Virtual de destino:** por padrão, ASR criará uma nova rede virtual na região de destino Olá com nome com o sufixo "asr". Isso será mapeada tooyour rede de origem e será usado para qualquer proteção futuras.

    > [!NOTE]
    > [Verifique os detalhes de rede](site-recovery-network-mapping-azure-to-azure.md) tooknow mais sobre mapeamento de rede.

4. **Contas de armazenamento de destino:** por padrão, a ASR criará Olá novo destino conta de armazenamento imitando sua configuração de armazenamento de máquina virtual de origem. No caso de conta de armazenamento criada por ASR já existir, ela será reutilizada.

5. **Contas de armazenamento de cache:** ASR precisa chamada armazenamento em cache na região de origem de saudação de conta de armazenamento extra. Todos os Olá alterações ocorrendo no hello VMs de origem são rastreadas e enviadas toocache conta de armazenamento antes de replicar esses local de destino toohello.

6. **Conjunto de disponibilidade:** por padrão, o ASR criará uma novo conjunto de disponibilidade na região de destino Olá com nome com o sufixo "asr". No caso de conjunto de disponibilidade criado pelo ASR já existir, ela será reutilizada.

7.  **Política de replicação:** ele define as configurações de saudação para recuperação ponto retenção aplicativo e o histórico de instantâneo consistente com frequência. Por padrão, o ASR criará uma nova política de replicação com configurações padrão de '24 horas’ para retenção de ponto de recuperação e '60 minutos’ para a frequência do instantâneo consistente de aplicativo.

    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Personalizar os recursos de destino

Caso você deseje toochange saudação padrão ASR, você pode alterar configurações de saudação com base em suas necessidades.

1. **Personalizar:** clique em toochange Olá os padrões usados pelos ASR.

2. **Grupo de recursos de destino:** você pode selecionar o grupo de recursos de saudação da lista de saudação de todos os grupos de recursos Olá existente no local de destino de saudação de assinatura de saudação.

3. **Rede Virtual de destino:** você pode encontrar a lista de saudação da rede virtual de saudação todos os no local de destino hello.

4. **Conjunto de disponibilidade:** você só pode adicionar disponibilidade conjuntos de configurações toohello VMs que fazem parte de disponibilidade na região de origem.

5. **Contas de Armazenamento de Destino:**

![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Clique em **Criar o recurso de destino** e Habilitar a replicação


Depois que as máquinas virtuais são protegidas você pode verificar o status de saudação de integridade de VMs em **replicadas itens**

>[!NOTE]
>Durante a saudação momento da replicação inicial existe pode ser uma possibilidade de que o status leva tempo toorefresh e você não vir o andamento por algum tempo. Você pode clicar em botão de atualização de saudação na parte superior da saudação de status mais recente do Olá Olá folha tooget.
>

![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Próximas etapas
- [Saiba mais](site-recovery-test-failover-to-azure.md) sobre a execução de failovers de teste.
- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- Saiba mais sobre [usando planos de recuperação](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Saiba mais sobre [proteger novamente as VMs do Azure](site-recovery-how-to-reprotect.md) após o failover.
