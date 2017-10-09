---
title: "aaaReplicate VMs Hyper-V tooa site secundário com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooreplicate VMs Hyper-V no VMM nuvens tooa secundário do VMM site usando Olá portal do Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Replicar máquinas virtuais de Hyper-V no VMM nuvens tooa site VMM secundário usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Este artigo descreve como tooreplicate local máquinas virtuais de Hyper-V gerenciados nas nuvens do System Center Virtual Machine Manager (VMM), usando o site secundário tooa [do Azure Site Recovery](site-recovery-overview.md) em Olá portal do Azure. Saiba mais sobre isso [arquitetura de cenário](site-recovery-components.md).

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Pré-requisitos

**Pré-requisito** | **Detalhes**
--- | ---
**As tabelas** | Você precisa de uma conta do [Microsoft Azure](http://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site.
**VMM local** | Recomendamos que você tenha dois servidores do VMM, um site primário hello e um em Olá secundário.<br/><br/> Você pode replicar entre nuvens em um único servidor VMM.<br/><br/> Servidores do VMM devem estar executando pelo menos System Center 2012 SP1 com atualizações mais recentes de saudação.<br/><br/> Servidores VMM precisam de acesso à Internet.
**Nuvens do VMM** | Cada servidor do VMM deve ter em uma ou mais nuvens, e todas as nuvens devem ter perfil de capacidade do Hyper-V Olá definida. <br/><br/>As nuvens devem conter um ou mais grupos de hosts do VMM.<br/><br/> Se você tiver apenas um servidor do VMM, ele precisa de pelo menos duas nuvens, tooact como primário e secundário.
**Hyper-V** | Servidores Hyper-V devem estar executando pelo menos o Windows Server 2012 com a função hello Hyper-V, e ter Olá as últimas atualizações instaladas.<br/><br/> Um servidor Hyper-V deve conter uma ou mais VMs.<br/><br/>  Servidores de host Hyper-V devem estar localizados em grupos de host em nuvens do VMM Olá primários e secundários.<br/><br/> Se você estiver executando o Hyper-V em um cluster no Windows Server 2012 R2, instale a [atualização 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se estiver executando o Hyper-V em um cluster no Windows Server 2012, o agente de cluster não será criado automaticamente se você tiver um cluster baseado em endereço IP estático. Configure manualmente o agente do cluster hello. [Leia mais](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Os servidores do Hyper-V precisam de acesso à Internet.
**URLs** | Servidores do VMM e hosts Hyper-V devem ser capaz de tooreach essas URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Etapas de implantação.

Veja o que fazer:

1. Verifique se os pré-requisitos.
2. Prepare o servidor do VMM hello e hosts Hyper-V.
3. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e coordena a replicação.
4. Especifique as configurações de origem, destino e replicação.
5. Implantando o serviço de mobilidade Olá em máquinas virtuais que você deseja tooreplicate.
6. Preparar para replicação e habilitar a replicação para máquinas virtuais do Hyper-V.
7. Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>Preparar servidores VMM e hosts Hyper-V

tooprepare para implantação:

1. Verifique se o servidor do VMM hello e hosts Hyper-V cumprir os pré-requisitos de saudação descritos acima e podem alcançar URLs Olá necessário.
2. Configure as redes de VMM de modo que você possa configurar o [mapeamento de rede](#network-mapping-overview).

    - Certifique-se de que as VMs no servidor host Hyper-V de origem de saudação são conectado tooa rede VM do VMM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.
    Verifica se a nuvem secundária de saudação que você usar para recuperação tem uma rede VM correspondente configurada. Essa rede VM deve ser vinculado tooa rede lógica associada com a nuvem secundária hello.

3. Preparar para uma [única de implantação de servidor](#single-vmm-server-deployment), se você deseja tooreplicate VMs entre nuvens em Olá mesmo servidor do VMM.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Gerenciamento** > **Serviços de Recuperação**.
3. Em **nome**, especifique um cofre de saudação tooidentify nome amigável. Se você tiver mais de uma assinatura, selecione uma delas.
4. [Crie um grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md)ou selecione um existente. Especifique uma região do Azure. Os computadores são replicados toothis região. regiões toocheck suporte consulte disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Se você quiser tooquickly acesso Olá cofre da saudação painel, clique em **Pin toodashboard** > **criar cofre**.

    ![Novo cofre](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

novo cofre de saudação aparece na Olá **painel**, na **todos os recursos**e em Olá principal **cofres de serviços de recuperação** folha.


## <a name="choose-a-protection-goal"></a>Escolher um objetivo de proteção

Selecione o que você deseja tooreplicate e onde você deseja tooreplicate para.

2. Clique em **Site Recovery** > **Etapa 1: Preparar a Infraestrutura** > **Meta de proteção**.
3. Selecione **toorecovery site**e selecione **Sim, com o Hyper-V**.
4. Selecione **Sim** tooindicate você estiver usando os hosts do VMM toomanage Olá Hyper-V.
5. Selecione **Sim** se você tiver um servidor VMM secundário. Se você estiver implantando a replicação entre nuvens em um único servidor VMM, clique em **Não**. Em seguida, clique em **OK**.

    ![Escolher metas](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Instale Olá provedor Azure Site Recovery em servidores do VMM e descobrir e registrar servidores no cofre de saudação.

1. Clique em **Etapa 1: Preparar a Infraestrutura** > **Origem**.

    ![Configurar origem](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. Em **preparar fonte**, clique em **+ VMM** tooadd um servidor do VMM.

    ![Configurar origem](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. Em **Adicionar servidor**, verifique se **servidor do System Center VMM** aparece na **tipo de servidor** e servidor do VMM Olá atende Olá [pré-requisitos](#prerequisites).
4. Baixe o arquivo de instalação do provedor Azure Site Recovery hello.
5. Baixe a chave de registro de saudação. Você precisará dela quando executar a instalação. chave de saudação é válida por cinco dias depois que ele é gerado.

    ![Configurar origem](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Instale Olá provedor Azure Site Recovery no servidor do VMM hello. Você não precisa tooexplicitly instalar nada nos servidores de host do Hyper-V.


### <a name="install-hello-azure-site-recovery-provider"></a>Instalar Olá provedor Azure Site Recovery

1. Execute o arquivo de instalação do provedor de saudação em cada servidor do VMM. Se o VMM for implantado em um cluster, a seguir Olá Olá primeira vez que você instala:
    -  Instalar o provedor de saudação em um nó ativo e concluir o servidor do VMM Olá instalação tooregister Olá no cofre hello.
    - Em seguida, instale Olá provedor em Olá outros nós. Nós de cluster devem todos executados Olá mesma versão do provedor de saudação.
2. A instalação executa algumas verificações de pré-requisitos e solicitações permissão toostop saudação do serviço do VMM. saudação de serviço do VMM será reiniciada automaticamente quando a instalação for concluída. Se você instalar em um cluster do VMM, você está função de Cluster Olá toostop solicitada.
3. Em **Microsoft Update**, você pode aceitar toospecify que provedor serão instaladas de acordo com a política do Microsoft Update.
4. Em **instalação**, aceite ou modifique o local de instalação padrão hello e clique em **instalar**.

    ![Local de instalação](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Após a conclusão da instalação, clique em **registrar** tooregister servidor de saudação no cofre hello.

    ![Local de instalação](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. Em **nome do cofre**, verificar nome de saudação do cofre Olá quais saudação servidor será registrado. Clique em *Avançar*.

    ![Registros do servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. Em **Conexão de Internet**, especifique como o provedor de saudação em execução no servidor do VMM Olá se conecta tooAzure.

    ![Configurações da Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - Você pode especificar o provedor Olá deve se conectar diretamente toohello internet, ou por meio de um proxy.
   - Especifique as configurações de proxy, se necessário.
   - Se você usar um proxy, uma conta de RunAs VMM (DRAProxyAccount) é criada automaticamente Olá especificado, usando as credenciais do proxy. Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito. Olá configurações da conta executar como podem ser modificadas no console do VMM hello > **configurações** > **segurança** > **contas executar como**. Reinicie a alterações de tooupdate de serviço do VMM hello.
8. Em **chave de registro**, selecione chave Olá que você baixou do Azure Site Recovery e copiou toohello o servidor do VMM.
9. configuração de criptografia de saudação é usada apenas quando você estiver replicando máquinas virtuais do Hyper-V no tooAzure de nuvens do VMM. Se você estiver replicando o site secundário tooa não é usado.
10. Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello. Em uma configuração de cluster, especifique nome de função de cluster saudação do VMM.
11. Em **sincronizar metadados de nuvem**, selecione se deseja toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello. Essa ação precisa apenas toohappen uma vez em cada servidor. Se você não quiser toosynchronize todas as nuvens, deixe essa configuração desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello.
12. Clique em **próximo** toocomplete processo de saudação. Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery. saudação do servidor é exibida em Olá **servidores VMM** guia Olá **servidores** página no cofre hello.

    ![Servidor](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Depois que o servidor hello está disponível no console de recuperação de Site Olá, em **fonte** > **preparar fonte** Selecionar servidor do VMM hello e nuvem Olá selecione em quais Olá Hyper-V host está localizado. Em seguida, clique em **OK**.

Você também pode instalar o provedor Olá Olá linha de comando:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Selecione a nuvem e o servidor do VMM de destino hello.

1. Clique em **preparar infraestrutura** > **destino**e servidor do VMM de destino select Olá toouse desejado.
2. Nuvens no servidor de saudação que são sincronizadas com a recuperação de Site serão exibidas. Selecione a nuvem de destino hello.

   ![Destino](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Definir as configurações de replicação

- Quando você cria uma política de replicação, todos os hosts usando a política de saudação deve ter Olá mesmo sistema operacional. saudação de nuvem do VMM pode conter hosts Hyper-V executando diferentes versões do Windows Server, mas nesse caso, você precisa de várias políticas de replicação.
- Você pode executar Olá a replicação inicial offline. [Saiba mais](#prepare-for-initial-offline-replication)

1. Clique em uma nova política de replicação de toocreate **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.

    ![Rede](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política. Olá tipo de origem e destino deve ser **Hyper-V**.
3. Em **versão de host do Hyper-V**, selecione o sistema operacional que está em execução no host de saudação.
4. Em **tipo de autenticação** e **porta de autenticação**, especifique como o tráfego será autenticado entre hello primário e servidores de host do Hyper-V de recuperação. Selecione **Certificado** , a menos que você tenha um ambiente Kerberos em funcionamento. A Recuperação de Site do Azure configurará automaticamente os certificados para autenticação HTTPS. Você não precisa toodo nada manualmente. Por padrão, as portas 8083 e 8084 (para certificados) serão aberta no hello Firewall do Windows nos servidores de host do Hyper-V hello. Se você selecionar **Kerberos**, um tíquete Kerberos será usado para autenticação mútua dos servidores de host de saudação. Observe que esta configuração só é relevante para servidores de host Hyper-V no Windows Server 2012 R2.
5. Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).
6. Em **retenção de ponto de recuperação**, especifique, em horas, quanto tempo uma janela de retenção Olá será possível para cada ponto de recuperação. Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela.
7. Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que contêm instantâneos consistentes com o aplicativo. Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação. Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado. Se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de saudação de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.
8. Em **Compactação da transferência de dados**, especifique se os dados replicados transferidos devem ser compactados.
9. Selecione **excluir réplica VM**, toospecify que Olá a máquina virtual de réplica deve ser excluída se você desabilitar a proteção para a VM de origem hello. Se você habilitar essa configuração, quando você desativar a proteção para a fonte de saudação VM, ele será removido do console de recuperação de Site hello, configurações de recuperação de Site para Olá VMM serão removidas do console do VMM hello e Olá réplica será excluída.
10. Em **inicial do método de replicação**, se você estiver replicando em rede hello, especifique se toostart Olá a replicação inicial ou agendá-la. toosave a largura de banda de rede, talvez você queira tooschedule-lo fora do horário de ocupado. Em seguida, clique em **OK**.

     ![Política de replicação](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Quando você cria uma nova política está associado automaticamente Olá nuvem do VMM. Em **Política de replicação**, clique em **OK**. Você pode associar nuvens do VMM adicionais (e Olá VMs neles) com esta política de replicação em **replicação** > nome da política > **associar VMM nuvem**.

     ![Política de replicação](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Configurar o mapeamento de rede

- Saiba mais sobre [mapeamento de rede](#prepare-for-network-mapping) antes de iniciar.
- Verifique se máquinas virtuais nos servidores VMM estão conectados tooa rede VM.


1. Em **Infraestrutura do Site Recovery** > **Mapeamento de Rede** > **Mapeamentos de rede**, clique em **+Mapeamento de Rede**.

    ![Mapeamento de rede](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. Em **Adicionar mapeamento de rede** , selecione a fonte de saudação e servidores do VMM de destino. redes VM Olá associados aos servidores do VMM Olá são recuperados.
3. Em **rede de origem**, selecione rede hello serão toouse de lista de saudação de redes VM associadas Olá servidor primário do VMM.
4. Em **rede de destino**, selecione rede hello serão toouse no servidor VMM secundário de saudação. Em seguida, clique em **OK**.

    ![Mapeamento de rede](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Veja o que acontece quando começa o mapeamento de rede:

* Qualquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será conectado toohello rede VM de destino.
* Novas máquinas virtuais que estão conectados toohello rede VM de origem será conectado toohello destino mapeadas rede após a replicação.
* Se você modificar um mapeamento existente com uma nova rede, máquinas virtuais de réplica serão conectadas usando Olá novas configurações.
* Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.

### <a name="configure-storage-mapping"></a>Configure o mapeamento de armazenamento.

[Mapeamento de armazenamento](#prepare-for-storage-mapping) não tem suporte no novo portal do Azure de saudação. No entanto, ele pode ser habilitado com o PowerShell. [Saiba mais](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Etapa 5: Planejamento de capacidade

Agora que você tem a infraestrutura básica configurada, pense no planejamento de capacidade e confira se precisa de recursos adicionais.

- Baixe e execute Olá [Planejador de capacidade de recuperação de Site do Azure](site-recovery-capacity-planner.md), toogather informações sobre o ambiente de replicação, incluindo as VMs, discos por VM e armazenamento por disco.
- Depois que você coletou informações de replicação em tempo real, você pode modificar Olá NetQos política toocontrol replicação da largura de banda para VMs. Leia mais sobre [limitação tráfego de réplica do Hyper-V](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/), no blog de Thomas Maurer. Obter mais informações sobre Olá [cmdlet New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Habilitar a replicação

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**. Depois de habilitar a replicação para Olá primeira vez, você clicar em **+ replicar** em replicação de tooenable Olá cofre para outras máquinas.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. Em **fonte**, selecione o servidor do VMM hello e Olá nuvem na qual Olá hosts Hyper-V que você deseja tooreplicate estão localizados. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. Em **destino**, verifique se Olá servidor secundário do VMM e a nuvem.
4. Em **máquinas virtuais**, selecione VMs Olá deseja tooprotect da lista de saudação.

    ![Habilitar Proteção da Máquina Virtual](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Você pode acompanhar o progresso da saudação **Habilitar proteção** ação **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** trabalho for concluído, Olá máquina de virtual está pronta para failover.

Observe que:

- Você também pode habilitar a proteção para máquinas virtuais no console do VMM hello. Clique em **Habilitar proteção** na barra de ferramentas Olá nas propriedades de máquina virtual hello > **do Azure Site Recovery** guia.
- Depois de habilitar a replicação, você pode exibir propriedades para Olá VM em **itens duplicados**. Em Olá **Essentials** painel, você pode ver informações sobre a política de replicação Olá Olá VM e seu status. Clique em **Propriedades** para obter mais detalhes.

### <a name="onboard-existing-virtual-machines"></a>Integrar máquinas virtuais existentes
Se você tiver máquinas virtuais existentes no VMM replicadas com a Réplica do Hyper-V, poderá carregá-las na replicação do Azure Site Recovery da seguinte maneira:

1. Verifique se o servidor Olá Hyper-V hospeda Olá que VM existente está localizado na nuvem primária hello e servidor Hyper-V Olá Olá máquina de virtual de réplica de hospedagem está localizado na nuvem secundária hello.
2. Certifique-se de que uma política de replicação é configurada para nuvem VMM primária de saudação.
3. Habilite a replicação para máquina virtual primária de saudação. Do Azure Site Recovery e o VMM Certifique-se de que hello mesmo host de réplica e máquina virtual for detectado e reutilizar o Azure Site Recovery e restabelecer a replicação usando Olá especificar configurações.

## <a name="test-your-deployment"></a>Testar a implantação

tootest sua implantação, você pode executar um [failover de teste](site-recovery-test-failover-vmm-to-vmm.md) para uma única máquina virtual, ou [criar um plano de recuperação](site-recovery-create-recovery-plans.md) que contém uma ou mais máquinas virtuais.



## <a name="prepare-for-offline-initial-replication"></a>Preparar a replicação inicial offline

Você pode fazer a replicação offline para cópia de dados iniciais de saudação. Você pode preparar isso da seguinte maneira:

* No servidor de origem Olá, você deve especificar um caminho local do qual Olá exportação de dados ocorrerá. Atribua controle total para permissões de NTFS e compartilhamento de serviço do VMM toohello no caminho de exportação de saudação. No servidor de destino hello, você especificar um caminho local do qual importar dados de saudação ocorrerá. Atribua Olá mesmas permissões neste caminho de importação.
* Se hello importar ou exportar caminho for compartilhado, atribua a associação de grupo de administrador, usuário avançado, operador de impressão ou operador de servidor para a conta de serviço do VMM Olá no computador remoto Olá no qual Olá compartilhado está localizado.
* Se você estiver usando quaisquer hosts de tooadd da contas executar como, em Olá importar e exportar caminhos, atribuir a leitura e permissões de gravação toohello as contas executar como no VMM.
* Olá importar e exportar compartilhamentos não deve estar localizado em qualquer computador usado como um servidor de host do Hyper-V, porque não há suporte para a configuração de loopback pelo Hyper-V.
* No Active Directory, em cada servidor de host do Hyper-V que contém máquinas virtuais que você deseja tooprotect, habilitar e configurar a delegação restrita tootrust Olá computadores remotos nos quais Olá importação e exportação do caminhos estão localizados, da seguinte maneira:
  1. No controlador de domínio hello, abra **computadores e usuários do Active Directory**.
  2. Na árvore de console hello, clique em **DomainName** > **computadores**.
  3. Nome do servidor de host com o botão direito Olá Hyper-V > **propriedades**.
  4. Em Olá **delegação** , clique em **confiar no computador para delegação toospecified dos serviços somente**.
  5. Clique em **Usar qualquer protocolo de autenticação**.
  6. Clique em **Adicionar** > **Usuários e Computadores**.
  7. Nome do tipo saudação do computador de saudação que hospeda o caminho de exportação hello > **Okey**. Na lista de saudação de serviços disponíveis, mantenha pressionada a tecla CTRL de saudação e clique em **cifs** > **Okey**. Repita para nome de saudação do computador Olá desse caminho de importação de saudação hosts. Repita conforme necessário para servidores host Hyper-V adicionais.



## <a name="prepare-for-network-mapping"></a>Prepare-se para o mapeamento de rede
Mapas de mapeamento de rede entre redes de VM do VMM nos servidores VMM primários e secundários de saudação para:

* Colocar de maneira ideal VMs de réplica em hosts secundários do Hyper-V após o failover.
* Conecte a redes VM de tooappropriate de máquinas virtuais de réplica após o failover.

Observe que:
- Mapeamento de rede pode ser configurado entre redes VM em dois servidores do VMM ou em um único servidor do VMM se dois sites forem gerenciados pelo Olá mesmo servidor.
- Quando o mapeamento for configurado corretamente e a replicação está habilitada, uma VM no local primário Olá será conectado tooa rede e sua réplica no local de destino hello será conectada tooits mapeado rede.
- Se redes tem sido instaladas corretamente no VMM, quando você seleciona uma rede de VM de destino durante o mapeamento de rede, nuvens de origem do VMM Olá que usam a rede VM de origem Olá serão exibidas, juntamente com redes VM de destino disponíveis Olá em nuvens de destino de saudação que são usadas para proteção.
- Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes Olá mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá máquina virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.


Aqui está um exemplo tooillustrate esse mecanismo. Vamos usar uma organização com dois locais, Nova Iorque e Chicago.

| **Localidade** | **Servidor VMM** | **Redes VM** | **Mapeado para** |
| --- | --- | --- | --- |
| Nova Iorque |VMM-NewYork |VMNetwork1-NewYork |TooVMNetwork1 mapeada-Chicago |
| VMNetwork2-NewYork |Não mapeado | | |
| Chicago |VMM-Chicago |VMNetwork1-Chicago |TooVMNetwork1-NewYork mapeada |
| VMNetwork2-Chicago |Não mapeado | | |

Neste exemplo:

* Quando uma máquina virtual de réplica é criada para qualquer máquina virtual que está conectada tooVMNetwork1-NewYork, ela será conectado tooVMNetwork1-Chicago.
* Quando uma máquina virtual de réplica é criada para VMNetwork2-NewYork ou VMNetwork2-Chicago, ele não será conectado tooany rede.

Aqui está como nuvens do VMM são configurados em nossa organização de exemplo e redes lógicas de saudação associados Olá nuvens.

### <a name="cloud-protection-settings"></a>Configurações de proteção de nuvem
| **Nuvem protegida** | **Protegendo a nuvem** | **Rede lógica (Nova Iorque)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>ND</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |
| SilverCloud2 |<p>ND</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Configurações de rede lógica e de VM
| **Localidade** | **Rede lógica** | **Rede VM associada** |
| --- | --- | --- |
| Nova Iorque |LogicalNetwork1-NewYork |VMNetwork1-NewYork |
| Chicago |LogicalNetwork1-Chicago |VMNetwork1-Chicago |
| LogicalNetwork2Chicago |VMNetwork2-Chicago | |

### <a name="target-networks"></a>Redes de destino
Com base nessas configurações, quando você seleciona a rede VM de destino hello, Olá a tabela a seguir mostra opções Olá que estarão disponíveis.

| **Seleção** | **Nuvem protegida** | **Protegendo a nuvem** | **Rede de destino disponível** |
| --- | --- | --- | --- |
| VMNetwork1-Chicago |SilverCloud1 |SilverCloud2 |Disponível |
| GoldCloud1 |GoldCloud2 |Disponível | |
| VMNetwork2-Chicago |SilverCloud1 |SilverCloud2 |Não disponível |
| GoldCloud1 |GoldCloud2 |Disponível | |


### <a name="failback"></a>Failback
toosee o que acontece no caso de saudação de failback (replicação inversa), vamos supor que a VMNetwork1-NewYork é mapeado tooVMNetwork1-Chicago, com hello configurações a seguir.

| **Máquina virtual** | **Rede tooVM conectado** |
| --- | --- |
| VM1 |VMNetwork1-Rede |
| VM2 (réplica de VM1) |VMNetwork1-Chicago |

Com essas configurações, vamos analisar o que acontece em alguns cenários possíveis.

| **Cenário** | **Resultado** |
| --- | --- |
| Nenhuma alteração nas propriedades de rede Olá de VM-2 após o failover. |VM-1 permanece conectado toohello rede de origem. |
| As propriedades de rede de VM-2 são alteradas após o failover e ela é desconectada. |A VM-1 é desconectada. |
| Propriedades de rede de VM-2 são alteradas depois do failover e é conectado tooVMNetwork2-Chicago. |Se a VMNetwork2-Chicago não estiver mapeada, a VM-1 será desconectada. |
| O mapeamento de rede da VMNetwork1-Chicago é alterado. |VM-1 será conectado toohello de rede mapeada agora tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Preparar para a implantação de servidor único


Se você tiver apenas um único servidor VMM, você pode replicar máquinas virtuais em hosts Hyper-V na nuvem do VMM de saudação muito[Azure](site-recovery-vmm-to-azure.md) ou tooa na nuvem do VMM secundário. É recomendável opção primeira Olá porque a replicação entre nuvens não contínua. Se você quiser tooreplicate entre nuvens, você pode replicar com um servidor do VMM autônomo único ou com um único servidor VMM implantado em um cluster de Windows ampliado

### <a name="standalone-vmm-server"></a>Servidor VMM Autônomo

Nesse cenário, implantar o servidor VMM único de saudação como uma máquina virtual no site primário hello e replicar VM tooa site secundário usando a réplica do Hyper-V e recuperação de Site.

1. **Configure o VMM em uma VM Hyper-V**. Sugerimos que você colocar a instância do SQL Server Olá usada pelo VMM em Olá mesma VM. Isso economiza tempo, como apenas uma VM tem toobe criado. Se você quiser toouse a instância remota do SQL Server e ocorrer uma interrupção, você precisa toorecover essa instância para que você possa recuperar do VMM.
2. **Certifique-se de que o servidor do VMM Olá tem pelo menos duas nuvens configuradas**. Uma nuvem conterá Olá VMs que você deseja tooreplicate e Olá outros nuvem funciona como o local secundário hello. Olá nuvem que contém as VMs Olá deseja tooprotect devem ser compatíveis com [pré-requisitos](#prerequisites).
3. Configure a Recuperação de Site conforme descrito neste artigo. Criar e registrar o servidor do VMM Olá em um cofre, configure uma política de replicação e habilitar a replicação. nomes VMM de origem e destino Hello serão Olá mesmo. Especifica que se a replicação inicial ocorre em rede hello.
4. Quando você configurar o mapeamento de rede você mapeie Olá da rede VM para a rede da VM toohello Olá nuvem primária para a nuvem secundária hello.
5. No console do Gerenciador do Hyper-V hello, habilitar a réplica do Hyper-V no host do Hyper-V Olá que contém Olá VMM VM e habilitar a replicação em Olá VM. Verifique se que você não adicionar tooclouds de máquina virtual do VMM Olá são protegidos pela recuperação de Site, tooensure que as configurações de réplica do Hyper-V não são substituídas pela recuperação de Site.
6. Se você criar planos de recuperação para failover que usar Olá mesmo servidor do VMM de origem e de destino.
7. Uma falha completa, failover e recuperação da seguinte maneira:

   1. Execute um failover não planejado no console do Gerenciador do Hyper-V Olá no site secundário hello, toofail sobre Olá primário VMM VM toohello site secundário.
   2. Verificar que Olá que VM VMM está ativo e em execução e no cofre hello, executar toofail um failover não planejado na Olá VMs de nuvens toosecondary primário. Confirmar failover hello e selecione um ponto de recuperação alternativo, se necessário.
   3. Após hello failover não planejado concluído, todos os recursos podem ser acessados de site primário Olá novamente.
   4. Quando o site primário Olá estiver disponível, no console do Gerenciador do Hyper-V Olá no site secundário hello, habilite a replicação inversa para Olá VMM VM. Isso inicia a replicação para Olá VM tooprimary secundário.
   5. Execute um failover planejado no console do Gerenciador do Hyper-V Olá no site secundário hello, toofail sobre Olá site primário do VMM VM toohello. Confirme failover de saudação. Em seguida, habilite a replicação inversa, para que hello VMM VM é novamente replicando de toosecondary primário.
   6. No cofre de serviços de recuperação hello, habilite a replicação inversa para carga de trabalho Olá VMs, toostart replicando-os de tooprimary secundário.
   7. No cofre de serviços de recuperação de hello, execute um failover planejado toofail Olá back cargas de trabalho VMs toohello site primário. Confirmar Olá failover toocomplete-lo. Em seguida, habilite a replicação inversa toostart replicação Olá carga de trabalho VMs de toosecondary primário.

### <a name="stretched-vmm-cluster"></a>Cluster do VMM ampliado

Em vez de implantar um servidor do VMM autônomo como uma VM que replica o site secundário tooa, você pode fazer o VMM altamente disponível, implantando-a como uma máquina virtual em um cluster de failover do Windows. Isso fornece resiliência de carga de trabalho e proteção contra falhas de hardware. toodeploy com hello de recuperação de Site VMM VM deve ser implantado em um cluster de ampliação em locais geograficamente separados. toodo isso:

1. Instalação do VMM em uma máquina virtual em um cluster de failover do Windows e selecione o servidor de saudação do hello opção toorun como altamente disponível durante a instalação.
2. instância do SQL Server de saudação que é usada pelo VMM deve ser replicada com grupos de disponibilidade do AlwaysOn do SQL Server, para que haja uma réplica de banco de dados de saudação no site secundário hello.
3. Siga as instruções de saudação toocreate este artigo um cofre, registrar o servidor de saudação e configurar a proteção. É necessário tooregister cada servidor do VMM no hello cluster no cofre de serviços de recuperação de saudação. toodo isso, instale Olá provedor em um nó ativo e registrar o servidor do VMM hello. Em seguida, você deve instalar Olá provedor em outros nós.
4. Quando ocorre uma paralisação, o servidor do VMM hello e seu banco de dados do SQL Server correspondente são failover e acessados a partir do site secundário hello.



## <a name="prepare-for-storage-mapping"></a>Preparar para realizar mapeamento de armazenamento


Configurar o armazenamento de mapeamento por mapeamento classificações de armazenamento em uma fonte e a seguir de saudação do toodo de servidores VMM de destino:

  * **Identificar o armazenamento de destino para máquinas virtuais de réplica**— um disco VM de origem serão replicadas armazenamento toohello especificado (compartilhamento SMB ou o cluster CSVs (volumes compartilhados)) no local de destino hello.
  * **Posicionamento de máquina virtual de réplica**— o mapeamento de armazenamento é usada toooptimally máquinas de virtuais de réplica local nos servidores de host do Hyper-V. Máquinas virtuais de réplica serão colocadas em hosts que podem acessar a classificação de armazenamento Olá mapeado.
  * **Nenhum mapeamento de armazenamento**— se você não configurar o mapeamento de armazenamento, máquinas virtuais serão replicadas toohello local de armazenamento de padrão especificado no servidor de host de saudação Hyper-V associado à máquina de virtual de réplica Olá.

Observe que:
- Você pode configurar o mapeamento entre duas nuvens do VMM em um único servidor.
- Classificações de armazenamento devem estar disponível toohello grupos de hosts localizados nas nuvens de origem e destino.
- Não é necessário classificações toohave Olá mesmo tipo de armazenamento. Por exemplo, você pode mapear uma classificação de origem que contém o SMB compartilhamentos tooa classificação de destino que contém CSVs.

### <a name="example"></a>Exemplo
Se as classificações estiverem configuradas corretamente no VMM quando você selecionar origem de saudação e o servidor do VMM de destino durante o mapeamento de armazenamento, classificações de origem e destino de saudação serão exibidas. Veja um exemplo de compartilhamentos de arquivos de armazenamento e classificações para uma organização com duas localizações, Nova Iorque e Chicago.

| **Localidade** | **Servidor VMM** | **Compartilhamento de arquivos (origem)** | **Classificação (origem)** | **Mapeado para** | **Compartilhamento de arquivos (destino)** |
| --- | --- | --- | --- | --- | --- |
| Nova Iorque |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Não mapeado | |
|  |SILVER_TARGET |Não mapeado | | | |
|  |BRONZE_TARGET |Não mapeado | | | |

Neste exemplo:

* Quando uma máquina virtual de réplica é criada para qualquer máquina virtual no armazenamento ouro (SourceShare1), ele será replicada tooa GOLD_TARGET armazenamento (TargetShare1).
* Quando uma máquina virtual de réplica é criada para qualquer máquina virtual no armazenamento prata (SourceShare2), ele será seja replicado tooa SILVER_TARGET (TargetShare2) de armazenamento e assim por diante.

### <a name="multiple-storage-locations"></a>Vários locais de armazenamento
Se for atribuída a classificação de destino Olá compartilhamentos SMB toomultiple ou CSVs, local de armazenamento ideal de saudação será selecionado automaticamente quando a máquina virtual hello está protegida. Se nenhum armazenamento de destino adequado está disponível com hello especificou a classificação, o padrão de saudação especificado no host do Hyper-V de saudação do local de armazenamento é usada tooplace Olá réplica os discos rígidos virtuais.

Olá, a tabela a seguir mostra como classificação de armazenamento e volumes compartilhados do cluster estão configurados em nosso exemplo.

| **Localidade** | **Classificação** | **Armazenamento associado** |
| --- | --- | --- |
| Nova Iorque |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Esta tabela resume o comportamento de hello quando você habilita a proteção para máquinas virtuais (VM1 - VM5) nesse ambiente de exemplo.

| **Máquina virtual** | **Armazenamento de origem** | **Classificação de origem** | **Armazenamento de destino mapeado** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Ambos GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Ambos GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Ambos SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |N/D |Nenhum mapeamento para que o local de armazenamento padrão saudação do host do Hyper-V de saudação é usado |



### <a name="data-privacy-overview"></a>Visão geral de privacidade de dados

Esta tabela resume como os dados são armazenados neste cenário:

- - -
| Ação | **Detalhes** | **Dados coletados** | **Uso** | **Obrigatório** |
| --- | --- | --- | --- | --- |
| **Registro** | Você registra um servidor VMM em um cofre de Serviços de Recuperação. Se você quiser mais tarde toounregister um servidor, você pode fazer isso excluindo informações de saudação do servidor de saudação portal do Azure. | Depois que um servidor do VMM está registrado o Site Recovery coleta, processa e transfere os metadados sobre o servidor do VMM hello e nomes de saudação de nuvens do VMM Olá detectados pela recuperação de Site. | Olá dados tooidentify usado e se comunicar com o servidor do VMM apropriado hello e definir configurações para nuvens do VMM apropriados. | Este recurso é necessário. Se você não quiser toosend este tooSite informações recuperação você não deve usar o serviço de recuperação de Site hello. |
| **Habilitar a replicação** | Olá provedor Azure Site Recovery está instalado no servidor do VMM hello e é Olá canal de comunicação com hello serviço de recuperação de Site. Olá provedor é uma biblioteca de vínculo dinâmico (DLL) hospedada no processo do VMM hello. Após Olá que provedor está instalado, recurso de "Recuperação do Datacenter" hello obtém habilitado no console do administrador do VMM hello. Máquinas virtuais novas e existentes podem habilitar essa proteção tooenable de recurso para uma máquina virtual. |Com essa propriedade definida, Olá provedor envia Olá nome e ID Olá VM tooSite recuperação.  A replicação é habilitada pelo Windows Server 2012 ou Réplica do Hyper-V do Windows Server 2012 R2. dados da máquina virtual Olá são replicados de um tooanother de host do Hyper-V (normalmente localizado em um data center diferente de "recuperação"). |Recuperação de site usa informações de VM do hello metadados toopopulate Olá Olá portal do Azure. | Esse recurso é uma parte essencial do serviço hello e não pode ser desativado. Se você não quiser toosend essas informações, não habilite a proteção de recuperação de Site para VMs. Observe que todos os dados enviados pelo provedor de saudação tooSite recuperação é enviado via HTTPS. |
| **Plano de recuperação** | Planos de recuperação ajudam a criar um plano de orquestração do data center de recuperação de saudação. Você pode definir a ordem de saudação em que VMs ou um grupo de máquinas virtuais deve ser iniciado no site de recuperação de saudação. Você também pode especificar qualquer toobe scripts automatizados executar ou qualquer toobe manual ação adotada, no tempo de saudação de recuperação para cada VM. Normalmente, o failover é acionado no nível de plano de recuperação Olá para a recuperação coordenada. | Recuperação de site coleta, processa e transmite metadados Olá plano de recuperação, incluindo os metadados da máquina virtual e quaisquer scripts de automação e Observações da ação manual. |Olá metadados são o plano de recuperação de saudação toobuild usado em Olá portal do Azure. |Esse recurso é uma parte essencial do serviço hello e não pode ser desativado. Se você não quiser toosend este tooSite informações recuperação, não crie planos de recuperação. |
| **Mapeamento de rede** | Mapas de informações de data center Olá dados primários center toohello recuperação de rede. Quando as VMs são recuperadas no site de recuperação hello, mapeamento de rede ajuda a estabelecer a conectividade de rede. |Recuperação de site coleta, processa e transmite metadados Olá de redes lógicas de saudação para cada site (primário e datacenter). |Olá metadados são usado toopopulate as configurações de rede para que você pode mapear as informações de rede hello. | Esse recurso é uma parte essencial do serviço hello e não pode ser desativado. Se você não quiser toosend este tooSite informações recuperação, não use o mapeamento de rede. |
| **Failover (planejado/não planejado/teste)** | Failover falhar em VMs do tooanother do Centro de dados gerenciados do VMM. ação de failover de saudação é disparada manualmente no portal do Azure de saudação. |Olá provedor no servidor do VMM Olá será notificado de evento de failover Olá pela recuperação de Site e executa uma ação de failover no host do Hyper-V Olá por meio das interfaces do VMM. Failover real de uma VM é de um tooanother de host do Hyper-V e tratada pelo Windows Server 2012 ou Windows Server 2012 R2 Hyper-V Replica. AFT recuperação de Site usa informações de saudação enviadas toopopulate status de saudação de informações de ação de failover de saudação em Olá portal do Azure. | Esse recurso é uma parte essencial do serviço hello e não pode ser desativado. Se você não quiser toosend este tooSite informações recuperação, não use o failover. |

## <a name="next-steps"></a>Próximas etapas

Depois que você testou implantação hello, saiba mais sobre outros tipos de [failover](site-recovery-failover.md)
