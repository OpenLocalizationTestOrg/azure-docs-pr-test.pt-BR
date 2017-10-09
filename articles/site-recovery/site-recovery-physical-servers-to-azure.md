---
title: "aaaReplicate servidores físicos tooAzure | Microsoft Docs"
description: "Descreve como a replicação toodeploy Azure Site Recovery tooorchestrate, failover e recuperação de local tooAzure de servidores físicos do Windows/Linux usando Olá portal do Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Replicar máquinas físicas tooAzure usando recuperação de Site


Este artigo descreve como tooreplicate local tooAzure de computadores físicos usando o serviço do Azure Site Recovery Olá no hello portal do Azure.

Se você quiser toomigrate máquinas físicas tooAzure (somente failover), leitura [migrar tooAzure com a recuperação de Site](site-recovery-migrate-to-azure.md) toolearn mais.

Postar perguntas e comentários na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Pré-requisitos

**Requisito de suporte** | **Detalhes**
--- | ---
**As tabelas** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidor de configuração local** | Computador local (físico ou VM do VMware) executando o Windows Server 2012 R2 ou posterior. Você pode configurar o servidor de configuração Olá durante a implantação da recuperação de Site.<br/><br/> Por padrão, o servidor de processo hello e o servidor de destino mestre também são instalados neste computador. Quando você escala verticalmente, talvez seja necessário um servidor de processo separado e tem Olá mesmos requisitos do servidor de configuração de saudação.<br/><br/> Saiba mais sobre esses componentes nas [configurar o ambiente de origem Olá](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**VMs locais** | Máquinas que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e estar em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | servidor de configuração de Olá precisa acessar toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e hello porta HTTPS (443).<br/></br> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidades e controle de acesso).<br/><br/> Permitir que essa URL para download do MySQL Olá: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Serviço de mobilidade** | Esse serviço é instalado em cada computador que você deseja tooreplicate.

## <a name="limitations"></a>Limitações

**Limitação** | **Detalhes**
--- | ---
**As tabelas** | Contas de armazenamento e de rede devem estar no hello mesma região Olá cofre.<br/><br/> Se você usar uma conta de armazenamento premium, você também precisa de um padrão de armazenar os logs de conta toostore de replicação.<br/><br/> Você não pode replicar contas toopremium no centro e Sul da Índia.
**Servidor de configuração local** | Se você instalar o servidor de configuração de saudação em uma VM do VMware, Olá tipo de adaptador VM deve ser VMXNET3. Se não for, [instale esta atualização](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Se você estiver usando uma VM do VMware, o vSphere 6.0 PowerCLI deverá ser instalado nela.<br/><br> máquina de saudação não deve ser um controlador de domínio.<br/><br/> máquina de saudação deve ter um endereço IP estático.<br/><br/> nome do host Olá deve ser de 15 caracteres ou menos, e o sistema operacional de saudação deve estar em inglês.
**Computadores replicados** | Verifique as [Limitações de VM do Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Se você quiser tooenable consistência de várias VMs, que permite que máquinas em execução Olá mesmo toobe de carga de trabalho recuperado dados consistentes tooa juntos ponto, abrir a porta 20004 na máquina de saudação.<br/><br/> Tipos específicos de [armazenamento do Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) têm suporte.
**Failback** | Não é possível reprovar da máquina física tooa do Azure. Se você quiser local tooon toobe toofail capaz de backup após o failover, terá um ambiente VMware para que você possa fazer back tooa VM do VMware.


## <a name="set-up-azure"></a>Configurar o Azure

1. [Configure uma rede do Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. As VMs do Azure são colocadas nessa rede quando são criadas após o failover.

      b. Você pode configurar uma rede no Azure [Resource Manager](../resource-manager-deployment-model.md) ou no modo clássico.

2. [Configure uma conta de armazenamento do Azure](../storage/storage-create-storage-account.md#create-a-storage-account) para os dados replicados.

    a. conta de saudação pode ser padrão ou [premium](../storage/storage-premium-storage.md).

    b. Você pode configurar uma conta no Resource Manager ou no modo clássico.

## <a name="prepare-hello-configuration-server"></a>Preparar o servidor de configuração de saudação

1. Instale o Windows Server 2012 R2 ou posterior em um servidor físico local ou VM do VMware.

2. Certifique-se de máquina Olá tem acesso toohello URLs listadas na [pré-requisitos](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Preparar para a instalação do serviço de mobilidade

Se você quiser toopush Olá mobilidade serviço tooa máquina física, você precisa de uma conta que pode ser usada por máquinas de Olá Olá processo server tooaccess. Olá conta é usada apenas para a instalação por push hello. Você pode usar uma conta local ou de domínio:

  - Para Windows, se você não estiver usando uma conta de domínio, você precisa toodisable controle de acesso de usuário remoto na máquina local hello. toodo isso, no registro de saudação em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar entrada DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1. Entrada de registro tooadd Olá para Windows de uma interface de linha de comando, digite:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Para o Linux, a conta de saudação deve ser um usuário raiz no servidor do hello origem Linux.


## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção Olá

Selecione o que você deseja tooreplicate e onde você deseja tooreplicate para.

1. Clique em **Cofres dos Serviços de Recuperação** > **cofre**.
2. Em Olá **recurso** menu, clique em **recuperação de Site** > **preparar a infraestrutura** > **objetivo de proteção**.

    ![Escolher metas](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. Em **objetivo de proteção**, selecione **tooAzure** > **não virtualizados / outros**.


## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar o servidor de configuração de hello, registrá-lo no cofre hello e descobrir máquinas virtuais.

1. Clique em **Site Recovery** > **Preparar a infraestrutura** > **Origem**.
2. Se não tiver um servidor de configuração, clique em **+Servidor de Configuração**.

    ![Configurar origem](./media/site-recovery-vmware-to-azure/set-source1.png)

3. Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.
4. Baixar Olá **unificada de configuração do Site Recovery** arquivo de instalação.
5. Baixar Olá **chave de registro de cofre**. Você precisa dessa chave ao executar a Configuração Unificada. chave de saudação é válida por cinco dias depois que ele é gerado.

   ![Configurar origem](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Execute a Configuração Unificada da Recuperação de Site

Antes de começar, Olá a seguir:

- Obtenha uma rápida visão geral em vídeo. (Olá vídeo descreve como máquinas virtuais do VMware tooreplicate, mas Olá o processo é semelhante para a replicação de máquina física.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Na máquina de servidor de configuração de saudação, certifique-se de que o relógio do sistema hello está sincronizado com um [tempo server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Se estiver 15 minutos adiantado ou atrasado, a Instalação poderá falhar.
- Execute a instalação como um administrador local no computador do servidor de configuração de saudação.
- Certifique-se de que TLS 1.0 está habilitada no computador de saudação.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> também pode ser instalado o servidor de configuração de saudação [da linha de comando Olá](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Antes de configurar o ambiente de destino hello, verifique toomake-se de que você tenha um [conta de armazenamento do Azure e rede](#set-up-azure).

1. Clique em **preparar a infraestrutura** > **destino**, e selecione Olá assinatura do Azure que você deseja toouse.
2. Especifique se o seu modelo de implantação de destino é Resource Manager ou clássico.
3. Recuperação de site verifica toomake-se de que você tenha uma ou mais contas de armazenamento do Azure compatíveis e redes.

   ![Destino](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Se você não tiver criado uma conta de armazenamento ou de rede, clique em **+ conta de armazenamento** ou **+ rede** toocreate embutido de rede ou a conta de um Gerenciador de recursos.

## <a name="set-up-replication-settings"></a>Definir as configurações de replicação

Antes de começar assista a uma rápida visão geral em vídeo. (Olá vídeo descreve como máquinas virtuais do VMware tooreplicate, mas Olá o processo é semelhante para a replicação de máquina física.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate uma nova política de replicação, clique em **infra-estrutura de recuperação de Site** > **políticas de replicação** > **+ política de replicação**.
2. Em **Criar política de replicação**, especifique um nome de política.
3. Em **limite de RPO**, especifique o limite RPO hello. Esse valor especifica com que frequência os pontos de recuperação de dados são criados. Um alerta será gerado se a replicação contínua exceder esse limite.
4. Em **retenção de ponto de recuperação**, especifique quanto tempo (em horas) é uma janela de retenção Olá para cada ponto de recuperação. Máquinas virtuais replicadas podem ser recuperados tooany ponto em uma janela. Backup too24 retenção horas tem suporte para armazenamento replicado toopremium de máquinas. Backup too72 retenção horas tem suporte para armazenamento replicado toostandard de máquinas.
5. Em **Frequência de instantâneos consistentes com o aplicativo**, especifique com que frequência (em minutos) serão criados os pontos de recuperação que contenham instantâneos consistentes com o aplicativo. Clique em **Okey** toocreate política de saudação.

    ![Política de replicação](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Quando você cria uma nova política, ela automaticamente está associada com o servidor de configuração de saudação. Por padrão, uma política de correspondência é criada automaticamente para failback. Por exemplo, se hello política de replicação é **política rep**, e a diretiva de failback Olá é **representante de diretiva de failback**. Essa política não é usada até você iniciar um failback do Azure.  


## <a name="plan-capacity"></a>Planejar a capacidade

1. Agora que você tem a infraestrutura básica configurada, pode pensar no planejamento da capacidade e descobrir se precisa de recursos adicionais. [Saiba mais](site-recovery-plan-capacity-vmware.md).
2. Quando terminar o planejamento de capacidade, selecione **Sim** em **Você concluiu o planejamento de capacidade?**

   ![Planejamento da capacidade](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparar VMs para replicação

Todos os computadores que você deseja tooreplicate devem ter o serviço de mobilidade Olá instalado. Você pode instalar o serviço de mobilidade de saudação de várias maneiras:

- Instale serviço de saudação com uma instalação por push saudação do servidor de processo. É necessário tooprepare máquinas antecipada toouse esse método.
- Instale serviço de saudação usando ferramentas de implantação, como o System Center Configuration Manager ou a configuração de estado desejado do Azure Automation.
- Instale manualmente o serviço de saudação.

[Saiba mais](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Habilitar a replicação

Antes de começar:

- Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.
- Quando você adiciona ou modifica máquinas virtuais, pode levar a too15 minutos ou mais para efeito de tootake de alterações e para que eles tooappear no portal de saudação.
- Você pode verificar o tempo de saudação do último descoberto para VMs no **servidores de configuração** > **último contato em**.
- tooadd VMs sem aguardar a descoberta agendada hello, servidor de configuração de saudação do realce (não clique nele) e clique em **atualizar**.
- Se uma VM está preparada para a instalação por push, servidor de processo Olá instala automaticamente o serviço de mobilidade hello quando você habilitar a replicação.
- Obtenha uma rápida visão geral em vídeo. (Olá vídeo descreve como máquinas virtuais do VMware tooreplicate, mas Olá o processo é semelhante para a replicação de máquina física.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por padrão, todos os discos em um computador são replicados. Você pode excluir discos da replicação. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que é atualizado a cada hora um reinicializações do computador ou do aplicativo (por exemplo, pagefile.sys ou tempdb do SQL Server).

### <a name="replicate-vms"></a>Replicar VMs

1. Clique em **Replicar aplicativo** > **Origem**.
2. Em **Origem**, selecione **Local**.
3. Em **local de origem**, selecione o nome de servidor de configuração hello.
4. Em **Tipo de máquina**, selecione **Máquinas Físicas**.
5. Em **servidor de processo**, escolha o servidor de processo hello. Se você não criou nenhum servidor de processo adicional, esse servidor é o servidor de configuração de saudação. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-physical-to-azure/chooseVM.png)

6. Em **destino**, selecione Olá **assinatura** e hello **grupo de recursos** no qual você deseja toocreate Olá VMs do Azure após o failover. Escolha deployment Olá modelo que você deseja toouse no Azure (clássico ou Gerenciador de recursos) para Olá failover VMs.

7. Selecione conta de armazenamento do Azure Olá que desejar toouse para replicação de dados. Se você não quiser toouse uma conta que você já tenha configurado o, você pode criar um novo.

8. Selecione Olá **rede Azure** e **sub-rede** toowhich VMs do Azure se conectar após o failover. Selecione **configurar agora para os computadores selecionados** tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina. Se você não quiser toouse uma rede existente, você pode criar um.

    ![Habilitar a replicação](./media/site-recovery-physical-to-azure/targetsettings.png)

9. Em **máquinas físicas**, clique em **+ máquina física** e digite Olá **nome** e **endereço IP**. Escolha o sistema operacional de saudação da máquina Olá deseja tooreplicate. Leva alguns minutos até que os computadores são descobertos e mostrados na lista de saudação.

    ![Habilitar a replicação](./media/site-recovery-physical-to-azure/machineselect.png)

10. Em **propriedades** > **configurar propriedades**, selecione conta Olá toobe usado pelo tooautomatically de servidor de processo Olá instalar serviço de mobilidade de saudação na máquina de saudação.
11. Por padrão, todos os discos são replicados. Clique em **todos os discos**e desmarque os discos que você não deseja tooreplicate. Em seguida, clique em **OK**. Você pode definir propriedades de VM adicionais posteriormente.

    ![Habilitar a replicação](./media/site-recovery-physical-to-azure/configprop.png)

12. Em **as configurações de replicação** > **definir configurações de replicação**, verifique se esse Olá correto de política de replicação está selecionada. Se você modificar uma política, as alterações são aplicada toohello replicação de máquina e toonew máquinas.
13. Habilitar **consistência de várias VMs** toogather máquinas em um grupo de replicação, e especifique um nome para o grupo de saudação. Em seguida, clique em **OK**. Observe que:

    a. Os computadores nos grupos de replicação são replicados em conjunto e têm pontos de recuperação consistentes com falha e consistentes com aplicativos compartilhados quando executam failover.

    b. É recomendável que você colete VMs e servidores físicos para que espelhem suas cargas de trabalho. Habilitar a consistência de várias VMs pode afetar o desempenho da carga de trabalho. Ele deve ser usado somente se as máquinas estão Olá a mesma carga de trabalho em execução e você precisar de consistência.

    ![Habilitar a replicação](./media/site-recovery-physical-to-azure/policy.png)

14. Clique em **Habilitar a Replicação**. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** trabalho é executado, a máquina de saudação está pronta para failover.

Depois de habilitar a replicação, Olá serviço de mobilidade está instalado, se você configurar a instalação por push. Após Olá serviço de mobilidade push instalado em um computador, um trabalho de proteção é iniciado e falha. Depois de falha de saudação, você precisa toomanually reiniciar cada máquina. Trabalho de proteção Olá começará novamente e ocorre a replicação inicial.


### <a name="view-and-manage-azure-vm-properties"></a>Exibir e gerenciar as propriedades da VM do Azure

É recomendável que você verifique Olá propriedades da VM e faça quaisquer alterações que necessárias.

1. Clique em **replicadas itens**e selecione Olá máquina. Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.
2. Em **propriedades**, você pode exibir a replicação e failover informações para Olá VM.
3. Em **de computação e rede** > **propriedades de computação**, você pode especificar o tamanho de destino e o nome de VM do Azure hello. Modificar Olá nome toocomply com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se for necessário.
4. Modificar as configurações de rede de destino hello, sub-rede e endereço IP que recebem toohello VM do Azure:

    a. Você pode definir o endereço IP de destino hello.

    b.  Se você não fornecer um endereço, Olá failover usará DHCP.

    c. Se você definir um endereço que não esteja disponível no failover, o failover não funcionará.

    d. saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.

    e. número de saudação de adaptadores de rede é determinado pelo tamanho Olá especificado para a máquina de virtual de destino hello:

     - Se Olá vários adaptadores de rede no computador de origem de saudação é hello igual ou menor, número de saudação de adaptadores permitido para o tamanho de máquina de destino hello, destino Olá tem Olá mesmo número de adaptadores de fonte de saudação.
     - Se Olá número de adaptadores de saudação da máquina virtual de origem excede número Olá permitido para o tamanho de destino Olá, tamanho máximo da saudação destino é usado.
     - Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, o computador de destino Olá tem dois adaptadores. Se máquina de origem Olá tem dois adaptadores, mas o tamanho de destino Olá suporte oferece suporte a apenas um, o computador de destino Olá tenha apenas um adaptador.     
   - Se a máquina virtual de saudação tem vários adaptadores de rede, todos eles conectarem toohello mesma rede.
   - Se máquina virtual de saudação tem vários adaptadores de rede, hello primeiro mostrada na lista de saudação se torna Olá *padrão* adaptador de rede em Olá VM do Azure.
5. Em **discos**, você pode ver o sistema de operacional Olá VM e discos de dados de saudação que são replicados.

## <a name="run-a-test-failover"></a>Execute um teste de failover

Depois de configurar tudo, execute um toomake de failover de teste se que tudo está funcionando conforme o esperado. Assista uma rápida visão geral em vídeo antes de começar.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail em um único computador, em **configurações** > **itens replicados**, clique em **failover de teste**.

    ![Failover de Teste](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. Planejar toofail sobre a recuperação, em **configurações** > **planos de recuperação**, plano de saudação do botão direito do mouse > **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).  
3. Em **Failover de teste**, selecione toowhich de rede do Azure Olá VMs do Azure conectadas após o failover.
4. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando Olá VM tooopen suas propriedades ou clicando Olá **Failover de teste** trabalho em nome do cofre > **configurações** > **trabalhos**  >  **Trabalhos de recuperação de site**.
5. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure > **máquinas virtuais**. Certifique-se de que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.
6. Se você [preparado para conexões após o failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), você deve ser capaz de tooconnect toohello VM do Azure.
7. Depois de terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. Esta etapa exclui máquinas virtuais Olá que foram criadas durante o failover de teste.

Para obter mais informações, consulte Olá [tooAzure de failover de teste](site-recovery-test-failover-to-azure.md) documento.

## <a name="next-steps"></a>Próximas etapas

Depois de você começar a replicação e em execução, quando ocorre uma paralisação failover tooAzure e VMs do Azure são criadas a partir de dados replicado de saudação. Você pode acessar as cargas de trabalho e aplicativos no Azure, até que a falha local primário tooyour voltar ao retornar toonormal operações.

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- Se estiver migrando máquinas em vez de replicar e fazer failback, [leia mais](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Ao replicar computadores físicos, você pode apenas failback tooa VMware ambiente. [Leia sobre failback](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Avisos e informações de softwares de terceiros
Do Not Translate or Localize

software Hello e firmware em execução no hello produto da Microsoft ou o serviço se baseia em ou incorpora material dos Olá projetos listados abaixo (coletivamente, "código de terceiros"). A Microsoft não é o autor original Olá Olá código de terceiros. Olá original de direitos autorais e licença, sob a qual a Microsoft recebeu esse código de terceiros, estão definidos abaixo.

informações de saudação na seção A é em relação ao código de terceiros componentes de projetos de saudação listados abaixo. Such licenses and information are provided for informational purposes only. Esse código de terceiros está sendo tooyou relicensed pela Microsoft em termos de produto da Microsoft hello ou o serviço de licenciamento de software da Microsoft.  

informações de saudação na seção B for referente a componentes de código de terceiros que estão sendo feitas tooyou disponível pela Microsoft em termos de licenciamento original hello.

arquivo completo Olá pode ser encontrado no hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). A Microsoft reserva todos os direitos não explicitamente concedidos neste documento, seja por implicação, preclusão ou de outra forma.
