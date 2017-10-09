---
title: "aaaFail fazer VMware VMs do Azure no portal clássico Olá | Microsoft Docs"
description: "Saiba mais sobre a falha toohello back local após o failover de máquinas virtuais do VMware e servidores físicos tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Fazer back máquinas virtuais de VMware e servidores físicos toohello no site local (portal clássico)
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portal Clássico do Azure](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portal Clássico do Azure (Herdado)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Este artigo descreve como toofail fazer máquinas virtuais do Azure de site do Azure toohello local. Siga as instruções do hello neste artigo, quando você estiver pronto toofail fazer suas máquinas virtuais VMware ou servidores físicos do Windows/Linux depois que tiver falha de saudação local site tooAzure usando esse [tutorial](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Visão geral
Este diagrama mostra a arquitetura de failback Olá para esse cenário.

Use essa arquitetura ao servidor de processo de saudação é local e você estiver usando uma rota expressa.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Use essa arquitetura ao servidor de processo Olá é no Azure e você tiver uma VPN ou uma conexão de rota expressa.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

lista completa de saudação de toosee de portas e diagrama de arquitetura de failback Olá consulte toohello imagem abaixo

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Veja a seguir como o failback funciona:

* Após o failover tooAzure, você não tooyour back local em alguns estágios:
  * **Estágio 1**: Proteja hello Azure VMs para que eles são iniciados replicando tooVMware back VMs em execução no seu site local. Habilitando a reproteção move Olá VM em um grupo de proteção de failback criada automaticamente quando você criou o grupo de proteção de failover Olá originalmente. Se você adicionou seu plano de recuperação failover proteção grupo tooa grupo de proteção de failback Olá automaticamente foi adicionado toohello plano.  Durante a nova proteção, você especificar como tooplan toofail fazer.
  * **Fase 2**: depois que suas VMs do Azure estiver replicando tooyour no site local, execute uma falha em toofail do Azure.
  * **Fase 3**: após a falharam volta seus dados, você proteja Olá VMs locais que você não faça, para que eles são iniciados replicando tooAzure.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Failback toohello original ou alternativo local
Se o failover de uma VM do VMware, você pode fazer back toohello mesmo VM de origem, se ele ainda existe no local. Neste cenário apenas as alterações do delta Olá realizarão novamente. Observe que:

* Se você fez failover servidores físicos e failback sempre é tooa nova VM do VMware.
  * Antes de realizar failback em uma máquina física, observe que
  * Máquina física protegida voltará como uma máquina Virtual quando o failover do Azure tooVMware
  * Certifique-se de que você descobrir que pelo menos um servidor de destino mestre junto com toowhich de hosts ESX/ESXi necessário Olá necessário toofailback.
* Você pode realizar failback toohello original VM Olá, é necessário:

  * Se hello VM é gerenciada por um servidor do vCenter host do ESX do destino do hello mestre deve ter acesso toohello VMs datastore.
  * Se hello VM estiver em um host ESX, mas não é gerenciada pelo vCenter depois de disco rígido Olá Olá VM deve ser em um repositório de dados acessível pelo host de saudação do MT.
  * Se sua VM estiver em um host ESX e não usa o vCenter você deve concluir a descoberta de host do ESX Olá de saudação MT antes de você proteger novamente. Isso se aplicará se você também estiver realizando o failback de servidores físicos.
  * Outra opção (se Olá local existe VM) é toodelete antes de você fazer um failback. Em seguida, failback, em seguida, criará uma nova VM no hello mesmo host como host do ESX Olá destino mestre.
* Quando dados de saudação do failback tooan local alternativo será recuperado toohello mesmo repositório de dados e hello mesmo host ESX que é usada pelo servidor de destino mestre local hello.

## <a name="prerequisites"></a>Pré-requisitos
* Você precisará de um ambiente VMware em volta de toofail de ordem VMs VMware e servidores físicos. Falha na tooa back servidor físico não tem suporte.
* Em ordem toofail volta você deve ter criado uma rede do Azure quando configurar inicialmente a proteção. Failback precisa de uma conexão VPN ou rota expressa do hello Azure rede na qual Olá VMs do Azure são toohello localizado no site local.
* Se Olá VMs que você deseja toofail tooare back gerenciado por um servidor vCenter, você precisará toomake se que você tem permissões de saudação necessários para a descoberta de máquinas virtuais em servidores vCenter. [Leia mais](site-recovery-vmware-to-azure-classic.md).
* Se houver instantâneos em uma VM, a nova proteção falhará. Você pode excluir instantâneos hello ou discos de saudação.
* Antes de você failback, você precisará toocreate vários componentes:
  * **Crie um servidor de processos no Azure**. Isso é uma VM do Azure que você precisará toocreate e em execução durante o failback. Você pode excluir a máquina de saudação após a conclusão do failback.
  * **Criar um servidor de destino mestre**: servidor de destino mestre Olá envia e recebe dados de failback. servidor de gerenciamento de saudação criada no local tem um servidor de destino mestre instalado por padrão. No entanto, dependendo do volume de saudação do tráfego de backup com falha, talvez seja necessário toocreate um servidor de destino mestre separada para failback.
  * Se você quiser toocreate um servidor de destino mestre adicionais em execução no Linux, você precisará tooset backup Olá VM Linux antes de instalar o servidor de destino mestre hello, conforme descrito abaixo.
* O servidor de configuração é necessário localmente para fazer um failback. Durante o failback, máquina virtual de saudação deve existir no hello configuração servidor banco de dados, falhando o failback não seja bem-sucedida. Sendo assim, certifique-se de fazer o backup agendado regular de seu servidor. No caso de um desastre, você precisará toorestore com hello mesmo endereço IP para que o failback funcione.

## <a name="set-up-hello-process-server-in-azure"></a>Configurar o servidor de processo Olá no Azure
É necessário tooinstall um servidor de processo no Azure para que hello Azure VMs pode enviar o servidor de destino mestre Olá dados back tooon local.

1. No portal de recuperação de Site hello > **servidores de configuração** selecione tooadd um novo servidor de processo.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Especifique um nome de servidor de processo e insira um nome e a senha que você usará tooconnect toohello VM do Azure como administrador. Em **servidor de configuração** Selecionar servidor de gerenciamento local hello e especificar hello Azure rede na qual saudação do servidor em processo deve ser implantado. Isso deve ser rede Olá no qual hello Azure VMs estão localizadas. Especifique um endereço IP exclusivo da sub-rede selecione hello e iniciar a implantação.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Um servidor de processo do trabalho toodeploy Olá será disparado

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Depois de saudação do servidor em processo é implantado no Azure pode fazer logon usando credenciais de saudação especificado. Olá primeira vez que você faça logon na caixa de diálogo de servidor de processo Olá será executado. Digite hello endereço IP do servidor de gerenciamento local hello e sua senha. Deixe a configuração de porta 443 saudação padrão. Você também pode deixar Olá porta de 9443 padrão para replicação de dados, a menos que especificamente você modificou esta configuração quando você configura o servidor de gerenciamento de local de saudação.

   > [!NOTE]
   > servidor de saudação não ficarão visível em **propriedades da VM**. Só é visível em Olá **servidores** guia Olá toowhich de servidor de gerenciamento está registrado. Ele pode levar cerca de 10 a 15 minutos para Olá tooappear de servidor de processo.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Configurar Olá destino mestre server local
o servidor de destino mestre Olá recebe dados de failback de saudação. Um servidor de destino mestre é instalado automaticamente no servidor de gerenciamento local hello, mas se você estiver falhando volta muitos dados, talvez seja necessário tooset um servidor de destino mestre adicionais. Faça isso da seguinte forma:

> [!NOTE]
> Se você quiser tooinstall um servidor de destino mestre no Linux, siga as instruções de saudação no procedimento a seguir hello.
>
>

1. Se você estiver instalando o servidor de destino mestre Olá no Windows, abra a página de início rápido de Olá Olá VM em que estiver instalando o servidor de destino mestre hello e baixar o arquivo de instalação Olá para o Assistente de configuração do Azure Site Recovery unificado hello.
2. Execute a instalação e, em **antes de começar a** selecione **adicionar tooscale de servidores de processo adicional implantação**.
3. Assistente de saudação completa no hello como fazia quando você [configurar o servidor de gerenciamento Olá](site-recovery-vmware-to-azure-classic.md). Em Olá **detalhes do servidor de configuração** , especifique o endereço IP hello este servidor de destino mestre e saudação de tooaccess uma frase secreta VM.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurar uma VM do Linux como servidor de destino mestre Olá
sistema de operacional mínimo S 6.6 de tooset o servidor de gerenciamento de Olá executando o servidor de destino mestre hello como uma VM, você precisará tooinstall Olá centavos Linux), recuperar as IDs de SCSI Olá cada disco de SCSI, instalar alguns pacotes adicionais e aplicar algumas alterações personalizadas.

#### <a name="install-centos-66"></a>Instalar o CentOS 6.6
1. Instale Olá CentOS 6.6 mínimos do sistema operacional no servidor de gerenciamento de saudação VM. Lembre-Olá ISO em um sistema de saudação de inicialização e a unidade de DVD. Ignorar Olá mídia de teste, selecione inglês (EUA) no idioma hello, selecione **dispositivos de armazenamento básico**, verifique se Olá a unidade de disco rígido não tem dados importantes e clique em **Sim**, descartar todos os dados. Insira nome de host Olá saudação do servidor de gerenciamento e selecione o adaptador de rede do servidor de saudação.  Em Olá **sistema edição** caixa de diálogo Selecionar * * conectar automaticamente * * e adicionar um endereço IP estático, rede e as configurações de DNS. Especifique um fuso horário e um servidor de gerenciamento raiz senha tooaccess hello.
2. Quando perguntado tipo hello de instalação que deseja selecionar **Create Custom Layout** como partição de saudação. Depois de clicar em **Avançar** select **Gratuito** e clique em Criar. Crie partições **/**, **/var/crash** e **/home** com Tipo **FS:**  **ext4**. Criar a partição de troca hello como **FS tipo: troca**.
3. Se algum dispositivo pré-existente for encontrado, uma mensagem de aviso será exibida. Clique em **formato** tooformat unidade de saudação com configurações de partição de saudação. Clique em **gravação alterar toodisk** tooapply alterações de partição de saudação.
4. Selecione **carregador de inicialização de instalação** > **próximo** tooinstall carregador de inicialização Olá na partição de raiz de saudação.
5. Após a conclusão da instalação, clique em **Reiniciar**.

#### <a name="retrieve-hello-scsi-ids"></a>Recuperar as IDs de SCSI Olá
1. Após a instalação recupere Olá IDs de SCSI para cada disco rígido SCSI Olá VM. toodo isso desligar o servidor de gerenciamento de saudação VM, no hello VM propriedades no VMware clique entrada VM hello > **editar configurações de** > **opções**.
2. Escolha **Avançado** > **Item geral** e clique em **Parâmetros de Configuração**. Essa opção será de-active quando Olá máquina está em execução. toomake it Olá active máquina deve ser desligada.
3. Se hello linha **em disco. EnableUUID** existe Verifique se o valor de saudação está definido muito**True** (com distinção entre maiusculas e minúsculas). Se já estiver, você pode cancelar e testar o comando de SCSI hello dentro de um sistema operacional convidado após a inicialização.
4. Se a linha hello não existente clique **Adicionar linha** – e adicioná-la com hello **True** valor. Não use aspas duplas.

#### <a name="install-additional-packages"></a>Instalar pacotes adicionais
Você precisa toodownload e instalar alguns pacotes adicionais.

1. Verifique se o servidor de destino mestre Olá é toohello conectado à internet.
2. Execute toodownload esse comando e instalar 15 pacotes do repositório de CentOS Olá: **# yum instalar – y xfsprogs perl lsscsi rsync wget kexec-tools**.
3. Se estiver executando máquinas de origem Olá que estiver protegendo Linux wit Reiser XFS sistema para a raiz de saudação de arquivos ou dispositivo de inicialização, você deverá baixar e instalar outros pacotes da seguinte maneira:

   * # <a name="cd-usrlocal"></a>cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Aplicar alterações personalizadas
Faça Olá alterações personalizadas tooapply a seguir após a etapas de pós-instalação Olá completa e pacotes de saudação instalado:

1. Copie toohello binário do hello RHEL 6-64 unificado agente VM. Executar este Olá toountar de comando binário: **tar – zxvf<file name>**
2. Permissões de toogive esse comando de execução: **# chmod 755./ApplyCustomChanges.sh**
3. Execute o script hello: **./ApplyCustomChanges.sh #**. Você só deve executar script hello uma vez. Reinicialize o servidor de saudação após Olá script ser executado com êxito.

## <a name="run-hello-failback"></a>Execute o failback Olá
### <a name="reprotect-hello-azure-vms"></a>Proteja hello Azure VMs
1. No portal de recuperação de Site hello > **máquinas** selecione Olá VM que passou por failover e clique em **proteger novamente**.
2. Em **servidor de destino mestre** e **servidor de processo** Selecionar servidor de destino mestre local hello e servidor de processo Olá VM do Azure.
3. Selecione a conta de saudação configurado para se conectar toohello VM.
4. Selecione a versão de failback de Olá Olá do grupo de proteção. Por exemplo, se Olá VM está protegido na PG1, em seguida, você precisará tooselect PG1_Failback.
5. Se você quiser toorecover tooan alternativo local, selecione unidade de retenção hello e configurado para o servidor de destino mestre de saudação do repositório de dados. Quando você não toohello back local site Olá VMs VMware no plano de proteção de failback Olá usará Olá mesmo repositório de dados como o servidor de destino mestre hello. Se você quiser toorecover Olá réplica Azure VM toohello mesmo local VM, Olá VM deve já ao local ser em Olá mesmo repositório de dados como Olá mestre servidor de destino. Se não houver uma VM local, uma nova será criada durante a nova proteção.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Depois de clicar em **Okey** toobegin reproteção um trabalho começa tooreplicate Olá VM do Azure toohello no site local. Você pode acompanhar o progresso de saudação em Olá **trabalhos** guia.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Executar um failover toohello no site local
Após Olá reproteção VM é movido toohello failback versão de seu grupo de proteção e é adicionada automaticamente o plano de recuperação de toohello que você usou para Olá tooAzure de failover, se houver um.

1. Em Olá **planos de recuperação** plano de recuperação Olá select de página que contém o grupo de failback hello e clique em **Failover** > **Failover não planejado**.
2. Em **confirmar Failover** Verifique a direção do failover hello (tooAzure) e selecione o ponto de recuperação de saudação desejado toouse Olá failover (mais recente). Se você habilitou o **várias VMs** ao configurar propriedades de replicação pode recuperar o aplicativo mais recente toohello ou ponto de recuperação consistente. Clique em Olá marca de seleção toostart Olá failover.
3. Durante o failover de recuperação de Site será encerrado Olá VMs do Azure. Depois de verificar que o failback foi concluído como esperado, você pode no qual você pode verificar que Olá que VMs do Azure ter sido desligadas conforme o esperado.

### <a name="reprotect-hello--on-premises-site"></a>Proteja Olá no site local
Após a conclusão do failback seus dados de volta no Olá no site local, mas não estará protegidos. tooAzure replicação toostart novamente Olá a seguir:

1. No portal de recuperação de Site hello > **máquinas** guia VMs Olá select que falharam novamente e clique em **proteger novamente**.
2. Depois de verificar que tooAzure de replicação está funcionando conforme o esperado, no Azure, você pode excluir Olá máquinas virtuais do Azure (não está em execução) que foram falha novamente.

### <a name="common-issues-in-failback"></a>Problemas Comuns de failback
1. Se você executar a descoberta de vCenter de Usuário Somente Leitura e proteger as máquinas virtuais, ela terá êxito e o failover funcionará. Em tempo de saudação de nova proteção, ele falhará pois Olá armazenamentos de dados não podem ser descobertos. Como um sintoma você não verá Olá armazenamentos de dados relacionados ao proteger novamente. tooresolve isso, você pode atualizar credencial do vCenter Olá com conta apropriada que tenha permissões e repita o trabalho de saudação. [Leia mais](site-recovery-vmware-to-azure-classic.md)
2. Quando você failback uma VM do Linux e execute-o no local, você verá esse pacote de Gerenciador de rede Olá é desinstalado do computador hello. Isso ocorre porque quando Olá VM é recuperado no Azure, o pacote de Gerenciador de rede de saudação é removido.
3. Quando uma máquina virtual é configurada com o endereço IP estático e failover tooAzure, endereço IP de saudação é adquirido por meio de DHCP. Quando houver falha local tooOn voltar, Olá VM continua o endereço IP do toouse DHCP tooacquire hello. Você precisará toomanually logon na máquina hello e definir o endereço IP de saudação fazer tooStatic endereço, se necessário.
4. Se você estivesse usando a edição gratuita ESXi 5.5 ou a edição gratuita do 6 vSphere Hypervisor, o failover teria êxito, mas isso não acontecerá. Você vai precisam tooupgrade tooeither licença de avaliação tooenable failback.

## <a name="failing-back-with-expressroute"></a>Realizar o failback com o ExpressRoute
Você pode realizar o failback em uma conexão VPN ou pelo Azure ExpressRoute. Se você desejar a seguir toouse ExpressRoute Observação hello:

* Rota expressa deve ser configurada no momento da saudação rede virtual do Azure toowhich fonte máquinas falha em, em que as VMs do Azure estão localizadas após o failover de saudação.
* Os dados são replicado tooan conta de armazenamento do Azure em um ponto de extremidade público. Você deve configurar o emparelhamento público na rota expressa com o Centro de dados de destino Olá para recuperação de Site replicação toouse rota expressa.
