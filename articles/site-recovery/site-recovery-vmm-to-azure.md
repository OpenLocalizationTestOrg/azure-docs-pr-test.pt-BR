---
title: aaaReplicate VMs Hyper-V no VMM nuvens tooAzure | Microsoft Docs
description: "Orquestrar a replicação, failover e recuperação de máquinas virtuais do Hyper-V gerenciados no tooAzure de nuvens do System Center VMM"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replicar máquinas virtuais Hyper-V no tooAzure de nuvens do VMM usando o Site Recovery no portal do Azure de saudação
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-azure.md)
> * [Azure clássico](site-recovery-vmm-to-azure-classic.md)
> * [Implantação do Resource Manager do PowerShell](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Implantação clássica do PowerShell](site-recovery-deploy-with-powershell.md)


Este artigo descreve como tooreplicate local máquinas virtuais de Hyper-V gerenciados no System Center VMM nuvens tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Se você quiser toomigrate máquinas tooAzure (sem failback), saiba mais em [neste artigo](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Etapas de implantação.

Siga estas etapas de implantação de saudação artigo toocomplete:


1. [Saiba mais](site-recovery-components.md) sobre arquitetura de saudação para essa implantação. Além disso, [saiba mais sobre](site-recovery-hyper-v-azure-architecture.md) como funciona a replicação do Hyper-V no Site Recovery.
2. Verifique os pré-requisitos e as limitações.
3. Configure contas de rede e armazenamento do Azure.
4. Prepare o servidor do VMM local hello e hosts Hyper-V.
5. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.
6. Especifique as configurações de origem. Registre servidor do VMM Olá no cofre de saudação. Instale Olá provedor Azure Site Recovery no hello VMM server instalação Olá dos serviços de recuperação do Microsoft agent nos hosts Hyper-V.
7. Defina as configurações de destino e de replicação.
8. Habilite a replicação para Olá VMs.
9. Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.



## <a name="prerequisites"></a>Pré-requisitos


**Requisito de suporte** | **Detalhes**
--- | ---
**As tabelas** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidores locais** | [Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) sobre os requisitos para o servidor do VMM local hello e hosts Hyper-V.
**VMs do Hyper-V locais** | Máquinas virtuais que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs do Azure** | servidor do VMM Olá precisa acessar toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).


## <a name="prepare-for-deployment"></a>Preparar para a implantação
tooprepare para implantação, você precisa:

1. [Configurar uma rede do Azure](#set-up-an-azure-network) na qual as VMs do Azure estarão localizadas após o failover.
2. [Configure uma conta de armazenamento do Azure](#set-up-an-azure-storage-account) para os dados replicados.
3. [Preparar o servidor do VMM Olá](#prepare-the-vmm-server) para implantação da recuperação de Site.
4. Prepare-se para o mapeamento de rede. Configure as redes de modo que você possa configurar o mapeamento de rede durante a implantação da Recuperação de Site.

### <a name="set-up-an-azure-network"></a>Configurar uma rede do Azure
Você precisa de um toowhich de rede do Azure VMs do Azure criados após o failover será conectado.

* rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região hello.
* Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar Olá rede do Azure [Gerenciador de recursos de modo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou [modo clássico](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* É recomendável configurar uma rede antes de começar. Se você não fizer isso, você precisa toodo-lo durante a implantação da recuperação de Site.
Redes do Azure usadas pela recuperação de Site não podem ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro Olá mesmo, ou em assinaturas diferentes,.

### <a name="set-up-an-azure-storage-account"></a>Configure uma conta de armazenamento do Azure
* Você precisa de um conta de armazenamento do Azure toohold dados replicados tooAzure padrão/premium. [Armazenamento premium](../storage/common/storage-premium-storage.md) é usada para máquinas virtuais que precisam de um desempenho de e/s consistentemente alto e baixa latência toohost e/s intensivas cargas de trabalho. Se você quiser toouse dados replicados de um toostore de conta premium, você também precisa de um armazenamento padrão toostore replicação logs de conta de captura contínua altera dados tooon locais. Olá conta deve ser no hello Cofre de serviços de recuperação com a mesma região hello.
* Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar uma conta no [Gerenciador de recursos de modo](../storage/common/storage-create-storage-account.md) ou [modo clássico](../storage/common/storage-create-storage-account.md).
* É recomendável que você configure uma conta antes de começar. Se você não fizer isso, você precisa toodo-lo durante a implantação da recuperação de Site.
- Observe que as contas de armazenamento usadas pela recuperação de Site não podem ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro Olá mesmo, ou em assinaturas diferentes,.

### <a name="prepare-hello-vmm-server"></a>Preparar o servidor do VMM Olá
* Verifique se o servidor VMM Olá obedece Olá [pré-requisitos](#prerequisites).
* Durante a implantação da recuperação de Site, você pode especificar que todas as nuvens em um servidor VMM devem estar disponíveis no hello portal do Azure. Se você quiser apenas tooappear de nuvens específicas no portal de saudação, você pode habilitar essa configuração em nuvem Olá no console do administrador do VMM hello.

### <a name="prepare-for-network-mapping"></a>Prepare-se para o mapeamento de rede
É necessário configurar o mapeamento de rede durante a implantação do Site Recovery. Mapeamento de rede mapeia entre redes VM do VMM de origem e destino redes do Azure, Olá tooenable a seguir:

* Máquinas failover em Olá mesma rede podem se conectar tooeach outra, mesmo se não estiver passou por failover em Olá mesmo propósito ou Olá mesmo plano de recuperação.
* Se um gateway de rede é configurado na rede Azure de destino hello, máquinas virtuais do Azure pode se conectar a máquinas virtuais locais tooon.
* tooset o mapeamento de rede, aqui está o que você precisa:

  * Certifique-se de que as VMs no servidor host Hyper-V de origem de saudação são conectado tooa rede VM do VMM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.
  * Uma rede do Azure conforme descrito [acima](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Monitoramento + Gerenciamento** > **Backup e Site Recovery (OMS)**.

    ![Novo cofre](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. Em **nome**, especifique um cofre de saudação tooidentify nome amigável. Se você tiver mais de uma assinatura, selecione uma delas.
4. [Crie um grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md)ou selecione um existente. Especifique uma região do Azure. Máquinas serão replicadas toothis região. regiões toocheck suporte consulte disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Se você quiser tooquickly acesso Olá cofre da saudação painel, clique em **Pin toodashboard** > **criar cofre**.

    ![Novo cofre](./media/site-recovery-vmm-to-azure/new-vault.png)

novo cofre de saudação aparece na Olá **painel** > **todos os recursos**e em Olá principal **os cofres de serviços de recuperação** folha.


## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção Olá

Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.

1. Em **os cofres de serviços de recuperação**, selecione o Cofre de saudação.
2. Em **Introdução**, clique em **Site Recovery** > **Preparar a infraestrutura** > **Meta de proteção**.

    ![Escolher metas](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. Em **objetivo de proteção** selecione **tooAzure**e selecione **Sim, com o Hyper-V**. Selecione **Sim** tooconfirm você estiver usando hosts do VMM toomanage Hyper-V e o site de recuperação de saudação. Em seguida, clique em **OK**.

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Instalar Olá provedor Azure Site Recovery no servidor do VMM Olá e registrar o servidor de saudação no cofre hello. Instale o agente de serviços de recuperação do Azure de saudação nos hosts Hyper-V.

1. Clique em **Preparar a Infraestrutura** > **Origem**.

    ![Configurar origem](./media/site-recovery-vmm-to-azure/set-source1.png)

2. Em **preparar fonte**, clique em **+ VMM** tooadd um servidor do VMM.

    ![Configurar origem](./media/site-recovery-vmm-to-azure/set-source2.png)

3. Em **Adicionar servidor**, verifique se **servidor do System Center VMM** aparece na **tipo de servidor** e servidor do VMM Olá atende Olá [pré-requisitos e URL requisitos de](#prerequisites).
4. Baixe o arquivo de instalação do provedor Azure Site Recovery hello.
5. Baixe a chave de registro de saudação. Você precisará dela quando executar a instalação. chave de saudação é válida por cinco dias depois que ele é gerado.

    ![Configurar origem](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Instalar Olá provedor no servidor do VMM Olá

1. Execute o arquivo de instalação do provedor Olá no servidor do VMM hello.
2. No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.
3. Em **instalação**, aceite ou modifique o local de instalação do provedor de padrão de saudação e clique em **instalar**.

    ![Local de instalação](./media/site-recovery-vmm-to-azure/provider2.png)
4. Quando a instalação for concluída, clique em **registrar** servidor do VMM Olá tooregister no cofre hello.
5. Em Olá **as configurações do cofre** , clique em **procurar** tooselect arquivo de chave do Cofre de saudação. Especifique a assinatura do Azure Site Recovery hello e nome do cofre hello.

    ![Registros do servidor](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. Em **Conexão de Internet**, especifique como Olá provedor em execução no servidor do VMM Olá conectará tooSite recuperação sobre Olá da internet.

   * Se você desejar Olá provedor tooconnect diretamente, selecione **se conectar diretamente tooAzure recuperação de Site sem um proxy**.
   * Se o proxy existente exige autenticação ou deseja toouse um proxy personalizado, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.
   * Se você usar um proxy personalizado, especifique as credenciais, porta e endereço de saudação.
   * Se você estiver usando um proxy, você deve ter já Olá URLs permitidas descritos em [pré-requisitos](#on-premises-prerequisites).
   * Se você usar um proxy personalizado, uma conta de RunAs VMM (DRAProxyAccount) será criada automaticamente Olá especificado, usando as credenciais do proxy. Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito. configurações de conta de RunAs VMM Olá podem ser modificadas no console do VMM hello. Em **configurações**, expanda **segurança** > **contas executar como**e, em seguida, modificar a senha Olá para DRAProxyAccount. O serviço VMM toorestart hello, será necessário para que essa configuração tenha efeito.

     ![internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Aceite ou modifique o local de saudação de um certificado SSL que é gerado automaticamente para a criptografia de dados. Este certificado será usado se você habilitar a criptografia de dados para uma nuvem protegida pelo Azure no portal do Azure Site Recovery hello. Mantenha esse certificado protegido. Quando você executa um failover tooAzure você precisará dele toodecrypt, se a criptografia de dados está habilitada.

    > [!NOTE]
    > É recomendável toouse o recurso de criptografia de saudação fornecido pelo Azure para criptografar dados em repouso, em vez de usar a opção de criptografia de dados Olá fornecida pelo Azure Site Recovery. o recurso de criptografia de saudação fornecido pelo Azure pode ser ativado para um armazenamento > conta e ajuda a melhorar o desempenho conforme Olá criptografia/descriptografia é tratada pelo armazenamento do Azure.
    > [Saiba mais sobre a Criptografia do Serviço de Armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello. Em uma configuração de cluster, especifique o nome de função de cluster saudação do VMM.
9. Habilitar **sincronizar metadados de nuvem**, se você quiser toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello. Essa ação precisa apenas toohappen uma vez em cada servidor. Se você não quiser toosynchronize todas as nuvens, você pode deixar essa configuração está desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello. Clique em **registrar** toocomplete processo de saudação.

    ![Registros do servidor](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. O registro é iniciado. Após a conclusão do registro, o servidor de saudação é exibido na **infra-estrutura de recuperação de Site** > **servidores VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Instalar o agente de serviços de recuperação do Azure Olá nos hosts Hyper-V

1. Depois de configurar Olá provedor, você precisa arquivo de instalação toodownload Olá para agente de serviços de recuperação do Azure hello. Execute a instalação em cada servidor Hyper-V Olá nuvem do VMM.

    ![Sites do Hyper-V](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. Em **Verificação de Pré-requisitos**, clique em **Avançar**. Quaisquer pré-requisitos faltantes serão instalados automaticamente.

    ![Agente de Serviços de Recuperação de Pré-requisitos](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. Em **configurações de instalação**, aceite ou modifique o local de instalação hello e Olá cache local. Você pode configurar o cache de saudação em uma unidade que tenha pelo menos 5 GB de armazenamento disponível, mas é recomendável uma unidade de cache com 600 GB ou mais de espaço livre. Em seguida, clique em **Instalar**.
4. Após a conclusão da instalação, clique em **fechar** toofinish.

    ![Registrar o Agente MARS](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Instalação de linha de comando
Você pode instalar Olá Microsoft Azure Recovery Services Agent na linha de comando usando o comando a seguir de saudação:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurar tooSite de acesso de proxy de internet recuperação a partir de hosts Hyper-V

Agente de serviços de recuperação de saudação em execução em hosts do Hyper-V precisa tooAzure de acesso à internet para replicação de VM. Se você estiver acessando Olá internet através de um proxy, configurá-lo da seguinte maneira:

1. Abra o snap-in MMC do Backup do Microsoft Azure de saudação no host do Hyper-V hello. Por padrão, um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Olá snap-in, clique em **alterar propriedades**.
3. Em Olá **configuração de Proxy** especifique as informações do servidor proxy.

    ![Registrar o Agente MARS](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Verifique que o agente Olá pode alcançar Olá URLs descritos em Olá [pré-requisitos](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá
Especifique Olá toobe de conta de armazenamento do Azure usado para replicação e Olá toowhich de rede do Azure VMs do Azure irão se conectar após o failover.

1. Clique em **preparar infraestrutura** > **destino**, selecione a assinatura hello e Olá onde você deseja toocreate Olá failover de máquinas virtuais do grupo de recursos. Escolha o modelo de implantação de saudação que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá máquinas virtuais com failover.

    ![Armazenamento](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

    ![Armazenamento](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Se você não tiver criado uma conta de armazenamento, e você desejar toocreate um usando o Gerenciador de recursos, clique em **+ conta de armazenamento** toodo que embutido.  Em Olá **criar conta de armazenamento** folha especificar um nome de conta, tipo, assinatura e local. Olá conta deve ser no hello Cofre de serviços de recuperação do mesmo local que hello.

   ![Armazenamento](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Se você quiser toocreate uma conta de armazenamento usando o modelo clássico hello, use Olá portal do Azure. [Saiba mais](../storage/common/storage-create-storage-account.md)
   * Se você estiver usando uma conta de armazenamento premium para os dados replicados, configure uma conta de armazenamento padrão, os logs de replicação toostore capturam alterações contínuas tooon de dados locais.
5. Se você não tiver criado uma rede do Azure, e você desejar toocreate um usando o Gerenciador de recursos, clique em **+ rede** toodo que embutido. Em Olá **criar rede virtual** folha especificar um nome de rede, intervalo de endereços, detalhes de sub-rede, assinatura e local. rede Olá deve estar no hello Cofre de serviços de recuperação do mesmo local que hello.

   ![Rede](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Se você quiser toocreate uma rede usando o modelo clássico hello, use Olá portal do Azure. [Saiba mais](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Configurar o mapeamento de rede

* [Leia](#prepare-for-network-mapping) uma rápida visão geral sobre o que o mapeamento de rede faz.
* Verifique se que máquinas virtuais no servidor do VMM Olá são conectados tooa rede VM e que você criou pelo menos uma rede virtual do Azure. Várias redes VM podem ser mapeado tooa única rede do Azure.

Configure o mapeamento da seguinte maneira:

1. Em **infra-estrutura de recuperação de Site** > **mapeamentos de rede** > **mapeamento de rede**, clique em Olá **+ de mapeamento de rede**  ícone.

    ![Mapeamento de rede](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. Em **Adicionar mapeamento de rede**, selecione servidor VMM de origem Olá, e **Azure** como destino de saudação.
3. Verifique se a assinatura hello e modelo de implantação de saudação após o failover.
4. Em **rede de origem**, selecione rede VM do local de origem de saudação desejado toomap da lista de saudação associada ao servidor do VMM hello.
5. Em **rede de destino**, selecione Olá rede do Azure no qual réplica VMs do Azure serão localizadas quando eles são criados. Em seguida, clique em **OK**.

    ![Mapeamento de rede](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Veja o que acontece quando começa o mapeamento de rede:

* Máquinas virtuais existentes na rede VM de origem de saudação são conectados toohello rede de destino quando iniciar o mapeamento. Nova rede VM de origem para toohello conectado VMs estão conectados toohello mapeadas de rede do Azure quando a replicação ocorre.
* Se você modificar um mapeamento de rede existente, máquinas virtuais de réplica se conectar usando Olá novas configurações.
* Se a rede de destino Olá possui várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica se conecta a sub-rede de destino toothat após o failover.
* Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá VM conecta toohello primeira sub-rede na rede de saudação.

## <a name="configure-replication-settings"></a>Definir configurações de replicação
1. toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.

    ![Rede](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política.
3. Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).

    > [!NOTE]
    >  Uma frequência de segundo 30 não tem suporte durante a replicação de armazenamento toopremium. limitação de saudação é determinada pelo número de saudação de instantâneos por blob (100) com suporte pelo armazenamento premium. [Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. Em **retenção de ponto de recuperação**, especifique, em horas, quanto tempo uma janela de retenção Olá será possível para cada ponto de recuperação. Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela.
5. Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que incluam instantâneos consistentes com aplicativos. Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação. Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado. Observe que, se você habilitar instantâneos consistentes com aplicativos, isso afetará Olá desempenho de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.
6. Em **hora de início da replicação inicial**, indicar quando toostart Olá a replicação inicial. replicação Olá ocorre sobre a largura de banda de internet, portanto, talvez você queira tooschedule-lo fora do horário de ocupado.
7. Em **criptografar dados armazenados no Azure**, especifique se tooencrypt dados rest no armazenamento do Azure. Em seguida, clique em **OK**.

    ![Política de replicação](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Quando você cria uma nova política está associado automaticamente Olá nuvem do VMM. Clique em **OK**. Você pode associar nuvens do VMM adicionais (e Olá VMs neles) com esta política de replicação em **replicação** > nome da política > **associar VMM nuvem**.

    ![Política de replicação](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Planejamento da capacidade

Agora que você tem a infraestrutura básica configurada, pense no planejamento de capacidade e confira se precisa de recursos adicionais.

Recuperação de site fornece um toohelp do Planejador de capacidade alocar recursos Olá para seu ambiente de origem, componentes do Site Recovery, rede e armazenamento. Você pode executar o Planejador de saudação em modo rápido para estimativas com base em um número médio de VMs, discos e armazenamento, ou em modo detalhado em que você inserir números no nível de carga de trabalho de saudação. Antes de começar:

* Reunir informações sobre seu ambiente de replicação, inclusive VMs, discos por VMs e armazenamento por disco.
* Estimar a taxa de alteração (variação) diária Olá que você terá de dados replicados. Você pode usar o hello [Planejador de capacidade para réplica do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp fazer isso.

1. Clique em **baixar**, toodownload Olá ferramenta e, em seguida, executá-lo. [Leia o artigo Olá](site-recovery-capacity-planner.md) que acompanha a ferramenta de saudação.
2. Quando terminar, selecione **Sim** na **você executou Olá Capacity Planner**?

   ![Planejamento da capacidade](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Saiba mais sobre [controle de largura de banda de rede](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Habilitar a replicação

Antes de começar, certifique-se de que sua conta de usuário do Azure tem Olá necessário [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.

Agora habilite a replicação da seguinte maneira:

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**. Depois de habilitar a replicação para Olá primeira vez, clique em **+ replicar** em replicação de tooenable Olá cofre para outras máquinas.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. Em Olá **fonte** folha, selecione Olá servidor do VMM e nuvem Olá no qual Olá Hyper-V hosts estão localizados. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. Em **destino**, selecione a assinatura hello, o modelo de implantação após o failover, e Olá conta de armazenamento que você está usando para os dados replicados.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Selecione a conta de armazenamento de saudação que toouse desejado. Se você quiser toouse uma conta de armazenamento diferentes daquelas que você tem, você pode [criar um](#set-up-an-azure-storage-account). Se você estiver usando uma conta de armazenamento premium para os dados replicados, você precisa tooselect um logs de replicação de toostore conta de armazenamento padrão adicionais que captura alterações contínuas local tooon data.toocreate uma conta de armazenamento usando o modelo do Gerenciador de recursos de saudação Clique em **criar novo**. Se você quiser toocreate uma conta de armazenamento usando o modelo clássico hello, isso [no portal do Azure de saudação](../storage/common/storage-create-storage-account.md). Em seguida, clique em **OK**.
5. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure conectará quando eles são criados após o failover. Selecione **configurar agora para os computadores selecionados**, tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente**, Olá tooselect rede do Azure por máquina. Se você quiser toouse uma rede diferente daquelas que você tem, você pode [criar um](#set-up-an-azure-network). Gerenciador de recursos, clique em modelo de Olá toocreate usando uma rede **criar novo**. Se você quiser toocreate uma rede usando o modelo clássico hello, isso [no portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecione uma sub-rede, se aplicável. Em seguida, clique em **OK**.
6. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. Em **propriedades** > **configurar propriedades**, selecione o sistema operacional de saudação para VMs Olá selecionado e Olá disco do sistema operacional.

    - Verifique se esse nome de VM do Azure hello (nome de destino) está em conformidade com [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Por padrão, todos os discos de saudação da saudação VM são selecionados para replicação, mas você pode desmarcar discos tooexclude-los.

        - Talvez você queira largura de banda de replicação tooreduce tooexclude discos. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que tem atualizados sempre que um computador ou aplicativos reinicia (como pagefile.sys ou tempdb do Microsoft SQL Server). Você pode excluir o disco de saudação da replicação por disco de saudação desmarque.
        - Apenas discos básicos podem ser excluídos. Você não pode excluir discos do sistema operacional.
        - É recomendável que você não exclua discos dinâmicos. O Site Recovery não pode identificar se um disco rígido virtual dentro de uma VM convidada é básico ou dinâmico. Se todos os discos de volume dinâmico dependentes não são excluídos, disco dinâmico protegido de saudação será mostrado como um disco com falha quando hello VM failover, e os dados no disco Olá não poderão ser acessados.
        - Depois que a replicação estiver habilitada, você não poderá adicionar ou remover discos para replicação. Se você quiser tooadd ou excluir um disco, é necessário toodisable proteção para Olá VM e reabilitá-la.
        - Discos que você criar manualmente no Azure não sofrerão failback. Por exemplo, se você falha em três discos e cria duas diretamente na VM do Azure, somente Olá três discos que sofreram failover serão falhou da tooHyper-V do Azure. Você não pode incluir discos criados manualmente no failback ou na replicação inversa do Hyper-V tooAzure.
        - Se você excluir um disco que é necessário para um aplicativo toooperate, após o failover tooAzure é necessário toocreate-lo manualmente no Azure, portanto esse Olá replicadas aplicativo pode executar. Como alternativa, você pode integrar a automação do Azure em um plano de recuperação, o disco de saudação toocreate durante o failover da máquina de saudação.

    Clique em **Okey** toosave alterações. Você pode definir propriedades adicionais posteriormente.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. Em **as configurações de replicação** > **definir configurações de replicação**, selecione Olá política de replicação você deseja tooapply para Olá protegido VMs. Em seguida, clique em **OK**. Você pode modificar a política de replicação de saudação em **políticas de replicação** > nome da política > **editar configurações de**. As alterações aplicadas são usadas para computadores que já estejam replicando e para novas máquinas.

   ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/enable-replication7.png)

Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** trabalho é executado, a máquina de saudação está pronta para failover.

### <a name="view-and-manage-vm-properties"></a>Exibir e gerenciar as propriedades da VM

É recomendável que você verifique propriedades Olá Olá computador de origem. Lembre-se deve estar de acordo com esse nome de VM do Azure Olá [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Em **itens protegidos**, clique em **itens replicados**, e selecione Olá máquina toosee seus detalhes.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. Em **propriedades**, você pode exibir a replicação e failover informações para Olá VM.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. Em **de computação e rede** > **propriedades de computação**, você pode especificar o tamanho de destino e o nome de VM do Azure hello. Modificar Olá nome toocomply com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se for necessário. Você também pode exibir e modificar informações sobre a rede de destino hello, sub-rede e endereço IP de saudação que é atribuído toohello VM do Azure.
Observe que:

   * Você pode definir o endereço IP de destino hello. Se você não fornecer um endereço, Olá failover máquina usará o DHCP. Se você definir um endereço que não está disponível em failover, Olá failover falhará. saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.
   * número de saudação de adaptadores de rede é determinado pelo tamanho de saudação especificado para a máquina de virtual de destino Olá, da seguinte maneira:

     * Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
     * Se Olá número de adaptadores de saudação da máquina virtual de origem excede número Olá permitido para o tamanho de destino Olá, tamanho máximo da saudação destino é usado.
     * Por exemplo, se um computador de origem tem dois adaptadores de rede e tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um, o computador de destino Olá terá apenas um adaptador.     
     * Se Olá VM tiver vários adaptadores de rede, eles todos se conectarão toohello mesma rede.

     ![Habilitar a replicação](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. Em **discos** você pode ver o sistema de operacional hello e discos de dados no Olá VM que será replicado.

#### <a name="managed-disks"></a>Discos gerenciados

Em **de computação e rede** > **propriedades de computação**, você pode configurar "Usar gerenciada discos" muito "Sim" para Olá VM se você quiser tooattach discos gerenciado tooyour máquina em tooAzure de migração. Discos gerenciados simplifica o gerenciamento de disco para VMs de IaaS do Azure por meio do gerenciamento de contas de armazenamento Olá associadas Olá discos VM. [Saiba mais sobre managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Discos gerenciados são toohello criado e anexado máquina de virtual somente em um tooAzure de failover. Ao habilitar a proteção, dados de máquinas locais continuarão tooreplicate toostorage contas.
   Discos gerenciados podem ser criados somente para máquinas virtuais implantadas usando o modelo de implantação do Gerenciador de recursos de hello.  

  > [!NOTE]
  > Failback do ambiente do Hyper-V local tooon do Azure atualmente não há suporte para computadores com discos gerenciados. Defina "Usar gerenciada discos" muito "Sim" somente se você pretende toomigrate esta máquina do Azure.

   - Quando você define "Usar gerenciada discos" muito "Sim", apenas conjuntos de disponibilidade no grupo de recursos de saudação com conjunto "Usar gerenciada discos" muito "Sim" seria disponíveis para seleção. Isso ocorre porque as máquinas virtuais com discos gerenciados só pode ser parte dos conjuntos de disponibilidade com o conjunto de propriedades "Use gerenciado discos" muito "Sim". Certifique-se de que você crie conjuntos de disponibilidade com conjunto de propriedades de "Discos Use gerenciado", com base em seus discos toouse intenção gerenciado no failover.  Da mesma forma, quando você define "Usar gerenciada discos" muito "não", apenas conjuntos de disponibilidade no grupo de recursos de saudação com a propriedade "Usar gerenciada discos" definido muito "não" estariam disponíveis para seleção. [Saiba mais sobre managed disks e conjuntos de disponibilidade](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se a conta de armazenamento Olá usada para a replicação foi criptografada com criptografia do serviço de armazenamento em qualquer ponto no tempo, haverá falha na criação de discos gerenciados durante o failover. Você pode definir "Usar gerenciada discos" muito "Nenhum" e tente realizar o failover ou desabilite a proteção para a máquina virtual de saudação e protegê-lo tooa conta de armazenamento que não tem criptografia do serviço de armazenamento habilitada em qualquer ponto no tempo.
  > [Saiba mais sobre Criptografia do serviço de armazenamento e managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Implantação de saudação do teste

implantação de saudação tootest você pode executar um failover de teste para uma única máquina virtual ou um plano de recuperação que contém uma ou mais máquinas virtuais.

### <a name="before-you-start"></a>Antes de começar

 - Se você quiser tooconnect tooAzure VMs usando o RDP após o failover, saiba mais sobre [Preparando tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessário toocopy do Active Directory e DNS em seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Execute um teste de failover

1. toofail em uma única VM, em **itens replicados**, clique em Olá VM > **+ Failover de teste**.
2. Planejar toofail sobre a recuperação, em **planos de recuperação**, plano de saudação do botão direito do mouse > **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).
3. Em **Failover de teste**, selecione Olá toowhich de rede do Azure VMs do Azure se conectar após o failover.
4. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando no hello VM tooopen suas propriedades, ou em Olá **Failover de teste** trabalho em **trabalhos de recuperação de Site**.
5. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure > **máquinas virtuais**. Você deve garantir que Olá VM é o tamanho apropriado hello, que se conectou a rede apropriada toohello e está em execução.
6. Se você preparou para conexões após o failover, deve ser capaz de tooconnect toohello VM do Azure.
7. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas** registrar e salvar todas as observações associadas Olá failover de teste. Isso excluirá as máquinas virtuais Olá que foram criadas durante o failover de teste.

Para obter mais detalhes, leia Olá [tooAzure de failover de teste](site-recovery-test-failover-to-azure.md) artigo.

## <a name="monitor-hello-deployment"></a>Implantação de saudação do monitor

Aqui está como você pode monitorar as definições de configuração, status e integridade para Olá implantação da recuperação de Site:

1. Clique em Olá Olá de tooaccess de nome de cofre **Essentials** painel. Neste painel, você pode ver os trabalhos da Recuperação de Site, o status da replicação, os planos de recuperação, a integridade do servidor e os eventos.  Você pode personalizar **Essentials** tooshow Olá blocos e layouts de tooyou mais úteis, incluindo status de saudação de outros cofres de Backup e recuperação de Site.

    ![Conceitos básicos](./media/site-recovery-vmm-to-azure/essentials.png)
2. Em **integridade**, você pode monitorar problemas em servidores locais (servidores do VMM ou configuração) e Olá eventos gerados pela recuperação de Site no hello últimas 24 horas.
3. Em Olá **itens replicados**, **planos de recuperação**, e **trabalhos de recuperação de Site** blocos, você pode gerenciar e monitorar a replicação. É possível analisar detalhadamente os trabalhos em **Trabalhos** > **Trabalhos do Site Recovery**.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Instalação de linha de comando para Olá provedor Azure Site Recovery

Olá provedor Azure Site Recovery pode ser instalado do hello de linha de comando. Esse método pode ser usado tooinstall Olá provedor no Server Core para Windows Server 2012 R2.

1. Baixe Olá provedor de arquivo e registro tooa chave pasta de instalação. Por exemplo, C:\ASR.
2. Em um prompt de comando com privilégios elevados, execute o instalador do provedor esses comandos tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Execute este comando tooinstall componentes hello:

            C:\ASR> setupdr.exe /i
4. Em seguida, execute esses comandos, o servidor de saudação tooregister no cofre hello:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Em que:

* **/ Credenciais**: parâmetro obrigatório que especifica onde o arquivo de chave de registro hello está localizado.  
* **/ FriendlyName**: parâmetro obrigatório para o nome de saudação do servidor de host de saudação Hyper-V que aparece no portal do Azure Site Recovery hello.
* * **/ EncryptionEnabled**: tooAzure de nuvens de parâmetro opcional quando você estiver replicando máquinas virtuais do Hyper-V no VMM. Especifique se deseja tooencrypt máquinas virtuais do Azure (a criptografia em repouso). Certifique-se de que Olá o nome do arquivo hello tem um **. pfx** extensão. A criptografia está desativado por padrão.

    > [!NOTE]
    > É recomendável toouse o recurso de criptografia de saudação fornecido pelo Azure para criptografar dados em repouso, em vez de usar a opção de criptografia de saudação (opção EncryptionEnabled) fornecida pelo Azure Site Recovery. o recurso de criptografia de saudação fornecido pelo Azure pode ser ativado para uma conta de armazenamento e ajuda a obter um melhor desempenho, como criptografia/descriptografia Olá é feita pelo Azure  
    > Azure.
    > [Saiba mais sobre a Criptografia do Serviço de Armazenamento no Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/proxyAddress**: parâmetro opcional que especifica o endereço de saudação do servidor de proxy de saudação.
* **/proxyPort**: parâmetro opcional que especifica a porta de saudação do servidor de proxy de saudação.
* **/proxyUsername**: parâmetro opcional que especifica o nome de usuário de proxy de saudação (se o proxy exige autenticação).
* **/proxyPassword**: parâmetro opcional que especifica Olá senha tooauthenticate com o servidor proxy (se o proxy de saudação exige autenticação).


### <a name="network-bandwidth-considerations"></a>Considerações sobre largura de banda de rede
Você pode usar o hello capacidade Planejador ferramenta toocalculate Olá largura de banda que é necessário para a replicação (replicação inicial e, em seguida, delta). quantidade de saudação toocontrol de uso de largura de banda para replicação, você tem algumas opções:

* **Limitação da largura de banda**: tráfego Hyper-V que replica o site secundário tooa passa por um host Hyper-V específico. Você pode reduzir a largura de banda no servidor de host de saudação.
* **Ajustar a largura de banda**: você pode influenciar a largura de banda de saudação usada para replicação usando duas chaves do registro.

#### <a name="throttle-bandwidth"></a>Restringir a largura de banda
1. Abra o snap-in MMC do Backup do Microsoft Azure de saudação no servidor de host do Hyper-V hello. Por padrão, um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Olá snap-in, clique em **alterar propriedades**.
3. Em Olá **limitação** guia, selecione **habilitar limitação para operações de backup do uso de largura de banda de internet**e definir limites de saudação do trabalho e folga horas. Intervalos válidos são de 512 Mbps de too102 Kbps por segundo.

    ![Restringir a largura de banda](./media/site-recovery-vmm-to-azure/throttle2.png)

Você também pode usar o hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Veja um exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que nenhuma limitação é necessária.

#### <a name="influence-network-bandwidth"></a>Influência da largura de banda de rede
Olá **UploadThreadsPerVM** controles de valor do registro Olá número de threads que são usados para a transferência de dados (replicação inicial ou delta) de um disco. Um valor mais alto aumenta a largura de banda de rede Olá usada para replicação. Olá **DownloadThreadsPerVM** valor de registro Especifica o número de saudação de threads usados para transferência de dados durante o failback.

1. No registro de hello, navegue muito**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * Modificar o valor de saudação **UploadThreadsPerVM** (ou criar a chave de saudação se ele não existir) toocontrol threads usados para replicação de disco.
   * Modificar o valor de saudação **DownloadThreadsPerVM** (ou criar a chave de saudação se ele não existir) threads toocontrol usados para o tráfego de failback do Azure.
2. valor padrão de saudação é 4. Em uma rede de "sobreprovisionada", essas chaves do registro devem ser diferente dos valores padrão de saudação. Olá máximo é 32. Monitorar o tráfego toooptimize Olá valor.

## <a name="next-steps"></a>Próximas etapas

Depois que a replicação inicial for concluída e você testou implantação hello, você pode chamar failovers conforme a necessidade de saudação. [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
