---
title: aaaReprotect de tooan do Azure no site local | Microsoft Docs
description: "Após o failover de máquinas virtuais tooAzure, você pode iniciar toobring um failback local de tooon back VMs. Saiba como tooreprotect antes de um failback."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Nova proteção do Azure tooan site local



## <a name="overview"></a>Visão geral
Este artigo descreve como tooreprotect Azure máquinas virtuais do Azure tooan no site local. Siga as instruções do hello neste artigo, quando você estiver pronto toofail fazer suas máquinas virtuais VMware ou servidores físicos do Windows/Linux depois que tiver falha de saudação local site tooAzure (conforme descrito em [replicar VMware virtual computadores e servidores físicos tooAzure com o Azure Site Recovery](site-recovery-failover.md)).

> [!WARNING]
> Você não pode falhar após você [concluir a migração](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), mover um grupo de recursos de tooanother de máquina virtual ou excluir uma máquina virtual do Azure.


Após a conclusão de que passou por failover e hello máquinas virtuais protegidas estiver replicando, você pode iniciar um failback em Olá máquinas virtuais toobring-los toohello no site local.

Poste comentários ou perguntas no final da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Para obter uma visão rápida, assista a saudação vídeo sobre como toofail através de tooan do Azure no site local a seguir.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Pré-requisitos
Quando você prepara as máquinas virtuais de tooreprotect, levar ou considere Olá ações pré-requisitos a seguir:

* Se um servidor do vCenter gerencia Olá de máquinas virtuais que você deseja toofail de volta para, certifique-se de que você tenha Olá [as permissões necessárias](site-recovery-vmware-to-azure-classic.md) para a descoberta de máquinas virtuais em servidores vCenter.

  > [!WARNING]
  > Se houver instantâneos no Olá no mestre destino ou hello máquina virtual local, que passou por failover falhar. Você pode excluir instantâneos Olá no destino mestre Olá antes de continuar tooreprotect. instantâneos de saudação na máquina virtual de saudação são mesclados automaticamente durante a nova proteção do trabalho.

* Antes de realizar o failback, crie dois componentes adicionais:

  * **Servidor de processo**: Olá [servidor de processo](site-recovery-vmware-setup-azure-ps-resource-manager.md) recebe dados da máquina virtual de saudação protegida no Azure e envia dados toohello no site local. Uma rede de baixa latência é necessária entre o servidor de processo Olá e máquina virtual de saudação protegida. Assim, você poderá ter um servidor de processo local se estiver usando uma conexão do Azure ExpressRoute ou um servidor de processo baseado no Azure e uma VPN.
  
  * **Servidor de destino mestre**: servidor de destino mestre Olá recebe dados de failback. servidor de gerenciamento local de saudação que você criou tem um servidor de destino mestre instalado por padrão. No entanto, dependendo do volume de saudação do tráfego de failback, talvez seja necessário toocreate um servidor de destino mestre separada para failback.
    * [Uma máquina virtual Linux precisa de um servidor de destino mestre do Linux](site-recovery-how-to-install-linux-master-target.md).
    * Uma máquina virtual Windows precisa de um servidor de destino mestre do Windows. Você pode usar o hello processo mestre e servidor de destino máquinas locais novamente.

    destino mestre Olá tem outros pré-requisitos listados na [toocheck de itens comuns em um destino mestre antes de nova proteção](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Um servidor de configuração é necessário localmente ao fazer um failback. Durante o failback, máquina virtual de saudação deve existir no banco de dados de servidor de configuração hello. Caso contrário, o failback será malsucedido. 

> [!IMPORTANT]
> Faça o backup agendado regular de seu servidor. de configuração. Se houver um desastre, restaure o servidor de saudação com hello mesmo IP de endereços para que funcione de failback.

* Saudação de conjunto `disk.EnableUUID=true` definindo parâmetros de configuração Olá Olá mestre virtual da máquina de destino no VMware. Se essa linha não existir, adicione-a. Essa configuração é necessária tooprovide um disco da máquina virtual de toohello do UUID consistente (VMDK) para que ele monta corretamente.

* *Você não pode usar vMotion de armazenamento no servidor de destino mestre Olá*. Isso pode causar Olá toofail de failback. máquina virtual de saudação não pode iniciar porque Olá discos não são tooit disponível. tooprevent esse problema, os servidores de destino mestre Olá excluir da lista vMotion.

* Adicionar um novo servidor de destino mestre unidade toohello: uma unidade de retenção. Adicione uma nova unidade de saudação do disco e o formato.


### <a name="frequently-asked-questions"></a>Perguntas frequentes

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>Por que preciso uma VPN S2S ou em um site de local ExpressRoute conexão tooreplicate dados toohello back?
Enquanto a replicação do local tooAzure pode acontecer em Olá Internet ou uma conexão com o emparelhamento público, que passou por failover e failback rota expressa exigem uma site a site (S2S) dados tooreplicate VPN. Fornece rede Olá para que Olá máquinas de virtuais de failover no Azure pode alcançar o servidor de configuração de local de saudação (ping). Você também pode implantar um servidor de processo no hello Azure rede da máquina de virtual Olá failover. Este servidor de processo também deve ser capaz de toocommunicate com o servidor de configuração local hello.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Quando instalar um servidor de processo no Azure?


Olá máquinas virtuais do Azure que você deseja tooreprotect enviar o servidor de processo de tooa de dados de replicação. Configure sua rede para que Olá máquinas virtuais do Azure pode alcançar o servidor de processo hello.

Você pode implantar um servidor de processo no Azure ou usar Olá existente servidor de processo que você usou durante o failover. Olá importante ponto tooconsider é dados da saudação toosend Olá latência na saudação de máquinas virtuais no servidor de processo toohello do Azure.

Se você tiver uma conexão de rota expressa configurado, você pode usar um processo servidor toosend de dados locais porque a latência de saudação entre Olá VM e o servidor de processo de saudação é insuficiente.

 ![Diagrama da arquitetura para ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



No entanto, se você tiver apenas uma VPN S2S, é recomendável implantar o servidor de processo Olá no Azure.

 ![Diagrama da arquitetura para VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


Lembre-se de que a replicação ocorra apenas em Olá VPN S2S ou hello privada de emparelhamento da sua rede de rota expressa. Certifique-se de que há largura de banda suficiente disponível através desse canal de rede.

Para obter informações sobre a instalação de um servidor de processo baseado no Azure, consulte [Gerenciar um servidor de processo em execução no Azure](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> É recomendável usar um servidor de processo com base no Azure durante o failback. desempenho da replicação Olá é maior se o servidor de processo de saudação é toohello mais próxima replicação de máquina virtual (Olá failover de máquina no Azure). No entanto, durante sua prova de conceito (POC) ou demonstração, você pode usar o servidor de processo de local de Olá junto com a rota expressa com hello emparelhamento toocomplete privada POC mais rápido.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>Quais portas devo abrir nos diferentes componentes para que a nova proteção possa funcionar?

![Portas para failover e failback](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>Qual servidor de destino mestre devo usar para a nova proteção?
Um servidor de destino mestre local é necessário tooreceive dados saudação do servidor de processo e, em seguida, gravar VMDK toohello local na máquina virtual. Se você estiver protegendo máquinas virtuais do Windows, precisará de um servidor de destino mestre do Windows. Você pode reutilizar o servidor de processo Olá local e o destino mestre<!-- !todo component -->. Para máquinas virtuais Linux, você precisa tooset a um destino mestre do Linux de locais adicionais.


Para obter informações sobre como instalar um servidor de destino mestre, consulte:

* [Como o servidor de destino de mestre tooinstall Windows](site-recovery-vmware-to-azure.md)
* [Como o servidor de destino de mestre tooinstall Linux](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>Quais tipos de repositório de dados têm suporte no host de ESXi Olá local durante o failback?

No momento, recuperação de Site do Azure dá suporte a falha faça apenas tooa sistema de arquivos de máquina virtual (VMFS) ou vSAN repositório de dados. Não há suporte para um armazenamento de dados NFS. Devido a limitação de toothis, seleção de repositório de dados Olá entrada hello nova proteção de tela está vazia no caso de saudação de armazenamentos de dados do NFS ou mostra o armazenamento de dados do hello vSAN, mas falhar durante o trabalho de saudação. Se você pretende toofail novamente, você pode criar um repositório de dados VMFS local e falhar tooit voltar. Este failback fará com que um download completo do hello VMDK.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Comuns toocheck coisas depois de concluir a instalação do servidor de destino mestre Olá

* Se hello máquina virtual está presente no local em Olá servidor vCenter, hello servidor de destino mestre precisa acessar VMDK toohello local na máquina virtual. O acesso é necessário toowrite Olá replicado dados toohello discos máquina virtual. Verifique se o que repositório de dados da máquina que Olá local virtual está montado no host de destino mestre saudação com acesso de leitura/gravação.

* Se a máquina virtual de saudação não está presente no local no servidor do vCenter hello, Olá serviço de recuperação de Site deve toocreate uma nova máquina virtual durante a nova proteção. Esta máquina virtual é criada no host do ESX Olá na qual você cria o destino mestre hello. Escolha um host ESX Olá com cuidado, para que a máquina de virtual de failback Olá é criada no host de saudação que você deseja.

* *Você não pode usar vMotion de armazenamento para o servidor de destino mestre Olá*. Isso pode causar Olá toofail de failback. máquina virtual de saudação não pode iniciar porque Olá discos não são tooit disponível.

  > [!WARNING]
  > Se um destino mestre sofrer uma tarefa de vMotion de armazenamento após a reproteção, Olá protegido discos de máquinas virtuais que são o destino mestre toohello anexado migrar toohello destino da tarefa de vMotion hello. Se você tentar toofail após isso, desconexão do disco Olá falhará porque não foram encontrados discos hello. Então se torna toofind rígido discos de saudação em suas contas de armazenamento. Você precisa toofind-los manualmente e anexá-los a máquina virtual de toohello. Depois disso, a máquina virtual no local, Olá pode ser inicializada.

* Adicione um retenção unidade tooyour existente Windows servidor de destino mestre. Adicione uma nova unidade de saudação do disco e o formato. unidade de retenção de saudação é usado toostop Olá pontos no tempo quando a máquina virtual de saudação são replicados toohello Voltar no site local. A seguir estão alguns critérios de uma unidade de retenção. Sem esses critérios, unidade de saudação não será listada para o servidor de destino mestre hello.

   * volume de saudação não é usado para nenhum outro propósito, como um destino de replicação.

   * Olá volume não está no modo de bloqueio.

   * volume de saudação não é um volume de cache. instalação de destino mestre Olá não deve existir no volume. volume de instalação personalizada Olá para Olá processo mestre e servidor de destino não está qualificado para um volume de retenção. Quando o servidor de processo de saudação e de destino mestre estão instalados em um volume, o volume de saudação é um volume de cache de destino mestre hello.

   * tipo de sistema de arquivos de saudação do volume de saudação não é FAT ou FAT32.

   * a capacidade de volume Olá é diferente de zero.

   * volume de retenção saudação padrão para o Windows é o volume de saudação R.

   * volume de retenção padrão Olá para Linux é /mnt/retention.

  > [!IMPORTANT]
  > Se você estiver usando uma máquina de servidor de configuração do servidor de processo existente ou uma escala ou um computador de servidor de destino do processo mestre/servidor, você precisa tooadd uma nova unidade. nova unidade de saudação deve atender Olá anterior requisitos. Se não houver uma unidade de retenção hello, ele não aparecer na lista de lista suspensa de seleção Olá no portal de saudação. Depois de adicionar um destino mestre do toohello no local de unidade, ela ocupa too15 minutos para Olá unidade tooappear seleção Olá no portal de saudação. Você também pode atualizar o servidor de configuração de saudação se unidade Olá não aparecer após 15 minutos.

* Uma máquina virtual do Linux que passou por failover exige um servidor de destino mestre do Linux. Uma máquina virtual do Windows após failover precisa de um servidor de destino mestre do Windows.

* Instale as ferramentas do VMware no servidor de destino mestre hello. Sem as ferramentas do VMware hello, Olá armazenamentos de dados no host de ESXi do destino mestre Olá não podem ser detectados.

* Habilitar Olá `disk.EnableUUID=true` parâmetro na máquina de virtual de destino mestre hello usando Olá vCenter propriedades. <!-- !todo Needs link. -->

* destino mestre Olá deve ter pelo menos um datastore VMFS anexado. Se não houver nenhum, Olá **Datastore** entrada na página de nova proteção Olá estará vazia e não pode continuar.

* o servidor de destino mestre Olá não pode ter instantâneos de discos de saudação. Se houver instantâneos, a nova proteção e o failback falharão.

* destino mestre Olá não pode ter um controlador SCSI Paravirtual. controlador Olá só pode ser um controlador LSI lógica. Sem um controlador de Lógica LSI, a nova proteção falha.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Etapas tooreprotect

> [!NOTE]
> Depois de inicializar uma máquina virtual no Azure, levará algum tempo para agente Olá tooregister toohello back configuração server (too15 minutos). Durante esse tempo, que passou por failover falhará e uma mensagem de erro indica que o agente de saudação não está instalado. Aguarde alguns minutos e tente a nova proteção outra vez.



1. Em **cofre** > **replicadas itens**, Olá VM que passou por failover e, em seguida, selecione **proteger novamente**. Você também pode clicar em Olá máquina e selecione **proteger novamente** de botões de comando hello.
2. Na folha de Olá, observe a direção Olá de proteção, **tooOn-local do Azure**, já está selecionado.
3. Em **servidor de destino mestre** e **servidor de processo**, selecione o servidor de destino mestre local hello e Olá servidor de processo.
4. Para **Datastore**, selecione Olá toowhich repositório de dados que você deseja toorecover Olá discos locais. Essa opção é usada quando a máquina virtual no local, Olá é excluída e você precisa toocreate novos discos. Essa opção será ignorada se discos Olá já existem, mas você ainda precisa toospecify um valor.
5. Escolha a unidade de retenção de saudação.
6. diretiva de failback Olá é selecionada automaticamente.
7. Clique em **Okey** toobegin que passou por failover. Um trabalho começa tooreplicate Olá VM do Azure toohello no site local. Você pode acompanhar o progresso de saudação em Olá **trabalhos** guia.

Se você quiser toorecover tooan local alternativo (quando a máquina virtual no local, Olá é excluída), selecione a unidade de retenção hello e repositório de dados que estão configurados para o servidor de destino mestre hello. Quando você não toohello Voltar no site local, hello VMware máquinas virtuais em uso de plano de proteção de failback Olá Olá mesmo repositório de dados como Olá mestre servidor de destino. Então, uma nova máquina virtual é criada no vCenter.

Se você quiser toorecover Olá máquina virtual existente do Azure tooan máquina virtual local, Olá de montagem local armazenamentos de dados da máquina virtual com acesso de leitura/gravação no host de ESXi do servidor de destino mestre hello.
    ![Proteger novamente a caixa de diálogo](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Você também pode proteger novamente no nível de saudação de um plano de recuperação. Um grupo de replicação pode ser protegido novamente somente por meio de um plano de recuperação. Quando você proteger novamente usando um plano de recuperação, você precisa os valores hello tooprovide para todos os computadores protegidos.

> [!NOTE]
> Use Olá mesmo tooreprotect de servidor de destino mestre em um grupo de replicação. Se você usar um servidor de destino mestre diferente tooreprotect um grupo de replicação, servidor de saudação não pode fornecer um ponto de comuns no tempo.

> [!NOTE]
> máquina virtual local, Olá é desligada durante a reproteção. Isso ajuda a garantir a consistência de dados durante a replicação. Não ligar Olá máquina virtual após a conclusão da nova proteção.

Depois que a reproteção Olá for bem-sucedida, máquina virtual de saudação entrará em um estado protegido.

## <a name="next-steps"></a>Próximas etapas

Depois de máquina virtual de saudação entrou em um estado protegido, você poderá [iniciar um failback](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

Olá failback desligará Olá máquina virtual do Azure e máquina virtual local, inicialização hello. Espere algum tempo de inatividade para o aplicativo hello. Escolha um horário para failback quando o aplicativo hello pode tolerar tempo de inatividade.

## <a name="common-problems"></a>Problemas comuns

* Se você tiver usado um modelo toocreate suas máquinas virtuais, certifique-se de que cada máquina virtual tem seu próprio UUID para discos de saudação. Se Olá local conflitos de UUID da máquina virtual com o de destino mestre Olá porque ambos criadas a partir de saudação mesmo modelo, que passou por failover falhar. Implantar outro destino mestre que não foi criado de saudação mesmo modelo.

* Se você executar a descoberta de vCenter de Usuário somente leitura e proteger as máquinas virtuais, a proteção terá êxito e o failover funcionará. Durante a nova proteção, o failover falhar porque Olá armazenamentos de dados não podem ser descobertos. Um sintoma é que hello armazenamentos de dados não estão listados durante que passou por failover. tooresolve esse problema, você pode atualizar a credencial do vCenter Olá com uma conta apropriada que tenha permissões, e tente novamente o trabalho de saudação. Para obter mais informações, consulte [tooAzure de servidores físicos com o Azure Site Recovery e de máquinas virtuais VMware replicar](site-recovery-vmware-to-azure-classic.md).

* Quando você failback de uma máquina virtual Linux e executá-lo no local, você pode ver que esse pacote de Gerenciador de rede Olá foi desinstalado do computador hello. Essa desinstalação acontece porque o pacote do Gerenciador de rede Olá é removido quando a máquina virtual de saudação é recuperada no Azure.

* Quando uma máquina virtual Linux é configurada com um endereço IP estático e failover tooAzure, endereço IP de saudação é adquirido do DHCP. Quando você fizer failover tooon local, a máquina virtual em Olá continua o endereço IP do toouse DHCP tooacquire hello. Manualmente entrar toohello máquina e definir endereço estático de tooa back Olá de endereço IP, se necessário. Uma máquina virtual Windows pode adquirir novamente seu endereço IP estático.

* Se você usa a edição gratuita ESXi 5.5 ou a edição gratuita do 6 vSphere Hypervisor, o failover tem êxito, mas não acontece. failback tooenable, licença de avaliação de atualização tooeither do programa.

* Se você não conseguir acessar o servidor de configuração de saudação saudação do servidor de processo, use o servidor de configuração do Telnet toocheck conectividade toohello na porta 443. Você também pode tentar o servidor de configuração de saudação tooping saudação do servidor de processo. Um servidor de processo também deve ter uma pulsação quando é conectado toohello servidor de configuração.

* Se você estiver tentando toofail tooan back alternativo vCenter, certifique-se de que seu novo vCenter e o servidor de destino mestre Olá sejam descobertos. Um sintoma típico é Olá armazenamentos de dados não são acessíveis ou visível no hello **proteja** caixa de diálogo.

* Um servidor do Windows Server 2008 R2 SP1 que é protegido como um físico servidor local não pode ser falha do site do Azure tooan local.
