---
title: aaaReplicate VMs Hyper-V tooAzure | Microsoft Docs
description: "Descreve como tooorchestrate replicação, failover e recuperação de local Hyper-V VMs tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Replicar tooAzure de máquinas virtuais (sem VMM) do Hyper-V usando o Azure Site Recovery com hello portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure clássico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Este artigo descreve como tooreplicate local tooAzure de máquinas virtuais do Hyper-V, usando [do Azure Site Recovery](site-recovery-overview.md) em Olá portal do Azure. Nessa implantação, VMs de Hyper-V não são gerenciadas pelo System Center Virtual Machine Manager (VMM).

Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Se você quiser toomigrate máquinas tooAzure (sem failback), saiba mais em [neste artigo](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Etapas de implantação.

Siga estas etapas de implantação de saudação artigo toocomplete:

1. [Saiba mais](site-recovery-components.md#hyper-v-to-azure) sobre arquitetura de saudação para essa implantação. Além disso, [saiba mais sobre](site-recovery-hyper-v-azure-architecture.md) como funciona a replicação do Hyper-V no Site Recovery.
2. Verifique os pré-requisitos e as limitações.
3. Configure contas de rede e armazenamento do Azure.
4. Prepare os hosts do Hyper-V.
5. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.
6. Especifique as configurações de origem. Criar um site do Hyper-V que contém hosts do Hyper-V Olá e registre o site Olá no cofre de saudação. Instale Olá provedor Azure Site Recovery e o agente de serviços de recuperação do Microsoft hello, nos hosts do Hyper-V de saudação.
7. Defina as configurações de destino e de replicação.
8. Habilite a replicação para Olá VMs.
9. Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.



## <a name="prerequisites"></a>Pré-requisitos


**Requisito** | **Detalhes** |
--- | --- |
**As tabelas** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidores locais** | [Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) sobre os requisitos para hosts de Hyper-V local hello.
**VMs do Hyper-V locais** | Máquinas virtuais que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs do Azure** | Hosts Hyper-V precisará de acesso toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).



## <a name="prepare-for-deployment"></a>Preparar para a implantação

tooprepare para implantação, que você precisa:

1. [Configure uma rede do Azure](#set-up-an-azure-network) na qual as VMs do Azure estarão localizadas quando criadas após o failover.
2. [Configure uma conta de armazenamento do Azure](#set-up-an-azure-storage-account) para os dados replicados.
3. [Preparar os hosts do Hyper-V de saudação](#prepare-the-hyper-v-hosts) tooensure acessarem Olá necessário URLs.

### <a name="set-up-an-azure-network"></a>Configurar uma rede do Azure

Configure uma rede do Azure. Isso será necessário para que VMs do Azure Olá criados após o failover estão conectados tooa rede.

* rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região hello.
* Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar Olá rede do Azure [Gerenciador de recursos de modo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), ou [modo clássico](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* É recomendável configurar uma rede antes de começar. Se você não fizer isso, você precisa toodo-lo durante a implantação da recuperação de Site.
- Contas de armazenamento usadas pela recuperação de Site não podem ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro Olá mesmo, ou em assinaturas diferentes,.


### <a name="set-up-an-azure-storage-account"></a>Configure uma conta de armazenamento do Azure

- Você precisa de um conta de armazenamento do Azure toohold dados replicados tooAzure padrão/premium. [Armazenamento premium](../storage/storage-premium-storage.md) é normalmente usado para máquinas virtuais que precisam de um desempenho de e/s consistentemente alto e baixa latência toohost e/s intensivas cargas de trabalho.
- Se você quiser toouse dados replicados de um toostore de conta premium, você também precisa de um armazenamento padrão toostore replicação logs de conta de captura contínua altera dados tooon locais.
- Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar uma conta no [Gerenciador de recursos de modo](../storage/storage-create-storage-account.md), ou [modo clássico](../storage/storage-create-storage-account-classic-portal.md).
- É recomendável que você configure uma conta de armazenamento antes de começar. Se você não é necessário toodo-lo durante a implantação da recuperação de Site. Olá devem estar no hello Cofre de serviços de recuperação com a mesma região hello.
- Não é possível mover contas de armazenamento usada pela recuperação de Site em grupos de recursos dentro de saudação mesma assinatura, ou em assinaturas diferentes.


### <a name="prepare-hello-hyper-v-hosts"></a>Preparar os hosts do Hyper-V Olá

* Verifique se os hosts Hyper-V de saudação atendem Olá [pré-requisitos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Certifique-se de que os hosts de saudação podem acessar URLs Olá necessário.


## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Monitoramento + Gerenciamento** > **Backup e Site Recovery (OMS)**.  

    ![Novo cofre](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. Em **nome**, especifique um cofre de saudação tooidentify nome amigável. Se você tiver mais de uma assinatura, selecione uma delas.

4. [Crie um novo grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md) ou selecione um existente e especifique uma região do Azure. Máquinas serão replicadas toothis região. regiões toocheck com suporte, consulte a disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Se você quiser tooquickly acesso Olá cofre da saudação painel, clique em **Pin toodashboard**e, em seguida, clique em **criar**.

    ![Novo cofre](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

novo cofre de saudação aparece no hello **painel** > **todos os recursos** lista e, em Olá principal **os cofres de serviços de recuperação** folha.



## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção Olá

Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.

1. Em hello **os cofres de serviços de recuperação**, selecione o Cofre de saudação.
2. Em **Introdução**, clique em **Site Recovery** > **Preparar a infraestrutura** > **Meta de proteção**.

    ![Escolher metas](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. Em **objetivo de proteção**, selecione **tooAzure**e selecione **Sim, com o Hyper-V**. Selecione **não** tooconfirm não estiver usando o VMM. Em seguida, clique em **OK**.

    ![Escolher metas](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar site Olá Hyper-V, instale hello provedor Azure Site Recovery e o agente de serviços de recuperação do Azure Olá nos hosts Hyper-V e registrar site Olá no cofre de saudação.

1. Em **Preparar a infraestrutura**, clique em **Origem**. Clique em um novo site de Hyper-V como um contêiner para seus hosts Hyper-V ou clusters de tooadd **+ Site Hyper-V**.

    ![Configurar origem](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. Em **site Hyper-V criar**, especifique um nome para o site de saudação. Em seguida, clique em **OK**. Agora, selecione o site Olá você criou e clique em **+ servidor Hyper-V** tooadd um site de toohello do servidor.

    ![Configurar origem](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. Em **Adicionar Servidor** > **Tipo de servidor**, verifique se **Servidor Hyper-V** é exibido.

    - Verifique se o servidor Olá Hyper-V você deseja tooadd está em conformidade com hello [pré-requisitos](#on-premises-prerequisites), e é capaz de tooaccess Olá URLs especificadas.
    - Baixe o arquivo de instalação do provedor Azure Site Recovery hello. Executar este Olá tooinstall do arquivo provedor e Olá agente de serviços de recuperação em cada host Hyper-V.

    ![Configurar origem](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Instalar hello provedor e agente

1. Execute o arquivo de instalação do provedor de saudação em cada host que você adicionou site toohello Hyper-V. Se você estiver instalando em um cluster do Hyper-V, execute a instalação em cada nó de cluster. Instalar e registrar cada nó de cluster do Hyper-V garante que as VMs estarão protegidas, mesmo se migrarem entre nós.
2. No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.
3. Em **instalação**, aceite ou modifique o local de instalação do provedor de padrão de saudação e clique em **instalar**.
4. Em **as configurações do cofre**, clique em **procurar** tooselect Olá cofre arquivo de chave que você baixou. Especifique a assinatura do Azure Site Recovery Olá, nome do cofre Olá, e Olá Hyper-V site toowhich Olá Hyper-V servidor pertence.

    ![Registros do servidor](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. Em **as configurações de Proxy**, especifique como Olá tooAzure recuperação de Site se conecta de provedor em execução em hosts Hyper-V em Olá da internet.

    * Se você quiser Olá provedor tooconnect diretamente selecione **se conectar diretamente tooAzure recuperação de Site sem um proxy**.
    * Se o proxy existente exige autenticação ou deseja toouse um proxy personalizado para conexão de provedor hello, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.
    * Se você usar um proxy:
        - Especificar credenciais, porta e endereço Olá
        - Criar URLs de saudação se descrito em Olá [pré-requisitos](#prerequisites) são permitidas por meio do proxy de saudação.

    ![internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Após a conclusão da instalação, clique em **registrar** tooregister servidor de saudação no cofre hello.

    ![Local de instalação](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Após a conclusão do registro, os metadados do servidor de saudação Hyper-V são recuperados pelo Azure Site Recovery e saudação do servidor é exibida no **infra-estrutura de recuperação de Site** > **Hosts Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Especifique a conta de armazenamento do Azure Olá para replicação e Olá toowhich de rede do Azure VMs do Azure irão se conectar após o failover.

1. Clique em **Preparar a Infraestrutura** > **Destino**.
2. Selecione a assinatura de saudação e grupo de recursos de saudação no qual você deseja toocreate Olá VMs do Azure após o failover. Escolha deployment Olá modelo que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá VMs.

3. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

    - Se você não tiver uma conta de armazenamento, clique em **+ armazenamento** toocreate embutido uma conta baseada no Gerenciador de recursos. Leia sobre [requisitos de armazenamento](site-recovery-prereq.md#azure-requirements).
    - Se você não tiver uma rede do Azure, clique em **+ rede** toocreate embutido um Gerenciador de recursos de rede.

    ![Armazenamento](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Definir configurações de replicação

1. toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.

    ![Rede](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política.
3. Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).

    > [!NOTE]
    > Uma frequência de segundo 30 não tem suporte durante a replicação de armazenamento toopremium. limitação de saudação é determinada pelo número de saudação de instantâneos por blob (100) com suporte pelo armazenamento premium. [Saiba mais](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. Em **retenção de ponto de recuperação**, especifique em horas quanto tempo é uma janela de retenção Olá para cada ponto de recuperação. Máquinas virtuais podem ser recuperados tooany ponto dentro de uma janela.
5. Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que contêm instantâneos consistentes com o aplicativo.

    - Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação.
    - Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado.
    - Se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de saudação de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.

6. Em **hora de início da replicação inicial**, especifique quando toostart Olá a replicação inicial. replicação Olá ocorre sobre a largura de banda de internet, portanto, talvez você queira tooschedule-lo fora do horário de ocupado. Em seguida, clique em **OK**.

    ![Política de replicação](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Quando você cria uma nova política, ela está associada automaticamente com o site do Hyper-V hello. Você pode associar um site Hyper-V (e hello VMs nele) com várias políticas de replicação no **replicação** > nome da política > **associar o Site de Hyper-V**.

## <a name="capacity-planning"></a>Planejamento da capacidade

Agora que você tem a infraestrutura básica configurada, pode pensar sobre o planejamento de capacidade e descobrir se precisa de recursos adicionais.

Recuperação de site fornece um toohelp do Planejador de capacidade alocar recursos Olá para computação, rede e armazenamento. Você pode executar Planejador Olá em modo rápido para estimativas com base em um número médio de VMs, discos e armazenamento, ou em modo detalhado com números personalizados no nível de carga de trabalho de saudação. Antes de começar, é necessário:

* Reunir informações sobre seu ambiente de replicação, inclusive VMs, discos por VMs e armazenamento por disco.
* Estimar a taxa de alteração (variação) diária Olá para os dados replicados. Você pode usar o hello [Planejador de capacidade para réplica do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp fazer isso.

1. Clique em **baixar** toodownload Olá ferramenta e, em seguida, executá-lo. [Leia o artigo Olá](site-recovery-capacity-planner.md) que acompanha a ferramenta de saudação.
2. Quando terminar, selecione **Sim** na **você executou Olá Capacity Planner**?

   ![Planejamento da capacidade](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

Saiba mais sobre [controle de largura de banda de rede](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Habilitar a replicação

Antes de começar, certifique-se de que sua conta de usuário do Azure tem Olá necessário [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.

Habilite a replicação para VMs conforme demonstrado a seguir:          

1. Clique em **Replicar aplicativo** > **Origem**. Depois de configurar a replicação para Olá primeira vez, você pode clicar em **+ replicar** tooenable replicação para máquinas adicionais.

    ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. Em **fonte**, selecione site Olá Hyper-V. Em seguida, clique em **OK**.
3. Em **destino**, selecione a assinatura do cofre hello e Olá failover modelo toouse no Azure (clássico ou o recurso de gerenciamento) após o failover.
4. Selecione a conta de armazenamento de saudação que toouse desejado. Se você não tiver uma conta que você deseja toouse, você pode [criar um](#set-up-an-azure-storage-account). Em seguida, clique em **OK**.
5. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure se conectará quando eles são criados o failover.

    - Selecione tooapply Olá configurações tooall máquinas de rede habilitar para replicação, **configurar agora para os computadores selecionados**.
    - Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina.
    - Se você não tiver uma rede que você deseja toouse, você pode [criar um](#set-up-an-azure-network). Selecione uma sub-rede, se aplicável. Em seguida, clique em **OK**.

   ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. Em **propriedades** > **configurar propriedades**, selecione o sistema operacional de saudação para VMs Olá selecionado e Olá disco do sistema operacional.
8. Verifique se esse nome de VM do Azure hello (nome de destino) está em conformidade com [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Por padrão, todos os discos de saudação da saudação VM são selecionados para replicação, mas você pode desmarcar discos tooexclude-los.
    - Talvez você queira largura de banda de replicação tooreduce tooexclude discos. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que tem atualizados sempre que um computador ou aplicativos reinicia (como pagefile.sys ou tempdb do Microsoft SQL Server). Você pode excluir o disco de saudação da replicação por disco de saudação desmarque.
    - Apenas discos básicos podem ser excluídos. Você não pode excluir discos do sistema operacional.
    - É recomendável que você não exclua discos dinâmicos. O Site Recovery não pode identificar se um disco rígido virtual dentro de uma VM convidada é básico ou dinâmico. Se todos os discos de volume dinâmico dependentes não são excluídos, disco dinâmico protegido de saudação será mostrado como um disco com falha quando hello VM failover, e os dados no disco Olá não poderão ser acessados.
        - Depois que a replicação estiver habilitada, você não poderá adicionar ou remover discos para replicação. Se você quiser tooadd ou excluir um disco, é necessário toodisable proteção para Olá VM e reabilitá-la.
        - Discos que você criar manualmente no Azure não sofrerão failback. Por exemplo, se você falha em três discos e cria duas diretamente na VM do Azure, somente Olá três discos que sofreram failover serão falhou da tooHyper-V do Azure. Você não pode incluir discos criados manualmente no failback ou na replicação inversa do Hyper-V tooAzure.
        - Se você excluir um disco que é necessário para um aplicativo toooperate, após o failover tooAzure é necessário toocreate-lo manualmente no Azure, portanto esse Olá replicadas aplicativo pode executar. Como alternativa, você pode integrar a automação do Azure em um plano de recuperação, o disco de saudação toocreate durante o failover da máquina de saudação.

10. Clique em **Okey** toosave alterações. Você pode definir propriedades adicionais posteriormente.

    ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. Em **as configurações de replicação** > **definir configurações de replicação**, selecione Olá política de replicação você deseja tooapply para Olá protegido VMs. Em seguida, clique em **OK**. Você pode modificar a política de replicação de saudação em **políticas de replicação** > nome da política > **editar configurações de**. As alterações aplicadas serão usadas para computadores que já estejam replicando e para novas máquinas.


   ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.

### <a name="view-and-manage-vm-properties"></a>Exibir e gerenciar as propriedades da VM

É recomendável que você verifique propriedades Olá Olá computador de origem.

1. Em **itens protegidos**, clique em **itens replicados**e selecione Olá máquina.

    ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. Em **propriedades**, você pode exibir a replicação e failover informações para Olá VM.

    ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. Em **de computação e rede** > **propriedades de computação**, você pode especificar o tamanho de destino e o nome de VM do Azure hello. Se for necessário, modifique Olá nome toocomply com os requisitos do Azure. Você também pode exibir e modificar informações sobre a rede de destino hello, sub-rede e endereço IP que será atribuído toohello VM do Azure. Observe o seguinte hello:

   * Você pode definir o endereço IP de destino hello. Se você não fornecer um endereço, Olá failover máquina usará o DHCP. Se você definir um endereço que não está disponível em failover, Olá failover falhará. saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.
   * número de saudação de adaptadores de rede é determinado pelo tamanho de saudação especificado para a máquina de virtual de destino Olá, da seguinte maneira:

     * Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
     * Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.
     * Por exemplo, se um computador de origem tem dois adaptadores de rede e tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.     
     * Se Olá VM tem vários adaptadores de rede conectará todos toohello mesma rede.
     * Se a máquina virtual de saudação tem vários adaptadores de rede, Olá primeiro mostrada na lista de saudação se torna Olá *padrão* adaptador de rede na máquina virtual do Azure de saudação.

     ![Habilitar a replicação](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. Em **discos**, você pode ver o sistema operacional de saudação e discos de dados Olá VM que será replicado.

#### <a name="managed-disks"></a>Discos gerenciados

Em **de computação e rede** > **propriedades de computação**, você pode configurar "Usar gerenciada discos" muito "Sim" para Olá VM se você quiser tooattach discos gerenciado tooyour máquina em tooAzure de migração. Discos gerenciados simplifica o gerenciamento de disco para VMs de IaaS do Azure por meio do gerenciamento de contas de armazenamento Olá associadas Olá discos VM. [Saiba mais sobre managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Discos gerenciados são toohello criado e anexado máquina de virtual somente em um tooAzure de failover. Ao habilitar a proteção, dados de máquinas locais continuarão tooreplicate toostorage contas.
   Discos gerenciados podem ser criados somente para máquinas virtuais implantadas usando o modelo de implantação do Gerenciador de recursos de hello.

  > [!NOTE]
  > Failback do ambiente do Hyper-V local tooon do Azure atualmente não há suporte para computadores com discos gerenciados. Defina "Usar gerenciada discos" muito "Sim" somente se você pretende toomigrate tooAzure neste computador.

   - Quando você define "Usar gerenciada discos" muito "Sim", apenas conjuntos de disponibilidade no grupo de recursos de saudação com conjunto "Usar gerenciada discos" muito "Sim" seria disponíveis para seleção. Isso ocorre porque as máquinas virtuais com discos gerenciados só pode ser parte dos conjuntos de disponibilidade com o conjunto de propriedades "Use gerenciado discos" muito "Sim". Certifique-se de que você crie conjuntos de disponibilidade com conjunto de propriedades de "Discos Use gerenciado", com base em seus discos toouse intenção gerenciado no failover. Da mesma forma, quando você define "Usar gerenciada discos" muito "não", apenas conjuntos de disponibilidade no grupo de recursos de saudação com a propriedade "Usar gerenciada discos" definido muito "não" estariam disponíveis para seleção. [Saiba mais sobre managed disks e conjuntos de disponibilidade](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se a conta de armazenamento Olá usada para a replicação foi criptografada com criptografia do serviço de armazenamento em qualquer ponto no tempo, haverá falha na criação de discos gerenciados durante o failover. Você pode definir "Usar gerenciada discos" muito "Nenhum" e tente realizar o failover ou desabilite a proteção para a máquina virtual de saudação e protegê-lo tooa conta de armazenamento que não tem criptografia do serviço de armazenamento habilitada em qualquer ponto no tempo.
  > [Saiba mais sobre Criptografia do serviço de armazenamento e managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Implantação de saudação do teste

implantação de saudação tootest você pode executar um failover de teste para uma única máquina virtual ou um plano de recuperação que contém uma ou mais máquinas virtuais.

### <a name="before-you-start"></a>Antes de começar

 - Se você quiser tooconnect tooAzure VMs usando o RDP após o failover, saiba mais sobre [Preparando tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessário toocopy do Active Directory e DNS em seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Execute um teste de failover

1. toofail em um único computador, em **itens replicados**, clique em Olá VM > **+ Failover de teste** ícone.
2. Planejar toofail sobre a recuperação, em **planos de recuperação**, plano de saudação do botão direito do mouse > **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).
3. Em **Failover de teste**, selecione toowhich de rede do Azure Olá VMs do Azure será conectada após o failover.
4. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando no hello VM tooopen suas propriedades, ou em Olá **Failover de teste** trabalho em nome do cofre > **trabalhos** > **trabalhos de recuperação de Site**.
5. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure > **máquinas virtuais**. Você deve garantir que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.
6. Se você preparou para conexões após o failover, deve ser capaz de tooconnect toohello VM do Azure.
7. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas** registrar e salvar todas as observações associadas Olá failover de teste. Isso excluirá as máquinas virtuais Olá que foram criadas durante o failover de teste.

Para obter mais detalhes, leia Olá [tooAzure de failover de teste](site-recovery-test-failover-to-azure.md) artigo.



## <a name="monitor-hello-deployment"></a>Implantação de saudação do monitor

Definições de configuração do monitor hello, status e integridade para sua implantação de recuperação de Site:

1. Clique em Olá Olá de tooaccess de nome de cofre **Essentials** painel. Neste painel, você pode acompanhar os trabalhos do Site Recovery, o status da replicação, os planos de recuperação, a integridade do servidor e os eventos.  

    ![Conceitos básicos](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. Em Olá **integridade** bloco que você pode monitorar os servidores de site que estão enfrentando o problema e Olá eventos gerados pela recuperação de Site no hello últimas 24 horas. Você pode personalizar os blocos de saudação do Essentials tooshow e layouts de tooyou mais úteis, incluindo status de saudação do outro Site Recovery e cofres de Backup.
3. Você pode gerenciar e monitorar a replicação no hello **itens replicados**, **planos de recuperação**, e **trabalhos de recuperação de Site** lado a lado. É possível fazer uma busca detalhada nos trabalhos para obter mais detalhes em **Trabalhos** > **Trabalhos do Site Recovery**.

## <a name="command-line-provider-and-agent-installation"></a>Instalação do provedor e do agente pela linha de comando

Olá provedor Azure Site Recovery e o agente também podem ser instalados usando a seguinte linha de comando de saudação. Esse método pode ser um provedor de saudação tooinstall usado em um núcleo de servidor para o Windows Server 2012 R2.

1. Baixe Olá provedor de arquivo e registro tooa chave pasta de instalação. Por exemplo, C:\ASR.
2. Em um prompt de comando com privilégios elevados, execute o instalador do provedor esses comandos tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Execute este comando tooinstall componentes hello:

            C:\ASR> setupdr.exe /i
4. Em seguida, execute servidor comandos tooregister Olá no cofre hello:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Em que:

* **/ Credenciais**: parâmetro obrigatório que especifica o local de saudação em qual Olá arquivo de chave do registro está localizado  
* **/ FriendlyName**: parâmetro obrigatório para o nome de saudação do servidor de host de saudação Hyper-V que aparece no portal do Azure Site Recovery hello.
* **/proxyAddress**: parâmetro opcional que especifica o endereço de saudação do servidor de proxy de saudação.
* **/proxyPort** : parâmetro opcional que especifica a porta de saudação do servidor de proxy de saudação.
* **/proxyUsername**: parâmetro opcional que especifica o nome de usuário de Proxy de saudação (se o proxy exige autenticação).
* **/proxyPassword**: parâmetro opcional que especifica Olá senha para autenticar com o servidor de proxy de saudação (se o proxy exige autenticação).


## <a name="network-bandwidth-considerations"></a>Considerações sobre largura de banda de rede
Você pode usar o hello [ferramenta do Planejador de capacidade de Hyper-V](site-recovery-capacity-planner.md) largura de banda de saudação toocalculate é necessário para a replicação (replicação inicial e, em seguida, delta). quantidade de saudação toocontrol de uso de largura de banda para replicação, você tem algumas opções:

* **Limitação da largura de banda**: tráfego Hyper-V que replica tooAzure passa por um host Hyper-V específico. Você pode reduzir a largura de banda no servidor de host de saudação.
* **Ajustar a largura de banda**: você pode influenciar a largura de banda de saudação usada para replicação usando duas chaves do registro.

### <a name="throttle-bandwidth"></a>Restringir a largura de banda
1. Abra o snap-in MMC do Backup do Microsoft Azure de saudação no servidor de host do Hyper-V hello. Por padrão um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. No snap-in Olá clique **alterar propriedades**.
3. Em Olá **limitação** guia **habilitar limitação para operações de backup do uso de largura de banda de internet**e definir limites de saudação do trabalho e folga horas. Intervalos válidos são de 512 Mbps de too102 Kbps por segundo.

    ![Restringir a largura de banda](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

Você também pode usar o hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Veja um exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que nenhuma limitação é necessária.

### <a name="influence-network-bandwidth"></a>Influência da largura de banda de rede
1. No registro de saudação navegue muito**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de saudação tooinfluence em um disco de replicação, modificar Olá Olá do valor **UploadThreadsPerVM**, ou criar a chave de saudação se ele não existir.
   * largura de banda tooinfluence Olá para o tráfego de failback do Azure, modifique o valor de saudação **DownloadThreadsPerVM**.
2. valor padrão de saudação é 4. Em uma rede de "sobreprovisionada", essas chaves do registro devem ser diferente dos valores padrão de saudação. Olá máximo é 32. Monitorar o tráfego toooptimize Olá valor.

## <a name="next-steps"></a>Próximas etapas

Depois que a replicação inicial for concluída e você testou implantação hello, você pode chamar failovers conforme a necessidade de saudação. [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
