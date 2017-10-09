---
title: aaaReplicate VMs VMware tooAzure | Microsoft Docs
description: "Resume as etapas de saudação que é necessário para replicar as cargas de trabalho em execução em máquinas virtuais do VMware tooAzure armazenamento"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Replicar tooAzure de máquinas virtuais VMware com a recuperação de Site

> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmware-to-azure.md)
> * [Azure clássico](site-recovery-vmware-to-azure-classic.md)


Este artigo descreve como tooreplicate local tooAzure de máquinas virtuais VMware, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Se você quiser toomigrate VMs VMware tooAzure (somente failover), leitura [neste artigo](site-recovery-migrate-to-azure.md) toolearn mais.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Etapas de implantação.

Aqui está o que você precisa toodo:

1. Verifique os pré-requisitos e as limitações.
2. Configure contas de rede e armazenamento do Azure.
3. Preparar a máquina local, Olá que você deseja toodeploy como servidor de configuração de saudação.
4. Prepare contas VMware toobe usado para a descoberta automática de máquinas virtuais e, opcionalmente, para a instalação por push do serviço de mobilidade de saudação.
4. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.
5. Especifique as configurações de origem, destino e replicação.
6. Implantar o serviço de mobilidade Olá em máquinas virtuais que você deseja tooreplicate.
7. Habilite a replicação para Olá VMs.
7. Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.

## <a name="prerequisites"></a>Pré-requisitos

**Requisito de suporte** | **Detalhes**
--- | ---
**As tabelas** | Saiba mais sobre [requisitos do Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuração local** | Você precisa de uma VM VMware que esteja executando o Windows Server 2012 R2 ou posterior. Você pode configurar este servidor durante a implantação de Site Recovery.<br/><br/> Pelo processo de saudação padrão o servidor e o servidor de destino mestre também são instalados nessa VM. Quando você escala verticalmente, talvez seja necessário um servidor de processo separado e tem Olá mesmos requisitos do servidor de configuração de saudação.<br/><br/> Saiba mais sobre esses componentes [aqui](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Servidores VMware locais** | Um ou mais servidores VMware vSphere, executando 6.0, 5.5, 5.1 com as últimas atualizações. Servidores devem estar localizados no hello mesma rede como o servidor de configuração de hello (ou servidor de processo separado).<br/><br/> Recomendamos um vCenter toomanage hosts do servidor de execução 6.0 ou 5.5 com atualizações mais recentes de saudação. Somente recursos que estão disponíveis no 5.5 têm suporte quando você implanta a versão 6.0.
**VMs locais** | Máquinas virtuais que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). A VM deve ter ferramentas VMware em execução.
**URLs** | servidor de configuração de Olá precisa acessar toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).<br/><br/> Permitir que essa URL para download do MySQL Olá: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Serviço de mobilidade** | Instalado em todas as VMs replicadas.




## <a name="limitations"></a>Limitações

**Limitação** | **Detalhes**
--- | ---
**As tabelas** | Contas de armazenamento e de rede devem estar no hello mesma região Olá cofre<br/><br/> Se você usar uma conta de armazenamento premium, você também precisa de um padrão de armazenar os logs de conta de replicação toostore<br/><br/> Você não pode replicar contas toopremium no centro e Sul da Índia.
**Servidor de configuração local** | O tipo de adaptador de VM VMware deve ser VMXNET3. Caso contrário, [instale esta atualização](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> O vSphere PowerCLI 6.0 deve estar instalado.<br/><br> máquina de saudação não deve ser um controlador de domínio. máquina de saudação deve ter um endereço IP estático.<br/><br/> nome do host Olá deve ser de 15 caracteres ou menos, e o sistema operacional deve estar em inglês.
**VMware** | Apenas recursos 5.5 têm suporte no vCenter 6.0. O Site Recovery não dá suporte aos novos recursos do vCenter e vSphere 6.0, como o vCenter vMotion cruzado, os volumes virtuais e o DRS de armazenamento.
**VMs** | Verifique [Limitações de VM do Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Você não pode replicar máquinas virtuais com discos criptografados ou máquinas virtuais com inicialização EFI/UEFI.<br/><br> Não há suporte para clusters de disco compartilhado. Se a VM de origem Olá tem agrupamento NIC, ele será convertido tooa única NIC após o failover.<br/><br/> Se as VMs têm um disco iSCSI, recuperação de Site converte arquivo VHD tooa após o failover. Se o destino de iSCSI Olá possa ser alcançado por Olá VM do Azure, ele se conecta tooit e vê-lo e hello VHD. Se isso acontecer, desconecte do destino iSCSI hello.<br/><br/> Se você quiser tooenable consistência de várias VMs, que permite que as VMs em execução Olá mesmo toobe de carga de trabalho recuperado dados consistentes tooa juntos ponto, abrir a porta 20004 no hello VM.<br/><br/> Windows deve ser instalado na unidade C do hello. disco do sistema operacional Olá deve ser básico e não dinâmico. disco de dados Olá pode ser dinâmico.<br/><br/> Linux /etc/hosts arquivos em VMs devem conter entradas que mapeiam Olá host local nome tooIP endereços associados a todos os adaptadores de rede. Olá, nome de host, pontos de montagem, nome do dispositivo, os caminhos de sistema e nomes de arquivo (/ etc; em /usr.) deve ser apenas em inglês.<br/><br/> Tipos específicos de [armazenamento do Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) têm suporte.<br/><br/>Criar ou definir **disk.enableUUID=true** nas configurações de VM hello. Isso fornece uma consistente toohello UUID VMDK, para que ele monta corretamente e garante que as alterações delta somente são transferidos back tooon local durante o failback sem replicação completa.

## <a name="set-up-azure"></a>Configurar o Azure

1. [Configure uma rede do Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - As VMs do Azure serão colocadas nessa rede quando forem criadas após o failover.
    - Você pode configurar uma rede no [Gerenciador de Recursos](../resource-manager-deployment-model.md) ou no modo clássico.

2. [Configure uma conta de armazenamento do Azure](../storage/storage-create-storage-account.md#create-a-storage-account) para os dados replicados.
    - conta de saudação pode ser padrão ou [premium](../storage/storage-premium-storage.md).
    - Você pode configurar uma conta no Gerenciador de Recursos ou no modo clássico.

3. [Preparar uma conta](#prepare-for-automatic-discovery-and-push-installation) no servidor do vCenter hello ou hosts vSphere, portanto essa recuperação de Site pode detectar automaticamente VMs VMware.

## <a name="prepare-hello-configuration-server"></a>Preparar o servidor de configuração de saudação

1. Instale o Windows Server 2012 R2 ou posterior em uma VM VMware.
2. Certifique-se de saudação VM tem acesso toohello URLs listadas na [pré-requisitos](#prerequisites).
3. Instale o [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Preparar para instalação automática de descoberta e por push

- **Preparar uma conta para a descoberta automática**: servidor de processo de recuperação de Site Olá descobre automaticamente as máquinas virtuais. toodo, credenciais de necessidades de recuperação de Site que podem acessar servidores vCenter e hosts de ESXi vSphere.

    1. toouse uma conta dedicada, crie uma função (no nível do vCenter hello, com estas [permissões](#vmware-account-permissions). Use um nome como **Azure_Site_Recovery**.
    2. Em seguida, crie um usuário no servidor de vCenter/host vSphere hello e atribuir Olá função toohello usuário. Você especifica essa conta de usuário durante a implantação de Site Recovery.

- **Preparar uma saudação de toopush conta Serviço de mobilidade**: se você quiser tooVMs de serviço de mobilidade toopush hello, você precisa de uma conta que pode ser usada por tooaccess do servidor de processo Olá Olá VM. Olá conta só é usada para a instalação por push hello. Você pode usar uma conta local ou de domínio:

    - Para Windows, se você não estiver usando uma conta de domínio, você precisa toodisable controle de acesso de usuário remoto na máquina local hello. toodo, Olá registrar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar entrada DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.
    - Entrada de registro tooadd Olá para Windows de uma CLI, digite:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Para o Linux, a conta de Olá deve ser raiz no servidor do hello origem Linux.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção Olá

Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.

1. Clique em **Cofres dos Serviços de Recuperação** > cofre.
2. No hello recurso de Menu, clique em **recuperação de Site** > **etapa 1: preparar a infraestrutura** > **objetivo de proteção**.

    ![Escolher metas](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. Em **objetivo de proteção**, selecione **tooAzure** > **Sim, com VMware vSphere hipervisor**.

    ![Escolher metas](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar o servidor de configuração de hello, registrá-lo no cofre hello e descobrir máquinas virtuais.

1. Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.
2. Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.

    ![Configurar origem](./media/site-recovery-vmware-to-azure/set-source1.png)
3. Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.
4. Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.
5. Baixe a chave de registro de cofre hello. Você precisará dela quando executar a Configuração Unificada. chave de saudação é válida por cinco dias depois que ele é gerado.

   ![Configurar origem](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Execute a Configuração Unificada da Recuperação de Site

Seguinte Olá antes de iniciar, em seguida executar instalação unificado tooinstall Olá configuração server, Olá processo server e o servidor de destino mestre hello.
    - Obter uma rápida visão geral em vídeo

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - No servidor de configuração de saudação VM, certifique-se de que o relógio do sistema hello está sincronizado com um [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Ele deve ser correspondente. Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.
    - Execute a instalação como Administrador Local no servidor de configuração de saudação VM.
    - Certifique-se de que TLS 1.0 está ativado Olá VM.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> também pode ser instalado o servidor de configuração de saudação [da linha de comando Olá](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Adicionar conta Olá para descoberta automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>Conectar servidores tooVMware

Conecte hosts de ESXi toovSphere ou servidores vCenter, toodiscover VMware VMs.

- Se você adicionar o servidor do vCenter hello ou vSphere hosts com uma conta sem privilégios de administrador no servidor de saudação, conta Olá precisa desses privilégios habilitados:
    - Datacenter, Repositório de Dados, Pasta, Host, Rede, Recurso, Máquina Virtual, vSphere Distributed Switch.
    - servidor do vCenter Olá precisa de permissões de exibições de armazenamento.
- Quando você adiciona servidores VMware, pode levar 15 minutos ou mais para que eles tooappear no portal de saudação.
tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente local, você precisará tooconnect o VMware vCenter Server ou hosts de ESXi vSphere com a recuperação de Site.

Selecione **+ vCenter** toostart conectando um VMware vCenter server ou um host do VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Recuperação de site se conecta a servidores tooVMware usar Olá especificado as configurações e descobre máquinas virtuais.

## <a name="set-up-hello-target"></a>Configurar o destino de saudação

Antes de configurar o ambiente de destino hello, verifique que você tem um [conta de armazenamento do Azure e rede](#set-up-azure)

1. Clique em **preparar infraestrutura** > **destino**, e selecione Olá assinatura do Azure que você deseja toouse.
2. Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.
3. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

   ![Destino](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Se você não tiver criado uma conta de armazenamento ou de rede, clique em **+ conta de armazenamento** ou **+ rede**, toocreate embutido de rede ou a conta de um Gerenciador de recursos.

## <a name="set-up-replication-settings"></a>Definir as configurações de replicação

Obtenha uma rápida visão geral em vídeo antes de começar:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate uma nova política de replicação, clique em **infra-estrutura de recuperação de Site** > **políticas de replicação** > **+ política de replicação**.
2. Em **Criar política de replicação**, especifique um nome de política.
3. Em **limite de RPO**, especifique o limite RPO hello. Esse valor especifica com que frequência os pontos de recuperação de dados são criados. Um alerta será gerado se a replicação contínua exceder esse limite.
4. Em **retenção de ponto de recuperação**, especifique quanto tempo (em horas) é uma janela de retenção Olá para cada ponto de recuperação. Máquinas virtuais replicadas podem ser recuperados tooany ponto em uma janela. A retenção horas tem suporte para máquinas de too24 replicado toopremium armazenamento e 72 horas para o armazenamento padrão.
5. Em **Frequência do instantâneo consistente com o aplicativo**, especifique com que frequência (em minutos) os pontos de recuperação contendo instantâneos consistentes com aplicativos serão criados. Clique em **Okey** toocreate política de saudação.

    ![Política de replicação](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Quando você cria uma nova política automaticamente associado com o servidor de configuração de saudação. Por padrão, uma política de correspondência é criada automaticamente para failback. Por exemplo, se hello política de replicação é **política rep** diretiva de failback hello serão **representante de diretiva de failback**. Essa política não é usada até você iniciar um failback do Azure.  



## <a name="plan-capacity"></a>Planejar a capacidade

1. Agora que você tem a infraestrutura básica configurada, pense sobre o planejamento da capacidade e descubra se precisa de recursos adicionais. [Saiba mais](site-recovery-plan-capacity-vmware.md).
2. Quando terminar o planejamento de capacidade, selecione **Sim** em **Você concluiu o planejamento de capacidade?**

   ![Planejamento da capacidade](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparar VMs para replicação

Olá serviço de mobilidade deve ser instalado em todas as máquinas virtuais do VMware que você deseja tooreplicate. Você pode instalar o serviço de mobilidade de saudação de várias maneiras:

1. Instale com uma instalação por push saudação do servidor de processo. Você precisará tooprepare VMs toouse deste método.
2. Instale usando ferramentas de implantação, como System Center Configuration Manager ou DSC de automação do Azure.
3.  Instalar manualmente.

[Saiba mais](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Habilitar a replicação

Antes de começar:

- Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.
- Quando você adiciona ou modifica máquinas virtuais, pode levar a too15 minutos ou mais para efeito de tootake de alterações e, para que eles tooappear no portal de saudação.
- Você pode verificar o tempo de saudação do último descoberto para VMs no **servidores de configuração** > **último contato em**.
- tooadd VMs sem aguardar a descoberta agendada hello, servidor de configuração de saudação do realce (não clique nele) e clique em **atualizar**.
- Se uma VM está preparada para a instalação por push, servidor de processo Olá instala automaticamente o serviço de mobilidade hello quando você habilitar a replicação.


### <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por padrão, todos os discos em um computador são replicados. Você pode excluir discos da replicação. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que foi atualizada cada vez que uma máquina ou aplicativo reinicia (por exemplo, pagefile.sys ou tempdb do SQL Server).

### <a name="replicate-vms"></a>Replicar VMs

Antes de começar, assista a uma rápida visão geral em vídeo

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**.
2. Em **fonte**, selecione o servidor de configuração hello.
3. Em **Tipo de máquina**, selecione **Máquinas Virtuais**.
4. Em **vCenter/vSphere hipervisor**, selecione o servidor do vCenter Olá que gerencia o host do vSphere hello, ou selecione host hello.
5. Selecione o servidor de processo hello. Se você não criou nenhum servidor de processo adicional esse será o servidor de configuração de saudação. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. Em **destino**, selecione a assinatura hello e Olá no qual você deseja Olá toocreate failover de máquinas virtuais do grupo de recursos. Escolha o modelo de implantação de saudação que você deseja toouse no Azure (clássico ou o recurso de gerenciamento), para Olá failover VMs.


7. Selecione conta de armazenamento do Azure Olá que desejar toouse para replicação de dados. Se você não quiser toouse uma conta que você já tenha configurado o, você pode criar um novo.

8. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure conectará quando eles são criados após o failover. Selecione **configurar agora para os computadores selecionados**, tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina. Se você não quiser toouse uma rede existente, você pode criar um.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. Em **propriedades** > **configurar propriedades**, selecione conta Olá que será usada por tooautomatically de servidor de processo Olá instalar serviço de mobilidade de saudação na máquina de saudação.
11. Por padrão, todos os discos são replicados. Clique em **todos os discos** e desmarque os discos que você não deseja tooreplicate. Em seguida, clique em **OK**. Você pode definir propriedades de VM adicionais posteriormente.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. Em **as configurações de replicação** > **definir configurações de replicação**, verifique se esse Olá correto de política de replicação está selecionada. Se você modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.
12. Habilitar **consistência de várias VMs** toogather máquinas em um grupo de replicação, e especifique um nome para o grupo de saudação. Em seguida, clique em **OK**. Observe que:

    * Os computadores nos grupos de replicação são replicados em conjunto e têm pontos de recuperação consistentes compartilhados com o aplicativo e com falhas quando executam failover.
    * É recomendável que você colete VMs e servidores físicos para que espelhem suas cargas de trabalho. Habilitar a consistência de várias VMs pode afetar o desempenho da carga de trabalho e só deve ser usado se as máquinas estão executando Olá mesma carga de trabalho e você precisa de consistência.

    ![Habilitar a replicação](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Clique em **Habilitar a Replicação**. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.

### <a name="view-and-manage-vm-properties"></a>Exibir e gerenciar as propriedades da VM

É recomendável que você verifique Olá propriedades da VM e faça as alterações que você precisa.

1. Clique em **replicadas itens** > e selecione Olá máquina. Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.
2. Em **propriedades**, você pode exibir a replicação e failover informações para Olá VM.
3. Em **de computação e rede** > **propriedades de computação**, você pode especificar o tamanho de destino e o nome de VM do Azure hello. Modificar Olá nome toocomply com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se for necessário.
4. Modificar as configurações de rede de destino hello, sub-rede e endereço IP que será atribuído toohello VM do Azure:

   - Você pode definir o endereço IP de destino hello.

    - Se você não fornecer um endereço, Olá failover máquina usará o DHCP.
    - Se definir um endereço que não esteja disponível no failover, o failover não funcionará.
    - saudação do mesmo endereço IP de destino pode ser usado para failover de teste, se o endereço de saudação está disponível na rede de failover de teste de saudação.

   - número de saudação de adaptadores de rede é determinado pelo tamanho Olá especificado para a máquina de virtual de destino hello:

     - Se Olá vários adaptadores de rede no computador de origem de saudação é hello igual ou menor, número de saudação de adaptadores permitido para o tamanho de máquina de destino hello, destino Olá terá Olá o mesmo número de adaptadores de fonte de saudação.
     - Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino Olá, tamanho máximo da saudação destino será usado.
     - Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.     
   - Se a máquina virtual de saudação tem vários adaptadores de rede conectará todos toohello mesma rede.
   - Se a máquina virtual de saudação tem vários adaptadores de rede, Olá primeiro mostrada na lista de saudação se torna Olá *padrão* adaptador de rede na máquina virtual do Azure de saudação.
4. Em **discos**, você pode ver o sistema de operacional VM hello e dados saudação discos que serão replicados.

#### <a name="managed-disks"></a>Discos gerenciados

Em **de computação e rede** > **propriedades de computação**, você pode configurar "Usar gerenciada discos" muito "Sim" para Olá VM se você quiser tooattach discos gerenciado tooyour máquina em tooAzure de failover. Discos gerenciados simplifica o gerenciamento de disco para VMs de IaaS do Azure por meio do gerenciamento de contas de armazenamento Olá associadas Olá discos VM. [Saiba mais sobre managed disks.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Discos gerenciados são toohello criado e anexado máquina de virtual somente em um tooAzure de failover. Ao habilitar a proteção, dados de máquinas locais continuarão tooreplicate toostorage contas.  Discos gerenciados podem ser criados somente para máquinas virtuais implantadas usando o modelo de implantação do Gerenciador de recursos de hello.  

   - Quando você define "Usar gerenciada discos" muito "Sim", apenas conjuntos de disponibilidade no grupo de recursos de saudação com conjunto "Usar gerenciada discos" muito "Sim" seria disponíveis para seleção. Isso ocorre porque as máquinas virtuais com discos gerenciados só pode ser parte dos conjuntos de disponibilidade com o conjunto de propriedades "Use gerenciado discos" muito "Sim". Certifique-se de que você crie conjuntos de disponibilidade com conjunto de propriedades de "Discos Use gerenciado", com base em seus discos toouse intenção gerenciado no failover.  Da mesma forma, quando você define "Usar gerenciada discos" muito "não", apenas conjuntos de disponibilidade no grupo de recursos de saudação com a propriedade "Usar gerenciada discos" definido muito "não" estariam disponíveis para seleção. [Saiba mais sobre managed disks e conjuntos de disponibilidade](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se a conta de armazenamento Olá usada para a replicação foi criptografada com criptografia do serviço de armazenamento em qualquer ponto no tempo, haverá falha na criação de discos gerenciados durante o failover. Você pode definir "Usar gerenciada discos" muito "Nenhum" e tente realizar o failover ou desabilite a proteção para a máquina virtual de saudação e protegê-lo tooa conta de armazenamento que não tem criptografia do serviço de armazenamento habilitada em qualquer ponto no tempo.
  > [Saiba mais sobre Criptografia do serviço de armazenamento e managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Execute um teste de failover


Depois que você configurou tudo, execute um toomake de failover de teste se que tudo está funcionando conforme o esperado. Obter uma rápida visão geral em vídeo antes de começar
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail em um único computador, em **configurações** > **itens duplicados**, clique em Olá VM > **+ Failover de teste** ícone.

    ![Failover de Teste](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. Planejar toofail sobre a recuperação, em **configurações** > **planos de recuperação**, plano de saudação do botão direito do mouse > **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).  

1. Em **Failover de teste**, selecione toowhich de rede do Azure Olá VMs do Azure será conectada após o failover.

1. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando no hello VM tooopen suas propriedades, ou em Olá **Failover de teste** trabalho em nome do cofre > **configurações** > **trabalhos**  >  **Trabalhos de recuperação de site**.

1. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure > **máquinas virtuais**. Você deve garantir que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.

1. Se você [preparado para conexões após o failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), você deve ser capaz de tooconnect toohello VM do Azure.

1. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. Isso excluirá Olá VMs que foram criados durante o failover de teste.

[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.


## <a name="vmware-account-permissions"></a>Permissões de conta do VMware

Recuperação de site precisa de acesso tooVMware para tooautomatically de servidor de processo Olá descobrir máquinas virtuais e para failover e failback de máquinas virtuais.

- **Migrar**: se você quiser apenas toomigrate VMs VMware tooAzure, sem nunca failback-los, você pode usar uma conta do VMware com uma função somente leitura. Essa função pode executar o failover, mas não pode desligar máquinas de origem protegidas. Isso não é necessário para a migração.
- **Replicar/recuperar**: se você quiser toodeploy conta de saudação de replicação completo (replicação, failover e failback) deve ser capaz de toorun operações como criar e remover discos, ligar VMs etc.
- **Descoberta automática**: é necessário ter pelo menos uma conta somente leitura.


**Tarefa** | **Conta/função necessária** | **Permissões** | **Detalhes**
--- | --- | --- | ---
**Servidor de processo descobre automaticamente as VMs VMware** | Você precisa de pelo menos um usuário somente leitura | Objeto de Data Center –> Propagate tooChild objeto, função = somente leitura | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** de objetos, toohello filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes).
**Failover** | Você precisa de pelo menos um usuário somente leitura | Objeto de Data Center –> Propagate tooChild objeto, função = somente leitura | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** toohello os objetos filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes) do objeto.<br/><br/> É útil para fins de migração, mas não para replicação completa, failover ou failback.
**Failover e failback** | Sugerimos que você cria uma função (Azure_Site_Recovery) com permissões necessárias de saudação e, em seguida, atribuir Olá função tooa VMware usuário ou grupo | Objeto de Data Center –> Propagate tooChild objeto, função = Azure_Site_Recovery<br/><br/> Armazenamento de dados -> alocar espaço, procurar armazenamento de dados, operações de arquivo de baixo nível, remover arquivo, atualizar arquivos de máquina virtual<br/><br/> Rede -> Atribuição de rede<br/><br/> Recursos -> pool de tooresource atribuir VM, migrar desligado a VM, migrar ligados a VM<br/><br/> Tarefas -> Criar tarefa, atualizar tarefa<br/><br/> Máquina virtual -> Configuração<br/><br/> Máquina virtual -> Interagir -> responder à pergunta, conexão de dispositivo, configurar mídia de CD, configurar mídia de disquete, desligar, ligar, instalação de ferramentas VMware<br/><br/> Máquina virtual -> Inventário -> Criar, registrar, cancelar registro<br/><br/> Máquina virtual -> Provisionamento -> Permitir download de máquina virtual, permitir upload de arquivos de máquina virtual<br/><br/> Máquina virtual -> Instantâneos -> Remover instantâneos | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** de objetos, toohello filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes).


## <a name="next-steps"></a>Próximas etapas

Depois de você começar a replicação e em execução, quando ocorre uma paralisação failover tooAzure e VMs do Azure são criadas a partir de dados replicado de saudação. Você pode acessar as cargas de trabalho e aplicativos no Azure, até que a falha local primário tooyour voltar ao retornar toonormal operações.

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- Se estiver migrando máquinas em vez de replicar e fazer failback, [leia mais](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Leia sobre failback](site-recovery-failback-azure-to-vmware.md), toofail back e replicação de máquinas virtuais do Azure novamente toohello principal no site local.

## <a name="third-party-software-notices-and-information"></a>Avisos e informações de software de terceiros
Do Not Translate or Localize

software Hello e firmware em execução no hello produto da Microsoft ou o serviço se baseia em ou incorpora material dos Olá projetos listados abaixo (coletivamente, "código de terceiros").  A Microsoft está Olá autor original não Olá código de terceiros.  Olá original de direitos autorais e licença, sob a qual a Microsoft recebeu esse código de terceiros, estão definidos abaixo.

informações de saudação na seção A é em relação ao código de terceiros, componentes de projetos de saudação listados abaixo. Such licenses and information are provided for informational purposes only.  Esse código de terceiros está sendo tooyou relicensed pela Microsoft em termos de produto da Microsoft hello ou o serviço de licenciamento de software da Microsoft.  

informações de saudação na seção B for referente a componentes de código de terceiros que estão sendo feitas tooyou disponível pela Microsoft em termos de licenciamento original hello.

arquivo completo Olá pode ser encontrado em Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
