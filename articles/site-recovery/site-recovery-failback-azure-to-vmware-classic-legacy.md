---
title: "aaaFail fazer VMware VMs do Azure no portal clássico de herdado Olá | Microsoft Docs"
description: "Este artigo descreve como toofail voltar uma máquina virtual VMware que tenha sido replicada tooAzure com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Fazer back máquinas virtuais de VMware e servidores físicos do tooVMware do Azure com o Azure Site Recovery (o legados)
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portal Clássico do Azure](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portal Clássico do Azure (Herdado)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Este artigo descreve como toofail back VMs VMware e servidores físicos do Windows/Linux do Azure tooyour no site local depois que você tenha replicado do local do site usando tooAzure [do Azure Site Recovery?](site-recovery-overview.md).

Este artigo descreve uma configuração antiga e não deve ser usado para novos cofres.

## <a name="architecture"></a>Arquitetura
Este diagrama representa um cenário de failover e failback de saudação. linhas de saudação azul são conexões Olá usadas durante o failover. linhas de saudação vermelho são conexões Olá usados durante o failback. linhas de saudação com setas ir Olá internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Antes de começar
* Você deve ter feito failover em suas máquinas virtuais VMware ou servidores físicos e eles devem estar em execução no Azure.
* Observe que você somente poderá falhar back máquinas virtuais de VMware e servidores físicos do Windows/Linux de máquinas virtuais de tooVMware do Azure no site primário do hello local.  Se você estiver falhando novamente um computador físico, failover tooAzure converterá tooan VM do Azure e failback tooVMware converterá tooa VM do VMware.

Veja como configurar o failback:

1. **Configurar componentes do failback**: você precisará tooset um servidor vContinuum no local e aponte-o servidor de configuração de toohello VM no Azure. Você também vai configurar um servidor de processo como um servidor de destino mestre VM do Azure toosend dados toohello back local. Registrar servidor de processo Olá com servidor de configuração de saudação que tratada Olá failover. Instale um servidor de destino mestre local. Se você precisar de um servidor de destino mestre Windows, ele será configurado automaticamente quando o vContinuum for instalado. Se você precisar de Linux, você precisará tooset-o manualmente em um servidor separado.
2. **Habilitar a proteção e failback**: depois de configurar os componentes de hello, em vContinuum você precisará tooenable proteção para o failover de máquinas virtuais do Azure. Você executar uma verificação de preparação Olá VMs e executar um failover de tooyour do Azure no site local. Após a conclusão do failback Proteja computadores locais, para que eles são iniciados replicando tooAzure.

## <a name="step-1-install-vcontinuum-on-premises"></a>Etapa 1: Instalar o vContinuum no local
Você precisa tooinstall um servidor vContinuum localmente e aponte-o servidor de configuração de toohello.

1. [Baixar o vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).
2. Baixe o hello [vContinuum atualização](http://go.microsoft.com/fwlink/?LinkID=533813) versão.
3. Instale a versão mais recente de saudação do vContinuum. Em Olá **bem-vindo** página clique **próximo**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Na primeira página de saudação do Assistente de saudação de especificar o endereço IP do servidor CX hello e porta do servidor CX hello. Escolha **Usar HTTPS**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Localizar o servidor de configuração de saudação endereço IP no hello **painel** guia saudação do servidor de configuração VM no Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Localizar o servidor de configuração de saudação HTTPS porta pública em Olá **pontos de extremidade** guia saudação do servidor de configuração VM no Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. Em Olá **CS senha detalhes** página especificar Olá frase secreta que você anotou para baixo ao registrar o servidor de configuração de saudação. Se você não lembrar-check-in **c:\\arquivos de programa (x86)\\InMage sistemas\\privada\\connection.passphrase** no servidor de configuração de saudação VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. Em Olá **Selecionar local de destino** página especifique onde você deseja tooinstall Olá vContinuum servidor e clique em **instalar**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Após a conclusão da instalação, inicie o vContinuum.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Etapa 2: Instalar um servidor de processo no Azure
É necessário tooinstall um servidor de processo no Azure para que Olá VMs no Azure podem enviar o servidor de destino mestre Olá dados tooan back local.

1. Em Olá **servidores de configuração** página no Azure, selecione tooadd um novo servidor de processo.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Especifique um nome de servidor de processo e um nome e senha tooconnect toohello das máquinas virtuais como um administrador. Selecione o servidor toowhich Olá configuração que você deseja que o servidor de processo tooregister hello. Isso deve ser Olá mesmo servidor que você está usando tooprotect e realizar failover suas máquinas virtuais.
3. Especificar hello Azure rede na qual saudação do servidor em processo deve ser implantado. Deve ser Olá mesma rede como o servidor de configuração de saudação. Especifique um endereço IP exclusivo na sub-rede selecionada e inicie a implantação.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Um trabalho é um servidor de processo Olá toodeploy disparados.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Depois que o servidor de processo Olá é implantado no Azure você pode fazer logon no servidor de saudação usando credenciais de saudação especificado. Registrar o servidor de processo Olá no hello mesma maneira que você registrou Olá local do servidor em processo.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> servidores de saudação registrados durante o failback não ficarão visíveis em Propriedades de máquina virtual na recuperação de Site. Eles são visíveis apenas em Olá **servidores** guia da saudação toowhich de servidor de configuração que estão registrados. Pode levar aproximadamente 10 a 15 minutos até que eles Olá o processo de servidor será exibido na guia hello.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Etapa 3: Instalar um servidor de destino mestre no local
Dependendo do seu sistema operacional de máquinas virtuais de origem, você precisa tooinstall um Linux ou um servidor de destino mestre Windows local.

### <a name="deploy-a-windows-master-target-server"></a>Implantar um servidor de destino mestre com Windows
Um destino mestre com Windows já faz parte da instalação do vContinuum. Quando você instala vContinuum hello, um servidor mestre também é implantado em Olá mesmo computador e o servidor de configuração de toohello registrado.

1. implantação de toobegin criar vazio do computador local no host do ESX Olá no qual você deseja toorecover Olá VMs do Azure.
2. Verifique se há pelo menos dois discos anexados toohello VM – um é usado para o sistema operacional de saudação e Olá outros é usado para a unidade de retenção de saudação.
3. Instale o sistema operacional de saudação.
4. Instale Olá vContinuum no servidor de saudação. Isso também conclui a instalação do servidor de destino mestre hello.

### <a name="deploy-a-linux-master-target-server"></a>Implantar um servidor de destino mestre com Linux
1. implantação de toobegin criar vazio do computador local no host do ESX Olá no qual você deseja toorecover Olá VMs do Azure.
2. Verifique se há pelo menos dois discos anexados toohello VM – um é usado para o sistema operacional de saudação e Olá outros é usado para a unidade de retenção de saudação.
3. Instale o sistema de operacional Linux hello. Olá sistema de destino mestre Linux não deve usar LVM raiz ou retenção dos espaços de armazenamento. Um Linux ao servidor de destino mestre está configurado a descoberta de partições/discos LVM tooavoid por padrão.
4. As partições que você pode criar são:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Realize Olá post etapas de instalação a seguir antes de iniciar a instalação de destino mestre hello.

#### <a name="post-os-installation-steps"></a>Etapas posteriores à instalação do SO:
Olá tooget IDs de SCSI para cada disco SCSI em uma máquina virtual Linux, habilitar o parâmetro hello "disco. EnableUUID = TRUE "da seguinte maneira:

1. Desligue sua máquina virtual.
2. Clique a entrada VM Olá no painel esquerdo do hello > **editar configurações de**.
3. Clique em Olá **opções** guia. Selecione **Avançado\>Item geral** > **Parâmetros de Configuração**. Olá **parâmetros de configuração** opção só está disponível quando a saudação máquina está desligada.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Verifica se há uma linha com **disk.EnableUUID** . Se e é definido muito**False** , em seguida, defini-lo muito**True** (não entre maiusculas e minúsculas). Se existe e está definido tootrue, clique em **Cancelar** e testar o comando de SCSI hello dentro do sistema operacional Olá depois que ele for inicializado. Se não houver uma, clique em **Adicionar Linha**.
5. Adicione o disco. EnableUUID em Olá **nome** coluna. Defina seu valor como TRUE. Não adicione Olá acima valores juntamente com aspas duplas.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Baixar e instalar pacotes de saudação adicionais
Observação: Verifique se o sistema Olá tem conectividade com a internet antes de baixar e instalar os pacotes de saudação adicionais.

\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

Esse comando baixa estes 15 pacotes do repositório CentOS 6.6 e os instala:

bc-1.06.95-1.el6.x86\_64.rpm

busybox-1.15.1-20.el6.x86\_64.rpm

elfutils-libs-0.158-3.2.el6.x86\_64.rpm

kexec-tools-2.0.0-280.el6.x86\_64.rpm

lsscsi-0.23-2.el6.x86\_64.rpm

lzo-2.03-3.1.el6\_5.1.x86\_64.rpm

perl-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm

perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm

perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm

perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-version-0.77-136.el6\_6.1.x86\_64.rpm

rsync-3.0.6-12.el6.x86\_64.rpm

snappy-1.1.0-1.el6.x86\_64.rpm

wget-1.12-5.el6\_6.1.x86\_64.rpm

Se máquina de origem Olá usa Reiser ou XFS filesystem para dispositivo de inicialização ou raiz hello, pacotes a seguir devem ser baixados e instalados em tooprotection anterior de destino mestre Linux.

\# cd /usr/local

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm

\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

#### <a name="apply-custom-configuration-changes"></a>Aplicar alterações de configuração personalizadas
Antes de aplicar essas alterações, verifique se você concluiu a seção anterior hello, siga estas etapas:

1. Copie toohello binário do RHEL 6-64 unificado agente Olá recém-criada em sistema operacional.
2. Executar este Olá toountar de comando binário: **tar - zxvf \<nome de arquivo\>**
3. Permissões de toogive esse comando de execução: \# **./ApplyCustomChanges.sh chmod 755**
4. Execute o script hello:  **\# ./ApplyCustomChanges.sh**. Execute o script de saudação apenas uma vez no servidor de saudação. Reinicie o servidor de saudação após a execução do script hello.

### <a name="install-hello-linux-server"></a>Instalar o servidor de saudação do Linux
1. [Baixar](http://go.microsoft.com/fwlink/?LinkID=529757) arquivo de instalação de saudação.
2. Copie Olá arquivo toohello máquina virtual de destino mestre Linux usando um utilitário de cliente de sftp de sua escolha. Como alternativa você pode fazer logon na máquina de virtual de destino mestre do Linux hello e usar o pacote de instalação do wget toodownload saudação do link fornecido
3. Faça logon na máquina virtual Olá Linux destino mestre servidor usando um ssh cliente de sua escolha
4. Se você estiver conectado toohello do Azure no qual você implantado o servidor de destino mestre Linux por meio de uma conexão VPN, use o endereço IP interno para o servidor de saudação que você pode encontrar na máquina virtual de rede **painel** guia e porta 22 tooconnect toohello Linux mestre usando Secure Shell do servidor de destino.
5. Se você estiver se conectando toohello servidor de destino mestre Linux em uma conexão de internet pública use o endereço IP público virtual para o do servidor de destino mestre Linux hello (de máquinas virtuais de saudação **painel** guia) e Olá ponto de extremidade público criado para ssh toologin toohello Linux servder.
6. Extrair arquivos de saudação do hello gzip Linux destino mestre instalador tar arquivo morto Server executando: *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6 64"* do diretório de saudação que contém o arquivo do instalador hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Se você Olá extraídos instalador arquivos tooa outro diretório alterar conteúdo da saudação toowhich toohello diretório do arquivo morto tar de saudação foram extraído. Desse caminho de diretório, execute “sudo ./install.sh”.

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Quando seleciona toochoose solicitada uma função primária **2 (destino mestre)**. Deixe Olá outras opções de instalação interativo com seus valores padrão.
9. Aguarde a instalação toocontinue e hello tooappear de Interface de configuração do Host. Olá utilitário de configuração do Host de destino mestre do Linux do hello Server é um utilitário de linha de comando. Não redimensione Olá ssh janela do utilitário de cliente. Use Olá seta chaves tooselect Olá **Global** opção e pressione ENTER no teclado.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. No campo Olá **IP** insira o endereço IP interno de saudação do servidor de configuração de saudação (você pode encontrar no hello **painel** guia saudação do servidor de configuração VM) e pressione ENTER. Em **Porta** insira **22** e pressione ENTER.
11. Deixe **Usar HTTPS** como **Sim** e pressione ENTER.
12. Digite hello frase secreta que foi gerada no servidor de configuração de saudação. Se você estiver usando um cliente PUTTY de uma máquina virtual Windows máquina toossh toohello Linux, você pode usar conteúdo de saudação do Shift + Insert toopaste da área de transferência de saudação. Copie Olá frase secreta toohello local da área de transferência usando Ctrl-C e use Shift + Insert toopaste-lo. Pressione ENTER.
13. Use Olá seta para a direita chave toonavigate tooquit e pressione ENTER. Aguarde a instalação toocomplete.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Se por alguma razão você não tooregister seu servidor de configuração do Linux destino mestre server toohello você pode fazer novamente executando o host do utilitário de configuração de /usr/local/ASR/Vx/bin/hostconfigcli (você precisará tooset toothis de permissões de acesso diretório executando chmod como um superusuário).

#### <a name="validate-master-target-registration"></a>Validar o registro de destino mestre
Você pode validar que Olá o servidor de destino mestre foi registrado com êxito toohello o servidor de configuração no cofre do Azure Site Recovery > **servidor de configuração** > **detalhes do servidor**.

> [!NOTE]
> Depois de registrar o servidor de destino mestre hello, se você receber erros de configuração que Olá máquina virtual pode ter sido excluído do Azure ou que os pontos de extremidade não estão configurados corretamente, isso ocorre porque embora hello configuração de destino mestre seja detectada por hello Azure dndpoints ao destino mestre Olá é implantado no Azure, isso não é verdadeiro para um local destino mestre server local. Isso não afetará o failback e você pode ignorar esses erros.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Etapa 4: Proteger a saudação máquinas virtuais toohello no site local
Você precisa tooprotect VMs toohello no site local antes de você failback.

### <a name="before-you-begin"></a>Antes de começar
Quando uma VM failover tooAzure, ele adiciona uma unidade temporária extra para o arquivo de paginação. Essa unidade extra normalmente não é exigida por sua VM em estado de failover, pois ele já pode ter uma unidade dedicada ao arquivo de paginação. Antes de começar inversa proteção de máquinas virtuais de Olá, você precisa garantir que essa unidade seja colocada offline para que ele não fique protegido. Faça isso da seguinte forma:

1. Abra o gerenciamento do computador e selecione gerenciamento de armazenamento para que ela lista máquina do hello discos toohello on-line e anexado.
2. Selecione Olá temporário em disco anexado toohello máquina e escolha toobring-lo offline.

### <a name="protect-hello-vms"></a>Proteger a saudação VMs
1. Olá portal do Azure, verifique estados de saudação do hello tooensure de máquina virtual que está failover.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. Inicie o vContinuum em sua máquina.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Clique em **nova proteção** e selecione o tipo de sistema de operação hello, o
4. Em nova janela de saudação que abrem Olá selecione **tipo de SO** > **obter detalhes** Olá VMs deseja toofail novamente. Em **detalhes do servidor primário**, identificar e selecione Olá máquinas virtuais que você deseja tooprotect. As VMs são listadas sob o nome de host do vCenter Olá estivesse em antes do failover.
5. Quando você seleciona uma máquina virtual tooprotect (e que já tenha falhado em tooAzure) uma janela pop-up fornece duas entradas para a máquina virtual de saudação. Isso ocorre porque o servidor de configuração de saudação detecta duas instâncias do hello tooit de máquinas virtuais registradas. Você precisa de entrada de saudação tooremove para Olá a VM para que você possa proteger Olá VM correto no local. tooidentify Olá VM do Azure a entrada correta aqui, você pode fazer logon no hello VM do Azure e vá tooC:\Program arquivos (x86) \Microsoft Azure Site Recovery\Application Data\etc. Olá arquivo drscout.conf, identificar Olá identificação de host. Na caixa de diálogo de vContinuum hello, mantenha entrada Olá para o qual você encontrado um ID de host Olá em Olá VM. Exclua todas as outras entradas. Olá tooselect corrigir VM, você pode consultar o endereço IP de tooits. Olá IP endereço intervalo local será Olá a VM local.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. No servidor do vCenter Olá pare de máquina virtual de saudação. Você também pode excluir Olá VMs locais.
7. Em seguida, especifique Olá local MT server toowhich deseja tooprotect Olá VMs. toodo, conectar-se o servidor toowhich toohello vCenter que você deseja toofail novamente.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. O servidor de destino mestre Olá Select com base em Olá host toowhich deseja toorecover Olá VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Fornece a opção de replicação de saudação para cada uma das máquinas virtuais de saudação. toodo isso é necessário tooselect Olá recuperação lado datastore toowhich Olá VMs serão recuperadas. tabela de saudação resume opções diferentes de saudação precisar tooprovide para cada VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Opção** | **Valor recomendado para a opção** |
   | --- | --- |
   |  Processar o endereço IP do servidor |Selecionar servidor de processo Olá implantado no Azure |
   |  Tamanho de retenção em MB | |
   |  Valor de retenção |1 |
   |  Dias/Horas |Dias |
   |  Intervalo de consistência |1 |
   |  Selecione o Armazenamento de Dados de Destino |Olá repositório de dados disponível no site de recuperação de saudação. Olá repositório de dados deve ter espaço suficiente e ser o host do ESX toohello disponíveis no qual você deseja toorestore Olá virtual machine. |
10. Configure Olá propriedades Olá máquina virtual irá adquirir depois local tooon de failover. Propriedades de saudação são resumidas na Olá a tabela a seguir.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Propriedade** | **Detalhes** |
    | --- | --- |
    | Configuração de rede |Para cada adaptador de rede detectado, selecione-o e clique em **alteração** endereço IP do tooconfigure Olá failback para a máquina virtual de saudação. |
    | Configuração de hardware |Especifique Olá CPU e memória Olá Olá VM. Configurações podem ser aplicadas tooall Olá VMs que você está tentando tooprotect. tooidentify Olá valores corretos da saudação da CPU e memória, você pode consultar o tamanho da função toohello VMs de IAAS e ver Olá número de núcleos e memória atribuída. |
    | Nome de exibição |Depois de failback tooon local, você pode renomear máquinas virtuais de saudação conforme elas aparecerão no inventário do vCenter hello. nome do padrão de saudação é nome de host do computador de máquina virtual de saudação. nome da VM tooidentify hello, você pode consultar toohello lista VM no grupo de proteção de saudação. |
    | Configuração de NAT |Discutido com mais detalhes abaixo |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>Definir as configurações de NAT
1. tooenable proteção de máquinas virtuais de hello, dois canais de comunicação necessário toobe estabelecida. canal primeiro Olá é entre máquinas virtuais de saudação e o servidor de processo hello. Esse canal coleta dados de saudação do hello VM e o envia toohello que, em seguida, envia Olá servidor de destino mestre toohello de dados do servidor em processo. Se o servidor de processo hello e Olá toobe de máquina virtual protegida estão em Olá mesma rede virtual do Azure, você não terá as configurações de NAT toouse. Caso contrário, especifique as configurações de NAT. Exibir o endereço IP público de saudação saudação do servidor de processo no Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. canal de segundo Olá é entre o servidor de processo hello e servidor de destino mestre hello. Olá toouse opção NAT ou não depende de se você estiver usando uma conexão VPN com base ou se comunicando por hello internet. Não selecione NAT se você estiver usando VPN, mas apenas se você estiver usando uma conexão com a internet.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Se não tiver sido excluído Olá em máquinas virtuais conforme especificado e se Olá repositório de dados que você está toostill back falha contiver VMDK antigo hello, será necessário tooensure que o failback Olá VM é criada em um novo local. toodo este select Olá **avançado** configurações e especifique uma alternativa toorestore tooin da pasta **as configurações de nome de pasta**. Deixe Olá outras opções com suas configurações padrão. Se aplicam a servidores de Olá Olá pasta nome configurações tooall.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Executar uma verificação de preparação tooensure máquinas virtuais de saudação são toobe pronto protegida back tooon local.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Aguarde até que ele toocomplete. Se estiver com êxito em todas as máquinas virtuais, você pode especificar um nome para o plano de proteção de saudação. Em seguida, clique em **proteger** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. Você pode monitorar o progresso no vContinuum.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Após a etapa de saudação **ativar proteção planejar** for concluída, você pode monitorar a proteção de VM no portal de recuperação de Site hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Você pode ver o status de exato de saudação clicando em Olá VM e monitorar seu progresso.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Preparar um plano de failback Olá
Você pode preparar um plano de failback usando vContinuum para que o aplicativo hello pode ser toohello voltar com falha no site local a qualquer momento. Esses planos de recuperação são muito semelhantes planos de recuperação de toohello na recuperação de Site.

1. Inicie o vContinuum e selecione **Gerenciar planos** > **Recuperar.** Você pode ver da lista de todos os planos de saudação que foram usado toofail mais máquinas virtuais. Você pode usar o hello mesmo planos toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Selecione o plano de proteção hello e todas as Olá VMs que você deseja toorecover nele. Quando você seleciona cada VM, você pode ver mais detalhes, incluindo Olá destino ESX server e o disco de VM de origem hello. Clique em **próximo** toobegin Olá Assistente para recuperar e selecione VMs Olá deseja toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. Você pode recuperar com base em várias opções, mas é recomendável que você use **marca mais recente** e selecione **aplicar para todas as VMs** tooensure que Olá dados mais recentes da máquina virtual de saudação será usado.
4. Executar Olá **verificação de preparação.** Isso irá verificar se parâmetros certos hello serão configurado tooenable VM recuperação. Clique em **próximo** se todas as verificações de saudação forem bem-sucedidas. Se não for log hello e resolver erros de saudação.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. Em **configuração da VM** Certifique-se de que as configurações de recuperação Olá estão definidas corretamente. Você pode alterar as configurações de VM Olá se for necessário.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Examine a lista de saudação de máquinas virtuais que serão recuperados e especificar uma ordem de recuperação. Observe que as VMs são listadas usando nome de host do computador hello. Talvez seja difícil toomap Olá computador host nome toohello VM.
   nomes de saudação toomap, máquinas virtuais de vá toohello **painel** no Azure e verificação de nome de host VM hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Especifique um nome de plano e selecione **Recuperar posteriormente**. É recomendável toorecover mais tarde porque a proteção de saudação inicial não pode ser concluída.
8. Clique em **recuperar** toosave Olá plano de gatilho Olá recuperação ou se você tiver selecionado toorecover agora e não mais tarde. Você pode verificar Olá toosee de status de recuperação se o plano de saudação do foi salvo.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Recuperar as máquinas virtuais
Depois que o plano de saudação do foi criado, você pode recuperar máquinas virtuais de saudação. Antes de você verificar que Olá virtual máquinas concluiu a sincronização. Se o status de replicação mostra Okey Olá proteção estiver concluída, e o limite de RPO Olá foram atendido. Você pode verificar a integridade nas propriedades VM hello.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Desative a saudação máquinas virtuais do Azure antes de você inicia a recuperação de saudação. Isso garante que não há nenhuma divisão de dados e que os usuários acessar somente uma cópia do aplicativo hello.

1. Inicie Olá plano foi salvo. No vContinuum selecione **Monitor** Olá planos. Lista todos os planos de saudação que foram executados.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Selecione Olá plano no **recuperação** e clique em **iniciar**. Você pode monitorar a recuperação. Depois que as VMs foram ativadas no, você pode conectar toothem no vCenter.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>Proteger tooAzure novamente depois de failback
Depois de concluir o failback você provavelmente vai querer tooprotect Olá VMs novamente. Faça isso da seguinte forma:

1. Verifique se Olá máquinas virtuais locais estão funcionando e que os aplicativos estejam acessíveis.
2. No portal do Azure Site Recovery hello, selecione as máquinas virtuais hello e excluí-los. Selecione toodisable Olá proteção de máquinas virtuais de saudação. Isso garante que VMs Olá não mais são protegidas.
3. No Azure excluir Olá failover de máquinas virtuais do Azure
4. Exclua máquina virtual antigo de saudação em vSpehere. Essas são as VMs Olá failover tooAzure anteriormente.
5. No portal de recuperação de Site Olá protege Olá VMs failover recentemente. Depois que eles são protegidos podem ser adicionados tooa plano de recuperação.

## <a name="next-steps"></a>Próximas etapas
* [Leia sobre](site-recovery-vmware-to-azure-classic.md) replicando máquinas virtuais VMware e tooAzure servidores físicos usando a implantação de saudação aprimorada.
