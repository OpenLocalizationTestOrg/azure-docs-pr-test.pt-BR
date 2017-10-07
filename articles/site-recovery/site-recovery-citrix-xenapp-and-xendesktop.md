---
title: "aaaReplicate uma implantação de várias camada Citrix XenDesktop e XenApp usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como implantações tooprotect e recupere o Citrix XenDesktop e XenApp usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Replicar uma implantação do Citrix XenApp e XenDesktop de várias camadas usando o Azure Site Recovery

## <a name="overview"></a>Visão geral

Citrix XenDesktop é uma solução de virtualização de área de trabalho que a entrega de aplicativos e áreas de trabalho como um ondemand tooany usuário do serviço, em qualquer lugar. Com tecnologia de entrega FlexCast XenDesktop pode rapidamente e com segurança fornecer aplicativos e áreas de trabalho toousers.
Hoje, o Citrix XenApp não fornece qualquer capacidade de recuperação de desastre.

Uma solução de recuperação de desastres BOM, deve permitir modelagem de planos de recuperação em torno de saudação acima arquiteturas de aplicativos complexos e também ter Olá capacidade tooadd personalizado etapas toohandle aplicativo mapeamentos entre várias camadas, portanto, fornecendo um Clique se captura solução no evento de saudação de um desastre esquerda tooa reduzir o RTO.

Este documento fornece uma orientação passo a passo para a criação de uma solução de recuperação de desastre para suas implantações locais do Citrix XenApp em plataformas do Hyper-V e VMware vSphere. Este documento descreve também como tooperform um failover de teste (análise de recuperação de desastres) e o failover não planejado tooAzure usando planos de recuperação, configurações de saudação com suporte e os pré-requisitos.


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que compreender o seguinte hello:

1. [Replicando tooAzure uma máquina virtual](site-recovery-vmware-to-azure.md)
1. Como muito[criar uma rede de recuperação](site-recovery-network-design.md)
1. [Fazer um tooAzure de failover de teste](site-recovery-test-failover-to-azure.md)
1. [Fazer um failover tooAzure](site-recovery-failover.md)
1. Como muito[replicar um controlador de domínio](site-recovery-active-directory.md)
1. Como muito[replicar do SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Padrões de implantação

Um farm do Citrix XenApp e XenDesktop normalmente tem saudação padrão de implantação a seguir:

**Padrão de implantação**

A implantação do Citrix XenApp e XenDesktop com servidor DNS AD, servidor de banco de dados SQL, Controlador de entrega Citrix, servidor StoreFront, XenApp Master (VDA), servidor de licenças do Citrix XenApp

![Padrão de Implantação 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Suporte do Site Recovery

Para fins de saudação deste artigo, Citrix implantações em máquinas virtuais VMware gerenciadas por vSphere 6.0 / System Center VMM 2012 R2 foram usado toosetup DR.

### <a name="source-and-target"></a>Origem e destino

**Cenário** | **site secundário tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Não está no escopo | Sim
**VMware** | Não está no escopo | Sim
**Servidor físico** | Não está no escopo | Sim

### <a name="versions"></a>Versões
Os clientes podem implantar componentes do XenApp como máquinas virtuais em execução no Hyper-V ou VMware, ou como servidores físicos. Recuperação de Site do Azure pode proteger tooAzure ambas as implantações físicas e virtuais.
Como XenApp 7,7 ou posterior tem suporte no Azure, somente implantações com essas versões podem sofrer failover tooAzure para recuperação de desastres ou migração.

### <a name="things-tookeep-in-mind"></a>Tookeep coisas em mente

1. Proteção e recuperação de local há suporte para implantações usando o sistema operacional Server máquinas toodeliver XenApp aplicativos publicados e XenApp publicado áreas de trabalho.

2. Não há suporte para a proteção e recuperação de implantações de local usando toodeliver de máquinas de SO da área de trabalho VDI de área de trabalho cliente áreas de trabalho virtuais, incluindo Windows 10. Isso ocorre porque a ASR não oferece suporte à recuperação de saudação de computadores com área de trabalho OS'es.  Além disso, alguns tipos de área de trabalho virtual do cliente (por exemplo, Windows 7) ainda não têm suporte para licenciamento no Azure. [Saiba mais](https://azure.microsoft.com/pricing/licensing-faq/) sobre licenciamento para áreas de trabalho de cliente/servidor no Azure.

3.  O Azure Site Recovery não pode replicar e proteger clones MCS ou PVS locais existentes.
É necessário toorecreate esses clones usando o Azure RM provisionamento do controlador de entrega.

4. O NetScaler não pode ser protegido usando o Azure Site Recovery conforme o NetScaler baseia-se em FreeBSD e o Azure Site Recovery não oferece suporte a proteção do sistema operacional do FreeBSD. Você precisa toodeploy e configurar um novo dispositivo NetScaler de mercado Azure após o failover tooAzure.


## <a name="replicating-virtual-machines"></a>Replicação de máquinas virtuais

Olá seguintes componentes do hello Citrix XenApp implantação necessário toobe protegido tooenable replicação e a recuperação.

* Proteção do servidor DNS AD
* Proteção do servidor de banco de dados SQL
* Proteção do Controlador de entrega do Citrix
* Proteção do servidor StoreFront.
* Proteção do XenApp Master (VDA)
* Proteção do servidor de licença do Citrix XenApp


**Replicação do servidor DNS AD**

Consulte também[proteger o Active Directory e DNS com o Azure Site Recovery](site-recovery-active-directory.md) na orientação para a replicação e configurar um controlador de domínio no Azure.

**Replicação do servidor de banco de dados SQL**

Consulte também[proteger o SQL Server com a recuperação de desastres do SQL Server e o Azure Site Recovery](site-recovery-sql.md) para orientações técnicas detalhadas sobre Olá recomendado opções para proteger os servidores SQL.

Execute [neste guia](site-recovery-vmware-to-azure.md) toostart replicando Olá outros tooAzure de máquinas virtuais do componente.

![Proteção dos componentes do XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**Configurações de rede e de computação**

Depois de máquinas Olá protegidas (status mostra como "Protected" em itens replicados), Olá computação e as configurações de rede necessário toobe configurado.
Em computação e rede > computação propriedades, você pode especificar o tamanho de destino e o nome de VM do Azure hello.
Se for necessário, modifique Olá nome toocomply com os requisitos do Azure. Você também pode exibir e adicionar informações sobre a rede de destino hello, sub-rede e endereço IP que será atribuído toohello VM do Azure.

Observe o seguinte hello:

* Você pode definir o endereço IP de destino hello. Se você não fornecer um endereço, Olá failover máquina usará o DHCP. Se você definir um endereço que não está disponível em failover, o failover de saudação não funcionará. saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.

* Para o servidor de AD/DNS hello, reter Olá local permite endereço que especificar Olá mesmo endereço como servidor DNS Olá para rede Virtual do Azure hello.

número de saudação de adaptadores de rede é determinado pelo tamanho de saudação especificado para a máquina de virtual de destino Olá, da seguinte maneira:

*   Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
*   Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.
* Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.
*   Se a máquina virtual de saudação tem vários adaptadores de rede conectará todos toohello mesma rede.
*   Se a máquina virtual de saudação tem vários adaptadores de rede, hello primeiro aquele mostrado na lista de saudação torna-se adaptador de rede saudação padrão em Olá máquina virtual do Azure.


## <a name="creating-a-recovery-plan"></a>Criar um plano de recuperação

Após a replicação está habilitada para Olá XenApp componente VMs, Olá próxima etapa é toocreate um plano de recuperação.
Uma plano de recuperação agrupa as máquinas virtuais com requisitos semelhantes para failover e recuperação.  

**Etapas toocreate um plano de recuperação**

1. Adicione máquinas virtuais do hello XenApp componente no plano de recuperação de saudação.
2. Clique em Planos de Recuperação -> + Plano de Recuperação. Forneça um nome intuitivo para o plano de recuperação de saudação.
3. Para máquinas virtuais do VMware: selecione a origem como o servidor de processo do VMware, o destino como o Microsoft Azure e o modelo de implantação como o Gerenciador de Recursos, e clique em Selecionar itens.
4. Para máquinas virtuais Hyper-V: Selecionar origem como o servidor do VMM, como o Microsoft Azure e o modelo de implantação como o Gerenciador de recursos de destino e clique em selecionar itens e selecione máquinas virtuais de implantação XenApp hello.

### <a name="adding-virtual-machines-toofailover-groups"></a>A adição de grupos de toofailover de máquinas virtuais

Planos de recuperação podem ser personalizado tooadd failover grupos para ações de manual, a ordem ou scripts de inicialização específica. Olá grupos a seguir precisa de plano de recuperação toobe toohello adicionado.

1. Grupo de failover 1: DNS AD
2. Grupo de failover 2: VMs do SQL Server
2. Grupo de failover 3: VM de imagem do VDA Master
3. Grupo de failover 4: controlador de entrega e VMs do servidor StoreFront


### <a name="adding-scripts-toohello-recovery-plan"></a>Adicionar plano de recuperação de toohello de scripts

Os scripts podem ser executados antes ou depois de um grupo específico em um plano de recuperação. Ações manuais podem ser também incluídas e executadas durante o failover.

plano de recuperação personalizada Olá aparência Olá abaixo:

1. Grupo de failover 1: DNS AD
2. Grupo de failover 2: VMs do SQL Server
3. Grupo de failover 3: VM de imagem do VDA Master

   >[!NOTE]     
   >As etapas 4, 6 e 7, que contém ações manuais ou de script são aplicável tooonly um XenApp local > ambiente com catálogos MCS/PVS.

4. Ação Manual ou script do grupo 3: Olá de VM VDA mestre desligamento mestre VDA VM quando o failover tooAzure estará em um estado de execução. toocreate novos catálogos MCS usando o Azure ARM de hospedagem, mestre de Olá VDA VM é necessário toobe em parado (de alocada) estado. Saudação de desligamento VM a partir do Portal do Azure.

5. Grupo de failover 4: controlador de entrega e VMs do servidor StoreFront
6. Ação manual ou de script do grupo 3 1:

    ***Adicionar conexão do host do Azure RM***

    Crie conexão de host do Azure ARM no controlador de entrega máquina tooprovision novos catálogos MCS no Azure. Execute as etapas de saudação conforme explicado neste [artigo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Ação manual ou de script do grupo 3 2:

    ***Recriar os catálogos MCS no Azure***

    Olá existente MCS ou PVS clones no site primário Olá não será replicada tooAzure. É necessário toorecreate esses clones usando Olá replicado VDA mestre e ARM Azure provisionamento do controlador de entrega. Execute as etapas de saudação conforme explicado neste [artigo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catálogos no Azure.

![Plano de recuperação para componentes do XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >Você pode usar scripts em [local](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate Olá DNS com hello novos IPs de saudação failover > máquinas virtuais ou tooattach um balanceador de carga Olá falha pela máquina virtual, se necessário.


## <a name="doing-a-test-failover"></a>Executar um failover de teste

Execute [neste guia](site-recovery-test-failover-to-azure.md) toodo um failover de teste.

![Plano de Recuperação](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>Executar um failover

Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.

## <a name="next-steps"></a>Próximas etapas

Você pode [saber mais](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sobre replicação de implantações do Citrix XenApp e XenDesktop neste white paper. Examinar a orientação de saudação muito[replicar outros aplicativos](site-recovery-workload.md) com a recuperação de Site.
