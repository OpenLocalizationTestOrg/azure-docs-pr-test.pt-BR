---
title: "aaaSet VMM e Hyper-V para o site secundário do tooa de replicação com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset servidores do System Center VMM e hosts de Hyper-V para o site do replication tooa secundário do VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Etapa 4: Configurar o VMM e Hyper-V para o site secundário de tooa de replicação de VM do Hyper-V 

Depois que você preparou de rede, configurar servidores do System Center Virtual Machine Manager (VMM) e hosts Hyper-V para Hyper-V máquina virtual (VM) replicação tooa site secundário, usando [do Azure Site Recovery](site-recovery-overview.md) em Olá portal do Azure. 

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>Preparar servidores VMM 

tooprepare para implantação:


1. Certifique-se de servidores do VMM está em conformidade com hello [oferecer suporte aos requisitos](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), e [os pré-requisitos de implantação](vmm-to-vmm-walkthrough-prerequisites.md).
2. Verifique se o VMM servidores toohello conectado à internet e têm acesso toothese URLs.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.
    - Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
    - Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).
3. Verifique se o servidor do VMM Olá é [preparado para mapeamento de rede](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Preparar os hosts/clusters do Hyper-V

1. Certifique-se / clusters de hosts Hyper-V está em conformidade com hello [oferecer suporte aos requisitos](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), e [os pré-requisitos de implantação](vmm-to-vmm-walkthrough-prerequisites.md).
2. Verifique os requisitos de saudação para [VMs Hyper-V](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Verifique os requisitos de [rede](site-recovery-support-matrix-to-sec-site.md#network-configuration) e de [armazenamento](site-recovery-support-matrix-to-sec-site.md#storage).
4. Certifique-se de hosts Hyper-V são toohello conectado à internet e têm acesso toothese URLs.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.
    - Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
    - Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).

## <a name="prepare-for-single-server-deployment"></a>Preparar para a implantação de servidor único


Se você tiver apenas um único servidor VMM, você pode replicar máquinas virtuais em hosts Hyper-V na nuvem do VMM de saudação muito[Azure](hyper-v-site-walkthrough-overview.md) ou nuvem VMM secundário tooa, conforme descrito neste documento. É recomendável opção primeira Olá porque a replicação entre nuvens não contínua.

Se você quiser tooreplicate entre nuvens, você pode replicar com um servidor do VMM autônomo único ou com um único servidor VMM implantado em um cluster de Windows ampliado

### <a name="replicate-with-a-standalone-vmm-server"></a>Replicar com um servidor VMM autônomo

Nesse cenário, implantar o servidor VMM único de saudação como uma máquina virtual no site primário hello e replicar VM tooa site secundário usando a réplica do Hyper-V e recuperação de Site.

1. **Configure o VMM em uma VM Hyper-V**. Sugerimos que você colocar a instância do SQL Server Olá usada pelo VMM em Olá mesma VM. Isso economiza tempo, como apenas uma VM tem toobe criado. Se você quiser toouse a instância remota do SQL Server e ocorrer uma interrupção, você precisa toorecover essa instância para que você possa recuperar do VMM.
2. **Certifique-se de que o servidor do VMM Olá tem pelo menos duas nuvens configuradas**. Uma nuvem conterá Olá VMs que você deseja tooreplicate e Olá outros nuvem funciona como o local secundário hello. Olá nuvem que contém as VMs Olá deseja tooprotect devem ser compatíveis com [pré-requisitos](#prerequisites).
3. Configure a Recuperação de Site conforme descrito neste artigo. Criar e registrar o servidor do VMM Olá em um cofre, configure uma política de replicação e habilitar a replicação. nomes VMM de origem e destino Hello serão Olá mesmo. Especifica que se a replicação inicial ocorre em rede hello.
4. Quando você configurar o mapeamento de rede você mapeie Olá da rede VM para a rede da VM toohello Olá nuvem primária para a nuvem secundária hello.
5. No console do Gerenciador do Hyper-V hello, habilitar a réplica do Hyper-V no host do Hyper-V Olá que contém Olá VMM VM e habilitar a replicação em Olá VM. Verifique se que você não adicionar tooclouds de máquina virtual do VMM Olá são protegidos pela recuperação de Site, tooensure que as configurações de réplica do Hyper-V não são substituídas pela recuperação de Site.
6. Se você criar planos de recuperação para failover que usar Olá mesmo servidor do VMM de origem e de destino.
7. Uma falha completa, failover e recuperação da seguinte maneira:

   1. Execute um failover não planejado no console do Gerenciador do Hyper-V Olá no site secundário hello, toofail sobre Olá primário VMM VM toohello site secundário.
   2. Verificar que Olá que VM VMM está ativo e em execução e no cofre hello, executar toofail um failover não planejado na Olá VMs de nuvens toosecondary primário. Confirmar failover hello e selecione um ponto de recuperação alternativo, se necessário.
   3. Após hello failover não planejado concluído, todos os recursos podem ser acessados de site primário Olá novamente.
   4. Quando o site primário Olá estiver disponível, no console do Gerenciador do Hyper-V Olá no site secundário hello, habilite a replicação inversa para Olá VMM VM. Isso inicia a replicação para Olá VM tooprimary secundário.
   5. Execute um failover planejado no console do Gerenciador do Hyper-V Olá no site secundário hello, toofail sobre Olá site primário do VMM VM toohello. Confirme failover de saudação. Em seguida, habilite a replicação inversa, para que hello VMM VM é novamente replicando de toosecondary primário.
   6. No cofre de serviços de recuperação hello, habilite a replicação inversa para carga de trabalho Olá VMs, toostart replicando-os de tooprimary secundário.
   7. No cofre de serviços de recuperação de hello, execute um failover planejado toofail Olá back cargas de trabalho VMs toohello site primário. Confirmar Olá failover toocomplete-lo. Em seguida, habilite a replicação inversa toostart replicação Olá carga de trabalho VMs de toosecondary primário.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Replicar com um cluster VMM ampliado

Em vez de implantar um servidor do VMM autônomo como uma VM que replica o site secundário tooa, você pode fazer o VMM altamente disponível, implantando-a como uma máquina virtual em um cluster de failover do Windows. Isso fornece resiliência de carga de trabalho e proteção contra falhas de hardware. toodeploy com hello de recuperação de Site VMM VM deve ser implantado em um cluster de ampliação em locais geograficamente separados. toodo isso:

1. Instalação do VMM em uma máquina virtual em um cluster de failover do Windows e selecione o servidor de saudação do hello opção toorun como altamente disponível durante a instalação.
2. instância do SQL Server de saudação que é usada pelo VMM deve ser replicada com grupos de disponibilidade do AlwaysOn do SQL Server, para que haja uma réplica de banco de dados de saudação no site secundário hello.
3. Siga as instruções de saudação toocreate este artigo um cofre, registrar o servidor de saudação e configurar a proteção. É necessário tooregister cada servidor do VMM no hello cluster no cofre de serviços de recuperação de saudação. toodo isso, instale Olá provedor em um nó ativo e registrar o servidor do VMM hello. Em seguida, você deve instalar Olá provedor em outros nós.
4. Quando ocorre uma paralisação, o servidor do VMM hello e seu banco de dados do SQL Server correspondente são failover e acessados a partir do site secundário hello.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 5: configurar um cofre](vmm-to-vmm-walkthrough-create-vault.md).
