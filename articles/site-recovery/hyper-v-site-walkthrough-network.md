---
title: "aaaPlan de rede para replicação do Hyper-V (sem o System Center VMM) tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve o planejamento da rede necessários ao replicar tooAzure de VMs Hyper-V (sem VMM)"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a>Etapa 4: Planejar a rede para replicação do Hyper-V tooAzure

Este artigo resume rede considerações de planejamento, quando a replicação local tooAzure de VMs Hyper-V (sem o System Center VMM) usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connecting-tooreplica-vms-after-failover"></a>Conectando VMs tooreplica após o failover

Ao planejar sua estratégia de failover e replicação, uma das perguntas mais importantes Olá é como tooconnect toohello VM do Azure após o failover. Há algumas opções ao criar sua estratégia de rede para VMs de réplica do Azure:

- **Endereço IP diferente**: você pode selecionar toouse um intervalo de endereço IP diferente para Olá replicadas a rede VM do Azure. No hello cenário VM obtém um novo endereço IP após o failover, e é necessária uma atualização DNS. [Saiba mais](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- **Mesmo endereço IP**: talvez você queira toouse Olá mesmo intervalo de endereços IP, como no local primário de rede, para Olá rede Azure após o failover.  Olá mantendo mesmos endereços IP simplifica recuperação hello, reduzindo problemas relacionados à rede após o failover. No entanto, quando você estiver replicando tooAzure, você precisará tooupdate rotas com o novo local Olá endereços IP hello após o failover.


## <a name="retain-ip-addresses"></a>Reter os endereços IP

Recuperação de site fornece endereços IP hello recurso tooretain fixo durante o failover tooAzure, com um failover de sub-rede.

Com o failover de sub-rede, uma sub-rede específica está presente no Site 1 ou Site 2, mas nunca em ambos os sites ao mesmo tempo. Em ordem toomaintain Olá espaço de endereço IP no evento de saudação de um failover, você organiza programaticamente para Olá roteador infraestrutura toomove Olá subredes de tooanother de um site. Durante o failover, Olá sub-redes mover com hello associados VMs protegidas. Olá principal desvantagem é na saudação de uma falha, você tem subrede inteira toomove hello.


### <a name="failover-example"></a>Exemplo de failover

Vejamos um exemplo de tooAzure de failover.

- Uma organização fictícia, o Woodgrove Bank, tem uma infraestrutura local que hospeda seus aplicativos de negócios. Seus aplicativos móveis são hospedados no Azure.
- Conectividade entre VMs do Woodgrove Bank em servidores locais e do Azure é fornecida por uma conexão de (VPN) site a site entre a rede de borda de local de saudação e Olá rede virtual do Azure.
- Isso significa VPN que Olá da rede virtual no Azure da empresa é exibido como uma extensão da sua rede local.
- O Woodgrove deseja toouse recuperação de Site tooreplicate local cargas de trabalho tooAzure.
 - O Woodgrove tem toodeal com aplicativos e configurações que dependem embutido endereços IP e, portanto, precisam tooretain endereços IP para seus aplicativos depois tooAzure de failover.
 - O Woodgrove tem endereços IP do intervalo 172.16.1.0/24, 172.16.2.0/24 tooits recursos atribuídos em execução no Azure.


Para Woodgrove toobe capaz de tooreplicate tooAzure suas VMs, enquanto retendo Olá IP endereços, é aqui que empresa Olá precisa toodo:

1. Crie uma rede virtual do Azure. Ele deve ser uma extensão da saudação de rede, no local para que os aplicativos podem fazer failover perfeitamente.
2. Azure permite que você tooadd site a site conectividade VPN, além de conectividade de site a toopoint toohello as redes virtuais criadas no Azure.
3. Ao configurar a conexão de site a site Olá, em hello Azure de rede, você pode rotear o tráfego toohello local (rede local) somente se o intervalo de endereços IP hello é diferente do intervalo de endereços IP hello local.
    - Isso ocorre porque o Azure não dá suporte a sub-redes ampliadas. Então se você tiver sub-redes 192.168.1.0/24 local, não é possível adicionar 192.168.1.0/24 um local de rede na rede do Azure de saudação.
    - Isso é esperado, pois o Azure não sabe que não há nenhuma VM active na sub-rede hello e sub-rede hello está sendo criado para a recuperação de desastres.
    - toobe toocorrectly capaz de rotear o tráfego de rede fora de um Azure Olá sub-redes na rede de saudação e saudação da rede local não deve estar em conflito.

![Antes do failover da sub-rede](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Antes do failover

1. Crie uma rede adicional (por exemplo, uma Rede de Recuperação). Esta é a rede de saudação que passou por failover de máquinas virtuais são criados.
2. tooensure que hello endereço IP para uma máquina virtual é mantido após um failover, nas propriedades VM hello > **configurar**, especifique Olá que Olá VM tem local e clique em de endereços IP mesmo **salvar**.
3. Quando Olá VM é feito o failover, Azure Site Recovery atribuirá Olá fornecido tooit de endereço IP.

    ![Propriedades da rede](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. Depois de failover disparador é acionado e Olá VMs são criadas no Azure com o endereço IP hello necessário, você pode se conectar toohello de rede usando um [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Essa ação pode ser inserida em um script.
5. Rotas necessário toobe modificado adequadamente, tooreflect que 192.168.1.0/24 agora foi movido tooAzure.

    ![Após o failover da sub-rede](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Após o failover

Caso você não tenha uma rede do Azure, conforme ilustrado acima, poderá criar uma conexão VPN site a site entre o site primário e o Azure, após o failover.

## <a name="change-ip-addresses"></a>Alterar os endereços IP

Isso [postagem de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica como tooset backup Olá infraestrutura de rede do Azure, quando você não precisar tooretain IP endereços após o failover. Começa com uma descrição do aplicativo, procura no como tooset uma rede local e no Azure e termina com as informações sobre como executar failovers.  

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 5: preparar o Azure](hyper-v-site-walkthrough-prepare-azure.md)
