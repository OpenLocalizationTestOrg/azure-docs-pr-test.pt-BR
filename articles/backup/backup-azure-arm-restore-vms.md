---
title: "O Backup do Azure: Restaurar máquinas virtuais usando Olá portal do Azure | Microsoft Docs"
description: "Restaurar uma máquina virtual do Azure por um ponto de recuperação usando o portal do Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "restaurar o backup. como toorestore; ponto de recuperação;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Usar máquinas virtuais de toorestore portal do Azure
> [!div class="op_single_selector"]
> * [Restaurar VMs no portal Clássico](backup-azure-restore-vms.md)
> * [Restaurar VMs no portal do Azure](backup-azure-arm-restore-vms.md)
>
>

Proteja seus dados criando instantâneos de dados em intervalos definidos. Esses instantâneos são conhecidos como pontos de recuperação e são armazenados no cofre de serviços de recuperação. Se ou quando é necessário toorepair ou recriar uma VM, você pode restaurar Olá VM de qualquer um dos Olá salva pontos de recuperação. Quando você restaura um ponto de recuperação, você pode criar uma nova VM que é uma representação de point-in-time da VM backup, ou restaurar discos e usar modelo Olá que vem junto com ele toocustomize Olá restaurado VM ou fazer uma recuperação de arquivos individuais. Este artigo explica como toorestore tooa uma VM novas VMs ou discos de restauração todos os backups. Para a recuperação de arquivos individuais, consulte muito[recuperar arquivos de backup de VM do Azure](backup-azure-restore-files-from-vm.md)

![3-ways-restore-from-vm-backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo fornece informações hello e procedimentos para restaurar as VMs implantadas usando o modelo do Gerenciador de recursos de saudação.
>
>

A restauração de uma VM ou de todos os discos do backup de VM envolve duas etapas:

1. Selecionar um ponto de restauração para restauração
2. Selecionando Olá restaurar tipo - criar uma nova VM ou restaurar discos e especifique os parâmetros necessários. 

## <a name="select-restore-point-for-restore"></a>Selecionar ponto de restauração para restauração
1. Entrar toohello [portal do Azure](http://portal.azure.com/)
2. No hello Azure menu, clique em **procurar** e, na lista de saudação de serviços, digite **dos serviços de recuperação**. lista de saudação de serviços ajusta toowhat que você digitar. Quando você vir a opção **cofres de Serviços de Recuperação**, selecione-a.

    ![Abrir cofre de Serviços de Recuperação](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Olá lista de cofres na assinatura de saudação é exibida.

    ![Listar cofres de Serviços de Recuperação](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Na lista de hello, cofre Olá selecione associado Olá VM que você deseja toorestore. Quando você clica em um cofre hello, abre o painel.

    ![Listar cofres de Serviços de Recuperação](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Agora que você está no painel do cofre hello. Em Olá **itens de Backup** lado a lado, clique em **máquinas virtuais do Azure** toodisplay Olá VMs associadas cofre hello.

    ![painel do cofre](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Olá **itens de Backup** folha é aberta e exibe a lista de saudação de máquinas virtuais do Azure.

    ![lista de VMs no cofre](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Na lista de saudação, selecione um painel de saudação do tooopen VM. painel da máquina virtual Olá abre toohello área de monitoramento, que contém o bloco de pontos de restauração hello.

    ![lista de VMs no cofre](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. No menu do painel VM hello, clique em **restaurar**

    ![lista de VMs no cofre](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    Abre a folha de restauração Hello.

    ![restaurar folha](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Em Olá **restaurar** folha, clique em **ponto de restauração** tooopen Olá **selecionar restaurar ponto** folha.

    ![restaurar folha](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Por padrão, a caixa de diálogo Olá exibe todos os pontos de restauração do hello últimos 30 dias. Saudação de uso **filtro** exibidos de pontos de restauração do intervalo de tempo de saudação tooalter da saudação. Por padrão, são exibidos pontos de restauração de todas as consistências. Modificar **restaurar todos os pontos** filtrar tooselect uma consistência específicas de pontos de restauração. Para obter mais informações sobre cada tipo de ponto de restauração, consulte Explicação de saudação do [consistência dos dados](backup-azure-vms-introduction.md#data-consistency).  

   * **Consistência de pontos de restauração** nessa lista, escolha:
     * Pontos de restauração consistentes de falha,
     * Pontos de restauração consistentes do aplicativo,
     * Pontos de restauração consistentes de sistema de arquivos
     * Todos os pontos de restauração.  
8. Escolha um Ponto de restauração e clique em **OK**.

    ![escolha o ponto de restauração](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Olá **restaurar** folha mostra Olá ponto de restauração é definida.

    ![ponto de restauração definido](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Em Olá **restaurar** folha, **restaurar configuração** é aberta automaticamente após o ponto de restauração é definido.

## <a name="choosing-a-vm-restore-configuration"></a>Escolhendo uma configuração de restauração de VM
Agora que você selecionou um ponto de restauração hello, escolha uma configuração para a sua restauração VM. As opções de configuração Olá restaurado VM são toouse: portal do Azure ou o PowerShell.

1. Se você não ainda estiver lá, vá toohello **restaurar** folha. Certifique-se de um [ponto de restauração tiver sido selecionado](#select-restore-point-for-restore)e clique em **restaurar configuração** tooopen Olá **configuração de recuperação** folha.

    ![o assistente de configuração de recuperação está definido](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Em Olá **restaurar configuração** folha, você tem duas opções:
   * Restaurar a máquina virtual completa
   * Restaurar discos com backup

O portal fornece uma opção de criação rápida para a VM restaurada. Se você quiser configuração da VM Olá toocustomize ou nomes de recursos de saudação criados como parte de criar uma nova opção VM, use o PowerShell ou toorestore portal foi feito discos e o uso do PowerShell comandos tooattach toochoice de modelo de configuração ou uso VM que é fornecido com a restauração Olá de toocustomize discos restaurados VM. Consulte [restaurar uma máquina virtual com configurações de rede especiais](#restoring-vms-with-special-network-configurations) para obter detalhes sobre como toorestore VM que tem várias NICs ou sob o balanceador de carga. Se sua VM do Windows usa [HUB licenciamento](../virtual-machines/windows/hybrid-use-benefit-licensing.md), precisa toorestore discos e usar o PowerShell/modelo conforme especificado abaixo toocreate Olá VM e certifique-se de que você especificar LicenseType como "Windows_Server" durante a criação de VM tooavail HUB sobre os benefícios de VM restaurada. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Criar uma nova VM a partir do ponto de restauração
Se você não ainda estiver lá, [selecionar um ponto de restauração](#restoring-vms-with-special-network-configurations) antes de continuar toocreating uma nova VM da restauração do ponto. Depois que o ponto de restauração é selecionado no hello **restaurar configuração** folha, insira ou selecione valores para cada Olá campos a seguir:

* **Tipo de Restauração** – Criar máquina virtual.
* **Nome da máquina virtual** -forneça um nome para Olá VM. nome de saudação deve ser exclusivo toohello o grupo de recursos (para uma VM implantada para o Gerenciador de recursos) ou o serviço de nuvem (para uma VM clássico). Você não pode substituir Olá máquina de virtual se ela já existe na assinatura de saudação.
* **Grupo de recursos** – use um grupo de recursos existente ou crie um novo. Se você estiver restaurando uma VM clássico, use esse nome de saudação do toospecify de campo de um novo serviço de nuvem. Se você estiver criando um novo serviço de nuvem/grupo de recursos, o nome de saudação deve ser globalmente exclusivo. Normalmente, o nome de serviço de nuvem Olá é associado uma URL de público - por exemplo: [cloudservice]. cloudapp.net. Se você tentar toouse um nome para o serviço nuvem/grupo de recursos de nuvem de Olá que já foi usado, o serviço de nuvem/grupo de recursos do Azure atribui Olá Olá mesmo nome como Olá VM. O Azure exibe serviços de nuvem/grupos de recursos e VMs não associadas a nenhum grupo de afinidades. Para obter mais informações, consulte [como toomigrate de tooa de grupos de afinidade de rede Virtual Regional (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Rede virtual** - selecione Olá de rede virtual da saudação (VNET) durante a criação de VM. campo Olá fornece todas as VNETs associadas à assinatura hello. Grupo de recursos Olá VM é exibido entre parênteses.
* **Subrede** -se Olá VNET tiver sub-redes, sub-rede primeiro Olá é selecionada por padrão. Se houver sub-redes adicionais, selecione a sub-rede de saudação desejada.
* **Conta de armazenamento** -esse menu lista as contas de armazenamento Olá Olá Cofre de serviços de recuperação do mesmo local que hello. Não há suporte para as contas de armazenamento com Zona redundante. Se não houver nenhuma conta de armazenamento com hello mesmo local que Olá serviços de recuperação de cofre, você deve criar uma antes de iniciar a operação de restauração de saudação. tipo de replicação da conta de armazenamento Olá mencionado entre parênteses.

![assistente de configuração de restauração definido](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Se você estiver restaurando uma VM implantada pelo Gerenciador de Recursos, deverá identificar uma VNET (rede virtual). Uma VNET (rede virtual) é opcional para uma VM Clássica.
> 2. Se você estiver restaurando VMs como discos gerenciados, certifique-se de que a conta de armazenamento selecionada não está habilitada para o Storage Service Encryption (SSE) em seu tempo de vida.
> 3. Com base no tipo de armazenamento de saudação da conta de armazenamento selecionada (premium ou padrão), todos os discos restaurados será discos padrão ou premium. Atualmente não há suporte para o modo misto de discos durante a restauração.  
>
>

Em Olá **restaurar configuração** folha, clique em **Okey** toofinalize a configuração de restauração hello. Em Olá **restaurar** folha, clique em **restaurar** tootrigger operação de restauração de saudação.

## <a name="restore-backed-up-disks"></a>Restaurar discos com backup
Se você deseja que a máquina de virtual Olá toocustomize que deseja toocreate de backup de discos do que está presente na folha de configuração de restauração, selecione **restaurar discos** como o valor para **restauração do tipo**. Essa opção solicita uma conta de armazenamento na qual os discos de backups são copiados. Ao escolher uma conta de armazenamento, selecione uma conta que compartilhamentos Olá mesmo local como o Cofre de serviços de recuperação de saudação. Não há suporte para as contas de armazenamento com Zona redundante. Se não houver nenhuma conta de armazenamento com hello mesmo local que Olá serviços de recuperação de cofre, você deve criar uma antes de iniciar a operação de restauração de saudação. tipo de replicação da conta de armazenamento Olá mencionado entre parênteses.

Após a conclusão da operação de restauração, você pode:
* [Saudação de toocustomize do modelo de uso restaurados VM](#use-templates-to-customize-restore-vm)
* [Saudação de uso restaurados máquina tooan virtual existente tooattach discos](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Criar uma nova máquina virtual usando o PowerShell de discos restaurados.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Em Olá **restaurar configuração** folha, clique em **Okey** toofinalize a configuração de restauração hello. Em Olá **restaurar** folha, clique em **restaurar** tootrigger operação de restauração de saudação.

![Configuração de recuperação concluída](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Controlar a operação de restauração Olá
Depois que você acionar a operação de restauração hello, Olá serviço de Backup cria um trabalho para rastrear a operação de restauração de saudação. Olá serviço de Backup também cria e exibe temporariamente a notificação de saudação na área de notificações do portal. Se você não vir a notificação de hello, basta clicar Olá notificações ícone tooview as notificações.

![Restauração disparada](./media/backup-azure-arm-restore-vms/restore-notification.png)

tooview Olá operação durante o processamento ou tooview quando ele for concluído, abra a lista de trabalhos de Backup hello.

1. No hello Azure menu, clique em **procurar** e, na lista de saudação de serviços, digite **dos serviços de recuperação**. lista de saudação de serviços ajusta toowhat que você digitar. Quando você vir a opção **cofres de Serviços de Recuperação**, selecione-a.

    ![Abrir cofre de Serviços de Recuperação](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Olá lista de cofres na assinatura de saudação é exibida.

    ![Listar cofres de Serviços de Recuperação](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Na lista de saudação cofre Olá selecione associado Olá VM restaurada. Quando você clica em um cofre hello, abre o painel.
3. No painel do Cofre de saudação na Olá **trabalhos de Backup** lado a lado, clique em **máquinas virtuais do Azure** toodisplay trabalhos de saudação associados Olá cofre.

    ![painel do cofre](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Olá **trabalhos de Backup** folha é aberta e exibe a lista de saudação de trabalhos.

    ![lista de VMs no cofre](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Usar modelos toocustomize restauração vm
Uma vez [restauração discos é concluída](#Track-the-restore-operation), você pode usar o modelo de saudação que é gerado como parte da operação de restauração toocreate uma nova VM com uma configuração diferente de nomes de configuração ou toocustomize backup de recursos criado como criar uma nova vm do ponto de restauração. 

> [!NOTE]
> Os modelos serão adicionados como parte da Restauração de Discos para pontos de recuperação feitos após 1º de março de 2017. Eles são aplicáveis para VMs de disco não criptografado e não gerenciados. O suporte para VMs criptografadas e VMs de disco gerenciado estará disponível em versões futuras. 
>
>

modelo de saudação tooget gerado como parte da opção de discos de restauração

1. Vá toorestore detalhes do trabalho correspondente toohello trabalho. 
2. Na tela de detalhes do trabalho de restauração hello, clique em *implantar modelo* tooinitiate implantação de modelo de botão. 

     ![restaurar detalhamento de trabalho](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Na folha de modelo de implantação de Olá para implantação personalizada, use a implantação de modelo muito[editar e implante o modelo de saudação](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) ou acrescentar mais personalizações por [criando um modelo de](../azure-resource-manager/resource-group-authoring-templates.md) antes de implantar. 

   ![implantação por carregamento de modelo](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Depois de inserir valores hello necessários, aceite Olá *termos e condições* e clique em **compra**.

   ![implantação por envio de modelo](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Etapas de pós-restauração
* Se você estiver usando uma distribuição do Linux baseada em inicialização da nuvem, como o Ubuntu, a senha será bloqueada após a restauração por motivos de segurança. Por favor, use a extensão VMAccess em Olá restaurado VM muito[redefinição da senha Olá](../virtual-machines/linux/classic/reset-access.md). É recomendável usar as chaves de SSH nesses tooavoid distribuições Redefinir senha postagem de restauração.
* Extensões presentes durante a configuração de backup hello serão instaladas, no entanto, eles não serão ativados. Se você vir qualquer problema, reinstale as extensões. 
* Se Olá backup VM tem um IP estático, a restauração de post, VM restaurada terá um conflito de tooavoid IP dinâmico quando criar restaurado VM. Saiba mais sobre como você pode [adicionar um toorestored IP estático VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* A VM restaurada não terá o valor de disponibilidade definido. Recomendamos o uso da opção de discos de restauração e [adição do conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md) ao criar uma VM do PowerShell ou modelos usando discos restaurados. 


## <a name="backup-for-restored-vms"></a>Backup de VMs restauradas
Se você tiver restaurado o VM toosame grupo de recursos com hello mesmo nome como originalmente backup de VM, backup continua em Olá restauração de postagem VM. Se você tiver restaurado o grupo de recursos diferente do VM tooa ou especificou um nome diferente para a VM restaurada, isso é tratado como uma nova VM e você precisará de toosetup para a VM restaurada.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restaurando uma VM durante desastres de data center do Azure
O Backup do Azure permite restaurar backup Centro de dados par toohello VMs no caso de dados primários Olá center onde VMs estão sendo executadas em experiências de desastre e configurado toobe de Cofre de Backup com redundância geográfica. Durante esses cenários, você precisa tooselect uma conta de armazenamento, que está presente no datacenter emparelhado e restante do processo de restauração de saudação permanece o mesmo. Backup do Azure usa o serviço de computação da máquina virtual do par geográfica toocreate Olá restaurado. Saiba mais sobre [Resiliência do data center do Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restaurando VMs do controlador de domínio
O backup de máquinas virtuais de controlador de domínio (DC) é um cenário com suporte no Backup do Azure. No entanto, deve ter cuidado durante o processo de restauração hello. processo de restauração correta Olá depende da estrutura de saudação do domínio de saudação. No caso mais simples de saudação você tem um único controlador de domínio em um único domínio. Mais comumente para cargas de produção, você terá um único domínio com vários controladores de domínio, talvez com alguns controladores de domínio no local. Por fim, você pode ter uma floresta com vários domínios. 

De uma saudação de perspectiva do Active Directory do Azure VM é como qualquer outra VM em um hipervisor com suporte moderno. Olá grande diferença com hipervisores do local é que nenhum console da VM está disponível no Azure. Um console é necessário para determinados cenários, como recuperação usando um backup do tipo de recuperação de Bare Metal (BMR). No entanto, a restauração de VM do Cofre de backup Olá é uma substituição completa para a BMR. Modo de restauração de diretório ativo (DSRM) também está disponível, portanto, todos os cenários de recuperação do Active Directory são viáveis. Para obter mais informações, consulte [as considerações de Backup e restauração para controladores de domínio virtualizado](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) e [Planejamento para Recuperação de Floresta do Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Controlador de domínio único em um único domínio
Olá VM pode ser restaurada (como qualquer outra VM) do hello Azure portal ou usando o PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Vários controladores de domínio em um único domínio
Quando outros controladores de domínio de saudação mesmo domínio pode ser acessado pela hello rede, Olá controlador de domínio pode ser restaurado como uma VM. Se for Olá último controlador de domínio restante no domínio hello, ou uma recuperação em uma rede isolada é executada, um procedimento de recuperação de floresta deve ser seguido.

### <a name="multiple-domains-in-one-forest"></a>Vários domínios em uma floresta
Quando outros controladores de domínio de saudação mesmo domínio pode ser acessado pela hello rede, Olá controlador de domínio pode ser restaurado como uma VM. No entanto, em todos os outros casos é recomendável uma recuperação de floresta.

## <a name="restoring-vms-with-special-network-configurations"></a>Restaurando VMs com configurações de rede especiais
É possível tooback backup e restauração de VMs com hello configurações de rede especiais a seguir. No entanto, essas configurações requerem alguma consideração especial ao passar pelo processo de restauração de saudação.

* VMs no balanceador de carga (interno e externo)
* VMs com vários IPs reservados
* VMs com vários NICs

> [!IMPORTANT]
> Ao criar a configuração de rede especiais Olá para máquinas virtuais, você deve usar o PowerShell toocreate VMs de discos Olá restaurados.
>
>

máquinas de virtuais de saudação toofully recrie após a restauração toodisk, siga estas etapas:

1. Restaurar discos de saudação de um cofre de serviços de recuperação usando [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Criar a configuração de VM Olá necessária para o balanceador de carga / vários NIC/vários reservado IP usando Olá cmdlets do PowerShell e usá-lo toocreate Olá VM da configuração desejada.

   * Criar a VM no serviço de nuvem com o [balanceador de carga interno ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Criar VM tooconnect muito[Internet voltada para o balanceador de carga](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Criar uma VM [com várias NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Criar VMs com [vários IPs reservados](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Próximas etapas
Agora que você pode restaurar suas VMs, consulte Olá artigo para obter informações sobre erros comuns com máquinas virtuais de solução de problemas. Além disso, confira o artigo Olá sobre como gerenciar tarefas com suas VMs.

* [Solucionar erros](backup-azure-vms-troubleshoot.md#restore)
* [Gerenciar máquinas virtuais](backup-azure-manage-vms.md)
