---
title: "máquinas virtuais de aaaReplicate Hyper-V no VMM nuvens tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooreplicate máquinas de virtuais de Hyper-V em hosts Hyper-V localizado em tooAzure de nuvens do System Center VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Replicar máquinas virtuais Hyper-V no tooAzure de nuvens do VMM
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portal clássico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - clássico](site-recovery-deploy-with-powershell.md)
>
>

Olá serviço Azure Site Recovery contribui tooyour continuidade de negócios e a estratégia de recuperação (BCDR) de desastres orquestração de replicação, failover e recuperação de máquinas virtuais e servidores físicos. Computadores podem ser replicado tooAzure ou tooa local secundário data center. Para ter uma breve visão geral, leia [O que é Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Visão geral
Este artigo descreve como toodeploy Site de recuperação Hyper-V de tooreplicate máquinas virtuais no Hyper-V host servidores que estão localizados em tooAzure de nuvens privadas do VMM.

artigo de saudação inclui os pré-requisitos para o cenário de saudação e mostra a você como tooset um cofre da recuperação de Site, obter Olá provedor Azure Site Recovery instalada no servidor do VMM de origem hello, registrar o servidor de saudação no cofre hello, adicione uma conta de armazenamento do Azure, instale Olá Agente de serviços de recuperação do Azure nos servidores de host do Hyper-V, definir configurações de proteção para nuvens do VMM que serão máquinas virtuais de tooall aplicada protegido e, em seguida, habilite a proteção para as máquinas virtuais. Concluir teste Olá failover toomake se que tudo está funcionando conforme o esperado.

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Arquitetura
![Arquitetura](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Olá provedor Azure Site Recovery está instalado em Olá VMM durante a implantação da recuperação de Site e servidor de saudação do VMM está registrado no cofre de recuperação de Site de saudação. Olá provedor se comunica com orquestração de replicação toohandle recuperação de Site.
* Agente de serviços de recuperação do Azure Hello está instalado nos servidores de host do Hyper-V durante a implantação da recuperação de Site. Ele trata o armazenamento de tooAzure de replicação de dados.

## <a name="azure-prerequisites"></a>Pré-requisitos do Azure
Veja o que será necessário no Azure.

| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **Conta do Azure** |Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site. |
| **Armazenamento do Azure** |Você precisará de um toostore replicado dados da conta de armazenamento do Azure. Os dados replicados são armazenados no armazenamento do Azure e as VMs do Azure se adaptam quando ocorre failover. <br/><br/>Você precisa de uma [conta de armazenamento com redundância geográfica standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Olá conta deve ser Olá mesma região que o serviço de recuperação de Site hello e ser associada Olá a mesma assinatura. Observe que as contas de armazenamento toopremium replicação atualmente não tem suporte e não deve ser usado.<br/><br/>[Leia sobre o](../storage/common/storage-introduction.md) armazenamento do Azure. |
| **Rede do Azure** |Você precisará de uma rede virtual do Azure que irá se conectar a máquinas virtuais do Azure toowhen failover ocorre. Olá rede virtual do Azure deve estar no hello mesma região Olá Cofre de recuperação de Site. |

## <a name="on-premises-prerequisites"></a>Pré-requisitos do local
Veja o que será necessário no local.

| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **VMM** |Você precisará de pelo menos um servidor do VMM implantado como servidor físico ou virtual autônomo ou como um cluster virtual. <br/><br/>servidor do VMM Olá deve estar executando o System Center 2012 R2 com hello últimas atualizações cumulativas.<br/><br/>Você precisará de pelo menos uma nuvem configurada no servidor do VMM hello.<br/><br/>nuvem de origem Olá que você deseja tooprotect deve conter um ou mais grupos de hosts do VMM.<br/><br/>Saiba mais sobre a configuração de nuvens do VMM em [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) (Passo a passo: Criando nuvens privadas com o System Center 2012 SP1 VMM) no blog de Keith Mayer. |
| **Hyper-V** |Você precisará de um ou mais servidores de host do Hyper-V ou clusters em Olá nuvem do VMM. servidor de host de saudação deve ter e uma ou mais máquinas virtuais. <br/><br/>servidor de saudação Hyper-V deve ser executado em pelo menos **Windows Server 2012 R2** com a função hello Hyper-V ou **Microsoft Hyper-V Server 2012 R2** e ter Olá as últimas atualizações instaladas.<br/><br/>Qualquer servidor Hyper-V que contém máquinas virtuais que você deseja tooprotect devem estar localizados em uma nuvem VMM.<br/><br/>Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos. Você precisará agente do cluster Olá tooconfigure manualmente. [Saiba mais](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) na entrada do blog de Aidan Finn. |
| **Computadores protegidos** | Máquinas virtuais que você deseja tooprotect devem ser compatíveis com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Pré-requisitos de mapeamento de rede
Quando você protege máquinas virtuais no mapeamento de rede do Azure mapeia entre redes VM no servidor do VMM de origem de saudação e procedimentos de saudação do destino redes do Azure tooenable:

* Todas as máquinas failover em Olá mesma rede pode se conectar a outro, independentemente do plano de recuperação que estão em tooeach.
* Se configurar um gateway de rede na rede do Azure de destino do hello, máquinas virtuais podem conectar-se tooother em máquinas virtuais.
* Se você não configurar rede mapeamento apenas as máquinas virtuais que fazem failover no hello mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de failover.

Se você quiser que o mapeamento de rede toodeploy você precisará seguir hello:

* saudação de máquinas virtuais que deseja tooprotect no servidor do VMM de origem de saudação deve ser conectado tooa rede VM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.
* Máquinas de virtuais de toowhich replicado uma rede do Azure podem se conectar após o failover. Você selecionará essa rede no tempo de saudação de failover. rede Olá deve estar no hello mesma região que sua assinatura do Azure Site Recovery.


Preparar redes no VMM:

   * [Configure redes lógicas](https://technet.microsoft.com/library/jj721568.aspx).
   * [Configure as redes de VMM](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>Etapa 1: criar um cofre de Recuperação de Site
1. Entrar toohello [Portal de gerenciamento](https://portal.azure.com) do servidor do VMM Olá deseja tooregister.
2. Clique em **Serviços de Dados** > **Serviços de Recuperação** > **Cofre de Recuperação de Site**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **nome**, insira um cofre de saudação tooidentify nome amigável.
5. Em **região**, selecione Olá região geográfica para Olá cofre. regiões toocheck suporte consulte disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Clique em **Criar cofre**.

    ![Novo cofre](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Verifique a saudação tooconfirm de barra de status que Olá cofre foi criado com êxito. Olá cofre será listado como **Active** na página principal de serviços de recuperação hello.

## <a name="step-2-generate-a-vault-registration-key"></a>Etapa 2: gerar uma chave de registro do cofre
Gere uma chave de registro no cofre de saudação. Depois de baixar Olá provedor Azure Site Recovery e instalá-lo no servidor do VMM hello, você usará esse servidor do VMM Olá tooregister chave no cofre de saudação.

1. Em Olá **dos serviços de recuperação** , clique em página de início rápido do hello cofre tooopen hello. Início rápido também pode ser aberto a qualquer momento usando o ícone de saudação.

    ![Ícone de Inicialização Rápida](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Na lista suspensa de saudação, selecione **entre um site do VMM no local e o Microsoft Azure**.
3. Em **Preparar Servidores VMM**, clique no arquivo **Gerar chave de registro**. arquivo de chave de saudação é gerado automaticamente e é válido por 5 dias depois que ele é gerado. Se você não estiver acessando Olá portal do Azure do servidor do VMM Olá precisará toocopy toohello servidor de arquivos.

    ![Chave de Registro](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Etapa 3: Instalar Olá provedor Azure Site Recovery
1. Em **início rápido** > **servidores VMM preparar**, clique em **baixar provedor Microsoft Azure Site Recovery para instalação nos servidores VMM** tooobtain Olá versão mais recente do arquivo de instalação do provedor de saudação.
2. Execute esse arquivo no servidor do VMM de origem de saudação.

   > [!NOTE]
   > Se o VMM for implantado em um cluster e você estiver instalando hello provedor para hello primeira vez instalá-lo em um nó ativo e concluir o servidor do VMM Olá instalação tooregister Olá no cofre de saudação. Em seguida, instale Olá provedor em Olá outros nós. Observe que, se você estiver atualizando Olá provedor, você precisará tooupgrade em todos os nós porque eles devem todos ser execução Olá mesma versão do provedor.
   >
   >
3. Olá instalador faz uma verificação de equisitos e solicitações de configuração do provedor permissão toostop Olá VMM serviço toobegin. saudação de serviço do VMM será reiniciada automaticamente quando a instalação for concluída. Se você estiver instalando em um cluster do VMM que você será solicitado toostop função de Cluster de saudação.
4. No **Microsoft Update** você pode optar por atualizações. Com essa configuração habilitada provedor serão instaladas de acordo com a política do tooyour Microsoft Update.

    ![Atualizações da Microsoft](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. Olá local de instalação para Olá provedor está definido muito**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Clique em **Instalar**.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Depois de saudação provedor está instalado, clique em **registrar** tooregister servidor de saudação no cofre hello.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. Em **nome do cofre**, verificar nome de saudação do cofre Olá quais saudação servidor será registrado. Clique em *Avançar*.

    ![Registros do servidor](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. Em **Conexão de Internet** especificar hello como o provedor em execução no hello VMM server conecta toohello da Internet. Selecione **conectar-se com as configurações de proxy existentes** configurações de conexão de Internet do toouse saudação padrão configuradas no servidor de saudação.

    ![Configurações da Internet](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Se você quiser toouse um proxy personalizado você deve configurá-lo antes de instalar o provedor de saudação. Quando você definir as configurações de proxy personalizadas um teste será executado toocheck conexão de proxy de saudação.
   * Se você usar um proxy personalizado, ou o proxy padrão exige autenticação, você precisará detalhes de proxy Olá tooenter, incluindo a porta e endereço de proxy de saudação.
   * Urls a seguir deve ser acessível pela hello servidor do VMM e hosts do Hyper-v Olá
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Permitir endereços IP hello descritos em [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e o protocolo HTTPS (443). Você teria de intervalos de IP de lista toowhite de saudação região do Azure que você planeje toouse e do Oeste dos EUA.
   * Se você usar um proxy personalizado uma conta de RunAs VMM (DRAProxyAccount) será criada automaticamente usando Olá especificado credenciais de proxy. Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito. configurações de conta de RunAs VMM Olá podem ser modificadas no console do VMM hello. toodo isso, abra Olá **configurações** espaço de trabalho, expanda **segurança**, clique em **contas executar como**e, em seguida, modificar a senha Olá para DRAProxyAccount. O serviço VMM toorestart hello, será necessário para que essa configuração tenha efeito.
9. Em **chave de registro**, selecione chave Olá que você baixou do Azure Site Recovery e copiou toohello o servidor do VMM.
10. configuração de criptografia de saudação é usada apenas quando você estiver replicando máquinas virtuais do Hyper-V no tooAzure de nuvens do VMM. Se você estiver replicando o site secundário tooa não é usado.
11. Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello. Em uma configuração de cluster, especifique nome de função de cluster saudação do VMM.
12. Em **sincronizar metadados de nuvem** selecione se deseja toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello. Essa ação precisa apenas toohappen uma vez em cada servidor. Se você não quiser toosynchronize todas as nuvens, você pode deixar essa configuração está desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello.
13. Clique em **próximo** toocomplete processo de saudação. Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery. saudação do servidor é exibida em Olá **servidores VMM** guia Olá **servidores** página no cofre hello.

    ![Última página](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery. saudação do servidor é exibida em Olá **servidores VMM** guia, Olá **servidores** página no cofre hello.

### <a name="command-line-installation"></a>Instalação de linha de comando
Olá provedor Azure Site Recovery pode ser instalado usando a seguinte linha de comando de saudação. Esse método pode ser um provedor de saudação tooinstall usado em um núcleo de servidor para o Windows Server 2012 R2.

1. Baixe Olá provedor de arquivo e registro tooa chave pasta de instalação. Por exemplo: C:\ASR.
2. Parar o serviço do System Center Virtual Machine Manager Olá
3. Em um prompt de comando com privilégios elevados, extraia o instalador do provedor Olá com estes comandos:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale o provedor de saudação da seguinte maneira:

        C:\ASR> setupdr.exe /i
5. Registre Olá provedor da seguinte maneira:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Em que parâmetros são os seguintes:

* **/ Credenciais** : parâmetro obrigatório que especifica o local de saudação em qual Olá arquivo de chave do registro está localizado  
* **/ FriendlyName** : parâmetro obrigatório para o nome de saudação do servidor de host de saudação Hyper-V que aparece no portal do Azure Site Recovery hello.
* **/ EncryptionEnabled** : toospecify parâmetro opcional, se você quiser tooencryption suas máquinas virtuais no Azure (a criptografia em repouso). nome do arquivo Hello deve ter uma **. pfx** extensão.
* **/proxyAddress** : parâmetro opcional que especifica o endereço de saudação do servidor de proxy de saudação.
* **/proxyPort** : parâmetro opcional que especifica a porta de saudação do servidor de proxy de saudação.
* **/proxyUsername** : parâmetro opcional que especifica o nome de usuário de proxy de saudação.
* **/proxyPassword** : parâmetro opcional que especifica a senha do proxy hello.  

## <a name="step-4-create-an-azure-storage-account"></a>Etapa 4: criar uma conta de armazenamento do Azure
1. Se você não tiver uma conta de armazenamento do Azure clique **adicionar uma conta de armazenamento do Azure** toocreate uma conta.
2. Crie uma conta com a replicação geográfica habilitada. Ele no deve Olá mesma região Olá serviço Azure Site Recovery e estar associada a saudação mesma assinatura.

    ![Conta de armazenamento](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Migração de contas de armazenamento](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para contas de armazenamento usadas para implantar a recuperação de Site.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>Etapa 5: Instalar hello Azure Recovery Services Agent
Instale o agente de serviços de recuperação do Azure de saudação em cada servidor de host do Hyper-V no hello nuvem do VMM.

1. Clique em **início rápido** > **Download do Azure Site Recovery Services Agent e instalar nos hosts** tooobtain Olá última versão do arquivo de instalação do agente de saudação.

    ![Instalar o Agente de Serviços de Recuperação](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Execute o arquivo de instalação de saudação em cada servidor de host do Hyper-V.
3. Em Olá **verificação de pré-requisitos** página clique **próximo**. Quaisquer pré-requisitos faltantes serão instalados automaticamente.

    ![Agente de Serviços de Recuperação de Pré-requisitos](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. Em Olá **configurações de instalação** , especifique onde você deseja o agente de saudação tooinstall e local do cache Olá selecione metadados de backup serão instalado. Em seguida, clique em **Instalar**.
5. Após a instalação for concluída, clique **fechar** toocomplete Assistente de saudação.

    ![Registrar o Agente MARS](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Instalação de linha de comando
Você também pode instalar Olá Microsoft Azure Recovery Services Agent da linha de comando de saudação usando este comando:

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>Etapa 6: definir as configurações da proteção de nuvem
Depois que o servidor do VMM Olá for registrado, você pode configurar as configurações de proteção de nuvem. Você habilitou a opção Olá **sincronizar dados da nuvem com o cofre Olá** quando você instalou Olá provedor para todas as nuvens no servidor do VMM hello serão exibidos no hello <b>itens protegidos</b> guia no cofre hello.

![Publicar uma nuvem](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Na página início rápido hello, clique em **configurar a proteção para nuvens do VMM**.
2. Em Olá **itens protegidos** guia, clique na nuvem Olá você deseja tooconfigure e ir toohello **configuração** guia.
3. Em **Destino** select **Azure**.
4. Em **conta de armazenamento** Selecionar conta de armazenamento do Azure Olá usada para replicação.
5. Definir **criptografar dados armazenados** muito**Off**. Essa configuração especifica que os dados devem ser criptografados durante a replicação entre Olá no site local e o Azure.
6. Em **frequência de cópia** deixe a configuração padrão de saudação. Esse valor especifica a frequência com que dados devem ser sincronizados entre os locais de origem e de destino.
7. Em **reter pontos de recuperação para**, deixe a configuração padrão de saudação. Com um valor padrão de zero, somente Olá último ponto de recuperação para uma máquina virtual primária é armazenado em um servidor de host de réplica.
8. Em **frequência dos instantâneos consistentes com aplicativos**, deixe a configuração padrão de saudação. Esse valor Especifica a frequência toocreate instantâneos. Instantâneos usam o Volume Shadow Copy Service (VSS) tooensure que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado.  Se você definir um valor, verifique se que ele for menor que o número de saudação de pontos de recuperação adicionais que você configurar.
9. Em **hora de início da replicação**, especifique quando a replicação inicial de dados tooAzure deve ser iniciada. fuso horário de saudação no servidor de host do Hyper-V Olá será usado. É recomendável que você agende a replicação inicial Olá fora do horário de pico.

    ![Configurações de replicação de nuvem](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Depois de salvar as configurações de saudação um trabalho será criado e pode ser monitorado na Olá **trabalhos** guia. Todos os servidores de host do Hyper-V no hello nuvem de origem do VMM serão configurados para replicação.

Depois de salvar, configurações de nuvem podem ser modificadas no hello **configurar** guia toomodify Olá destino local ou destino conta de armazenamento será precisam de configuração de nuvem Olá tooremove e, em seguida, reconfigure a nuvem de saudação. Observe que se você alterar a alteração de saudação da conta de armazenamento Olá só é aplicada para máquinas virtuais que estão habilitadas para proteção após a conta de armazenamento Olá foi modificada. Máquinas virtuais existentes não são migradas toohello nova conta de armazenamento.

## <a name="step-7-configure-network-mapping"></a>Etapa 7: configurar o mapeamento de rede
Antes de começar o mapeamento de rede Verifique se máquinas virtuais no servidor do VMM de origem de saudação tooa conectado rede VM. Além disso, crie uma ou mais redes virtuais do Azure. Observe que várias redes VM podem ser mapeadas tooa única rede do Azure.

1. Na página início rápido hello, clique em **mapear redes**.
2. Em hello **redes** guia **local de origem**, selecione o servidor VMM de origem Olá. Em **Local de destino** , selecione Azure.
3. Em **fonte** redes uma lista de redes VM com o servidor do VMM Olá são exibidos. Em **destino** redes hello Azure redes associadas Olá assinatura são exibidas.
4. Selecione a rede VM de origem hello e clique em **mapa**.
5. Em Olá **selecionar uma rede de destino** página, selecione Olá rede Azure de destino desejado toouse.
6. Clique em processo de mapeamento Olá marca de seleção toocomplete hello.

    ![Configurações de replicação de nuvem](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Depois de salvar as configurações de saudação progresso do mapeamento Olá tootrack um trabalho é iniciado e pode ser monitorado na guia trabalhos de saudação. Qualquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será conectado toohello redes Azure de destino. Novas máquinas virtuais que estão conectados toohello rede VM de origem será rede Azure mapeada de toohello conectado após a replicação. Se você modificar um mapeamento existente com uma nova rede, máquinas virtuais de réplica serão conectadas usando Olá novas configurações.

Observe que se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.

> [!NOTE]
> [Migração de redes](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para redes usados para implantar a recuperação de Site.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>Etapa 8: habilitar a proteção para máquinas virtuais
Depois de servidores, nuvens e redes configuradas corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem hello. Observe o seguinte hello:

* As máquinas virtuais devem atender os [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
* sistema operacional do tooenable proteção hello e propriedades do disco do sistema operacional devem ser definidas para a máquina virtual de saudação. Quando você cria uma máquina virtual no VMM usando um modelo de máquina virtual, você pode definir propriedade de saudação. Você também pode definir essas propriedades para máquinas virtuais existentes em Olá **geral** e **configuração de Hardware** guias de propriedades de máquina virtual de saudação. Se você não definir essas propriedades no VMM, você será capaz de tooconfigure-los no portal do Azure Site Recovery hello.

    ![Criar máquina virtual](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Modificar propriedades de máquina virtual](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. proteção de tooenable, na Olá **máquinas virtuais** na nuvem Olá no qual Olá a máquina virtual está localizada, clique em **Habilitar proteção** > **adicionar máquinas virtuais**.
2. Na lista de saudação de máquinas virtuais na nuvem hello, selecione Olá um deseja tooprotect.

    ![Habilitar Proteção da Máquina Virtual](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Acompanhar o progresso da saudação **Habilitar proteção** ação Olá **trabalhos** guia, incluindo a replicação inicial hello. Depois de saudação **finalizar proteção** execuções de trabalho Olá máquina de virtual está pronta para failover. Depois de habilitar a proteção e máquinas virtuais forem replicadas, você será capaz de tooview-los no Azure.

    ![Trabalho de proteção da máquina virtual](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Verifique se as propriedades de máquina virtual de saudação e modifique conforme necessário.

    ![Verificar as máquinas virtuais](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. Em Olá **configurar** guia de propriedades de máquina virtual Olá propriedades de rede a seguir pode ser modificado.

* **Número de adaptadores de rede na máquina de virtual de destino Olá** -número de saudação de adaptadores de rede é determinado pelo tamanho Olá especificado para a máquina de virtual de destino hello. Verificar [especificações de tamanho de máquina virtual](../virtual-machines/linux/sizes.md) para número de saudação de adaptadores suportados pelo tamanho da máquina virtual de saudação. Quando você modificar o tamanho de saudação para uma máquina virtual e salva as configurações de Olá, o número de saudação de adaptadores de rede mudará Olá próxima vez que abrir Olá **configurar** página. Olá vários adaptadores de rede de máquinas virtuais de destino é o número mínimo de saudação de adaptadores de rede na origem de máquina virtual e Olá número máximo de adaptadores de rede suportados pelo tamanho de saudação da máquina virtual de saudação escolhido, da seguinte maneira:

  * Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
  * Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.
  * Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.     
* **Rede de máquina de virtual de destino Olá** -Olá rede toowhich Olá VM conecta toois determinado pelo mapeamento de rede da rede de saudação da máquina virtual de origem. Se Olá da máquina virtual de origem tiver mais de uma rede adaptador e fonte de redes são redes toodifferent mapeadas no destino, e em seguida, você precisará toochoose entre um Olá redes de destino.
* **A sub-rede de cada adaptador de rede** - para cada adaptador de rede, você pode selecionar Olá Olá de toowhich de sub-rede failover da máquina virtual se conectará a.
* **Endereço IP de destino** - se o adaptador de rede de saudação da máquina virtual de origem é toouse configurado um endereço IP estático, em seguida, você pode fornecer o endereço IP de Olá Olá máquina de virtual de destino. Use este recurso retém o endereço IP de saudação de uma máquina virtual de origem após um failover. Se nenhum endereço IP é fornecido nenhum endereço IP disponível é fornecido toohello adaptador de rede no tempo de saudação de failover. Se o endereço IP de destino Olá for especificado, mas está sendo usado por outra máquina virtual em execução no Azure failover falhará.  

    ![Modificar propriedades de rede](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> Não há suporte para máquinas virtuais Linux com um endereço IP estático.
>
>

## <a name="test-hello-deployment"></a>Implantação de saudação do teste
planejar a sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar um failover de teste para Olá tootest.  

O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada. Observe que:

* Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após o failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação.
* Após o failover, você deve usar um tooconnect endereço IP público toohello VM do Azure usando a área de trabalho remota. Se você quiser toodo isso, certifique-se de que você não tem qualquer política de domínio que impedem a máquina de virtual tooa conectar usando um endereço público.

> [!NOTE]
> tooget Olá melhor desempenho quando você fizer failover tooAzure, certifique-se de que você instalou Olá agente do Azure no hello VM. Isso fornece uma inicialização mais rápida e ajuda na solução de problemas. Baixar Olá [agente Linux](https://github.com/Azure/WALinuxAgent), ou hello [agente do Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Criar um plano de recuperação
1. Em Olá **planos de recuperação** guia, adicione um novo plano. Especifique um nome, **VMM** na **tipo de fonte de**e o servidor do VMM de origem Olá em **fonte**. destino de saudação será o Azure.

    ![Criar plano de recuperação](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. Em Olá **selecionar máquinas virtuais** página, o plano de recuperação de toohello de tooadd de máquinas virtuais específicas. Essas máquinas virtuais são adicionadas toohello grupo de padrão de plano de recuperação — grupo 1. Foi testado um máximo de 100 máquinas virtuais em um único plano de recuperação.

* Propriedades da máquina virtual tooverify Olá antes de adicioná-los toohello plano, clique em máquina virtual de saudação na página de propriedades de saudação da nuvem Olá no qual ela está localizada. Você também pode configurar propriedades de máquina virtual Olá no console do VMM hello.
* Todas as máquinas virtuais de saudação que são exibidas foram habilitadas para proteção. lista de saudação inclui duas máquinas virtuais que são habilitadas para proteção e replicação inicial foi concluída, e aqueles que estão habilitadas para proteção com a replicação inicial pendente. Somente as máquinas virtuais com replicação inicial concluída podem realizar failover como parte de um plano de recuperação.

    ![Criar plano de recuperação](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Depois que um plano de recuperação tenha sido criado, ele aparece no hello **planos de recuperação** guia. Você também pode adicionar [runbooks de automação do Azure](site-recovery-runbook-automation.md) toohello plano tooautomate as ações de recuperação durante o failover.

### <a name="run-a-test-failover"></a>Execute um teste de failover
Há dois toorun de maneiras um tooAzure de failover de teste.

* **Failover de teste sem uma rede do Azure**— este tipo de failover de teste verifica se a máquina virtual Olá aparece corretamente no Azure. máquina virtual de saudação não será conectado tooany rede Azure após o failover.
* **Failover de teste com uma rede do Azure**— este tipo de failover verifica que Olá ambiente de replicação inteiro aparece como esperado e failover de máquinas virtuais de saudação será conectado toohello rede Azure de destino especificado. Para a manipulação de sub-rede, para failover de teste sub-rede Olá Olá máquina de virtual de teste será descoberta com base na sub-rede de saudação do hello máquina de virtual de réplica. Isso é tooregular diferentes de replicação quando sub-rede saudação de uma máquina virtual de réplica é baseada na sub-rede de saudação do hello da máquina virtual de origem.

Se você quiser toorun um failover de teste para uma máquina virtual habilitada para proteção tooAzure sem especificar uma rede de destino do Azure não é necessário tooprepare nada. toorun um failover de teste com um destino de rede do Azure, você precisará toocreate uma nova rede Azure isolada da rede de produção do Azure (comportamento padrão quando você cria uma nova rede no Azure). Examinar como muito[executar um failover de teste](site-recovery-failover.md) para obter mais detalhes.

Você também precisará tooset infra-estrutura Olá para toowork de máquina virtual Olá replicada conforme o esperado. Por exemplo, uma máquina virtual com o controlador de domínio e DNS podem ser replicado tooAzure usando o Azure Site Recovery e podem ser criada na rede de teste hello usando Failover de teste. Examine as [considerações sobre o failover de teste para o Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obter mais detalhes.

um failover de teste de toorun Olá a seguir:

1. Em Olá **planos de recuperação** , selecione o plano de saudação e clique em **Failover de teste**.
2. Em Olá **confirmar Failover de teste** página Selecione **nenhum** ou uma rede do Azure específica.  Observe que se você selecionar nenhuma Olá failover de teste será seleção que Olá máquina virtual replicada corretamente tooAzure, mas não verifica sua configuração de rede de replicação.

    ![Sem rede](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Se a criptografia de dados está habilitada para nuvem Olá, em **chave de criptografia** certificado Olá select que foi emitido durante a instalação do hello provedor no servidor do VMM hello, quando você ativou o hello opção tooenable a criptografia de dados para uma nuvem .
4. Em Olá **trabalhos** guia você pode acompanhar o progresso de failover. Você também deve ser toosee capaz de réplica de teste de máquina virtual Olá no hello portal do Azure. Se você estiver configurado em máquinas virtuais de tooaccess da sua rede local, você pode iniciar uma máquina virtual de toohello de conexão de área de trabalho remota.
5. Quando o failover de saudação atinge Olá **testes completos** fase, clique em **teste completo** toofinish-lo. Você pode fazer drill down toohello **trabalho** guia tootrack progresso de failover e o status e tooperform as ações que são necessários.
6. Após o failover, você pode ver a réplica de teste de máquina virtual Olá no hello portal do Azure. Se você estiver configurado em máquinas virtuais de tooaccess da sua rede local, você pode iniciar uma máquina virtual de toohello de conexão de área de trabalho remota. Olá a seguir:

   1. Verifique se que máquinas virtuais de saudação foi iniciada com êxito.
   2. Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após o failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação. Você também precisa tooadd um ponto de extremidade do RDP na máquina virtual de saudação. Você pode aproveitar um [Runbooks de automação do Azure](site-recovery-runbook-automation.md) toodo que.
   3. Após o failover, se você usar uma IP endereço tooconnect toohello virtual máquina público no Azure usando a área de trabalho remota, verifique se que você não tem qualquer política de domínio que impedem a conexão de máquina virtual de tooa usando um endereço público.
7. Após a conclusão da saudação teste Olá a seguir:

   * Clique em **Olá failover de teste for concluído**. Limpar Olá power de tooautomatically do ambiente de teste e exclua Olá máquinas de virtuais de teste.
   * Clique em **notas** toorecord e salvar todas as observações associadas Olá failover de teste.


## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [como configurar os planos de recuperação](site-recovery-create-recovery-plans.md) e o [failover](site-recovery-failover.md).
