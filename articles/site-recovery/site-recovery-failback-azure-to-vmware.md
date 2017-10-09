---
title: aaaFailback VMware VMs do Azure tooon-local | Microsoft Docs
description: "Saiba mais sobre a falha toohello back local após o failover de máquinas virtuais do VMware e servidores físicos tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Fazer back máquinas virtuais de VMware e servidores físicos toohello no site local


Este artigo descreve como toofailback Azure máquinas virtuais do Azure toohello no site local. Siga as instruções de saudação aqui quando estiver pronto toofail fazer suas máquinas virtuais VMware ou servidores físicos do Windows ou Linux depois de ter protegido novamente suas máquinas usando esse [referência](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Se você estiver usando o portal do Azure clássico de hello, consulte tooinstructions mencionado [aqui](site-recovery-failback-azure-to-vmware-classic.md) para arquitetura de tooAzure VMware avançada e [aqui](site-recovery-failback-azure-to-vmware-classic-legacy.md) para arquitetura de saudação herdados

## <a name="overview"></a>Visão geral
diagramas de saudação nesta seção mostram a arquitetura de failback Olá para esse cenário.

Quando a saudação do servidor em processo é o local e você estiver usando uma conexão de rota expressa do Azure, use essa arquitetura:

![Diagrama da arquitetura para ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Quando a saudação do servidor em processo é no Azure e você tiver uma VPN ou uma conexão de rota expressa, use essa arquitetura:

![Diagrama da arquitetura para VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Para obter uma lista completa de portas e diagrama de arquitetura de failback hello, consulte toohello a imagem a seguir:

![Lista de failover-failback para todas as portas](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Após o failover tooAzure, você não tooyour back local em três estágios:

* **Estágio 1**: Proteja hello Azure VMs para que eles são iniciados replicando toohello back VMware VMs em execução no seu site local.
* **Fase 2**: depois que suas VMs do Azure são replicados tooyour no site local, você executar um failover toofail do Azure.
* **Fase 3**: após a falharam volta seus dados, você proteja Olá VMs locais que você não faça, para que eles são iniciados replicando tooAzure.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Falha do local original toohello back ou um local alternativo
Depois de executar o failover de uma VM do VMware, você pode fazer back toohello mesmo VM de origem, se ele ainda existe no local. Nesse cenário, somente os deltas Olá são falha novamente.

Se o failover de servidores físicos, failback é sempre tooa nova VM do VMware. Antes de realizar failback em uma máquina física, observe que:
* Uma máquina física protegida voltará como uma máquina virtual quando ele é feito o failover da tooVMware do Azure. Um computador físico do Windows Server 2008 R2 SP1, se ele é protegido e failover tooAzure, não pode ser feito novamente. Uma máquina Windows Server 2008 R2 SP1 que foi iniciado como uma máquina virtual local será capaz de toofail novamente.
* Certifique-se de que você descobrir que pelo menos um servidor de destino mestre junto com hello hosts ESX/ESXi necessários que você precisa toofail fazer.

Se você não toohello back VM original, o seguinte Olá é necessários:

* Se hello VM é gerenciada por um servidor do vCenter, hello host do ESX do destino mestre deve ter acesso toohello VMs repositório de dados.
* Se hello VM estiver em um host ESX, mas não é gerenciada pelo vCenter, de disco rígido Olá Olá VM deve ser em um repositório de dados que é acessível pelo host de saudação do MT.
* Se sua VM estiver em um host ESX e não usa o vCenter, você deve concluir a descoberta de host do ESX Olá de saudação MT antes que você proteja. Isso se aplicará se você também estiver realizando o failback de servidores físicos.
* Outra opção (se Olá local existe VM) é toodelete antes de você fazer um failback. Failback, em seguida, cria uma nova VM no hello mesmo host como host do ESX Olá destino mestre.

Quando houver falha local alternativo tooan voltar, dados de saudação são recuperado toohello mesmo repositório de dados e hello mesmo host ESX que é usada pelo servidor de destino mestre local hello.

## <a name="prerequisites"></a>Pré-requisitos
* toofail back VMs VMware e servidores físicos, é necessário um ambiente VMware. Falha na tooa back servidor físico não tem suporte.
* toofail novamente, você deve ter criado uma rede do Azure ao configurar proteção inicialmente. Failback precisa de uma conexão VPN ou rota expressa do hello Azure rede na qual Olá VMs do Azure são toohello localizado no site local.
* Se hello VMs que você deseja toofail fazer tooare gerenciado por um servidor vCenter, certifique-se de que você tenha permissões de saudação necessários para a descoberta de máquinas virtuais em servidores vCenter. Para obter mais informações, consulte [tooAzure de servidores físicos com o Azure Site Recovery e de máquinas virtuais VMware replicar](site-recovery-vmware-to-azure-classic.md).
* Se houver instantâneos em uma VM, a nova proteção vai falhar. Você pode excluir instantâneos hello ou discos de saudação.
* Antes de realizar o failback, crie estes componentes:
  * **Crie um Servidor de processos no Azure**. Esse componente é uma VM do Azure que você cria e mantém em execução durante o failback. Você pode excluir Olá VM após a conclusão do failback.
  * **Criar um servidor de destino mestre**: servidor de destino mestre Olá envia e recebe dados de failback. servidor de gerenciamento de saudação que você criou no local tem um servidor de destino mestre que é instalado por padrão. No entanto, dependendo do volume de saudação do tráfego de failback, talvez seja necessário toocreate um servidor de destino mestre separada para failback.
  * toocreate um servidor de destino mestre adicionais que executa no Linux, configurar Olá VM Linux antes de instalar o servidor de destino mestre hello, conforme descrito posteriormente.
* O servidor de configuração é necessário localmente para fazer um failback. Durante o failback, máquina virtual de saudação deve existir no banco de dados de servidor de configuração hello. Se o banco de dados de servidor de configuração Olá não contém nenhuma VM, failback não pode ser bem-sucedida. Sendo assim, certifique-se de fazer backups agendados regulares de seu servidor. Em um desastre, você precisa toorestore com hello de endereços IP mesmo para que o failback funcione.
* Definir configuração de disk.enableUUID=true saudação **parâmetros de configuração** do mestre de saudação de VM no VMware de destino. Se essa linha não existir, adicione-a. Essa configuração é necessária tooprovide um arquivo de disco (VMDK) consistente do identificador universalmente exclusivo (UUID) toohello máquina virtual para que ele está montado corretamente.
* Lembre-se de um "mestre de servidor de destino não pode ser armazenamento vMotioned" condição, o que pode causar Olá failback toofail. Olá VM não pode ser ativado, pois discos de saudação não ficam disponível tooit.
* Adicione uma unidade, chamada de uma unidade de retenção, no servidor de destino mestre hello. Adicionar um disco e formatar a unidade de saudação.

## <a name="failback-policy"></a>Política de failback
tooreplicate back tooon local, você precisa de uma diretiva de failback. política de saudação é criada automaticamente quando você criar uma política de frente, e é associada automaticamente com o servidor de configuração de saudação. Ela não é editável. política de saudação tem Olá as configurações de replicação a seguir:

* Limite RPO = 15 minutos
* Retenção de ponto de recuperação = 24 horas
* Frequência de instantâneos consistentes com aplicativos = 60 minutos

 ![Configurações de replicação de política de saudação de failback](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Crie um Servidor de processo no Azure
Instale um servidor de processo no Azure para que as VMs do Azure de saudação possa enviar o servidor de destino mestre do hello dados toohello back local.

Se você protegeu suas máquinas virtuais como recursos clássicos (ou seja, Olá recuperada de VM no Azure é uma VM que foi criada usando o modelo de implantação clássico Olá), é necessário um servidor de processo no Azure. Se você tiver recuperado Olá VMs com o Azure Resource Manager como tipo de implantação Olá, saudação do servidor em processo deve ter o Gerenciador de recursos como o tipo de implantação de saudação. Olá tipo de implantação é selecionado por hello Azure rede virtual que você implantar Olá servidor de processo.

1. Em **cofre** > **configurações** > **infraestrutura de recuperação de Site** (em **gerenciar**) > **Servidores de configuração** (em **para VMware e máquinas físicas**), selecione o servidor de configuração hello.
2. Clique em **Servidor de processo**.

  ![Botão Servidor de processo](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Escolha toodeploy Olá servidor de processo como **implantar um servidor de processo no Azure failback**.
4. Selecione a assinatura de saudação que você recuperou Olá VMs.
5. Selecione Olá rede do Azure que você recuperou Olá VMs. Olá toobe de necessidades de servidor de processo no hello que mesmo de rede para que Olá recuperados VMs e hello processo servidor pode se comunicar.
6. Se você tiver selecionado um *modelo de implantação clássico* de rede, crie uma VM por meio de saudação do Azure Marketplace e, em seguida, instalar saudação do servidor em processo nele.

 ![janela de "Adicionar servidor de processo" Hello](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Como a criação de saudação do servidor em processo, paga a seguir toohello atenção:
 * Olá nome da imagem de saudação é *V2 de servidor do Microsoft Azure Site Recovery processo*. Selecione **clássico** como modelo de implantação de saudação.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Instalar saudação do servidor em processo acordo toohello instruções [tooAzure de servidores físicos com o Azure Site Recovery e de máquinas virtuais VMware replicar](site-recovery-vmware-to-azure-classic.md).
7. Se você selecionar Olá *Gerenciador de recursos* Azure de rede, implantar saudação do servidor em processo fornecendo Olá informações a seguir:

  * nome de Olá Olá do grupo de recursos que você deseja que o servidor Olá toodeploy
  * nome de saudação do servidor de saudação
  * Um nome de usuário e senha para entrar no servidor toohello
  * conta de armazenamento Olá que você deseja que o servidor Olá toodeploy
  * subrede Hello e interface de rede de saudação que você deseja tooconnect tooit
   >[!NOTE]
   >Você deve criar seu próprio [interface de rede](../virtual-network/virtual-networks-multiple-nics.md) (NIC) e selecioná-la enquanto você estiver implantando saudação do servidor em processo.

    ![Insira as informações na caixa de diálogo "Adicionar servidor de processo" hello](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Clique em **OK**. Essa ação aciona um trabalho que cria uma máquina virtual de tipo de implantação de Gerenciador de recursos durante a instalação do servidor de processo hello. tooregister Olá toohello configuração servidor, configuração de execução hello dentro Olá VM, seguindo as instruções de saudação do [tooAzure de servidores físicos com o Azure Site Recovery e de máquinas virtuais VMware replicar](site-recovery-vmware-to-azure-classic.md). Saudação de toodeploy um trabalho do servidor em processo também é disparada.

  Olá servidor de processo está listado na Olá **servidores de configuração** > **associado servidores** > **servidores de processo** guia.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Olá servidor de processo não estiver visível em **propriedades da VM**. Ele só é visível Olá **servidores** guia no servidor de gerenciamento de saudação que ele está registrado. Pode levar 10 minutos too15 Olá tooappear de servidor de processo.


## <a name="set-up-hello-master-target-server-on-premises"></a>Configurar Olá destino mestre server local
o servidor de destino mestre Olá recebe dados de failback de saudação. servidor de saudação é instalado automaticamente no servidor de gerenciamento local hello, mas se você estiver falhando volta muitos dados, talvez seja necessário tooset um servidor de destino mestre adicionais. tooset backup mestre de um local do servidor de destino, Olá a seguir:

> [!NOTE]
> tooset um servidor de destino mestre no Linux, ignore toohello próximo procedimento. Use somente CentOS 6.6 sistema operacional mínimo como Olá o sistema operacional de destino mestre.

1. Se você estiver configurando o servidor de destino mestre Olá no Windows, abra a página de início rápido de saudação da saudação VM que você está instalando o servidor de destino mestre Olá.
2. Baixe o arquivo de instalação de saudação para o Assistente de configuração do Azure Site Recovery unificado hello.
3. Execute a instalação do hello e, na **antes de começar a**, selecione **adicionar tooscale adicional de servidores de processo implantação**.
4. Assistente de saudação completa no hello como fazia quando você [configurar o servidor de gerenciamento Olá](site-recovery-vmware-to-azure-classic.md). Em Olá **detalhes do servidor de configuração** página, especifique o endereço IP de saudação do servidor de destino mestre hello e insira uma saudação de tooaccess senha VM.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurar uma VM do Linux como servidor de destino mestre Olá
tooset o servidor de gerenciamento de saudação executando o servidor de destino mestre hello como uma VM do Linux, instale Olá CentOS 6.6 mínimos do sistema operacional. Em seguida, recuperar as IDs de SCSI Olá cada disco de SCSI, instalar alguns pacotes adicionais e aplicar algumas alterações personalizadas.

#### <a name="install-centos-66"></a>Instalar o CentOS 6.6

1. Instale Olá CentOS 6.6 mínimos do sistema operacional no servidor de gerenciamento de saudação VM. Lembre-Olá ISO em uma unidade de DVD e Olá sistema de inicialização. Ignore o teste de mídia de saudação. Selecione **inglês (EUA)** como linguagem hello, selecione **dispositivos de armazenamento básico**, verifique se Olá a unidade de disco rígido não tem dados importantes, clique em **Sim**e descartar todos os dados. Insira nome de host Olá saudação do servidor de gerenciamento e selecione o adaptador de rede do servidor de saudação.  Em Olá **sistema edição** caixa de diálogo, selecione **conectar automaticamente**e, em seguida, adicione um endereço IP estático, rede e as configurações de DNS. Especifique um fuso horário. tooaccess Olá servidor de gerenciamento, digite a senha de raiz de saudação.
2. Quando for perguntado que tipo de instalação que você deseja, selecione **Create Custom Layout** como partição de saudação. Clique em **Avançar**. Selecione **Gratuito** e, em seguida, clique em **Criar**. Crie partições **/**, **/var/crash** e **/home** com Tipo **FS:**  **ext4**. Criar partição de permuta hello como **FS tipo: troca**.
3. Se algum dispositivo pré-existente for encontrado, uma mensagem de aviso é exibida. Clique em **formato** tooformat unidade de saudação com configurações de partição de saudação. Clique em **gravação alterar toodisk** tooapply alterações de partição de saudação.
4. Selecione **carregador de inicialização de instalação** > **próximo** tooinstall carregador de inicialização Olá na partição de raiz de saudação.
5. Quando a saudação instalação for concluída, clique em **reinicializar**.

#### <a name="retrieve-hello-scsi-ids"></a>Recuperar as IDs de SCSI Olá

1. Após a instalação do hello, recupere Olá IDs de SCSI para cada disco rígido SCSI Olá VM. toodo assim, desligar o servidor de gerenciamento de saudação VM. Nas propriedades da VM Olá no VMware, com o botão direito entrada VM hello > **editar configurações de** > **opções**.
2. Escolha **Avançado** > **Item geral** e, em seguida, clique em **Parâmetros de Configuração**. Essa opção não está disponível quando a saudação máquina está em execução. Para toobe de opção Olá disponível, Olá máquina deve ser desligada.
3. Siga um destes procedimentos hello:
 * Se hello linha **em disco. EnableUUID** existir, certifique-se de que o valor de saudação está definido muito**True** (com distinção entre maiusculas e minúsculas). Se o valor de saudação já está definido tooTrue, você pode cancelar e testar o comando de SCSI hello dentro de um sistema operacional convidado após a inicialização.
 * Se hello linha **em disco. EnableUUID** não existe, clique em **Adicionar linha**e, em seguida, adicioná-la com hello **True** valor. Não use aspas duplas.

#### <a name="install-additional-packages"></a>Instalar pacotes adicionais
Baixe e instale os pacotes adicionais.

1. Verifique se o servidor de destino mestre Olá toohello conectado à Internet.
2. toodownload e pacotes de instalação 15 de repositório de CentOS hello, execute este comando: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Se as máquinas de origem de saudação protegendo estiverem executando o Linux com um Reiser ou XFS sistema para o dispositivo de inicialização ou raiz de saudação do arquivo, baixe e instale pacotes adicionais da seguinte maneira:

   * \# cd /usr/local
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \# rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \# wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \# rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#yum Instalar dispositivo mapeador-multipath (pacotes multipath tooenable necessária no servidor de destino mestre Olá)

#### <a name="apply-custom-changes"></a>Aplicar alterações personalizadas
Depois de concluir as etapas de pós-instalação hello e pacotes de saudação instalado, aplica alterações personalizadas fazendo Olá seguinte:

1. Copie toohello binário do hello RHEL 6-64 unificado agente VM. Olá toountar binário, execute este comando: `tar –zxvf <file name>`.
2. permissões de toogive, execute este comando: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Execução hello script a seguir: `# ./ApplyCustomChanges.sh`. Execute apenas uma vez. Depois que ele é executado com êxito, reinicie o servidor de saudação.

## <a name="run-hello-failback"></a>Execute o failback Olá
### <a name="reprotect-hello-azure-vms"></a>Proteja hello Azure VMs
1. Em **cofre**, na **replicadas itens**, Olá VM que tenha um failover e, em seguida, selecione **proteger novamente**.
2. Na folha de hello, você pode ver nessa direção Olá de proteção **tooOn-local do Azure** já está selecionado.
3. Em **servidor de destino mestre** e **servidor de processo**, selecione o servidor de destino mestre local hello e Olá servidor de processo de VM do Azure.
4. Olá selecione repositório de dados que você deseja que discos de saudação toorecover local para. Use essa opção quando Olá local VM é excluída e é necessário toocreate novos discos. Ignore a opção de saudação se hello discos já existem, mas você ainda precisa toospecify um valor.
5. Use pontos de saudação do toostop de unidade de retenção no tempo quando Olá VM é replicado back tooon local. Alguns critérios de uma unidade de retenção estão listados aqui. Sem esses critérios, unidade de saudação não está listada para o servidor de destino mestre hello.

  * O volume não deve estar em uso para nenhuma outra finalidade (destino de replicação, entre outros).
  * O volume não deve estar no modo de bloqueio.
  * O volume não deve ser o volume de cache. (instalação de destino mestre Olá não deve existir no volume. Olá servidor de processo mais mestre volume de instalação personalizada de destino não está qualificado para o volume de retenção. Aqui, Olá instalado o servidor de processo e volume de destino mestre é o volume de cache de saudação do destino mestre hello.)
  * tipo de sistema de arquivos de volume Olá não deve ser FAT e FAT32.
  * a capacidade de volume Olá deve ser diferente de zero.
  * volume de retenção saudação padrão para o Windows é o volume de R.
  * volume de retenção padrão Olá para Linux é /mnt/retention.

6. diretiva de failback Olá é selecionada automaticamente.
7. Depois de clicar em **Okey** toobegin reproteção, um trabalho começa tooreplicate Olá VM do Azure toohello no site local. Você pode acompanhar o progresso de saudação em Olá **trabalhos** guia.

Se você quiser toorecover tooan alternativo local, selecione a unidade de retenção de Olá e repositório de dados que estão configurados para o servidor de destino mestre Olá. Quando você não toohello Voltar no site local, Olá VMs VMware no plano de proteção de failback Olá usar Olá mesmo repositório de dados como o servidor de destino mestre hello. Se você quiser toorecover Olá réplica Azure VM toohello mesmo local VM, Olá a VM deve já estar em Olá mesmo no local como servidor de destino mestre de saudação do repositório de dados. Se não houver uma VM local, uma nova será criada durante a nova proteção.

![Selecione "Tooon-local do Azure" no menu suspenso de saudação](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Também é possível proteger novamente em um nível do plano de recuperação. Caso você tenha um grupo de replicação, ele só poderá ser protegido novamente com o uso de um plano de recuperação. Quando você proteger novamente usando um plano de recuperação, use valores anteriores Olá para todos os computadores protegidos.

> [!NOTE]
> Grupos de replicação devem ser protegidos com o hello mesmo destino mestre. Se forem protegidos novamente com um servidor de destino mestre diferente, não será possível determinar um ponto comum no tempo para eles.

### <a name="run-a-failover-toohello-on-premises-site"></a>Executar um failover toohello no site local
Depois que você proteja Olá VM, você pode iniciar um failover de local de tooon do Azure.

1. Na página de itens replicados hello, Olá VM e, em seguida, selecione **Failover não planejado**.
2. Em **confirmar Failover**, verifique se a direção do failover hello (do Azure) e, em seguida, selecione o ponto de recuperação de saudação que você deseja toouse para failover hello (Olá mais recente ou Olá último consistente com o aplicativo de ponto de recuperação). Um ponto de recuperação consistente de aplicativo ocorre antes do ponto mais recente Olá no tempo e causará perda de dados.
3. Durante o failover, recuperação de Site desliga Olá VMs do Azure. Depois de verificar que o failback foi concluído como esperado, você pode verificar tooensure hello Azure VMs ter sido desligadas conforme o esperado.

### <a name="reprotect-hello-on-premises-site"></a>Proteja Olá no site local
Depois de concluir o failback, confirmação Olá máquina virtual tooensure que Olá VMs recuperadas no Azure são excluídos. Assim, toodo clique item Olá protegido e, em seguida, clique em **confirmar**. Essa ação aciona um trabalho que remove Olá antiga máquinas virtuais recuperado no Azure.

Após a confirmação de hello, seus dados devem ser em Olá no site local, mas ele não estará protegido. tooAzure replicação toostart novamente, Olá a seguir:

1. Em **cofre**, na **configuração** > **replicadas itens**, selecione VMs Olá que falharam novamente e, em seguida, clique em **proteger novamente**.
2. Atribua o valor de saudação de saudação do servidor em processo que precisa toobe usado toosend dados back tooAzure.
3. Clique em **OK**.

Após concluir a reproteção hello, Olá VM replica tooAzure voltar e você pode fazer um failover.

### <a name="resolve-common-failback-issues"></a>Resolver problemas comuns de failback
* Se você executar a descoberta de vCenter de Usuário somente leitura e proteger as máquinas virtuais, ela terá êxito e o failover funcionará. Durante a nova proteção, o failover falhar porque Olá armazenamentos de dados não podem ser descobertos. Como um sintoma, você não verá Olá armazenamentos de dados listados durante a nova proteção. tooresolve esse problema, você pode atualizar credencial do vCenter Olá com uma conta apropriada que tenha permissões e repita o trabalho de saudação. Para obter mais informações, consulte [máquinas virtuais VMware replicar e tooAzure servidores físicos com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Quando você failback uma VM do Linux e executá-lo no local, você pode ver que esse pacote de Gerenciador de rede Olá foi desinstalado do computador hello. Essa desinstalação acontece porque o pacote do Gerenciador de rede Olá é removido quando Olá VM é recuperado no Azure.
* Quando uma máquina virtual é configurada com um endereço IP estático e failover tooAzure, endereço IP de saudação é adquirido por meio de DHCP. Quando houver falha local tooon voltar, Olá VM continua o endereço IP do toouse DHCP tooacquire hello. Manualmente entre toohello máquina e definir endereço estático de tooa back Olá de endereço IP, se necessário.
* Se você estiver usando a edição gratuita ESXi 5.5 ou a edição gratuita do 6 vSphere Hypervisor, o failover terá êxito, mas o failback, não. failback tooenable, licença de avaliação de atualização tooeither do programa.
* Se você não conseguir acessar o servidor de configuração de saudação de saudação do servidor em processo, verifique o servidor de configuração de toohello conectividade por máquina do servidor de configuração do Telnet toohello na porta 443. Você também pode tentar o servidor de configuração de saudação tooping da máquina do servidor de processo hello. Um servidor de processo também deve ter uma pulsação quando é conectado toohello servidor de configuração.
* Se você estiver tentando toofail tooan back alternativo vCenter, certifique-se de que seu novo vCenter foi descoberto e esse servidor de destino mestre Olá também é descoberto. Um sintoma típico é Olá armazenamentos de dados não são acessíveis ou visível no hello **proteja** caixa de diálogo.
* Uma máquina WS2008R2SP1 protegido como uma máquina física local não pode ser falha do local de tooon do Azure.

## <a name="fail-back-with-expressroute"></a>Failback com o ExpressRoute
Você pode realizar o failback em uma conexão VPN ou usando uma conexão ExpressRoute. Se você quiser toouse uma conexão de rota expressa, observe o seguinte hello:

* Olá conexão de rota expressa deve ser configurado em Olá rede virtual do Azure que máquinas de origem Olá failover tooand Olá VMs do Azure encontram após o failover de saudação.
* Os dados são replicado tooan conta de armazenamento do Azure em um ponto de extremidade público. toouse uma conexão de rota expressa, configurar o emparelhamento público na rota expressa com o Centro de dados de destino Olá para replicação de recuperação de Site.
