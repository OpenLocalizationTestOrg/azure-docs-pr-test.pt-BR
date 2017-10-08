---
title: "aaaBack o Cofre de backup de tooa implantado clássico máquinas de virtuais do Azure | Microsoft Docs"
description: "Descubra suas máquinas virtuais, registre-as e faça backup delas com estes procedimentos para o backup de máquina virtual do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup de máquinas virtuais; fazer backup de máquina virtual, backup e recuperação de desastre; backup de vm"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Fazer backup de máquinas virtuais do Azure (portal clássico)
> [!div class="op_single_selector"]
> * [Fazer backup de Cofre de serviços de tooRecovery de VMs](backup-azure-arm-vms.md)
> * [Fazer backup de máquinas virtuais tooBackup cofre](backup-azure-vms.md)
>
>

Este artigo fornece procedimentos hello para fazer backup de um cofre de Backup tooa implantado clássico do Azure VM (máquina virtual). Há algumas tarefas que você precisa tootake aos cuidados de antes de você pode fazer backup de uma máquina virtual do Azure. Se você ainda não tiver feito Olá completa, portanto, [pré-requisitos](backup-azure-vms-prepare.md) tooprepare seu ambiente para fazer backup de suas VMs.

Para obter mais informações, consulte os artigos de saudação em [Planejando sua infra-estrutura de backup de VM no Azure](backup-azure-vms-introduction.md) e [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Um cofre de Backup só pode proteger VMs com implantação clássica. Você não pode proteger VMs implantadas pelo Resource Manager com um cofre de Backup. Consulte [VMs tooRecovery serviços Cofre de backup](backup-azure-arm-vms.md) para obter detalhes sobre como trabalhar com serviços de recuperação os cofres.
>
>

Fazer o backup de máquinas virtuais do Azure envolve três etapas principais:

![Três etapas tooback a uma máquina virtual IaaS do Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> O backup de máquinas virtuais é um processo local. Você não pode fazer backup de máquinas virtuais em uma região tooa Cofre de backup em outra região. Portanto, você deve criar um cofre de backup em cada região do Azure na qual existam VMs das quais serão feitos backups.
>
> [!IMPORTANT]
> A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
>- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Etapa 1 - Descobrir máquinas virtuais do Azure
tooensure qualquer nova assinatura adicionado toohello máquinas virtuais (VMs) são identificados antes de registrar, executar o processo de descoberta de saudação. Olá processar consultas do Azure para obter lista de saudação de máquinas virtuais na assinatura hello, juntamente com informações adicionais, como nome de serviço de nuvem hello e região Olá.

1. Entrar toohello [portal clássico](http://manage.windowsazure.com/)
2. Na lista de saudação de serviços do Azure, clique em **dos serviços de recuperação** tooopen lista de saudação de cofres de Backup e recuperação de Site.
    ![Abrir listas de cofres](./media/backup-azure-vms/choose-vault-list.png)
3. Na lista de saudação de cofres de Backup, selecione Olá cofre tooback backup de uma VM.

    Se esse for um novo portal de saudação do cofre abre toohello **início rápido** página.

    ![Abrir o menu Itens registrados](./media/backup-azure-vms/vault-quick-start.png)

    Se o cofre Olá tenha sido previamente configurada, o portal de saudação abre o menu de toohello usado mais recentemente.
4. No menu de cofre hello (na parte superior de saudação da página de saudação), clique em **itens registrados**.

    ![Abrir o menu Itens registrados](./media/backup-azure-vms/vault-menu.png)
5. De saudação **tipo** menu, selecione **Máquina Virtual do Azure**.

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
6. Clique em **DISCOVER** final Olá Olá página.
    ![Botão Descobrir](./media/backup-azure-vms/discover-button-only.png)

    o processo de descoberta Olá pode levar alguns minutos enquanto estão sendo tabuladas máquinas virtuais de saudação. Há uma notificação na parte inferior da saudação da tela de saudação que permite que você saiba que o processo de hello está sendo executado.

    ![Descobrir VMs](./media/backup-azure-vms/discovering-vms.png)

    Olá notificação muda quando Olá processo for concluído. Se o processo de descoberta de saudação não localizou máquinas virtuais de hello, primeiro verifique Olá VMs. Se houver VMs hello, certifique-se de Olá VMs estão em Olá mesmo região Olá Cofre de backup. Se as VMs de saudação existem e estão em Olá mesma região, certifique-se de que VMs Olá ainda não estiverem registrados tooa Cofre de backup. Se uma VM for atribuído tooa Cofre de backup não é disponível toobe atribuído tooother cofres de backup.

    ![Descoberta concluída](./media/backup-azure-vms/discovery-complete.png)

    Depois que você descobriu novos itens de hello, vá tooStep 2 e registrar suas VMs.

## <a name="step-2---register-azure-virtual-machines"></a>Etapa 2 - Registrar as máquinas virtuais do Azure
Registrar tooassociate uma máquina virtual do Azure com hello serviço Backup do Azure. Normalmente, é uma atividade realizada uma única vez.

1. Navegue toohello Cofre de backup em **dos serviços de recuperação** Olá portal do Azure e, em seguida, clique em **itens registrados**.
2. Selecione **Máquina Virtual do Azure** do menu suspenso de saudação.

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
3. Clique em **registrar** final Olá Olá página.
    ![Botão Registrar](./media/backup-azure-vms/register-button-only.png)
4. Em Olá **registrar itens** menu de atalho, selecione Olá máquinas de virtuais que você deseja tooregister. Se houver dois ou mais máquinas virtuais com hello mesmo nome, use toodistinguish de serviço de nuvem Olá entre eles.

   > [!TIP]
   > Várias máquinas virtuais podem ser registradas ao mesmo tempo.
   >
   >

    Um trabalho é criado para cada máquina virtual selecionada.
5. Clique em **Exibir trabalho** em Olá notificação toogo toohello **trabalhos** página.

    ![Registrar trabalho](./media/backup-azure-vms/register-create-job.png)

    máquina virtual de saudação também aparece na lista de saudação de itens registrados, junto com o status de saudação da operação de registro de saudação.

    ![Status de registro 1](./media/backup-azure-vms/register-status01.png)

    Quando Olá operação for concluída, o status de saudação muda Olá tooreflect *registrado* estado.

    ![Status de registro 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Etapa 3 - Proteger máquinas virtuais do Azure
Agora você pode configurar uma política de backup e retenção para a máquina virtual de saudação. Várias máquinas virtuais podem ser protegidas usando uma única ação de proteção.

Os cofres de Backup do Azure criados depois de maio de 2015 vem com uma política padrão incorporados cofre hello. Essa política padrão é fornecida com uma retenção padrão de 30 dias e agendamento de backup de uma vez por dia.

1. Navegue toohello Cofre de backup em **dos serviços de recuperação** Olá portal do Azure e, em seguida, clique em **itens registrados**.
2. Selecione **Máquina Virtual do Azure** do menu suspenso de saudação.

    ![Selecionar a carga de trabalho no portal](./media/backup-azure-vms/select-workload.png)
3. Clique em **proteger** final Olá Olá página.

    Olá **proteger itens assistente** é exibida. Assistente de saudação lista apenas máquinas virtuais que são registradas e não protegidas. Selecione a saudação de máquinas virtuais que você deseja tooprotect.

    Se houver dois ou mais máquinas virtuais com hello mesmo nome, use toodistinguish de serviço de nuvem Olá entre máquinas virtuais de saudação.

   > [!TIP]
   > Você pode proteger várias máquinas virtuais de uma só vez.
   >
   >

    ![Configurar proteção em escala](./media/backup-azure-vms/protect-at-scale.png)

4. Escolha um **agendamento de backup** tooback backup de máquinas virtuais Olá que você selecionou. Escolha um conjunto existente de políticas ou defina um novo.

    Cada política de backup pode ter várias máquinas virtuais associadas a ela. No entanto, máquina virtual de saudação só pode ser associada com uma política em qualquer ponto no tempo.

    ![Proteger com nova política](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Uma política de backup inclui um esquema de retenção para backups agendado de saudação. Se você selecionar uma política de backup existente, você não pode modificar as opções de retenção de saudação na próxima etapa do hello.
   >
   >

5. Escolha um **período de retenção** tooassociate com backups de saudação.

    ![Proteger com retenção flexível](./media/backup-azure-vms/policy-retention.png)

    Política de retenção Especifica Olá período de tempo para armazenar um backup. Você pode especificar diferentes políticas de retenção com base em quando é feito backup hello. Por exemplo, um ponto de backup feito diariamente (que funciona como um ponto de recuperação operacional) pode ser preservado durante 90 dias. Em comparação, um ponto de backup feito no final de saudação de cada trimestre (para fins de auditoria) talvez seja necessário toobe preservado para muitos meses ou anos.

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/long-term-retention.png)

    Nesta imagem de exemplo:

   * **Política de retenção diária**: os backups diários são armazenados por 30 dias.
   * **Política de retenção semanal**: os backups feitos todas as semanas aos domingos serão preservados por 104 semanas.
   * **Política de retenção mensal**: Backups feitos em Olá último domingo de cada mês são preservados para 120 meses.
   * **Política de retenção anual**: Backups feitos em Olá primeiro domingo de cada janeiro são preservados para 99 anos.

     Um trabalho é criado a política de proteção tooconfigure hello e associar a política de toothat Olá máquinas virtuais para cada máquina virtual que você selecionou.
6. lista de saudação tooview de **configurar proteção** trabalhos, no menu de cofres hello, clique em **trabalhos** e selecione **configurar proteção** de saudação **operação**  filtro.

    ![Configurar o trabalho de proteção](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Backup inicial
Depois que a máquina virtual de saudação é protegida com uma política, ele é exibido em Olá **itens protegidos** guia com o status de saudação do *protegido - (pendente backup inicial)*. Por padrão, o primeiro backup agendado de saudação é Olá *backup inicial*.

backup inicial de saudação de tootrigger imediatamente após a configuração de proteção:

1. Na parte inferior de saudação do hello **itens protegidos** , clique em **Backup agora**.

    Olá serviço Backup do Azure cria um trabalho de backup para a operação de backup inicial hello.
2. Clique em Olá **trabalhos** lista de saudação do guia tooview de trabalhos.

    ![Backup em andamento](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Durante a operação de backup Olá Olá serviço Backup do Azure emite uma extensão de backup comando toohello em tooflush cada máquina virtual, todos os trabalhos de gravação e tirar um instantâneo consistente.
>
>

Quando saudação inicial conclusão do backup, status de saudação da máquina virtual Olá Olá **itens protegidos** guia *protegidos*.

![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Exibindo detalhes e status do backup
Depois de protegido, contagem de máquina virtual Olá também aumenta em Olá **painel** página resumida. Olá **painel** página também mostra o número de saudação de trabalhos de saudação últimas 24 horas que foram *bem-sucedida*, ter *falha*e são *em andamento*. Em Olá **trabalhos** página, use Olá **Status**, **operação**, ou **de** e **para** toofilter menus trabalhos de saudação.

![Status do backup na página Painel](./media/backup-azure-vms/dashboard-protectedvms.png)

Os valores no painel de saudação são atualizados uma vez a cada 24 horas.

## <a name="troubleshooting-errors"></a>Solucionar erros
Se você tiver problemas durante a cópia sua máquina virtual, examine a saudação [artigo de solução de problemas de VM](backup-azure-vms-troubleshoot.md) para obter ajuda.

## <a name="next-steps"></a>Próximas etapas
* [Gerenciar e monitorar suas máquinas virtuais](backup-azure-manage-vms.md)
* [Restaurar máquinas virtuais](backup-azure-restore-vms.md)
