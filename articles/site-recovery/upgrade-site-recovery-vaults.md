---
title: "Cofre de serviços de recuperação do Azure tooan aaaUpgrade um cofre de recuperação de Site"
description: "Saiba como tooupgrade um cofre do Azure Site Recovery serviços de recuperação de tooa cofre"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>Atualizar um cofre de serviços de recuperação baseados no Gerenciador de recursos do Azure Site Recovery cofre tooan

Este artigo descreve como tooupgrade do Azure Site Recovery cofres cofres de serviços de recuperação com base em Gerenciador de recursos tooAzure sem nenhum impacto sobre replicação em andamento. Para saber mais sobre os recursos e benefícios do Azure Resource Manager, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Introdução
Um cofre de serviços de recuperação é um recurso do Gerenciador de recursos do Azure para o gerenciamento de backup e recuperação de desastres nativamente na nuvem de saudação. É um cofre unificado que você pode usar no novo portal do Azure Olá e substitui o backup clássico hello e cofres de recuperação de Site.

Os cofres dos Serviços de Recuperação oferecem uma matriz de recursos, incluindo:

* Suporte do Azure Resource Manager: você pode proteger e realizar o failover de suas máquinas virtuais e computadores físicos em uma pilha do Azure Resource Manager.

* Excluir disco: se você tiver arquivos temporários ou alta rotatividade de dados que você não deseja toouse toda a largura de banda para, você pode excluir volumes de replicação. Esse recurso foi habilitado no momento em *VMware tooAzure* e *tooAzure Hyper-V* e são estendidos tooother cenários bem.

* Suporte para premium e o armazenamento redundante localmente: agora você pode proteger servidores no armazenamento premium contas que permitem que os clientes tooprotect aplicativos com maior operações de entradam/saídam por segundo (IOPS). Esse recurso está habilitado no momento em *tooAzure VMware*.

* Simplificada de experiência do guia de Introdução: experiência de Introdução Olá Avançado foi projetada fácil da configuração de recuperação de desastres de toomake.

* Backup e recuperação de Site de gerenciamento de Olá mesmo cofre: agora você pode proteger servidores para recuperação de desastres ou realizar o backup do hello mesmo cofre, que pode reduzir o gerenciamento de sobrecarga significativamente.

Para obter mais informações sobre a experiência de saudação atualizada e recursos, consulte Olá [blog de armazenamento, Backup e recuperação](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Principais recursos

* Sem impacto na replicação em andamento: as replicações em andamento continuam sem qualquer interrupção durante e após a atualização.

* Sem custo adicional: obtenha um conjunto completo de recursos atualizados sem custo adicional.

* Sem perda de dados: como esse processo é uma atualização e não uma migração, pontos de recuperação de replicação existentes e configurações permanecem intactas durante e após a atualização de saudação.


## <a name="what-happens-during-hello-vault-upgrade"></a>O que acontece durante a atualização de cofre Olá?

Durante a atualização de saudação, você não pode executar operações como registrar um novo servidor ou habilitar a replicação para uma máquina virtual (VM). As operações que envolvem ler dados de ou gravar dados toohello cofre, como replicação contínua de itens protegidos toohello cofre, continuam sem interrupções.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Alterações tooautomation e ferramentas depois da atualização de saudação
Conforme você atualiza o tipo de Cofre de saudação do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos, atualize automação existentes hello ou ferramentas tooensure que ele continue toowork após a atualização de saudação.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Preparar o ambiente para a atualização de saudação

* [Instale o PowerShell ou atualizá-lo tooversion 5 ou posterior](https://www.microsoft.com/download/details.aspx?id=50395)
* [Instale a versão mais recente saudação do MSI do PowerShell do Azure](https://github.com/Azure/azure-powershell/releases)
* [Baixar o script de atualização do Cofre de serviços de recuperação de Olá](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Pré-requisitos
tooupgrade do Site Recovery cofres tooAzure cofres de serviços de recuperação com base em Gerenciador de recursos, você deve cumprir Olá requisitos a seguir:

* Versão mínima do agente: versão de saudação do provedor Azure Site Recovery instalado em seu servidor deve ser 5.1.1700.0 ou posterior.

* Configuração com suporte: não é possível configurar o cofre com a rede SAN (rede de área de armazenamento ) ou Grupos de Disponibilidade AlwaysOn do SQL Server. Há suporte para todas as outras configurações.

    >[!NOTE]
    >Após a atualização de saudação, você pode gerenciar o mapeamento de armazenamento somente por meio do PowerShell.

* Cenário de implantação com suporte: seu cofre não deve ser Olá *tooAzure VMware* modelo de implantação herdado. Antes de prosseguir, primeiro mova o modelo de implantação avançada do toohello.

* Nenhum trabalho ativo iniciada pelo usuário que envolvem o gerenciamento de operações de plano: porque o plano de gerenciamento de toohello de acesso é restrito durante a atualização, conclua todas as ações do plano de gerenciamento antes de disparar atualização hello. Esse processo não inclui a replicação em andamento.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Essa atualização afeta minha replicação em andamento?**

Não. A replicação em andamento continuará sem interrupção durante e após a atualização de saudação.

**O que acontece toonetwork configurações, como configurações de IP e de VPN site a site?**

atualização de saudação não afeta as configurações de rede hello. Todas as conexões Azure para local permanecem intactas.

**O que acontece cofres toomy se eu não planejar tooupgrade em Olá futuro próximo?**

Suporte para o Cofre de recuperação de Site no portal do Azure antigo Olá será preterido começando em setembro de 2017. É altamente recomendável que você use Olá recurso de atualização toomove toohello novo portal.

**O que este plano de migração significa para minhas ferramentas existentes?**  

A atualização de seu modelo de implantação do Gerenciador de recursos de toohello ferramentas é uma saudação alterações mais importantes que você deve considerar nos planos de atualização. Olá cofres de serviços de recuperação são baseados no modelo de implantação do Gerenciador de recursos de saudação. 

**Quanto tempo Olá plano de gerenciamento de tempo de inatividade última?**

atualização de saudação normalmente demora cerca de 15 minutos de too30 e pode levar até tooa máximo de uma hora.

**Posso reverter após a atualização?**

Não. A reversão não tem suporte depois recursos Olá foi atualizados com êxito.

**Eu Validar minha assinatura ou toosee recursos se eles podem ser atualizados?**

Sim. Opção atualização com suporte de plataforma hello, Olá primeira etapa na atualização de saudação é toovalidate que recursos Olá são capazes de fazer uma atualização. Se a validação de saudação falhar, você receberá mensagens de erro apropriadas ou avisos.

**Como faço para relatar um problema com a atualização de Olá?**

Se ocorrerem falhas durante a atualização Olá, observe o ID da operação Olá listado no erro de saudação. Microsoft Support proativamente funcionará para resolver o problema de saudação. Você também pode contatar a equipe de suporte de saudação com sua ID de assinatura, nome do cofre e ID da operação. Suporte funcionará problema de saudação tooresolve assim que possível. Não tente novamente a operação Olá a menos que seja explicitamente instruções toodo caso pela Microsoft.

## <a name="run-hello-script"></a>Execute o script hello

No PowerShell, execute o comando a seguir de saudação:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* SubscriptionID: Olá ID de assinatura que está associado ao Cofre Olá que você está atualizando.

* VaultName: o nome de saudação do cofre Olá que você estiver atualizando.

* : Olá local do cofre Olá que você está atualizando.

* ResourceType: HyperVRecoveryManagerVault para cofres do Site Recovery.

* TargetResourceGroupName: grupo de recursos de saudação no qual você deseja Olá atualizado toobe cofre colocado. O TargetResourceGroupName pode ser de um grupo de recursos existente no Azure Resource Manager ou um novo. Se não existir Olá TargetResourceGroupName for fornecido, ele é criado como parte da atualização de saudação no hello mesmo local Olá cofre. Para obter mais informações, consulte a seção "Grupos de recursos" hello [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Nomes de grupo de recursos é restrições de toocertain de assunto. cofre tooprevent atualização falha, ser se Olá tooobserve convenção de nomenclatura com cuidado.
    >
    >Por exemplo:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc

Como alternativa, você pode executar Olá script a seguir. Insira valores hello de parâmetros de Olá necessário.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Olá script do PowerShell solicitará que você tooenter suas credenciais. Digite-os em duas vezes, uma vez para a conta de modelo de implantação clássico hello e uma vez para Olá conta do Azure Resource Manager.

2. Depois de inserir suas credenciais, script hello executa toodetermine uma verificação se a saudação de atende infraestrutura instalação mencionado anteriormente requisitos.

3. Depois que os pré-requisitos de saudação foram verificados e confirmados, você está tooproceed solicitada com a atualização do cofre hello. o processo de atualização Olá inicia a atualização de seu cofre. atualização inteira Olá pode levar 15 toocomplete minutos de too30.

4. Depois Olá atualização foi concluída com êxito, você pode acessar o Cofre de saudação atualizado no novo portal do Azure de saudação.

## <a name="post-upgrade-vault-management"></a>Gerenciamento do cofre após a atualização

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Replicar usando o Azure Site Recovery no cofre de serviços de recuperação de saudação

* Agora você pode proteger suas VMs do Azure de uma região tooanother. Para obter mais informações, consulte [Replicar VMs do Azure entre regiões com o Azure Site Recovery](site-recovery-azure-to-azure.md).

* Para obter mais informações sobre a replicação de máquinas virtuais do VMware tooAzure, consulte [tooAzure replicar máquinas virtuais do VMware com a recuperação de Site](vmware-walkthrough-overview.md).

* Para obter mais informações sobre a replicação de máquinas virtuais do Hyper-V (sem VMM) tooAzure, consulte [tooAzure de máquinas virtuais (sem VMM) do Hyper-V replicar](hyper-v-site-walkthrough-overview.md).

* Para obter mais informações sobre a replicação de máquinas virtuais do Hyper-V (com o VMM) tooAzure, consulte [Olá de máquinas virtuais de Hyper-V replicar em tooAzure de nuvens do VMM com a recuperação de Site no portal do Azure](vmm-to-azure-walkthrough-overview.md).

* Para obter mais informações sobre a replicação de site secundário do tooa Hyper-VMs (com o VMM), consulte [Olá de máquinas virtuais de replicar Hyper-V no VMM nuvens tooa secundário do VMM site usando o portal do Azure](site-recovery-vmm-to-vmm.md).

* Para obter mais informações sobre a replicação de site secundário do VMs VMware tooa, consulte [replicar em máquinas virtuais VMware ou local site secundário do tooa servidores físicos no portal do Azure clássico de saudação](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>Exibir seus itens replicados

Olá imagem a seguir mostra Olá dos serviços de recuperação cofre página do painel que exibe as principais entidades para o cofre hello. Selecione tooview uma lista de entidades protegidas no cofre hello, **recuperação de Site** > **replicadas itens**.


![Itens replicados](./media/upgrade-site-recovery-vaults/replicateditems.png)

Olá, imagem a seguir mostra Olá de fluxo de trabalho para exibir seus itens replicados e hello **Failover** comando para iniciar um failover.

![Itens replicados](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Exibir suas configurações de replicação

No cofre de recuperação de Site hello, cada grupo de proteção é configurado com a frequência de cópia, retenção de ponto de recuperação, a frequência dos instantâneos consistentes por aplicativo e outras configurações de replicação. No cofre de serviços de recuperação hello, essas configurações são definidas como uma política de replicação. nome de saudação da política de saudação é nome de saudação do grupo de proteção Olá Olá *primarycloud_Policy*.

Para obter mais informações sobre a política de replicação, consulte [Gerenciar política de replicação para VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).
