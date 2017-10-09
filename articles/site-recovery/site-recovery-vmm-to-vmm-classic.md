---
title: "aaaReplicate VMs Hyper-V no site secundário do VMM tooa (clássico do Azure) | Microsoft Docs"
description: "Este artigo descreve como tooreplicate VMs Hyper-V no VMM nuvens tooa site do VMM secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicar máquinas virtuais Hyper-V no site tooa VMM secundário nuvens do VMM
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Olá serviço Azure Site Recovery contribui tooyour continuidade de negócios e a estratégia de recuperação (BCDR) de desastres orquestração de replicação, failover e recuperação de máquinas virtuais e servidores físicos. Computadores podem ser replicado tooAzure ou tooa local secundário data center. Para ter uma breve visão geral, leia [O que é Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Visão geral
Este artigo descreve como tooreplicate Hyper-V máquinas virtuais Hyper-V host servidores gerenciados no VMM nuvens toosecondary o site do VMM usando o Azure Site Recovery.

artigo Olá inclui pré-requisitos, mostra a você como tooset um cofre da recuperação de Site, instale Olá provedor do Azure Site Recovery na fonte e destino servidores do VMM, registrar servidores Olá no cofre hello, definir configurações de proteção para nuvens do VMM e, em seguida, habilitar proteção para máquinas virtuais do Hyper-V. Concluir teste Olá failover toomake se que tudo está funcionando conforme o esperado.

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Arquitetura
imagem de saudação abaixo mostra canais de comunicação diferente de saudação e portas usadas pelo Azure Site Recovery para replicação e orquestração

![Topologia E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Antes de começar
Verifique se estes pré-requisitos estão em vigor:

| **Pré-requisitos** | **Detalhes** |
| --- | --- |
| **As tabelas** |Você precisa de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site. |
| **VMM** |Você precisará de pelo menos um servidor do VMM.<br/><br/>servidor do VMM Olá deve estar executando pelo menos System Center 2012 SP1 com hello últimas atualizações cumulativas.<br/><br/>Se você quiser tooset a proteção com um único servidor VMM, você precisa de pelo menos duas nuvens configuradas no servidor de saudação.<br/><br/>Se você quiser toodeploy proteção com dois servidores do VMM, cada servidor deve ter pelo menos uma nuvem configurada no servidor VMM primário Olá deseja tooprotect e uma nuvem configurada no servidor do VMM secundário Olá deseja toouse para proteção e recuperação<br/><br/>Todas as nuvens do VMM devem ter o perfil de funcionalidade do Hyper-V Olá definido.<br/><br/>nuvem de origem Olá que você deseja tooprotect deve conter um ou mais grupos de hosts do VMM. |
| **Hyper-V** |Você precisa de um ou mais servidores de host do Hyper-V em grupos de host VMM de primário e secundários de saudação e uma ou mais máquinas virtuais em cada servidor de host do Hyper-V.<br/><br/>Olá servidores Hyper-V de host e de destino devem estar executando pelo menos o Windows Server 2012 com a função hello Hyper-V e ter Olá as últimas atualizações instaladas.<br/><br/>Qualquer servidor Hyper-V que contém máquinas virtuais que você deseja tooprotect devem estar localizados em uma nuvem VMM.<br/><br/>Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente caso tenha um cluster baseado em endereços IP estáticos. Você precisa de agente do cluster Olá tooconfigure manualmente. [Saiba mais](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) na entrada do blog de Aidan Finn. |
| **Mapeamento de rede** |Você pode configurar toomake de mapeamento de rede-se de que as máquinas virtuais replicadas são colocadas idealmente em servidores de host Hyper-V secundários após o failover, e que eles possam se conectar a redes VM tooappropriate. Se você não configurar o mapeamento de rede, máquinas virtuais de réplica não será conectada tooany rede após o failover.<br/><br/>tooset o mapeamento de rede durante a implantação, certifique-se de máquinas virtuais de saudação no servidor de host do Hyper-V de origem Olá são conectado tooa rede VM do VMM. Essa rede deve ser vinculado tooa rede lógica que está associado com a nuvem hello. < br /<br/>nuvem de destino Olá no servidor VMM secundário Olá que você usar para recuperação deve ter uma rede VM correspondente configurada e, por sua vez deve ser vinculado tooa correspondente a rede lógica que está associado com a nuvem de destino hello. |
| **Mapeamento de armazenamento** |Por padrão ao replicar uma máquina virtual em uma origem Hyper-V server tooa destino Hyper-V host servidor host, os dados replicados são armazenados no local padrão de saudação indicado para o host do Hyper-V de destino Olá no Gerenciador Hyper-V. Para obter mais controle sobre onde os dados replicados são armazenados, você pode configurar o mapeamento do armazenamento<br/><br/> armazenamento tooconfigure mapeamento, você precisa tooset backup classificações de armazenamento na fonte hello e servidores do VMM de destino antes de começar a implantação. |

## <a name="step-1-create-a-site-recovery-vault"></a>Etapa 1: criar um cofre de Recuperação de Site
1. Entrar toohello [Portal de gerenciamento](https://portal.azure.com) do servidor do VMM Olá deseja tooregister.
2. Expanda **Serviços de Dados** > **Serviços de Recuperação** e clique em **Cofre do Site Recovery**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **nome**, insira um cofre de saudação tooidentify nome amigável.
5. Em **região** selecione Olá região geográfica para Olá cofre. regiões toocheck suporte consulte disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Clique em **Criar cofre**.

    ![Criar cofre](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Check-in que cofre Olá da barra de status de saudação foi criado. Olá cofre será listado como **Active** na página principal de serviços de recuperação hello.

## <a name="step-2-generate-a-vault-registration-key"></a>Etapa 2: gerar uma chave de registro do cofre
Gere uma chave de registro no cofre de saudação. Depois de baixar Olá provedor Azure Site Recovery e instalá-lo no servidor do VMM hello, você usará esse servidor do VMM Olá tooregister chave no cofre de saudação.

1. Em Olá **dos serviços de recuperação** , clique em página de início rápido do hello cofre tooopen hello. Início rápido também pode ser aberto a qualquer momento usando o ícone de saudação.

    ![Ícone de Inicialização Rápida](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Na lista suspensa de saudação, selecione **entre dois sites do VMM local**.
3. Em **Preparar Servidores VMM**, clique em **Gerar arquivo de chave de registro**. arquivo de chave de saudação é gerado automaticamente e é válido por 5 dias depois que ele é gerado. Se você não estiver acessando Olá portal do Azure do servidor do VMM Olá necessário toocopy toohello servidor de arquivos.

    ![Chave de Registro](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Etapa 3: Instalar Olá provedor Azure Site Recovery
1. Em hello **início rápido** página **servidores VMM preparar**, clique em **baixar provedor Microsoft Azure Site Recovery para instalação nos servidores VMM** tooobtain hello mais recente versão do arquivo de instalação do provedor de saudação.
2. Execute esse arquivo no servidor do VMM de origem de saudação.

   > [!NOTE]
   > Se o VMM for implantado em um cluster e você estiver instalando hello provedor para hello primeira vez instalá-lo em um nó ativo e concluir o servidor do VMM Olá instalação tooregister Olá no cofre de saudação. Em seguida, instale Olá provedor em Olá outros nós. Observe que, se você estiver atualizando Olá provedor tooupgrade em todos os nós é necessário porque elas devem todas ser execução Olá mesma versão do provedor.
   >
   >
3. Olá instalador alguns **Verificar pré-requisitos** e solicitações toobegin a configuração do provedor de serviço Olá toostop de permissão do VMM. saudação de serviço do VMM será reiniciada automaticamente quando a instalação for concluída. Se você estiver instalando em um cluster do VMM que você será solicitado toostop função de Cluster de saudação.
4. No **Microsoft Update** você pode optar por atualizações. Com essa configuração habilitada provedor serão instaladas de acordo com a política do tooyour Microsoft Update.

    ![Atualizações da Microsoft](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. local de instalação de saudação é definido muito**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Clique em Olá toostart do botão de instalação instalando Olá provedor.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Depois de saudação provedor está instalado, clique em **registrar** tooregister servidor de saudação no cofre hello.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. Em **nome do cofre**, verificar nome de saudação do cofre Olá quais saudação servidor será registrado. Clique em *Avançar*.

    ![Registros do servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. Em **Conexão de Internet** especificar hello como o provedor em execução no hello VMM server conecta toohello da Internet. Selecione **conectar-se com as configurações de proxy existentes** configurações de conexão de Internet do toouse saudação padrão configuradas no servidor de saudação.

    ![Configurações da Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Se você quiser toouse um proxy personalizado você deve configurá-lo antes de instalar o provedor de saudação. Quando você definir as configurações de proxy personalizadas um teste será executado toocheck conexão de proxy de saudação.
   * Se você usar um proxy personalizado, ou o proxy padrão exige autenticação, você precisa tooenter os detalhes de proxy do hello, incluindo a porta e endereço de proxy de saudação.
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
13. Clique em **próximo** toocomplete processo de saudação. Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery. saudação do servidor é exibida no **servidores VMM** > **servidores** no cofre hello.

    ![Servidores](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Instalação de linha de comando
Olá provedor Azure Site Recovery também pode ser instalado da linha de comando hello. Esse método pode ser um provedor de saudação tooinstall usado em um núcleo de servidor para o Windows Server 2012 R2.

1. Baixe Olá provedor de arquivo e registro tooa chave pasta de instalação. Por exemplo, C:\ASR.
2. Parar Olá serviço do System Center Virtual Machine Manager
3. Extraia o instalador do provedor Olá executando esses comandos em um prompt de comando com **administrador** privilégios:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale o provedor de saudação executando:

        C:\ASR> setupdr.exe /i
5. Registre o provedor Olá executando:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Quais são os parâmetros de hello:

* **/ Credenciais**: parâmetro obrigatório que especifica o local de saudação em qual Olá arquivo de chave do registro está localizado  
* **/ FriendlyName**: parâmetro obrigatório para o nome de saudação do servidor de host de saudação Hyper-V que aparece no portal do Azure Site Recovery hello.
* **/ EncryptionEnabled**: parâmetro opcional que você precisa toouse somente em Olá VMM tooAzure cenário se você precisar de criptografia de suas máquinas virtuais em repouso no Azure. Verifique se esse nome de saudação do arquivo hello fornecido tem uma **. pfx** extensão.
* **/proxyAddress**: parâmetro opcional que especifica o endereço de saudação do servidor de proxy de saudação.
* **/proxyPort**: parâmetro opcional que especifica a porta de saudação do servidor de proxy de saudação.
* **/proxyUsername**: parâmetro opcional que especifica o nome de usuário de Proxy de saudação (se o proxy exige autenticação).
* **/proxyPassword**: parâmetro opcional que especifica Olá senha para autenticar com o servidor de proxy de saudação (se o proxy exige autenticação).  

## <a name="step-4-configure-cloud-protection-settings"></a>Etapa 4: definir as configurações da proteção de nuvem
Depois que os servidores VMM são registrados, você pode definir as configurações de proteção de nuvem. Se você habilitou a opção Olá **sincronizar dados da nuvem com o cofre Olá** quando você instalou Olá provedor para todas as nuvens no servidor do VMM hello serão exibidos no hello **itens protegidos** guia no cofre hello. Se você não pode sincronizar uma nuvem específica com o Azure Site Recovery no hello **geral** guia da página de propriedades da nuvem no console do VMM Olá Olá.

![Publicar uma nuvem](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Na página início rápido hello, clique em **configurar a proteção para nuvens do VMM**.
2. Em Olá **nuvens do VMM** , selecione a nuvem de saudação que você deseja tooconfigure e vá toohello **configuração** guia.
3. Em **Destino**, selecione **VMM**.
4. Em **local de destino**, selecione Olá servidor VMM no local que gerencia Olá nuvem você deseja toouse para recuperação.
5. Em **nuvem de destino**, selecione Olá destino nuvem você deseja toouse para failover de máquinas virtuais na nuvem de origem hello. Observe que:

   * É recomendável que você selecione uma nuvem de destino que atenda aos requisitos de recuperação para máquinas virtuais de saudação que você protegerá.
   * Uma nuvem pode pertencer somente tooa par de única nuvem — como primária ou uma nuvem de destino.
6. Em **Frequência de cópia**, especifique com que frequência os dados devem ser sincronizados entre os locais de origem e de destino. Observe que essa configuração é relevante apenas quando o host do Hyper-V hello está executando o Windows Server 2012 R2. Para outros servidores, é usada uma configuração padrão de cinco minutos.
7. Em **pontos de recuperação adicionais**, especifique se deseja toocreate outros pontos. valor de zero padrão Olá indica que apenas Olá último ponto de recuperação para uma máquina virtual primária é armazenado em um servidor de host de réplica. Observe que habilitar vários pontos de recuperação exige armazenamento adicional para instantâneos de saudação que são armazenados em cada ponto de recuperação. Por padrão, os pontos de recuperação são criados a cada hora, assim, cada ponto de recuperação contém dados válidos equivalentes a uma hora. valor de ponto de recuperação de saudação que você atribui para a máquina virtual de saudação no console do VMM Olá não deve ser menor que o valor Olá atribuído no console do Azure Site Recovery hello.
8. Em **frequência dos instantâneos consistentes com aplicativos**, especifique a frequência instantâneos consistentes por aplicativo toocreate. Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação. Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado. Observe que, se você habilitar instantâneos consistentes com aplicativos, isso afetará Olá desempenho de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.

    ![Definir configurações de proteção](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. Em **Compactação da transferência de dados**, especifique se os dados replicados transferidos devem ser compactados.
10. Em **autenticação**, especifique como o tráfego será autenticado entre hello primário e servidores de host do Hyper-V de recuperação. Selecione HTTPS, a menos que você tenha um ambiente Kerberos configurado em funcionamento. A Recuperação de Site do Azure configurará automaticamente os certificados para autenticação HTTPS. Nenhuma configuração manual é necessária. Se você selecionar Kerberos, um tíquete Kerberos será usado para autenticação mútua dos servidores de host de saudação. Por padrão, as portas 8083 e 8084 (para certificados) serão aberta no hello Firewall do Windows nos servidores de host do Hyper-V hello. Observe que esta configuração só é relevante para servidores de host Hyper-V no Windows Server 2012 R2.
11. Em **porta**, modifique Olá número da porta na qual fonte hello e escuta de computadores host para o tráfego de replicação de destino. Por exemplo, você pode modificar a configuração de saudação se você quiser tooapply qualidade de serviço (QoS) largura de banda de limitação para o tráfego de replicação. Verifique se a porta Olá não é usada por outro aplicativo e se ela está aberta nas configurações do firewall hello.
12. Em **método de replicação**, especifique como a replicação inicial de dados de origem tootarget locais Olá será tratada, antes do início da replicação normal:

    * **Rede**— copiar dados pela rede Olá pode ser demorada e de uso intensivo de recursos. É recomendável que você use esta opção se nuvem Olá contém máquinas virtuais com discos rígidos virtuais relativamente pequenos e se o site primário Olá é site secundário toohello conectados por uma conexão com largura de banda ampla. Você pode especificar cópia Olá deve iniciar imediatamente ou selecione uma hora. Se você usar a replicação de rede, recomendamos que você agende fora dos horários de pico.
    * **Offline**— esse método Especifica se a replicação saudação inicial será executada usando a mídia externa. É útil se você quiser tooavoid degradação no desempenho da rede, ou para locais geograficamente remotos. toouse esse método, especifique o local de exportação de saudação na nuvem de origem hello e local de importação de saudação na nuvem de destino hello. Quando você habilita a proteção para uma máquina virtual, Olá do disco rígido virtual é copiado toohello especificado Exportar local. Envie-toohello site de destino e copie-o local de importação toohello. saudação de cópias do sistema Olá importado máquinas virtuais da réplica informações toohello.
13. Selecione **excluir máquina de Virtual de réplica** toospecify que Olá a máquina virtual de réplica deve ser excluída se você interromper a proteção de máquina virtual de saudação selecionando Olá **excluir proteção da máquina virtual de saudação**  opção na guia de máquinas virtuais Olá das propriedades de nuvem hello. Com essa configuração habilitada, quando você desabilitar a proteção Olá VM é removido do Azure Site Recovery, configurações de recuperação de Site Olá para a máquina virtual de saudação são removidas no console do VMM hello e Olá réplica será excluída.

    ![Definir configurações de proteção](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Depois de salvar as configurações de saudação um trabalho será criado e pode ser monitorado na Olá **trabalhos** guia. Todos os servidores de host do Hyper-V no hello nuvem de origem do VMM serão configurados para replicação. Configurações de nuvem podem ser modificadas no hello **configurar** guia. Se desejar que o local de destino Olá toomodify ou nuvem de destino deve remover a configuração de nuvem Olá e reconfigure a nuvem de saudação.

### <a name="prepare-for-offline-initial-replication"></a>Preparar a replicação inicial offline
Você precisará Olá toodo tooprepare ações para a replicação inicial offline a seguir:

* No servidor de origem hello, você especificará um local do caminho do qual Olá exportação de dados ocorrerá. Atribua controle total para permissões de NTFS e compartilhamento de serviço do VMM toohello no caminho de exportação de saudação. No servidor de destino hello, você especificará um local do caminho do qual importar dados de saudação ocorrerá. Atribua Olá mesmas permissões neste caminho de importação.
* Se hello importar ou exportar caminho for compartilhado, atribua a associação de grupo de administrador, usuário avançado, operador de impressão ou operador de servidor para a conta de serviço do VMM Olá no computador remoto Olá no qual Olá compartilhado está localizado.
* Se você estiver usando quaisquer hosts de tooadd da contas executar como, em Olá importar e exportar caminhos, atribuir a leitura e permissões de gravação toohello as contas executar como no VMM.
* Olá importar e exportar compartilhamentos não deve estar localizado em qualquer computador usado como um servidor de host do Hyper-V, porque não há suporte para a configuração de loopback pelo Hyper-V.
* No Active Directory, em cada servidor de host do Hyper-V que contém máquinas virtuais que você deseja tooprotect, habilitar e configurar a delegação restrita tootrust Olá computadores remotos nos quais Olá importação e exportação do caminhos estão localizados, da seguinte maneira:
  1. No controlador de domínio hello, abra **computadores e usuários do Active Directory**.
  2. Na árvore de console Olá clique **DomainName** > **computadores**.
  3. Nome do servidor de host com o botão direito Olá Hyper-V > **propriedades**.
  4. Em Olá **delegação** , clique em T**rust neste computador delegação toospecified somente para serviços**.
  5. Clique em **Usar qualquer protocolo de autenticação**.
  6. Clique em **Adicionar** > **Usuários e Computadores**.
  7. Nome do tipo saudação do computador de saudação que hospeda o caminho de exportação hello > **Okey**. Na lista de saudação de serviços disponíveis, mantenha pressionada a tecla CTRL de saudação e clique em **cifs** > **Okey**. Repita para nome de saudação do computador Olá desse caminho de importação de saudação hosts. Repita conforme necessário para servidores host Hyper-V adicionais.

## <a name="step-5-configure-network-mapping"></a>Etapa 5: configurar o mapeamento de rede
1. Na página início rápido hello, clique em **mapear redes**.
2. Selecione o servidor VMM de origem de saudação do qual você deseja toomap redes e, em seguida, Olá Olá do destino do VMM server toowhich redes serão mapeadas. Olá lista de redes de origem e suas redes de destino associados é exibida. Um valor vazio é mostrado para redes que não estão mapeadas no momento.
3. Selecione uma rede em **Rede na origem** > **Mapear**. serviço de saudação detecta Olá redes de VM no servidor de destino hello e os exibe. Clique em Olá informações ícone próximo toohello origem e destino nomes tooview Olá sub-redes de rede para cada rede.

    ![Configurar o mapeamento de rede](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Na caixa de diálogo Olá, selecione uma das redes VM Olá Olá VMM do servidor de destino.

    ![Selecionar uma rede de destino](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Quando você seleciona uma rede de destino, hello nuvens protegidas que usam a rede de origem Olá são exibidas. Redes de destino disponíveis que estão associadas com hello nuvens usadas para proteção também serão exibidas. É recomendável que você selecione uma rede de destino é nuvens de saudação tooall disponíveis que está usando para proteção. Ou, você também pode ir toohello servidor do VMM e modificar Olá nuvem propriedades tooadd Olá rede lógica correspondente toohello rede de vm que você deseja toochoose.
6. Clique em processo de mapeamento Olá marca de seleção toocomplete hello. Progresso do mapeamento Olá tootrack um trabalho é iniciado. Você pode exibi-lo no hello **trabalhos** guia.

## <a name="step-6-configure-storage-mapping"></a>Etapa 6: configurar mapeamento de armazenamento
Por padrão ao replicar uma máquina virtual em uma origem Hyper-V server tooa destino Hyper-V host servidor host, os dados replicados são armazenados no local padrão de saudação indicado para o host do Hyper-V de destino Olá no Gerenciador Hyper-V. Para obter mais controle sobre onde os dados replicados são armazenados, você pode configurar mapeamentos de armazenamento da seguinte maneira:

1. Defina classificações de armazenamento em ambas as fonte hello e servidores do VMM de destino. [Saiba mais](https://technet.microsoft.com/library/gg610685.aspx). As classificações devem estar disponíveis toohello servidores de host Hyper-V nas nuvens de origem e destino. Não é necessário classificações toohave Olá mesmo tipo de armazenamento. Por exemplo, você pode mapear uma classificação de origem que contém o SMB compartilhamentos tooa classificação de destino que contém CSVs.
2. Depois que classificações estiverem em vigor, você poderá criar mapeamentos. toodo isso em Olá **início rápido** página > **mapear armazenamento**.
3. Clique em Olá **armazenamento** guia > **mapear classificações de armazenamento**.
4. Em Olá **mapear classificações de armazenamento** , selecione as classificações de origem hello e servidores VMM de destino. Salve suas configurações.

    ![Selecionar uma rede de destino](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Etapa 7: habilitar proteção da máquina virtual
Depois de servidores, nuvens e redes configuradas corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem hello.

1. Em Olá **máquinas virtuais** na nuvem Olá no qual Olá a máquina virtual está localizada, clique em **Habilitar proteção** > **adicionar máquinas virtuais**.
2. Na lista de saudação de máquinas virtuais na nuvem hello, selecione Olá um deseja tooprotect.

    ![Habilitar Proteção da Máquina Virtual](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Acompanhar o progresso da ação Habilitar proteção na saudação de saudação **trabalhos** guia, incluindo a replicação inicial hello. Após o trabalho finalizar proteção de saudação executa Olá VM está pronta para failover. Depois de habilitar a proteção e máquinas virtuais forem replicadas, você será capaz de tooview-los no Azure.

    ![Trabalho de proteção da máquina virtual](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Você também pode habilitar a proteção para máquinas virtuais no console do VMM hello. Clique em **Habilitar proteção** Olá da barra de ferramentas Olá **do Azure Site Recovery** guia nas propriedades de máquina virtual de saudação.
>
>

### <a name="on-board-existing-virtual-machines"></a>Integrar máquinas virtuais existentes
Se você tiver máquinas virtuais existentes no VMM que está replicando com a réplica do Hyper-V, você precisará tooonboard-los para proteção de recuperação de Site do Azure da seguinte maneira:

1. Verifique se que você tem nuvens primárias e secundárias. Certifique-se de que hospeda máquina virtual existente de saudação do servidor de saudação Hyper-V está localizado na nuvem primária hello e servidor Hyper-V Olá Olá máquina de virtual de réplica de hospedagem está localizado na nuvem secundária hello. Verifique se você configurou as configurações de proteção para nuvens de saudação. configurações de saudação devem corresponder às configuradas atualmente para réplica do Hyper-V. Caso contrário, a replicação de máquina virtual poderá não funcionar conforme o esperado.
2. Em seguida, habilite a proteção para a máquina virtual primária de saudação. Recuperação de Site do Azure e o VMM garantirá que hello mesmo host de réplica e máquina virtual sejam detectados e reutilizará e restabelecerá a replicação usando as configurações de saudação configuradas durante a configuração de nuvem do Azure Site Recovery.

## <a name="test-your-deployment"></a>Testar a implantação
planejar a sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar um failover de teste para Olá tootest.  O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.

### <a name="create-a-recovery-plan"></a>Criar um plano de recuperação
1. Em Olá **planos de recuperação** , clique em **criar plano de recuperação**.
2. Especifique um nome para o plano de recuperação hello e servidores do VMM de origem e destino. o servidor de origem Olá deve ter máquinas virtuais que são habilitadas para failover e recuperação. Selecione **Hyper-V** tooview somente nuvens configuradas para replicação do Hyper-V.

    ![Criar plano de recuperação](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. Em **Selecionar Máquina Virtual**, selecione os grupos de replicação. Todas as máquinas virtuais associadas ao grupo de replicação Olá serão selecionadas e adicionado toohello plano de recuperação. Essas máquinas virtuais são adicionadas toohello grupo de padrão de plano de recuperação — grupo 1. Você pode adicionar mais grupos se necessário. Observe que, depois de máquinas virtuais de replicação serão inicializadas de acordo com a ordem de saudação de grupos do plano de recuperação de saudação.

    ![Adicionar máquinas virtuais](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Depois que um plano de recuperação foi criado, ele aparece na lista Olá Olá **planos de recuperação** guia.

### <a name="run-a-test-failover"></a>Execute um teste de failover
1. Em Olá **planos de recuperação** , selecione o plano de saudação e clique em **Failover de teste**.
2. Em Olá **confirmar Failover de teste** página, selecione **nenhum**. Observe que com esta opção habilitada Olá failover de máquinas virtuais de réplica não será conectada tooany rede. Isso testará que Olá máquina virtual falhar em conforme o esperado, mas não testar seu ambiente de rede de replicação. Examinar como muito[executar um failover de teste](site-recovery-failover.md) para obter mais detalhes sobre como toouse diferentes opções de rede.
3. Olá máquina de virtual de teste será criada no mesmo host como host Olá na qual Olá máquina virtual de réplica existe de saudação. Ele é adicionado toohello mesma nuvem na qual Olá máquina virtual de réplica está localizada.

### <a name="run-a-recovery-plan"></a>Executar um plano de recuperação
Depois de máquina de virtual de réplica de saudação de replicação não pode ter um endereço IP que é hello mesmo que o endereço IP Olá Olá máquina virtual primária. Máquinas virtuais atualizará o servidor DNS Olá que eles estão usando depois que eles são iniciados. Você também pode adicionar um script tooupdate Olá servidor DNS tooensure uma atualização em tempo hábil.

#### <a name="script-tooretrieve-hello-ip-address"></a>Endereço IP do script tooretrieve Olá
Execute este endereço IP do exemplo script tooretrieve hello.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Script tooupdate DNS
Executar este script de exemplo tooupdate DNS, especificando o endereço IP hello recuperado usando o script de exemplo hello anterior.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informações de privacidade para Site Recovery
Esta seção fornece informações adicionais sobre privacidade para Olá serviço Microsoft Azure Site Recovery ("serviço"). declaração de privacidade tooview Olá para serviços do Microsoft Azure, consulte o [declaração de privacidade do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=324899)

**Recurso: Registro**

* **O que ele faz**: registra o servidor no serviço para que as máquinas virtuais possam ser protegidas
* **Informações coletadas**: depois de registrar Olá serviço coleta, processa e transmite as informações de certificado de gerenciamento do servidor do VMM Olá que designou tooprovide recuperação de desastres usando o nome do serviço de saudação do servidor do VMM Olá, e o nome da saudação de nuvens de máquina virtual no servidor do VMM.
* **Uso das informações**:

  * Certificado de gerenciamento — isso é usado toohelp identificar e autenticar o servidor do VMM Olá registrado para acesso toohello serviço. Olá serviço usa Olá parte da chave pública Olá certificado toosecure registrado um token que Olá apenas o servidor do VMM pode acessar. servidor de saudação precisa toouse esse recursos de serviço toohello toogain token de acesso.
  * Nome do servidor do VMM Olá — nome do servidor do VMM Olá é tooidentify necessário e se comunicar com o servidor do VMM apropriado Olá em qual Olá nuvens estão localizadas.
  * Nomes de nuvem do servidor do VMM hello – nome da nuvem Olá é necessária ao usar a nuvem de serviço Olá emparelhamento/desemparelhamento recurso descrito abaixo. Quando você decidir toopair sua nuvem de um data center primário com outra nuvem no data center de recuperação Olá, são apresentados nomes de saudação de todas as nuvens de saudação do data center de recuperação de saudação.
* **Escolha**: essas informações são uma parte essencial da saudação processo de registro de serviço porque ele ajuda e Olá Service tooidentify Olá VMM server para o qual você deseja tooprovide proteção de recuperação de Site do Azure, bem como tooidentify Olá servidor do VMM registrado correto. Se você não quiser toosend este toohello informações serviço, não use esse serviço. Se você registrar seu servidor e, em seguida, mais tarde quiser toounregister, poderá fazê-lo excluindo informações de saudação do servidor VMM do portal de serviço hello (que é Olá portal do Azure).

**Recurso: Habilitar a proteção do Azure Site Recovery**

* **O que ele faz**: Olá provedor Azure Site Recovery instalada no servidor do VMM Olá é o canal de saudação para se comunicar com o serviço de saudação. Olá provedor é uma biblioteca de vínculo dinâmico (DLL) hospedada no processo do VMM hello. Após Olá que provedor está instalado, recurso de "Recuperação do Datacenter" hello obtém habilitado no console do administrador do VMM hello. Quaisquer máquinas virtuais novas ou existentes em uma nuvem pode habilitar uma propriedade chamada "Recuperação do Datacenter" toohelp proteger a máquina virtual de saudação. Quando essa propriedade estiver definida, Olá provedor envia Olá nome e ID toohello de máquina virtual Olá serviço. proteção virtual Olá é habilitada pela tecnologia de replicação do Windows Server 2012 ou Windows Server 2012 R2 Hyper-V. dados da máquina virtual Olá são replicados de um tooanother de host do Hyper-V (normalmente localizado em um data center diferente de "recuperação").
* **Informações coletadas**: Olá serviço coleta, processa e transmite metadados para a máquina virtual de saudação, que inclui o nome hello, ID, rede virtual e nome de saudação da nuvem de saudação à qual ela pertence.
* **Uso de informações**: Olá serviço usa Olá acima informações toopopulate Olá máquina virtual em seu portal de serviço.
* **Escolha**: isso é uma parte essencial do serviço hello e não pode ser desativado. Se não quiser que essas informações sejam enviadas toohello serviço, não habilite a proteção do Azure Site Recovery para todas as máquinas virtuais. Observe que todos os dados enviados por Olá provedor toohello serviço é enviado via HTTPS.

**Recurso: Plano de recuperação**

* **O que ele faz**: esse recurso ajuda a toobuild um plano de orquestração do data center de "recuperação" hello. Você pode definir a ordem Olá no qual Olá máquinas virtuais ou um grupo de máquinas virtuais deve ser iniciado no local de recuperação de saudação. Você também pode especificar qualquer toobe scripts automatizados executar ou qualquer toobe manual ação adotada, no tempo de saudação de recuperação para cada máquina virtual. O failover (abordado na próxima seção, Olá) costuma ser disparado no nível de plano de recuperação para a recuperação coordenada de saudação.
* **Informações coletadas**: Olá serviço coleta, processa e transmite metadados Olá plano de recuperação, incluindo os metadados da máquina virtual e quaisquer scripts de automação e Observações da ação manual.
* **Uso de informações**: Olá metadados descrito acima são o plano de recuperação de saudação toobuild usado em seu portal de serviço.
* **Escolha**: isso é uma parte essencial do serviço hello e não pode ser desativado. Se não quiser que essas informações sejam enviadas toohello serviço, não crie planos de recuperação neste serviço.

**Recurso: Mapeamento de rede**

* **O que ele faz**: este recurso permite que você toomap informações de data center Olá dados primários center toohello recuperação de rede. Quando as máquinas virtuais de saudação são recuperadas no site de recuperação Olá, esse mapeamento ajuda a estabelecer a conectividade de rede para eles.
* **Informações coletadas**: como parte do recurso de mapeamento de rede hello, Olá serviço coleta, processa e transmite metadados Olá de redes lógicas de saudação para cada site (primário e datacenter).
* **Uso de informações**: Olá serviço usa Olá metadados toopopulate seu portal de serviço onde você pode mapear as informações de rede hello.
* **Escolha**: esta é uma parte essencial do serviço de saudação e não pode ser desativada. Se não quiser que essas informações sejam enviadas toohello serviço, não use o recurso de mapeamento de rede hello.

**Recurso: Failover — planejado, não planejado, teste**

* **O que ele faz**: esse recurso ajuda a failover de uma máquina virtual de um dados gerenciados no VMM center tooanother gerenciada pelo VMM data center. ação de saudação de failover é disparada pelo usuário Olá em seu portal de serviço. Os motivos possíveis para um failover incluem um evento não planejado (por exemplo no caso de saudação de um disaster0 natural; um evento planejado (por exemplo datacenter balanceamento de carga); um failover de teste (por exemplo um ensaio do plano de recuperação).

Olá provedor no servidor do VMM Olá seja notificado do evento Olá Olá serviço e executa uma ação de failover no host do Hyper-V Olá por meio das interfaces do VMM. O failover real da máquina virtual de saudação de um tooanother de host do Hyper-V (normalmente em execução em um data center diferente de "recuperação") é tratado pela tecnologia de replicação de Windows Server 2012 ou Windows Server 2012 R2 Hyper-V hello. Após a conclusão do failover hello, Olá provedor instalado no servidor do VMM de saudação do data center de "recuperação" hello envia Olá sucesso informações toohello serviço.

* **Informações coletadas**: Olá serviço usa Olá acima de status da saudação toopopulate informações de informações de ação de failover Olá no seu portal de serviço.
* **Uso de informações**: Olá serviço usa Olá acima informações da seguinte maneira:

  * Certificado de gerenciamento — isso é usado toohelp identificar e autenticar o servidor do VMM Olá registrado para acesso toohello serviço. Olá serviço usa Olá parte da chave pública Olá certificado toosecure registrado um token que Olá apenas o servidor do VMM pode acessar. servidor de saudação precisa toouse esse recursos de serviço toohello toogain token de acesso.
  * Nome do servidor do VMM Olá — nome do servidor do VMM Olá é tooidentify necessário e se comunicar com o servidor do VMM apropriado Olá em qual Olá nuvens estão localizadas.
  * Nomes de nuvem do servidor do VMM hello – nome da nuvem Olá é necessária ao usar a nuvem de serviço Olá emparelhamento/desemparelhamento recurso descrito abaixo. Quando você decidir toopair sua nuvem de um data center primário com outra nuvem no data center de recuperação Olá, são apresentados nomes de saudação de todas as nuvens de saudação do data center de recuperação de saudação.
* **Escolha**: isso é uma parte essencial do serviço hello e não pode ser desativado. Se não quiser que essas informações sejam enviadas toohello serviço, não use esse serviço.

## <a name="next-steps"></a>Próximas etapas
Depois de executar um toocheck de failover de teste que seu ambiente está funcionando conforme o esperado, [saber mais sobre](site-recovery-failover.md) diferentes tipos de failovers.
