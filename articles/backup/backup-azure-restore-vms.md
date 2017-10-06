---
title: "aaaRestore um backup de máquinas virtuais | Microsoft Docs"
description: "Saiba como toorestore uma máquina virtual do Azure da recuperação de uma ponto"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "restaurar o backup. como toorestore; ponto de recuperação;"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Restaurar máquinas virtuais no Azure
> [!div class="op_single_selector"]
> * [Restaurar VMs no portal do Azure](backup-azure-arm-restore-vms.md)
> * [Restaurar VMs no portal Clássico](backup-azure-restore-vms.md)
>
>

Restaure um tooa de máquina virtual nova VM de backups de saudação armazenados em um cofre de Backup do Azure com hello seguindo as etapas.

> [!IMPORTANT]
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> **15 de outubro de 2017**, não será capaz de toouse PowerShell toocreate os cofres de Backup. <br/> **A partir de 1º de novembro de 2017**:
>- Nenhum Cofre de Backup restante será automaticamente atualizado tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

## <a name="restore-workflow"></a>Restaurar o fluxo de trabalho
### <a name="step-1-choose-an-item-toorestore"></a>Etapa 1: Escolha um item toorestore
1. Navegue toohello **itens protegidos** Olá guia e selecione a máquina virtual que deseja toorestore tooa nova VM.

    ![Itens protegidos](./media/backup-azure-restore-vms/protected-items.png)

    Olá **ponto de recuperação** coluna Olá **itens protegidos** página informará Olá o número de pontos de recuperação para uma máquina virtual. Olá **mais novo ponto de recuperação** coluna informa Olá hora do backup mais recente de saudação do qual uma máquina virtual pode ser restaurada.
2. Clique em **restaurar** tooopen Olá **restaurar um Item** assistente.

    ![Restaurar um Item](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Etapa 2: Selecione um ponto de recuperação
1. Em Olá **selecionar um ponto de recuperação** tela, você pode restaurar de ponto de recuperação mais recente hello, ou de um ponto anterior no tempo. Olá opção padrão selecionada quando o assistente é aberto é *mais novo ponto de recuperação*.

    ![Selecionar um ponto de recuperação](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick um ponto anterior no tempo, escolha Olá **Selecionar data** opção na lista suspensa de saudação e selecione uma data no controle de calendário Olá clicando em Olá **ícone de calendário**. No controle hello, todas as datas que têm pontos de recuperação são preenchidas com um sombreado cinza claro em são selecionáveis pelo usuário hello.

    ![Selecione uma data](./media/backup-azure-restore-vms/select-date.png)

    Depois de clicar em uma data no controle de calendário hello, pontos disponíveis em que data será mostrada na tabela de pontos de recuperação abaixo de recuperação de saudação. Olá **tempo** coluna indica o tempo de saudação no qual Olá o instantâneo foi tirado. Olá **tipo** coluna exibe o saudação [consistência](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) saudação do ponto de recuperação. cabeçalho da tabela Olá mostra o número de saudação de pontos de recuperação disponíveis naquele dia entre parênteses.

    ![Pontos de Recuperação](./media/backup-azure-restore-vms/recovery-points.png)
3. Selecione o ponto de recuperação de saudação do hello **pontos de recuperação** tabela e clique em Olá próxima seta toogo toohello próxima tela.

### <a name="step-3-specify-a-destination-location"></a>Etapa 3: Especifique um local de destino
1. Em Olá **Selecione Restaurar instância** tela especificar detalhes de onde toorestore Olá a máquina virtual.

   * Especifique o nome da máquina virtual Olá: em um determinado serviço de nuvem, nome da máquina virtual Olá deve ser exclusivo. Não há suporte para substituição de VM existente.
   * Selecione um serviço de nuvem para Olá VM: isso é obrigatório para a criação de uma máquina virtual. Você pode escolher tooeither use um serviço de nuvem existente ou criar um novo serviço de nuvem.

        Qualquer nome de serviço de nuvem escolhido deve ser globalmente exclusivo. Normalmente, o nome de serviço de nuvem Olá é associado um URL público na forma de saudação de [cloudservice]. cloudapp.net. Azure não permitirá que você toocreate um novo serviço de nuvem se Olá nome já foi usado. Se você escolher toocreate um novo serviço de nuvem, ela será determinada Olá mesmo nome como máquina virtual de hello – quais Olá caso VM nome escolhido deve ser serviço de nuvem exclusivo suficiente toobe aplicada toohello associado.

        Podemos exibir apenas os serviços de nuvem e redes virtuais que não estão associadas a quaisquer grupos de afinidade de saudação restauração detalhes da instância. [Saiba mais](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Selecione uma conta de armazenamento para Olá VM: isso é obrigatório para a criação de saudação VM. Você pode selecionar contas de armazenamento existentes em Olá mesmo região Olá Cofre de Backup do Azure. Não há suporte para contas de armazenamento com redundância de zona ou do tipo de armazenamento Premium.

    Se não houver nenhuma conta de armazenamento com configuração com suporte, crie uma conta de armazenamento da operação de restauração anterior toostarting configuração com suporte.

    ![Selecione uma rede virtual](./media/backup-azure-restore-vms/restore-sa.png)
3. Selecione uma rede Virtual: Olá VPN (rede virtual) para máquina virtual de saudação deve ser selecionada no momento de saudação da criação Olá VM. Olá restaurar da interface do usuário mostra todas as VNETs Olá sob essa assinatura que pode ser usado. Não é obrigatório tooselect uma rede virtual para Olá restaurado VM – você será capaz de tooconnect toohello restaurado VM sobre Olá internet mesmo se hello rede virtual não é aplicada.

    Se Olá nuvem serviço selecionado está associado uma rede virtual, e em seguida, você não pode alterar a rede virtual hello.

    ![Selecione uma rede virtual](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Selecione uma sub-rede: no caso de Olá VNET tiver sub-redes, por padrão sub-rede primeiro Olá será selecionado. Escolha opções de lista suspensa de Olá sub-rede Olá de sua escolha. Para obter detalhes de sub-rede, vá tooNetworks extensão em Olá [home page do portal](https://manage.windowsazure.com/), ir muito**redes virtuais** e Olá selecione uma rede virtual e aprofundar nos detalhes de sub-rede toosee configurar.

    ![Selecione uma sub-rede](./media/backup-azure-restore-vms/select-subnet.png)
5. Clique em Olá **enviar** ícone Olá Assistente toosubmit Olá detalhes e criar um trabalho de restauração.

## <a name="track-hello-restore-operation"></a>Controlar a operação de restauração Olá
Depois de todas as informações de saudação no Assistente de restauração de saudação de entrada e enviou o Backup do Azure tentará toocreate uma operação de restauração do trabalho tootrack hello.

![Criando um trabalho de restauração](./media/backup-azure-restore-vms/create-restore-job.png)

Se a criação de trabalho Olá for bem-sucedida, você verá uma notificação de notificação do sistema indicando que o trabalho Olá é criado. Você pode obter mais detalhes clicando Olá **Exibir trabalho** botão que levará muito**trabalhos** guia.

![Trabalho de restauração criado](./media/backup-azure-restore-vms/restore-job-created.png)

Após a conclusão da operação de restauração de hello, ele será marcado como concluído em **trabalhos** guia.

![Trabalho de restauração concluído](./media/backup-azure-restore-vms/restore-job-complete.png)

Depois de restaurar Olá a máquina virtual, talvez seja necessário toore-instalar extensões de saudação existente no hello VM original e [modificar pontos de extremidade Olá](../virtual-machines/windows/classic/setup-endpoints.md) da máquina virtual Olá Olá portal do Azure.

## <a name="post-restore-steps"></a>Etapas de pós-restauração
Se você estiver usando uma distribuição do Linux baseada em inicialização da nuvem, como o Ubuntu, a senha será bloqueada após a restauração por motivos de segurança. Por favor, use a extensão VMAccess em Olá restaurado VM muito[redefinição da senha Olá](../virtual-machines/linux/classic/reset-access.md). É recomendável usar as chaves de SSH nesses tooavoid distribuições Redefinir senha postagem de restauração.

## <a name="backup-for-restored-vms"></a>Backup de VMs restauradas
Se você tiver restaurado o serviço de nuvem VM toosame com hello mesmo nome como originalmente backup de VM, backup continuará em Olá restauração de postagem VM. Se você tiver restaurado o serviço de nuvem diferente de tooa VM ou especificou um nome diferente para a VM restaurada, isso será tratado como uma nova VM e você precisará de toosetup para a VM restaurada.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restaurando uma máquina virtual durante desastres de data center do Azure
O Backup do Azure permite restaurar backup Centro de dados par toohello VMs no caso de dados primários Olá center onde VMs estão sendo executadas em experiências de desastre e configurado toobe de Cofre de Backup com redundância geográfica. Durante esses cenários, você precisa tooselect uma conta de armazenamento que está presente no datacenter emparelhado e restante do processo de restauração de saudação permanece o mesmo. Backup do Azure usa o serviço de computação da máquina virtual do par geográfica toocreate Olá restaurado. Saiba mais sobre [Resiliência do data center do Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restaurando VMs do controlador de domínio
O backup de máquinas virtuais de controlador de domínio (DC) é um cenário com suporte no Backup do Azure. No entanto, deve ter cuidado durante o processo de restauração hello. processo de restauração correta Olá depende da estrutura de saudação do domínio de saudação. No caso mais simples de saudação você tem um único controlador de domínio em um único domínio. Mais comumente para cargas de produção, você terá um único domínio com vários controladores de domínio, talvez com alguns controladores de domínio no local. Por fim, você pode ter uma floresta com vários domínios.

De uma saudação de perspectiva do Active Directory do Azure VM é como qualquer outra VM em um hipervisor com suporte moderno. Olá grande diferença com hipervisores do local é que nenhum console da VM está disponível no Azure. Um console é necessário para determinados cenários, como recuperação usando um backup do tipo de recuperação de Bare Metal (BMR). No entanto, a restauração de VM do Cofre de backup Olá é uma substituição completa para a BMR. Modo de restauração de diretório ativo (DSRM) também está disponível, portanto, todos os cenários de recuperação do Active Directory são viáveis. Para obter mais informações, consulte [as considerações de Backup e restauração para controladores de domínio virtualizado](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) e [Planejamento para Recuperação de Floresta do Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Controlador de domínio único em um único domínio
Olá VM pode ser restaurada (como qualquer outra VM) do hello Azure portal ou usando o PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Vários controladores de domínio em um único domínio
Quando outros controladores de domínio de saudação mesmo domínio pode ser acessado pela hello rede, Olá controlador de domínio pode ser restaurado como uma VM. Se for Olá último controlador de domínio restante no domínio hello, ou uma recuperação em uma rede isolada é executada, um procedimento de recuperação de floresta deve ser seguido.

### <a name="multiple-domains-in-one-forest"></a>Vários domínios em uma floresta
Quando outros controladores de domínio de saudação mesmo domínio pode ser acessado pela hello rede, Olá controlador de domínio pode ser restaurado como uma VM. No entanto, em todos os outros casos é recomendável uma recuperação de floresta.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Restaurando VMs com configurações de rede especiais
O Backup do Azure oferece suporte ao backup das seguintes configurações de rede especiais de máquinas virtuais.

* VMs no balanceador de carga (interno e externo)
* VMs com vários IPs reservados
* VMs com vários NICs

Essas configurações determinam as considerações a seguir ao restaurá-las.

> [!TIP]
> Use baseado em PowerShell restauração fluxo toorecreate Olá especial configuração de rede de VMs postagem de restauração.
>
>

### <a name="restoring-from-hello-ui"></a>A restauração de saudação da interface do usuário:
Ao restaurar da interface do usuário, **sempre escolha um novo serviço de nuvem**. . Observe que, desde que o portal usa apenas os parâmetros obrigatórios durante o fluxo de restauração, VMs restaurado usando a interface do usuário perderá configuração de rede especiais Olá que eles possuem. Em outras palavras, as VMs restauradas serão VMs normais sem a configuração do balanceador de carga ou de múltiplos NICs ou vários IP reservados.

### <a name="restoring-from-powershell"></a>Restaurando do PowerShell:
PowerShell tem Olá capacidade toojust restaurar discos de VM de saudação do backup e não criar a máquina virtual de saudação. Isso é útil ao restaurar máquinas virtuais que exigem as configurações de rede especiais mencionadas acima.

Em ordem toofully recriar post de máquina virtual Olá restauração de discos, siga estas etapas:

1. Restaurar discos de saudação do Cofre de backup usando [PowerShell de Backup do Azure](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Criar a configuração VM Olá necessária para o balanceador de carga / várias NIC/vários reservado IP usando Olá cmdlets do PowerShell e usá-lo toocreate Olá VM da configuração desejada.

   * Criar a VM no serviço de nuvem com o [balanceador de carga interno ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Criar VM tooconnect muito[Internet voltada para o balanceador de carga](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Criar uma VM [com várias NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Criar VMs com [vários IPs reservados](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Próximas etapas
* [Solucionar erros](backup-azure-vms-troubleshoot.md#restore)
* [Gerenciar máquinas virtuais](backup-azure-manage-vms.md)
