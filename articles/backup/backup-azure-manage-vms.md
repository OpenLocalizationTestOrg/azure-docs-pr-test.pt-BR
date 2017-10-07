---
title: "backups de máquina de virtual implantada para o Gerenciador de recursos de aaaManage | Microsoft Docs"
description: "Saiba como toomanage e monitor de backups de máquina de virtual implantada para o Gerenciador de recursos"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Gerenciar backups de máquinas virtuais do Azure
> [!div class="op_single_selector"]
> * [Gerenciar backups da VM do Azure](backup-azure-manage-vms.md)
> * [Gerenciar backups de VMs clássicas](backup-azure-manage-vms-classic.md)
>
>

Este artigo fornece orientação sobre como gerenciar backups VM e explica as informações de alertas de backup Olá disponíveis no painel do portal hello. diretrizes de saudação neste artigo se aplicam a toousing VMs com os cofres de serviços de recuperação. Este artigo não aborda a criação de saudação de máquinas virtuais, nem explicam como máquinas virtuais de tooprotect. Para um livro de instruções sobre como proteger VMs do Azure Resource Manager implantados no Azure com um cofre de serviços de recuperação, consulte [primeiro olhar: fazer backup de máquinas virtuais tooa Cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Gerenciar cofres e máquinas virtuais protegidas
Olá portal do Azure, painel de Cofre de serviços de recuperação de saudação fornece acesso tooinformation sobre Olá cofre, inclusive:

* Olá mais recente backup de instantâneo, que também é o ponto de restauração mais recente hello < br\>
* Olá a política de backup < br\>
* tamanho total de todos os instantâneos do backup <br\>
* número de máquinas virtuais que são protegidas com o cofre hello < br\>

Muitas tarefas de gerenciamento com um backup de máquinas virtuais começam com abrindo Olá cofre no painel de saudação. No entanto, como cofres podem ser usado tooprotect tooview detalhes sobre uma determinada VM, abrem vários itens (ou várias VMs), painel de item de cofre hello. Olá procedimento a seguir mostra como Olá tooopen *painel Cofre* e, em seguida, continue toohello *painel Cofre de item*. Há "dicas" nos dois procedimentos que destacam como tooadd Olá cofre e cofre toohello de item do painel do Azure usando o comando de toodashboard Olá Pin. Toodashboard de PIN é uma maneira de criar um cofre do atalho toohello ou item. Você também pode executar comandos comuns do atalho hello.

> [!TIP]
> Se você tiver vários painéis e abrir folhas, use o controle deslizante de azul escuro Olá final Olá Olá Olá de tooslide da janela do painel do Azure e para trás.
>
>

![Exibição completa com controle deslizante](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Abra um cofre de serviços de recuperação no painel de saudação:
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **procurar** e, na lista de saudação de recursos, digite **dos serviços de recuperação**. Como começar a digitar, Olá filtros de lista com base em sua entrada. Clique em **Cofre dos Serviços de Recuperação**.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    saudação de lista de cofres de serviços de recuperação é exibida.

    ![Listar cofres de Serviços de Recuperação ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Se você fixar um painel do Azure de toohello do cofre, esse cofre é imediatamente acessível quando você abre Olá portal do Azure. toopin um painel de toohello do cofre, na lista de cofre hello, cofre hello e selecione **toodashboard Pin**.
   >
   >
3. Saudação de cofres, selecione lista Olá cofre tooopen seu painel. Quando você seleciona o cofre hello, painel de cofre hello e Olá **configurações** folha aberta. Em Olá a imagem a seguir, Olá **Contoso cofre** painel é realçado.

    ![Abrir o painel do cofre e a folha de Configurações](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Abra o painel do item do cofre
No procedimento anterior Olá você abriu o painel Cofre de saudação. Painel de item do tooopen Olá cofre:

1. No painel do cofre hello, em Olá **itens de Backup** lado a lado, clique em **máquinas virtuais do Azure**.

    ![Bloco Abrir itens de backup](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Olá **itens de Backup** Olá último backup trabalho para cada item de lista de folha. Neste exemplo, há uma máquina virtual, demovm-markgal, protegida por esse cofre.  

    ![Bloco Itens de backup](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > Para facilidade de acesso, você pode fixar um item de cofre toohello painel do Azure. toopin um item de cofre, na lista de itens de cofre hello, item de saudação do botão direito do mouse e selecione **toodashboard Pin**.
   >
   >
2. Em Olá **itens de Backup** folha, clique em Painel de item Olá item tooopen Olá cofre.

    ![Bloco Itens de backup](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    Painel de item de cofre Hello e sua **configurações** folha aberta.

    ![Painel dos itens de backup com a folha Configurações](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    No painel de item de cofre hello, você pode executar várias tarefas de gerenciamento de chaves, como:

   * alterar as políticas ou criar uma nova política de backup <br\>
   * exibir pontos de restauração e ver seu estado de consistência <br\>
   * Backup sob demanda de uma máquina virtual <br\>
   * interromper a proteção das máquinas virtuais <br\>
   * retomar a proteção de uma máquina virtual <br\>
   * excluir os dados do backup (ou ponto de recuperação) <br\>
   * [restaurar discos de backup](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\>

Olá procedimentos a seguir, Olá ponto de partida é painel de item de cofre hello.

## <a name="manage-backup-policies"></a>Gerenciar políticas de backup
1. Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **todas as configurações** tooopen Olá **configurações** folha.

    ![Folha Política de backup](./media/backup-azure-manage-vms/all-settings-button.png)
2. Em Olá **configurações** folha, clique em **política de Backup** tooopen folha.

    Na folha de Olá, Olá retenção e frequência de intervalo detalhes de backup são mostradas.

    ![Folha Política de backup](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. De saudação **escolha a política de backup** menu:

   * políticas de toochange, selecione outra política e clique em **salvar**. nova política de saudação é aplicada imediatamente toohello cofre. <br\>
   * toocreate uma política, selecione **criar novo**.

     ![Backup de máquinas virtuais](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Para obter instruções sobre como criar uma política de backup, consulte [Definindo uma política de backup](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Ao gerenciar políticas de backup, verifique se Olá de toofollow [práticas recomendadas](backup-azure-vms-introduction.md#best-practices) para desempenho ideal de backup
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Backup sob demanda de uma máquina virtual
Você pode obter um backup sob demanda de uma máquina virtual quando ela estiver configurada para proteção. Se o backup de saudação inicial está pendente, o backup por demanda cria uma cópia completa da máquina virtual de saudação em Olá que Cofre de serviços de recuperação. Se o backup de saudação inicial for concluída, um backup sob demanda enviará apenas as alterações do instantâneo anterior hello, toohello Cofre de serviços de recuperação. Ou seja, os backups subsequentes serão sempre incrementais.

> [!NOTE]
> período de retenção de saudação para um backup sob demanda é o valor de retenção de saudação especificado para o ponto de backup diário Olá na política de saudação. Se nenhum ponto de backup diário é selecionado, o ponto de backup semanal Olá é usado.
>
>

backup tootrigger uma demanda de uma máquina virtual:

* Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **Backup agora**.

    ![Botão Fazer backup agora](./media/backup-azure-manage-vms/backup-now-button.png)

    portal de saudação certifica-se de que você deseja toostart um trabalho de backup sob demanda. Clique em **Sim** trabalho de backup toostart hello.

    ![Botão Fazer backup agora](./media/backup-azure-manage-vms/backup-now-check.png)

    trabalho de backup Olá cria um ponto de recuperação. período de retenção Olá Olá do ponto de recuperação é Olá mesmo que o período de retenção especificado na diretiva de saudação associada à máquina virtual hello. progresso de saudação tootrack para trabalho hello, no painel do cofre hello, clique em Olá **trabalhos de Backup** lado a lado.  

## <a name="stop-protecting-virtual-machines"></a>Interromper a proteção de máquinas virtuais
Se você escolher toostop proteger uma máquina virtual, você será solicitado a se quiser que os pontos de recuperação tooretain hello. Há duas maneiras de máquinas virtuais da proteção toostop:

* parar todos os trabalhos de backup futuros e excluir todos os pontos de recuperação ou
* parar todos os trabalhos de backup futuros, mas deixar Olá pontos de recuperação <br/>

Há um custo associado deixando Olá pontos de recuperação no armazenamento. No entanto, a vantagem de saudação do deixando Olá pontos de recuperação é que você pode restaurar a máquina virtual de hello mais tarde, se desejado. Para obter informações sobre o custo de saudação de deixar Olá pontos de recuperação, consulte Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/backup/). Se você escolher toodelete todos os pontos de recuperação, é possível restaurar a máquina virtual de saudação.

proteção de toostop para uma máquina virtual:

1. Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **parar backup**.

    ![Botão Interromper backup](./media/backup-azure-manage-vms/stop-backup-button.png)

    Abre a folha de parar Backup Hello.

    ![Folha Interromper backup](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. Em Olá **parar Backup** folha, escolha se tooretain ou delete Olá dados de backup. caixa de informações de saudação fornece detalhes sobre sua escolha.

    ![Parar a proteção](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Se você escolher os dados de backup tooretain hello, ignore toostep 4. Se você escolher os dados de backup toodelete, confirme que você deseja toostop trabalhos de backup hello e excluir pontos de recuperação Olá - nome de saudação do tipo de item de saudação.

    ![Interromper verificação](./media/backup-azure-manage-vms/item-verification-box.png)

    Se você não tiver certeza do nome do item hello, passe o mouse sobre o nome de Olá Olá exclamação tooview. Além disso, o nome de saudação do item de saudação é em **parar Backup** na parte superior de saudação da folha de saudação.
4. Como opção, forneça um **Motivo** ou **Comentário**.
5. trabalho de backup toostop Olá para o item atual do hello, clique em ![botão backup parar](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Uma mensagem de notificação permite que você saiba os trabalhos de backup Olá foram interrompidos.

    ![Confirmar a interrupção da proteção](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Retomar a proteção de uma máquina virtual
Se hello **reter dados de Backup** opção foi escolhida quando a proteção para a máquina virtual de saudação foi interrompida, é possível tooresume proteção. Se hello **excluir dados de Backup** opção foi escolhida, então não é possível retomar a proteção para a máquina virtual de saudação.

tooresume proteção para a máquina virtual de saudação

1. Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **retomar backup**.

    ![Retomar proteção](./media/backup-azure-manage-vms/resume-backup-button.png)

    Abre a folha de política de Backup de saudação.

   > [!NOTE]
   > Ao proteger novamente a máquina virtual de hello, você pode escolher uma regra diferente que a política de saudação com a qual a máquina virtual foi inicialmente protegida.
   >
   >
2. Siga as etapas de saudação em [gerenciar políticas de backup](backup-azure-manage-vms.md#manage-backup-policies) tooassign política de saudação para a máquina virtual de saudação.

    Após a política de backup Olá toohello aplicada virtual machine, você verá a seguinte mensagem de saudação.

    ![VM protegida com êxito](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Excluir dados de backup
Você pode excluir os dados de backup Olá associados a uma máquina virtual durante a saudação **parar backup** trabalho, ou a qualquer momento após Olá o trabalho de backup foi concluída. Ainda pode ser benéfico toowait dias ou semanas antes da exclusão de pontos de recuperação de saudação. Ao contrário de restaurar os pontos de recuperação, ao excluir dados de backup, você não pode escolher toodelete de pontos de recuperação específico. Se você escolher toodelete os dados de backup, você pode excluir todos os pontos de recuperação associados ao item de saudação.

Olá seguinte princípio de trabalho de Backup Olá para a máquina virtual de saudação foi interrompido ou desabilitado. Depois que o trabalho de Backup Olá estiver desabilitado, Olá **retomar backup** e **excluir backup** opções estão disponíveis no painel de item de cofre hello.

![Botões para retomar e excluir](./media/backup-azure-manage-vms/resume-delete-buttons.png)

dados de backup toodelete em uma máquina virtual com hello *Backup desabilitado*:

1. Em Olá [painel Cofre de item](backup-azure-manage-vms.md#open-a-vault-item-dashboard), clique em **excluir backup**.

    ![Tipo de VM](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Olá **excluir dados de Backup** folha é aberta.

    ![Tipo de VM](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Nome do tipo de saudação de Olá item tooconfirm você deseja que os pontos de recuperação toodelete hello.

    ![Interromper verificação](./media/backup-azure-manage-vms/item-verification-box.png)

    Se você não tiver certeza do nome do item hello, passe o mouse sobre o nome de Olá Olá exclamação tooview. Além disso, o nome de saudação do item de saudação é em **excluir dados de Backup** na parte superior de saudação da folha de saudação.
3. Como opção, forneça um **Motivo** ou **Comentário**.
4. os dados de backup toodelete Olá para o item atual do hello, clique em ![botão backup parar](./media/backup-azure-manage-vms/delete-button.png)

    Uma mensagem de notificação permite que você saiba os dados de backup Olá foi excluídos.

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre como recriar uma máquina virtual a partir de um ponto de recuperação, verifique [Restaurar VMs do Azure](backup-azure-restore-vms.md). Se você precisar obter informações sobre como proteger suas máquinas virtuais, consulte [primeiro olhar: fazer backup de máquinas virtuais tooa Cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md). Para obter informações sobre o monitoramento de eventos, confira [Monitorar alertas para backups de máquina virtual do Azure](backup-azure-monitor-vms.md).
