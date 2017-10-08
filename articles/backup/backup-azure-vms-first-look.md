---
title: "Introdução - Fazer backup de VMs do Azure com um cofre de backup | Microsoft Docs"
description: "Use tooback de portal clássico Olá o Cofre de Backup tooa VMs do Azure. Este tutorial explica todas as fases, incluindo criar Cofre de Backup hello, registrar Olá VMs, criar política de backup e executar o trabalho de backup inicial hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>Introdução: Fazendo backup de máquinas virtuais do Azure
> [!div class="op_single_selector"]
> * [Proteger VMs em um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md)
> * [Proteger as VMs do Azure com um cofre de backup](backup-azure-vms-first-look.md)
>
>

Este tutorial descreve as etapas de saudação para fazer backup de um cofre de backup tooa máquina virtual do Azure (VM) no Azure. Este artigo descreve o modelo clássico hello ou modelo de implantação do Service Manager, para fazer backup de máquinas virtuais. Olá etapas a seguir se aplicam somente cofres tooBackup criados no portal clássico do hello. A Microsoft recomenda usando o modelo do Gerenciador de recursos de saudação para novas implantações.

Se você estiver interessado em um cofre de serviços de recuperação de tooa VM que pertença tooa grupo de recursos de backup, consulte [primeiro olhar: proteger VMs com um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).

toosuccessfully concluir seguinte Olá tutorial, estes pré-requisitos devem existir:

* Você criou uma VM em sua assinatura do Azure.
* Olá VM tem endereços IP públicos de tooAzure conectividade. Para obter informações adicionais, veja [Conectividade de rede](backup-azure-vms-prepare.md#network-connectivity).


> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este tutorial é para uso com máquinas virtuais criadas no portal clássico do hello.
>
>

## <a name="create-a-backup-vault"></a>Criar um cofre de backup
Um cofre de backup é uma entidade que armazena todos os backups de saudação e pontos de recuperação que foram criados ao longo do tempo. Cofre de backup Olá também contém Olá as políticas de backup que estão sendo feitas backup de máquinas virtuais toohello aplicado.

> [!IMPORTANT]
> A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.
> Você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
>- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Descobrir e registrar máquinas virtuais do Azure
Antes de registrar Olá VM com um cofre, execute tooidentify de processo de descoberta de saudação novas VMs. Isso retorna uma lista de máquinas virtuais na assinatura hello, juntamente com informações adicionais, como o nome do serviço de nuvem hello e região hello.

1. Entrar toohello [portal clássico do Azure](http://manage.windowsazure.com/)
2. No portal clássico do Azure do hello, clique em **dos serviços de recuperação** tooopen lista de saudação de cofres de serviços de recuperação.
    ![Selecionar carga de trabalho](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. Saudação de cofres, selecione lista Olá cofre tooback backup de uma VM.

    Quando você seleciona o cofre, ele é aberto no hello **início rápido** página
4. No menu de cofre hello, clique em **itens registrados**.

    ![Selecionar carga de trabalho](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. De saudação **tipo** menu, selecione **Máquina Virtual do Azure**.

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
6. Clique em **DISCOVER** final Olá Olá página.
    ![Botão Descobrir](./media/backup-azure-vms/discover-button-only.png)

    o processo de descoberta Olá pode levar alguns minutos enquanto estão sendo tabuladas máquinas virtuais de saudação. Há uma notificação na parte inferior da saudação da tela de saudação que permite que você saiba que o processo de hello está sendo executado.

    ![Descobrir VMs](./media/backup-azure-vms/discovering-vms.png)

    Olá notificação muda quando Olá processo for concluído.

    ![Descoberta concluída](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Clique em **registrar** final Olá Olá página.
    ![Botão Registrar](./media/backup-azure-vms-first-look/register-icon.png)
8. Em Olá **registrar itens** menu de atalho, selecione Olá máquinas de virtuais que você deseja tooregister.

   > [!TIP]
   > Várias máquinas virtuais podem ser registradas ao mesmo tempo.
   >
   >

    Um trabalho é criado para cada máquina virtual selecionada.
9. Clique em **Exibir trabalho** em Olá notificação toogo toohello **trabalhos** página.

    ![Registrar trabalho](./media/backup-azure-vms/register-create-job.png)

    máquina virtual de saudação também aparece na lista de saudação de itens registrados, junto com o status de saudação da operação de registro de saudação.

    ![Status de registro 1](./media/backup-azure-vms/register-status01.png)

    Quando Olá operação for concluída, o status de saudação muda Olá tooreflect *registrado* estado.

    ![Status de registro 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar Olá agente de VM na máquina virtual de saudação
Hello Azure VM Agent deve ser instalado em Olá máquina virtual do Azure para Olá toowork de extensão de Backup. Se sua VM foi criada de saudação Galeria do Azure, Olá VM Agent já está presente no hello VM; Você pode ignorar muito[protegendo suas VMs](backup-azure-vms-first-look.md#create-the-backup-policy).

Se sua VM migrado de um datacenter local, Olá VM provavelmente não tem Olá que VM Agent instalado. Você deve instalar Olá agente de VM na máquina virtual Olá Olá de tooprotect continuar VM. Para obter etapas detalhadas sobre como instalar hello agente de VM, consulte Olá [seção agente de VM do artigo de VMs de Backup Olá](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Criar política de backup Olá
Antes de disparar o trabalho de backup inicial hello, defina o agendamento de saudação quando os instantâneos de backup são realizados. Olá agendar instantâneos de backup são realizados e Olá tempo esses instantâneos são mantidos, é política de backup hello. informações de retenção Olá baseia-se no esquema de rotação de backup avô-pai-filho.

1. Navegue toohello Cofre de backup em **dos serviços de recuperação** Olá portal clássico do Azure e clique em **itens registrados**.
2. Selecione **Máquina Virtual do Azure** do menu suspenso de saudação.

    ![Selecionar a carga de trabalho no portal](./media/backup-azure-vms/select-workload.png)
3. Clique em **proteger** final Olá Olá página.
    ![Clique em Proteger](./media/backup-azure-vms-first-look/protect-icon.png)

    Olá **proteger itens assistente** aparece e lista *somente* máquinas virtuais que são registradas e não protegidas.

    ![Configurar proteção em escala](./media/backup-azure-vms/protect-at-scale.png)
4. Selecione a saudação de máquinas virtuais que você deseja tooprotect.

    Se houver dois ou mais máquinas virtuais com hello mesmo nome, use Olá toodistinguish de serviço de nuvem entre máquinas virtuais de saudação.
5. Em Olá **configurar proteção** menu Selecione uma política existente ou crie um novo tooprotect de política máquinas virtuais Olá que você identificou.

    Novos cofres de Backup têm uma política de padrão associada Olá cofre. Esta política usa um diário de instantâneo a cada noite e instantâneo diário Olá é mantido por 30 dias. Cada política de backup pode ter várias máquinas virtuais associadas a ela. No entanto, máquina virtual de saudação só pode ser associada com uma política por vez.

    ![Proteger com nova política](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Uma política de backup inclui um esquema de retenção para backups agendado de saudação. Se você selecionar uma política de backup, você será opções de retenção Olá toomodify não é possível na próxima etapa do hello.
   >
   >
6. Em **período de retenção** definir Olá escopo diário, semanal, mensal e anual para pontos de backup específico hello.

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/long-term-retention.png)

    Política de retenção Especifica Olá período de tempo para armazenar um backup. Você pode especificar diferentes políticas de retenção com base em quando é feito backup hello.
7. Clique em **trabalhos** tooview lista de saudação do **configurar proteção** trabalhos.

    ![Configurar o trabalho de proteção](./media/backup-azure-vms/protect-configureprotection.png)

    Agora que estabelecida política Olá, vá toohello próxima etapa e executar o backup inicial hello.

## <a name="initial-backup"></a>Backup inicial
Depois que uma máquina virtual foi protegida com uma política, você pode exibir esse relacionamento na Olá **itens protegidos** guia. Até que o backup inicial Olá ocorre, hello **Status de proteção** mostra como **protegido - (pendente backup inicial)**. Por padrão, o primeiro backup agendado de saudação é Olá *backup inicial*.

![Backup pendente](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart saudação inicial backup agora:

1. Em Olá **itens protegidos** , clique em **Backup agora** final Olá Olá página.
    ![Ícone de Fazer Backup Agora](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Olá serviço Backup do Azure cria um trabalho de backup para a operação de backup inicial hello.
2. Clique em Olá **trabalhos** lista de saudação do guia tooview de trabalhos.

    ![Backup em andamento](./media/backup-azure-vms-first-look/protect-inprogress.png)

    Quando o backup inicial é concluída, o status de saudação de máquina virtual Olá Olá **itens protegidos** guia *protegidos*.

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > O backup de máquinas virtuais é um processo local. Você não pode fazer backup de máquinas virtuais de uma região tooa Cofre de backup em outra região. Portanto, para cada região do Azure com VMs que precisam de backup de toobe, pelo menos um cofre de backup deve ser criado nessa região.
   >
   >

## <a name="next-steps"></a>Próximas etapas
Agora que você já fez um backup de uma VM, há várias etapas subsequentes pode poderiam ser interessantes. Olá mais lógica etapa é toofamiliarize-se com a restauração de dados tooa VM. No entanto, há tarefas de gerenciamento que ajudarão você a entender como tookeep seus dados seguros e minimizar os custos.

* [Gerenciar e monitorar suas máquinas virtuais](backup-azure-manage-vms.md)
* [Restaurar máquinas virtuais](backup-azure-restore-vms.md)
* [Diretrizes de solução de problemas](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).
