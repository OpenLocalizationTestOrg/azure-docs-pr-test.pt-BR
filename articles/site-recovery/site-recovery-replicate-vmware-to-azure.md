---
title: Replicar aplicativos (VMware tooAzure) | Microsoft Docs
description: "Este artigo descreve como tooset a replicação virtual máquinas em execução no VMware no Azure."
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
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>Replicar aplicativos em execução nas VMs VMware tooAzure



Este artigo descreve como tooset a replicação virtual máquinas em execução no VMware no Azure.
## <a name="prerequisites"></a>Pré-requisitos

artigo de saudação pressupõe que você já

1.  [Configurado o ambiente de origem local](site-recovery-set-up-vmware-to-azure.md)
2.  [Configurado o ambiente de destino no Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Habilitar a replicação
#### <a name="before-you-start"></a>Antes de começar
Ao replicar máquinas virtuais VMware, observe o seguinte:

* Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.
* VMs VMware são descobertas a cada 15 minutos. Pode levar 15 minutos ou mais para que eles tooappear no portal de saudação após a descoberta. Da mesma forma, a descoberta pode levar 15 minutos ou mais quando você adiciona um novo servidor vCenter ou host vSphere.
* Alterações de ambiente na máquina virtual de saudação (como instalação de ferramentas do VMware) podem levar 15 minutos ou mais toobe atualizado no portal de saudação.
* Você pode verificar o último Olá descoberto tempo para VMs VMware em hello **último contato em** campo Olá vCenter server/host vSphere, em Olá **servidores de configuração** folha.
* tooadd máquinas para replicação sem aguardar a descoberta agendada do hello, realce o servidor de configuração hello (não clique nele) e clique em Olá **atualização** botão.
* Quando você habilitar a replicação, se a máquina hello está preparada, servidor de processo Olá instala automaticamente o serviço de mobilidade Olá nele.


**Agora habilite a replicação da seguinte maneira**:

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**. Depois de habilitar a replicação para Olá primeira vez, clique em **+ replicar** em replicação de tooenable Olá cofre para outras máquinas.
2. Em Olá **fonte** folha > **fonte**, selecione o servidor de configuração hello.
3. Em **Tipo de computador**, selecione **Máquinas Virtuais** ou **Computadores Físicos**.
4. Em **vCenter/vSphere hipervisor**, selecione o servidor do vCenter Olá que gerencia o host do vSphere hello, ou selecione host hello. Essa configuração não será relevante se você estiver replicando computadores físicos.
5. Selecione o servidor de processo hello. Se você não criou nenhum servidor de processo adicional esse será o nome de saudação saudação do servidor de configuração. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. Em **destino** selecione Olá assinatura e o grupo de recursos de saudação onde você deseja toocreate Olá máquinas virtuais com failover. Escolha o modelo de implantação de saudação que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá máquinas virtuais com failover.
7. Selecione conta de armazenamento do Azure Olá que desejar toouse para replicação de dados. Observe que:

   * Você pode selecionar uma conta de armazenamento padrão ou premium. Se você selecionar uma conta de premium, você precisará toospecify uma conta de armazenamento padrão para logs de replicação em andamento. As contas devem ser em Olá Cofre de serviços de recuperação com a mesma região hello.
   * Se você quiser toouse uma conta de armazenamento diferentes daquelas que você tem, você pode criar um*LInk de espaço reservado para a criação de conta de armazenamento usando o recurso Gerenciador que será abordado no guia de Introdução*. toocreate uma conta de armazenamento usando o Gerenciador de recursos, clique em **criar novo**. Se você quiser toocreate uma conta de armazenamento usando o modelo clássico hello, isso [no portal do Azure de saudação](../storage/common/storage-create-storage-account.md).

8. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure conectará quando eles são girados backup após o failover. Olá rede deve estar em Olá Cofre de serviços de recuperação com a mesma região hello. Selecione **configurar agora para os computadores selecionados**, tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina. Se você não tiver uma rede, será necessário muito[criar um](#set-up-an-azure-network). toocreate uma rede usando o Gerenciador de recursos, clique em **criar novo**. Se você quiser toocreate uma rede usando o modelo clássico hello, isso [no portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecione uma sub-rede, se aplicável. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. Em **propriedades** > **configurar propriedades**, selecione conta Olá que será usada por tooautomatically de servidor de processo Olá instalar serviço de mobilidade de saudação na máquina de saudação.  
11. Por padrão, todos os discos são replicados. discos tooexclude da replicação, clique em **todos os discos** e desmarque os discos que você não deseja tooreplicate.  Em seguida, clique em **OK**. Você pode definir propriedades adicionais posteriormente. [Saiba mais](site-recovery-exclude-disk.md) sobre a exclusão de discos.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. Em **as configurações de replicação** > **definir configurações de replicação**, verifique se esse Olá correto de política de replicação está selecionada. Você pode modificar as configurações da política de replicação em **Configurações** > **Políticas de replicação** > nome da política > **Editar Configurações**. Alterações aplicadas tooa política será aplicada tooreplicating e novas máquinas.
13. Habilitar **consistência de várias VMs** toogather máquinas em um grupo de replicação, e especifique um nome para o grupo de saudação. Em seguida, clique em **OK**. Observe que:

    * Os computadores no grupo de replicação são replicados em conjunto e têm pontos de recuperação consistentes compartilhados com o aplicativo e com falhas quando executam failover.
    * É recomendável que você colete VMs e servidores físicos para que espelhem suas cargas de trabalho. Habilitar a consistência de várias VMs pode afetar o desempenho da carga de trabalho e só deve ser usado se as máquinas estão executando Olá mesma carga de trabalho e você precisa de consistência.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Clique em **Habilitar a Replicação**. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.

> [!NOTE]
> Se a máquina hello está preparada para saudação de instalação por push mobilidade de componente de serviço será instalado quando a proteção está habilitada. Após Olá componente é instalado em falha e máquina Olá que inicia um trabalho de proteção. Depois de falha de saudação precisar toomanually reiniciar cada máquina. Após a proteção de saudação do hello reiniciar o trabalho começa novamente e ocorre a replicação inicial.
>
>

## <a name="view-and-manage-vm-properties"></a>Exibir e gerenciar as propriedades da VM

É recomendável que você verifique propriedades Olá Olá computador de origem. Lembre-se deve estar de acordo com esse nome de VM do Azure Olá [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Clique em **configurações** > **replicadas itens** > e selecione Olá máquina. Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.
2. Em **propriedades**, você pode exibir a replicação e failover informações para Olá VM.
3. Em **de computação e rede** > **propriedades de computação**, você pode especificar o tamanho de destino e o nome de VM do Azure hello. Se for necessário, modifique Olá nome toocomply com os requisitos do Azure.
    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  É possível selecionar um [grupo de recursos](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) do qual o computador fará parte do pós-failover. Você pode alterar essa configuração a qualquer momento antes do failover. Após o failover, se você migrar Olá máquina tooa outro grupo de recursos e configurações de proteção da máquina serão interrompido.
5. Você pode selecionar um [conjunto de disponibilidade](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) se sua máquina necessário toobe fazer parte de uma postagem failover. Durante a seleção do conjunto de disponibilidade, tenha em mente que:

    * Somente conjuntos de disponibilidade que pertencem toohello especificado será listado grupo de recursos  
    * Computadores com redes virtuais diferentes não podem fazer parte do mesmo conjunto de disponibilidade
    * Somente as máquinas virtuais do mesmo tamanho podem fazer parte do mesmo conjunto de disponibilidade
5. Você também pode exibir e adicionar informações sobre a rede de destino hello, sub-rede e endereço IP que será atribuído toohello VM do Azure.
6. Em **discos**, você pode ver o sistema operacional de saudação e discos de dados Olá VM que será replicado.

### <a name="network-adapters-and-ip-addressing"></a>Adaptadores de rede e endereçamento IP 

- Você pode definir o endereço IP de destino hello. Se você não fornecer um endereço, Olá failover máquina usará o DHCP. Se você definir um endereço que não está disponível em failover, o failover de saudação não funcionará. saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.
- número de saudação de adaptadores de rede é determinado pelo tamanho de saudação especificado para a máquina de virtual de destino Olá, da seguinte maneira:
    - Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
    - Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.
    - Por exemplo, se um computador de origem tem dois adaptadores de rede e tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.
    - Se a máquina virtual de saudação tem vários adaptadores de rede conectará todos toohello mesma rede.
    - Se a máquina virtual de saudação tem vários adaptadores de rede, Olá primeiro mostrada na lista de saudação se torna Olá *padrão* adaptador de rede na máquina virtual do Azure de saudação.
   



## <a name="common-issues"></a>Problemas comuns

* Cada disco deve ter menos de 1 TB de tamanho.
* disco Olá SO deve ser um disco básico e não dinâmico
* Para geração 2/UEFI habilitado máquinas virtuais, família de sistemas operacionais Olá deve ser Windows e o disco de inicialização deve ser menor que 300GB

## <a name="next-steps"></a>Próximas etapas

Depois de proteção de saudação é concluída, você pode tentar [failover](site-recovery-failover.md) toocheck se seu aplicativo aparece no Azure ou não.

Caso você deseje toodisable proteção, verifique como muito[limpar as configurações de registro e proteção](site-recovery-manage-registration-and-protection.md)
