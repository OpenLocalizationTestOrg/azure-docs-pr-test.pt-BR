---
title: aaaReplicate VMs Hyper-V no VMM com SAN usando o Azure Site Recovery | Microsoft Docs
description: "Este artigo descreve como máquinas virtuais de tooreplicate Hyper-V entre dois sites com o Azure Site Recovery usando a replicação SAN."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Replicar máquinas virtuais do Hyper-V no site secundário do VMM nuvens tooa com o Azure Site Recovery com SAN


Use este artigo se você quiser toodeploy [do Azure Site Recovery](site-recovery-overview.md) toomanage replicação de máquinas virtuais do Hyper-V (gerenciados nas nuvens do System Center Virtual Machine Manager) tooa site VMM secundário, usando o Azure Site Recovery no portal clássico do hello. Esse cenário não está disponível no novo portal do Azure de saudação.



Lança os comentários no final deste artigo hello. Obter respostas a perguntas tootechnical em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Por que replicar com SAN e Site Recovery?

* SAN fornece uma solução de replicação de nível corporativo e dimensionável para que um site primário que contém Hyper-V com SAN pode replicar o site secundário do tooa LUNs com SAN. O armazenamento é gerenciado pelo VMM e a replicação e o failover são gerenciados com o Site Recovery.
* Recuperação de site trabalha com vários [parceiros de armazenamento de SAN](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide a replicação entre armazenamento Fibre Channel e iSCSI.  
* Use seu SAN infraestrutura tooprotect críticos aplicativos existentes implantados em clusters Hyper-V. As VMs podem ser replicadas como um grupo para que os aplicativos com N camadas possam sofrer failover consistentemente.
* A replicação SAN garante a consistência da replicação nas diferentes camadas de um aplicativo com a replicação síncrona para o RTO e RPO baixos, e a replicação assíncrona para a alta flexibilidade (dependendo das capacidades da matriz de armazenamento).  
* Você pode gerenciar o armazenamento SAN no hello malha do VMM e use o SMI-S em um armazenamento existente do VMM toodiscover.  

Observe que:
- Replicação do site a site com SAN não está disponível no hello portal do Azure. Só está disponível no portal clássico do hello. Não não possível criar novos cofres no portal clássico do hello. Os cofres existentes podem ser mantidos.
- Não há suporte para replicação de SAN tooAzure.
- Você não pode replicar VHDXs compartilhados ou unidades lógicas (LUNs) que estão diretamente conectados tooVMs via iSCSI ou Fibre Channel. Os clusters de convidados podem ser replicados.


## <a name="architecture"></a>Arquitetura

![Arquitetura de SAN](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: configurar um cofre de recuperação de Site no portal do Azure de saudação.
- **Armazenamento de SAN**: armazenamento SAN é gerenciado no hello malha do VMM. Adicionar provedor de armazenamento hello, crie classificações de armazenamento e configurar pools de armazenamento.
- **VMM e Hyper-V**: recomendamos um servidor VMM em cada site. Configure as nuvens privadas do VMM e coloque os clusters Hyper-V nessas nuvens. Durante a implantação, Olá provedor Azure Site Recovery está instalado em cada servidor do VMM e servidor hello está registrado no cofre de saudação. Olá provedor se comunica com a replicação de toomanage do serviço de recuperação de Site hello, failover e failback.
- **Replicação**: depois de configurar o armazenamento no VMM e configurar a replicação na recuperação de Site, a replicação ocorre entre o armazenamento SAN primário e secundário hello. Nenhum dado de replicação é enviado tooSite recuperação.
- **Failover**: habilitar o failover no portal de recuperação de Site hello. Não há perda de dados durante o failover porque a replicação é síncrona.
- **Failback**: toofail novamente, habilite as alterações delta na tootransfer replicação inversa do site primário do toohello Olá site secundário. Após a conclusão da replicação inversa, executar um failover planejado de tooprimary secundário. Esse failover planejado para réplica Olá VMs no site secundário hello e inicia no site primário hello.


## <a name="before-you-start"></a>Antes de começar


**Pré-requisitos** | **Detalhes**
--- | ---
**As tabelas** |Você precisa de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site. Criar um tooconfigure do cofre Azure Site Recovery e gerenciar replicação e failover.
**VMM** | Você pode usar um único servidor do VMM e replicar entre nuvens diferentes, mas é recomendável um VMM no site primário hello e um no site secundário hello. Um VMM pode ser implantado como um servidor físico ou virtual autônomo, ou como um cluster. <br/><br/>servidor do VMM Olá deve estar executando o System Center 2012 R2 ou posterior com hello últimas atualizações cumulativas.<br/><br/> Você precisa de pelo menos uma nuvem configurada no servidor VMM primário Olá deseja tooprotect e uma nuvem configurada no servidor do VMM secundário Olá desejar toouse para failover.<br/><br/> nuvem de origem Olá deve conter um ou mais grupos de hosts do VMM.<br/><br/> Todas as nuvens do VMM devem ter o perfil de capacidade do Hyper-V Olá definido.<br/><br/> Para obter mais informações sobre como configurar as nuvens do VMM, consulte [Implantar uma nuvem VM privada](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | Você precisa de um ou mais clusters Hyper-V nas nuvens do VMM primárias e secundárias.<br/><br/> cluster de Hyper-V de origem Olá deve conter uma ou mais máquinas virtuais.<br/><br/> grupos de hosts do VMM Olá em sites primários e secundários do hello devem conter pelo menos um dos clusters do Hyper-V hello.<br/><br/>servidores de Hyper-V de host e de destino de saudação devem estar executando o Windows Server 2012 ou posterior com atualizações de mais recentes função e Olá Olá Hyper-V instalado.<br/><br/> Se você estiver executando o Hyper-V em um cluster e tiver um cluster baseado em endereços IP estáticos, o agente do cluster não será criado automaticamente. Você deve configurá-lo manualmente. Para obter mais informações, consulte [Preparando os clusters de hosts para a réplica do Hyper-V](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).
**Armazenamento SAN** | Você pode replicar as máquinas virtuais em cluster convidadas com o armazenamento iSCSI ou de canal, ou usando discos rígidos virtuais compartilhados (vhdx).<br/><br/> Você precisa de duas matrizes SAN: um no site primário hello e site secundário de uma saudação em.<br/><br/> Uma infraestrutura de rede deve ser configurada entre matrizes de saudação. Devem ser configurados o emparelhamento e a replicação. As licenças de replicação devem ser configuradas de acordo com requisitos de matriz de armazenamento de saudação.<br/><br/>Configure o sistema de rede entre os servidores de host de saudação Hyper-V e matriz de armazenamento Olá para que os hosts podem se comunicar com os LUNs de armazenamento utilizando iSCSI ou Fibre Channel.<br/><br/> Verificar [matrizes de armazenamento com suporte](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Provedores de SMI-S de fabricantes de matriz de armazenamento devem ser instalados e matrizes de SAN Olá devem ser gerenciados pelo provedor de saudação. Configure Olá provedor acordo toomanufacturer instruções.<br/><br/>Verifique se o provedor de SMI-S da matriz que hello está em um servidor que Olá VMM servidor possa acessar via rede de saudação com um endereço IP ou FQDN.<br/><br/> Cada matriz SAN deve ter um ou mais pools de armazenamento disponíveis.<br/><br/> Olá servidor primário do VMM deve gerenciar a matriz primária hello e Olá servidor secundário do VMM deve gerenciar a matriz secundária hello.
**Mapeamento de rede** | Configure mapeamento de rede para que as máquinas virtuais replicadas são colocadas idealmente em servidores de host Hyper-V secundários após o failover, e para que sejam conectados tooappropriate redes VM. Se você não configurar o mapeamento de rede, máquinas virtuais de réplica não será conectada tooany rede após o failover.<br/><br/> Verifique se as redes de VMM estão configuradas corretamente para poder configurar o mapeamento da rede durante a implantação do Site Recovery. No VMM, Olá VMs no host de Hyper-V de origem Olá deve ser conectado tooa rede VM do VMM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.<br/><br/> nuvem de destino Olá deve ter uma rede VM correspondente e, por sua vez deve ser vinculado tooa correspondente rede lógica que está associado com a nuvem de destino hello.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Etapa 1: Preparar a infraestrutura do VMM Olá
tooprepare sua infraestrutura do VMM, você precisa:

1. verificar as nuvens do VMM;
2. integrar e classificar o armazenamento de SAN no VMM.
3. criar LUNs e alocar armazenamento;
4. criar grupos de replicação;
5. configurar as redes de VMs.

### <a name="verify-vmm-clouds"></a>Verificar nuvens do VMM

Verifique se suas nuvens do VMM estão configuradas corretamente antes de começar a implantação do Site Recovery.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Integrar e classificar o armazenamento SAN no hello malha do VMM

1. No console do VMM hello, vá muito**malha** > **armazenamento** > **adicionar recursos** > **dedispositivosdearmazenamento**.
2. Em Olá **adicionar dispositivos de armazenamento** assistente, selecione **selecionar um tipo de provedor de armazenamento** e selecione **dispositivos SAN e NAS descobertos e gerenciados por um provedor de SMI-S**.

    ![Tipo de provedor](./media/site-recovery-vmm-san/provider-type.png)

3. Em Olá **especificar protocolo e endereço de provedor de SMI-S de armazenamento de hello** página, selecione **CIMXML SMI-S** e especifique as configurações para o provedor de conexão toohello hello.
4. Em **endereço IP do provedor ou FQDN** e **porta TCP/IP**, especifique as configurações de saudação para o provedor de conexão toohello. Você pode usar uma conexão SSL apenas para CIMXML de SMI-S.

    ![Conexão com o provedor](./media/site-recovery-vmm-san/connect-settings.png)
5. Em **conta executar como**, especifique uma conta executar como do VMM que pode acessar o provedor hello, ou criar uma conta.
6. Em Olá **reunir informações** página, o VMM tenta automaticamente toodiscover e importar informações de dispositivo de armazenamento de saudação. descoberta de tooretry, clique em **examinar provedor**. Se o processo de descoberta de saudação for bem-sucedida, Olá descobertos matrizes de armazenamento, pools de armazenamento, fabricante, modelo e capacidade são listados na página de saudação.

    ![Descoberta do armazenamento](./media/site-recovery-vmm-san/discover.png)
7. Em **selecione tooplace de pools de armazenamento sob gerenciamento e atribuir uma classificação**, selecione Olá pools de armazenamento que o VMM gerenciará e atribuí-los uma classificação. Informações de LUN são importadas de pools de armazenamento hello. Criar LUNs com base em aplicativos Olá precisar tooprotect, seus requisitos de capacidade e seus requisitos para o que precisa tooreplicate juntos.

    ![Classificação do armazenamento](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>Criar LUNs e alocar armazenamento

Criar LUNs com base em aplicativos Olá precisar tooprotect, requisitos de capacidade e seus requisitos para o que precisa tooreplicate juntos.

1. Depois de armazenamento Olá aparece no hello malha do VMM, você poderá [provisionar LUNs](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > Não adicione VHDs para Olá VM que são habilitados para replicação tooLUNs. Se as LUNs não estiverem em um grupo de replicação do Site Recovery, elas não serão detectadas pelo Site Recovery.
     >

2. Aloque o cluster de host Hyper-V do toohello de capacidade de armazenamento para que o VMM possa implantar o armazenamento da máquina virtual dados toohello provisionado:

   * Antes de alocar armazenamento toohello cluster, você precisa tooallocate-grupo de hosts do VMM toohello no qual Olá cluster reside. Para obter mais informações, consulte [como tooa de unidades lógicas de armazenamento tooallocate hospedar o grupo no VMM](https://technet.microsoft.com/library/gg610686.aspx) e [como os pools de armazenamento tooallocate tooa o grupo de hosts no VMM](https://technet.microsoft.com/library/gg610635.aspx).
   * Alocar armazenamento ao cluster toohello capacidade conforme descrito em [como cluster de armazenamento tooconfigure em um host Hyper-V no VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Tipo de provedor](./media/site-recovery-vmm-san/provider-type.png)
3. Em **especificar protocolo e endereço de provedor de SMI-S de armazenamento de hello**, selecione **CIMXML SMI-S**. Especifica configurações de Olá para conectar-se o provedor de toohello. Você pode usar uma conexão SSL apenas para o CIMXML do SMI-S.

    ![Conexão com o provedor](./media/site-recovery-vmm-san/connect-settings.png)
4. Em **conta executar como**, especifique uma conta executar como do VMM que pode acessar o provedor hello, ou criar uma conta.
5. Em **reunir informações**, o VMM tenta automaticamente toodiscover e importar informações de dispositivo de armazenamento de saudação. Se você precisar tooretry, clique em **examinar provedor**. Quando o processo de descoberta Olá tiver êxito, matrizes de armazenamento hello, capacidade, fabricante, modelo e pools de armazenamento são listados na página de saudação.

    ![Descoberta do armazenamento](./media/site-recovery-vmm-san/discover.png)
7. Em **selecione tooplace de pools de armazenamento sob gerenciamento e atribuir uma classificação**, selecione Olá pools de armazenamento que o VMM gerenciará e atribuí-los uma classificação. Informações de LUN são importadas de pools de armazenamento hello.

    ![Classificação do armazenamento](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Criar grupos de replicação

Crie um grupo de replicação que inclui todos os LUNs Olá precisará tooreplicate juntos.

1. No console do VMM hello, abra Olá **grupos de replicação** guia de propriedades de matriz de armazenamento hello e clique **novo**.
2. Crie grupo de replicação de saudação.

    ![Grupo de replicação de SAN](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Configurar redes

Se você quiser que o mapeamento de rede tooconfigure, Olá a seguir:

1. Consulte o mapeamento de rede do Site Recovery.
2. Prepare redes de VM no VMM:

   * [Configure redes lógicas](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Configure as redes de VMM](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Etapa 2: criar um cofre

1. Entrar toohello [portal do Azure](https://portal.azure.com) do servidor do VMM Olá deseja tooregister no cofre hello.
2. Expanda os **Serviços de Dados** > **Serviços de Recuperação** e clique em **Cofre do Site Recovery**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **nome**, insira um cofre de saudação tooidentify nome amigável.
5. Em **região**, selecione Olá região geográfica para Olá cofre. regiões de toocheck com suporte, consulte [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Clique em **Criar cofre**.

    ![Novo cofre](./media/site-recovery-vmm-san/create-vault.png)

Verifique a saudação tooconfirm de barra de status que Olá cofre foi criado com êxito. Olá cofre será listado como **Active** em Olá principal **dos serviços de recuperação** página.

### <a name="register-hello-vmm-servers"></a>Registrar servidores do VMM Olá

1. Olá abrir **início rápido** página Olá **dos serviços de recuperação** página. Início rápido também pode ser aberto a qualquer momento, escolhendo o ícone de saudação.

    ![Ícone de Inicialização Rápida](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Na caixa de lista suspensa hello, selecione **entre o Hyper-V usando a replicação de matriz de site local**.

    ![Chave de Registro](./media/site-recovery-vmm-san/select-san.png)
3. Em **servidores VMM preparar**, baixe a versão mais recente Olá Olá provedor Azure Site Recovery do arquivo de instalação.
4. Execute esse arquivo no servidor do VMM de origem de saudação. Se o VMM for implantado em um cluster e você estiver instalando hello provedor para hello primeira vez, instale Olá provedor em um nó ativo e concluir o servidor do VMM Olá instalação tooregister Olá no cofre hello. Em seguida, instale Olá provedor em Olá outros nós. Se você estiver atualizando Olá provedor, é necessário tooupgrade em todos os nós para que eles têm Olá a mesma versão do provedor.
5. Olá instalador verifica se os requisitos e solicitações permissão toostop Olá instalação de provedor de toobegin de serviço do VMM. Olá serviço será reiniciado automaticamente quando a instalação for concluída. Em um cluster do VMM, você estará função de Cluster Olá toostop solicitada.
6. Em **Microsoft Update**, você pode aceitar atualizações e atualizações de provedor serão instaladas de acordo com a política do Microsoft Update tooyour.

    ![Atualizações da Microsoft](./media/site-recovery-vmm-san/ms-update.png)

7. Por padrão, o local de instalação de saudação para Olá provedor é <SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin. Clique em **instalar** toobegin.

    ![Local de Instalação](./media/site-recovery-vmm-san/install-location.png)

8. Depois de saudação provedor estiver instalada, clique em **registrar** servidor do VMM Olá tooregister no cofre hello.

    ![Instalação Concluída](./media/site-recovery-vmm-san/install-complete.png)

9. Em **Conexão de Internet**, especifique como Olá provedor se conecta toohello da Internet. Selecione **usar configurações de proxy do sistema padrão** se quiser que as configurações de conexão de Internet toouse saudação padrão no servidor de saudação.

    ![Configurações da Internet](./media/site-recovery-vmm-san/proxy-details.png)

   * Se você quiser toouse um proxy personalizado, configurá-lo antes de instalar o provedor de saudação. Quando você define as configurações de proxy personalizado, um teste é executado em conexão de proxy Olá toocheck.
   * Se você usar um proxy personalizado, ou se o proxy padrão requer autenticação, você deve inserir os detalhes de proxy hello, incluindo a porta e endereço de saudação.
   * Olá necessário que URLs devem ser acessíveis do servidor do VMM hello.
   * Se você usar um proxy personalizado, uma conta executar como do VMM (DRAProxyAccount) é criada automaticamente usando Olá especificada credenciais de proxy. Configure o servidor de proxy de saudação para que essa conta possa autenticar. Você pode modificar Olá executar como configurações de conta no console do VMM hello (**configurações** > **segurança** > **contas executar como**  >  **DRAProxyAccount**). Você deve reiniciar o serviço do VMM de Olá para Olá alterar tootake efeito.
10. Em **chave de registro**, selecione chave Olá baixado do servidor do VMM Olá toohello portal e copiado.
11. Em **nome do cofre**, verificar nome de saudação do cofre Olá quais saudação servidor será registrado.

    ![Registros do servidor](./media/site-recovery-vmm-san/vault-creds.png)
12. configuração de criptografia de saudação é usada apenas para replicação de tooAzure do VMM. Você pode ignorá-la.

    ![Registros do servidor](./media/site-recovery-vmm-san/encrypt.png)
13. Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello. Em uma configuração de cluster, especifique o nome de função de cluster saudação do VMM.
14. Em **sincronização inicial de metadados de nuvem**, selecione se deseja toosynchronize metadados para todas as nuvens no servidor do VMM hello. Essa ação precisa apenas toohappen uma vez em cada servidor. Se você não quiser toosynchronize todas as nuvens, você pode deixar essa configuração está desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello.

    ![Registros do servidor](./media/site-recovery-vmm-san/friendly-name.png)

15. Clique em **próximo** toocomplete processo de saudação. Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery. saudação do servidor é exibida no **servidores** > **servidores VMM** no cofre hello.

### <a name="command-line-installation"></a>Instalação da linha de comando

Olá provedor Azure Site Recovery também pode ser instalado usando Olá a seguinte linha de comando. Esse método pode ser usado tooinstall provedor de saudação no Server Core para Windows Server 2012 R2.

1. Baixe Olá provedor de arquivo e registro tooa chave pasta de instalação. Por exemplo, C:\ASR.
2. Pare o serviço VMM hello.
3. Extraia o instalador do provedor hello. Execute estes comandos como administrador:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale Olá provedor:

        C:\ASR> setupdr.exe /i
5. Registre Olá provedor:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parâmetros:

* **/ Credenciais**: parâmetro obrigatório para o local de saudação em qual Olá arquivo de chave do registro está localizado.  
* **/ FriendlyName**: parâmetro obrigatório para o nome de saudação do servidor de host de saudação Hyper-V que aparece no portal do Azure Site Recovery hello.
* **/ EncryptionEnabled**: parâmetro opcional usado somente durante a replicação do VMM tooAzure.
* **/proxyAddress**: parâmetro opcional que especifica o endereço de saudação do servidor de proxy de saudação.
* **/proxyPort**: parâmetro opcional que especifica a porta de saudação do servidor de proxy de saudação.
* **/proxyUsername**: parâmetro opcional que especifica o nome de usuário de proxy de saudação (se o proxy de saudação exige autenticação).
* **/proxyPassword**: parâmetro opcional que especifica a senha Olá para autenticar com o servidor de proxy de saudação (se o proxy de saudação exige autenticação).

## <a name="step-3-map-storage-arrays-and-pools"></a>Etapa 3: Mapear as matrizes e pools de armazenamento

Mapear matrizes primários e secundários toospecify qual pool de armazenamento secundário recebe dados de replicação do pool principal hello. Mapear armazenamento antes de configurar a replicação, porque as informações de mapeamento de saudação são usadas quando você habilita a proteção para grupos de replicação.

Antes de começar, verifique se nuvens do VMM aparecem no cofre hello. As nuvens são detectadas quando você sincronizar todas as nuvens durante a instalação do provedor ou quando você sincronizar uma nuvem específica no console do VMM hello.

1. Clique em **Recursos** > **Armazenamento do Servidor** > **Mapear Matrizes de Origem e Destino**.
    ![Registro do servidor](./media/site-recovery-vmm-san/storage-map.png)

2. Selecione matrizes de armazenamento Olá no site primário hello e mapeá-los a matrizes de toostorage no site secundário Olá. Em **Pools de armazenamento**, selecione uma fonte e toomap de pool de armazenamento de destino.

    ![Registros do servidor](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Etapa 4: Definir configurações de replicação

Depois dos servidores VMM serem registrados, defina as configurações de proteção da nuvem.

1. Em Olá **início rápido** , clique em **configurar a proteção para nuvens do VMM**.
2. Em Olá **itens protegidos** , selecione a nuvem Olá **configuração**.
3. Em **Destino**, selecione **VMM**.
4. Em **local de destino**, selecione servidor VMM Olá que gerencia Olá nuvem você deseja toouse para recuperação.
5. Em **nuvem de destino**, selecione Olá destino nuvem você deseja toouse para failover de VM.
   * É recomendável que você selecione uma nuvem de destino que atenda aos requisitos de recuperação para máquinas virtuais de saudação que proteger.
   * Uma nuvem pode pertencer somente par de nuvem único tooa – como primária ou uma nuvem de destino.
6. Recuperação de site verifica se nuvens têm acesso tooSAN armazenamento e que o armazenamento Olá matrizes são mapeadas.
7. Se a verificação for bem-sucedida, em **Tipo de replicação**, selecione **SAN**.

Depois de salvar as configurações de saudação, um trabalho é criado que pode ser monitorado na Olá **trabalhos** guia. As configurações podem ser modificadas no hello **configurar** guia. Se quiser que o local de destino Olá toomodify ou nuvem de destino, deve remover a configuração de nuvem hello e reconfigure a nuvem de saudação.

## <a name="step-5-enable-network-mapping"></a>Etapa 5: Habilitar o mapeamento de rede

1. Em Olá **início rápido** , clique em **mapear redes**.
2. Selecione o servidor do VMM de origem hello e selecione Olá Olá destino VMM server toowhich redes serão mapeadas. Olá lista de redes de origem e suas redes de destino associados é exibida. Um valor vazio é mostrado para redes que não são mapeadas. Clique em Olá informações ícone próximo toohello origem e destino nomes tooview Olá sub-redes de rede para cada rede.
3. Selecione uma rede em **Rede na origem** e clique em **Mapear**. serviço de saudação detecta Olá redes de VM no servidor de destino hello e os exibe.

    ![Arquitetura de SAN](./media/site-recovery-vmm-san/network-map1.png)
4. Selecione uma das redes VM Olá Olá VMM do servidor de destino.

    ![Arquitetura de SAN](./media/site-recovery-vmm-san/network-map2.png)

5. Quando você seleciona uma rede de destino, hello nuvens protegidas que usam a rede de origem Olá são exibidas. As redes de destino disponíveis também são exibidas. É recomendável que você selecione uma rede de destino que está disponível tooall nuvens de saudação que você está usando para replicação.
6. Clique em processo de mapeamento Olá marca de seleção toocomplete hello. Um trabalho inicia e acompanha o andamento. Você pode exibi-lo no hello **trabalhos** guia.

## <a name="step-6-enable-replication-for-replication-groups"></a>Etapa 6: habilitar a replicação para grupos de replicação

Antes de habilitar a proteção para máquinas virtuais, você precisa tooenable replicação para grupos de replicação de armazenamento.

1. Em Olá **propriedades** página da nuvem de Olá principal no portal de recuperação de Site hello, abra Olá **máquinas virtuais** guia e clique em **adicionar grupo de replicação**.
2. Selecione um ou mais VMM grupos de replicação que estão associados com a nuvem hello, verifique matrizes de origem e destino hello e especifique a frequência de replicação hello.

Recuperação de site, o VMM e provedores de SMI-S da saudação provisionar LUNs de armazenamento de site de destino do hello e habilitar a replicação de armazenamento. Se o grupo de replicação Olá já estiver replicado, Site Recovery reutiliza o relacionamento de replicação existente hello e atualizações Olá informações.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Etapa 7: habilitar a proteção para máquinas virtuais


Quando um grupo de armazenamento está replicando, habilite a proteção para máquinas virtuais no console do VMM Olá com uma saudação métodos a seguir:

* **Nova máquina virtual**: quando você cria uma máquina virtual, habilitar a replicação e associar Olá VM com o grupo de replicação hello.
  Com essa opção, o VMM usa o armazenamento de máquina virtual de saudação do posicionamento inteligente toooptimally local em LUNs Olá Olá do grupo de replicação. Site Recovery coordena a criação de saudação de uma VM no site secundário Olá sombra e aloca a capacidade para que as máquinas virtuais de réplica podem ser iniciados após o failover.
* **Máquina virtual existente**: se uma máquina virtual já estiver implantada no VMM, você pode habilitar a replicação e executar um grupo de replicação de tooa de migração de armazenamento. Após a conclusão, o VMM e o Site Recovery detectar Olá nova máquina virtual e gerenciá-lo na recuperação de Site. Uma sombra VM é criada no site secundário hello e capacidade alocada para a réplica Olá VM pode ser iniciada após o failover.

![Habilitar proteção](./media/site-recovery-vmm-san/enable-protect.png)

Depois que as VMs habilitadas para replicação, aparecem no console de recuperação de Site hello. Você pode exibir as propriedades da VM, acompanhar o status e o failover dos grupos de replicação que contêm várias VMs. Na replicação de SAN, todas as VMs associadas a um grupo de replicação devem fazer failover juntas. Isso ocorre porque o failover ocorre na camada de armazenamento Olá primeiro. É importante toogroup a replicação agrupa corretamente e colocar somente máquinas virtuais associadas juntas.

> [!NOTE]
> Depois de habilitar a replicação para uma máquina virtual, não adicione tooLUNs seus VHDs, a menos que eles estão localizados em um grupo de replicação de recuperação de Site. Os VHDs só serão detectados pelo Site Recovery se estiverem localizados em um grupo de replicação do Site Recovery.
>
>

Você pode acompanhar o andamento, incluindo a replicação inicial hello, em Olá **trabalhos** guia. Após a execução do trabalho finalizar proteção de hello, Olá máquina de virtual está pronta para failover.

![Trabalho de proteção da máquina virtual](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Etapa 8: Testar a implantação de saudação

Teste sua toomake implantação-se de que as VMs failover conforme o esperado. toodo isso, crie um plano de recuperação e execute um failover de teste.

1. Em Olá **planos de recuperação** , clique em **criar plano de recuperação**.
2. Especifique um nome para o plano de recuperação de saudação e selecione os servidores VMM de origem e destino. o servidor de origem Olá deve ter VMs habilitadas para failover e recuperação. Selecione **SAN** tooview somente nuvens configuradas para replicação SAN.

    ![Criar plano de recuperação](./media/site-recovery-vmm-san/r-plan.png)

3. Em **Selecionar Máquinas Virtuais**, selecione os grupos de replicação. Todas as VMs associadas Olá grupo serão adicionadas toohello plano de recuperação. Essas VMs são adicionadas a grupo de padrão de plano de recuperação de toohello (grupo 1). Você pode adicionar mais grupos, se necessário. Após a replicação, VMs são numeradas de acordo com o toohello ordem de grupos do plano de recuperação de saudação.

    ![Selecionar máquinas virtuais](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Depois que o plano de recuperação Olá é criado, ele aparece na lista de saudação em Olá **planos de recuperação** guia. Selecione o plano de saudação e escolha **Failover de teste**.
5. Em Olá **confirmar Failover de teste** página, selecione **nenhum**. Com essa opção habilitada, Olá failover de máquinas virtuais de réplica não será conectada tooany rede. Isso testa que Olá VMs failover conforme o esperado, mas ele não testa o ambiente de rede hello. Para saber mais sobre outras opções de rede, consulte [Failover do Site Recovery](site-recovery-failover.md).

    ![Selecionar rede de teste](./media/site-recovery-vmm-san/test-fail1.png)

6. VM de teste de saudação é criado no hello mesmo host como host Olá em qual réplica Olá VM existe. Não será adicionada toohello nuvem na qual Olá VM de réplica está localizada.
2. Após a replicação, a VM de réplica Olá terá um endereço IP diferente que a máquina virtual primária de saudação. Se você estiver emitindo endereços do DHCP, ele será atualizado automaticamente. Se você não estiver usando DHCP e você desejar Olá mesmo endereços, é necessário toorun alguns scripts.
3. Execute este endereço IP do script tooretrieve hello:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Execute este script de exemplo tooupdate DNS. Especifique o endereço IP de saudação recuperado.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Próximas etapas

Depois de executar um toocheck de failover de teste que seu ambiente está funcionando como esperado, consulte [failover de recuperação de Site](site-recovery-failover.md) toolearn sobre os diferentes tipos de failovers.
