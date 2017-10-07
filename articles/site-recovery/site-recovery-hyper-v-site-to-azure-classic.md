---
title: "aaaReplicate tooAzure de VMs Hyper-V no portal clássico Olá | Microsoft Docs"
description: "Este artigo descreve como tooreplicate virtual Hyper-V máquinas tooAzure quando máquinas não são gerenciadas nas nuvens do VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Replicar entre máquinas virtuais Hyper-V no local e o Azure (sem VMM) com o Azure Site Recovery
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portal clássico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Este artigo descreve como tooreplicate local tooAzure de máquinas virtuais do Hyper-V, usando Olá [do Azure Site Recovery](site-recovery-overview.md) service, Olá portal do Azure. Nesse cenário, os servidores Hyper-V não são gerenciados em nuvens do VMM.

Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Recuperação de site no portal do Azure de saudação

O Azure tem dois [modelos de implantação](../resource-manager-deployment-model.md) diferentes para criar e trabalhar com recursos: o Azure Resource Manager e o clássico. O Azure também tem dois portais – Olá portal clássico do Azure e Olá portal do Azure.

Este artigo descreve como toodeploy no portal clássico do hello. portal clássico Olá pode ser cofres existentes toomaintain usado. Não é possível criar novos cofres usando o portal clássico do hello.

## <a name="site-recovery-in-your-business"></a>Recuperação de Site em sua empresa

As organizações precisam de uma estratégia BCDR que determina como os aplicativos e dados permanecem em execução e disponível durante o tempo de inatividade planejado e não planejado e recuperar toonormal condições de trabalho assim que possível. Aqui está o que a Recuperação de Site pode fazer:

* Proteção externa para aplicativos de negócios em execução em VMs Hyper-V.
* Tooset um único local, gerenciar e monitorar a replicação, failover e recuperação.
* TooAzure simples de failover e failback (Restaurar) dos servidores de host de tooHyper-V do Azure no seu site local.
* Planos de recuperação que incluem várias VMs, para que cargas de trabalho de aplicativo em camadas façam failover juntas.

## <a name="azure-prerequisites"></a>Pré-requisitos do Azure
* Você precisa de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* É necessário um toostore replicado dados da conta de armazenamento do Azure. conta de saudação precisa de replicação geográfica habilitada. Deve estar no hello mesma região do cofre do Azure Site Recovery hello e associar Olá a mesma assinatura. [Saiba mais sobre o Armazenamento do Azure](../storage/common/storage-introduction.md). Observe que não há suporte para mover contas de armazenamento criadas usando Olá [novo portal do Azure](../storage/common/storage-create-storage-account.md) entre grupos de recursos.
* Você precisará de uma rede virtual do Azure para que máquinas virtuais do Azure será conectado tooa rede quando você fizer failover no site primário.

## <a name="hyper-v-prerequisites"></a>Pré-requisitos do Hyper-V
* No site de local de origem Olá você precisará de um ou mais servidores executando **Windows Server 2012 R2** com a função hello Hyper-V instalada ou **Microsoft Hyper-V Server 2012 R2**. O servidor deve:
* Conter uma ou mais máquinas virtuais.
* Ser toohello conectado à Internet, diretamente ou por meio de um proxy.
* Executar correções de saudação descritas na KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Pré-requisitos de máquina virtual
Máquinas virtuais que você deseja tooprotect devem estar em conformidade com [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Pré-requisitos de provedor e do agente
Como parte da implantação do Azure Site Recovery você instalar Olá provedor Azure Site Recovery e hello Azure Recovery Services Agent em cada servidor Hyper-V. Observe que:

* Recomendamos que você sempre executar agente e versões mais recentes de saudação do hello provedor. Eles estão disponíveis no portal de recuperação de Site hello.
* Todos os servidores Hyper-V em um cofre deve ter Olá mesmo versões do hello provedor e agente.
* Provedor em execução no servidor de saudação Hello conecta tooSite recuperação sobre Olá internet. Você pode fazer isso sem um proxy, com as configurações de proxy Olá atualmente configuradas no servidor do Hyper-V hello, ou com as configurações de proxy personalizadas que você configurou durante a instalação do provedor. Você precisará toomake-se de que esse servidor de proxy Olá deseja toouse pode acessar essas URLs Olá para conectar-se tooAzure:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Além de permitir endereços IP de saudação descritos em [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) e o protocolo HTTPS (443). Você tem intervalos de IP de saudação tooallow de saudação região do Azure que você planeje toouse e do Oeste dos EUA.

Este gráfico mostra a canais de comunicação diferente hello e portas usadas pela recuperação de Site para replicação e de orquestração

![Topologia B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Etapa 1: criar um cofre
1. Entrar toohello [Portal de gerenciamento](https://portal.azure.com).
2. Expanda **Serviços de Dados** > **Serviços de Recuperação** e clique em **Cofre do Site Recovery**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **nome**, insira um cofre de saudação tooidentify nome amigável.
5. Em **região**, selecione Olá região geográfica para Olá cofre. regiões toocheck suporte consulte disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Clique em **Criar cofre**.

    ![Novo cofre](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Verifique a saudação tooconfirm de barra de status que Olá cofre foi criado com êxito. Olá cofre será listado como **Active** na página principal de serviços de recuperação hello.

## <a name="step-2-create-a-hyper-v-site"></a>Etapa 2: criar um site do Hyper-V
1. Na página de serviços de recuperação hello, clique em página de início rápido do hello cofre tooopen hello. Início rápido também pode ser aberto a qualquer momento usando o ícone de saudação.

    ![Início rápido](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Na lista suspensa de saudação, selecione **entre um site do Hyper-V local e o Azure**.

    ![Cenário de site do Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. Em **Criar um Site do Hyper-V**, clique em **Criar Site do Hyper-V**. Especifique um nome e salve.

    ![Site do Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Etapa 3: Instalar hello provedor e agente
Instale Olá provedor e o agente em cada servidor Hyper-V com máquinas virtuais que você deseja tooprotect.

Se você estiver instalando em um cluster Hyper-V, executa as etapas 5 a 11 em cada nó no cluster de failover de saudação. Depois que todos os nós são registrados e habilitar a proteção, máquinas virtuais serão protegidas, mesmo se eles migram entre nós de cluster de saudação.

1. Em **Preparar servidores Hyper-V**, clique em **Baixar um arquivo de chave de registro**.
2. Em Olá **baixar a chave de registro** , clique em **baixar** próximo site toohello. Baixe Olá tooa chave local seguro que possa ser facilmente acessado pelo servidor de saudação Hyper-V. chave de saudação é válida por 5 dias depois que ele é gerado.

    ![Chave de Registro](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Clique em **Download Olá provedor** versão mais recente do tooobtain hello.
4. Execute o arquivo de saudação em cada servidor Hyper-V que você deseja tooregister no cofre hello. arquivo Hello instala dois componentes:
   * **O provedor de recuperação de Site do Azure**— trata a comunicação e a coordenação entre o servidor de saudação Hyper-V e o portal do Azure Site Recovery Olá.
   * **Agente de serviços de recuperação do Azure**— lida com a transferência de dados entre máquinas virtuais em execução no servidor de origem Hyper-V de saudação e armazenamento do Azure.
5. No **Microsoft Update** você pode optar por atualizações. Com essa configuração habilitada, o provedor e agente serão instaladas de acordo com a política do tooyour Microsoft Update.

    ![Atualizações da Microsoft](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. Em **instalação** especifique onde você deseja tooinstall Olá provedor e Olá de agente no servidor Hyper-V.

    ![Local de instalação](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Após a conclusão da instalação continuar servidor de saudação do programa de instalação tooregister no cofre hello.
8. Em Olá **as configurações do cofre** , clique em **procurar** tooselect arquivo de chave de saudação. Especifique a assinatura do Azure Site Recovery Olá, nome do cofre Olá, e Olá Hyper-V site toowhich Olá Hyper-V servidor pertence.

    ![Registros do servidor](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. Em Olá **Conexão de Internet** página que você especificar como Olá provedor se conecta tooAzure recuperação de Site. Selecione **usar configurações de proxy do sistema padrão** configurações de conexão de Internet do toouse saudação padrão configuradas no servidor de saudação. Se você não especificar um padrão de saudação do valor configurações serão usadas.

   ![Configurações da Internet](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. Registro inicia o servidor de saudação do tooregister no cofre hello.

    ![Registros do servidor](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Após a conclusão de registro de metadados de saudação Hyper-V server é recuperado com o Azure Site Recovery e saudação do servidor é exibida em Olá **Sites Hyper-V** guia Olá **servidores** página no cofre hello.

### <a name="install-hello-provider-from-hello-command-line"></a>Instalar Olá provedor da linha de comando Olá
Como alternativa, você pode instalar Olá provedor Azure Site Recovery da linha de comando hello. Você deve usar esse método se você quiser tooinstall Olá provedor em um computador executando o Windows Server Core 2012 R2. Execute da linha de comando de saudação da seguinte maneira:

1. Baixe Olá provedor de arquivo e registro tooa chave pasta de instalação. Por exemplo, C:\ASR.
2. Execute um prompt de comando como Administrador e digite

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Em seguida, instale Olá provedor executando:

        C:\ASR> setupdr.exe /i
4. Execute Olá toocomplete registro a seguir:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Em que os parâmetros incluem:

* **/ Credenciais**: especificar local de saudação da chave de registro de saudação baixado.
* **/ FriendlyName**: especificar um servidor de host do nome tooidentify Olá Hyper-V. Esse nome aparecerá no portal de saudação
* **/EncryptionEnabled**: opcional. Especifique se deseja tooencrypt máquinas virtuais da réplica no Azure (a criptografia em repouso).
* **/proxyAddress**; **/proxyport**; **/proxyUsername**; **/proxyPassword**: Opcional. Especifica parâmetros de proxy, se você quiser toouse um proxy personalizado, ou o proxy existente exige autenticação.

## <a name="step-4-create-an-azure-storage-account"></a>Etapa 4: criar uma conta de armazenamento do Azure
* Em **preparar recursos** selecione **criar conta de armazenamento** toocreate uma conta de armazenamento do Azure se você não tiver um. conta de saudação deve ter replicação geográfica habilitada. Deve estar no hello mesma região do cofre do Azure Site Recovery hello e associar Olá a mesma assinatura.

    ![Criar Conta de Armazenamento](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Não há suporte para movimentação de saudação de contas de armazenamento criadas usando Olá [novo portal do Azure](../storage/common/storage-create-storage-account.md) entre grupos de recursos.
> 2. [Migração de contas de armazenamento](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para contas de armazenamento usadas para implantar a recuperação de Site.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Etapa 5: criar e configurar grupos de proteção
Grupos de proteção são agrupamentos lógicos de máquinas virtuais que você deseja usar tooprotect Olá mesmas configurações de proteção. Aplicar o grupo de proteção de tooa de configurações de proteção, e essas configurações são máquinas virtuais de tooall aplicado que você adicionar grupo toohello.

1. Em **Criar e configurar grupos de proteção**, clique em **Criar um grupo de proteção**. Se algum pré-requisito não estiver em vigor, uma mensagem será emitida e você poderá clicar em **Exibir detalhes** para saber mais.
2. Em Olá **grupos de proteção** guia, adicione um grupo de proteção. Especifique um nome, o site de origem Hyper-V de saudação, o destino de Olá **Azure**, seu nome de assinatura do Azure Site Recovery e Olá conta de armazenamento do Azure.

    ![Grupo de proteção](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. Em **as configurações de replicação** conjunto Olá **frequência de cópia** toospecify frequência delta de dados Olá deve ser sincronizada entre Olá origem e destino. Você pode definir too30 segundos, 5 minutos ou 15 minutos.
4. Em **Reter pontos de recuperação** , especifique quantas horas de histórico de recuperação devem ser armazenadas.
5. Em **frequência dos instantâneos consistentes por aplicativo** você pode especificar se os instantâneos tootake usar tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado. Por padrão, eles não obtidos. Verifique se que esse valor é definido tooless que número de saudação de pontos de recuperação adicionais que você configurar. Isso só é suportado se a máquina virtual de saudação está executando um sistema operacional Windows.
6. Em **hora de início da replicação inicial** especifique quando a replicação inicial de máquinas virtuais no grupo de proteção Olá deve ser enviada tooAzure.

    ![Grupo de proteção](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Etapa 6: habilitar a proteção da máquina virtual
Adicione máquinas virtuais tooa grupo tooenable proteção para eles.

> [!NOTE]
> Proteger VMs que executam o Linux com um endereço IP estático sem suporte.
>
>

1. Em Olá **máquinas** guia Olá grupo de proteção, clique em * * Adicionar máquinas virtuais tooprotection grupos de proteção tooenable * *.
2. Em Olá **Habilitar proteção da máquina Virtual** página Olá select de máquinas virtuais que deseja tooprotect.

    ![Habilitar Proteção da Máquina Virtual](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    trabalhos de proteção habilitar Olá começa. Você pode acompanhar o progresso na Olá **trabalhos** guia. Após o trabalho finalizar proteção de saudação executa Olá VM está pronta para failover.
3. Após a configuração da proteção, é possível:

   * Exibir máquinas virtuais em **itens protegidos** > **grupos de proteção** > *protectiongroup_name*  >  **Máquinas virtuais** pode analisar detalhes toomachine Olá **propriedades** guia...
   * Configurar propriedades de failover Olá para uma máquina virtual em **itens protegidos** > **grupos de proteção** > *protectiongroup_name*  >  **Máquinas virtuais** *virtual_machine_name* > **configurar**. Você pode configurar:

     * **Nome**: nome de saudação da máquina virtual de saudação no Azure.
     * **Tamanho**: Olá tamanho de destino da máquina virtual Olá que faz o failover.

       ![Configurar as propriedades da máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Defina as configurações adicionais de máquina virtual em *Itens Protegidos** > **Grupos de Proteção** > *nome_dogrupodeproteção* > **Máquinas Virtuais** *nome_da_máquina_virtual* > **Configurar**, incluindo:

     * **Adaptadores de rede**: número de saudação de adaptadores de rede é determinado pelo tamanho Olá especificado para a máquina de virtual de destino hello. Verificar [especificações de tamanho de máquina virtual](../virtual-machines/linux/sizes.md) para número de saudação de nics suportados pelo tamanho da máquina virtual de saudação.

       Quando você modificar o tamanho de saudação para uma máquina virtual e salva as configurações de hello, número de saudação do adaptador de rede será alterado quando você abrir **configurar** Olá página próxima vez. Olá vários adaptadores de rede de máquinas virtuais de destino é mínimo de saudação vários adaptadores de rede na máquina virtual de origem e o número máximo de adaptadores de rede suportados pelo tamanho de saudação da máquina virtual de saudação escolhida. É explicado abaixo:

       * Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
       * Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.
       * Por exemplo, se um computador de origem tem dois adaptadores de rede e tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.

     * **Rede do Azure**: especifique a máquina virtual do hello rede toowhich Olá devem executar failover. Se a máquina virtual de saudação tem vários adaptadores de rede todos os adaptadores deve toohello conectado mesma rede do Azure.
     * **Subrede** para cada adaptador de rede na máquina virtual de hello, sub-rede Olá select na máquina de Olá Olá rede Azure toowhich deve se conectar após o failover.
     * **Endereço IP de destino**: se o adaptador de rede de saudação da máquina virtual de origem é configurado toouse estático um de endereço IP, em seguida, você pode especificar o endereço IP de Olá Olá tooensure de máquina virtual de destino que Olá máquina tem Olá mesmo endereço IP após o failover .  Se você não especificar um endereço IP, em seguida, qualquer endereço disponível será atribuído em tempo de saudação de failover. Se você especificar um endereço que está sendo usado, o failover falhará.

     > [!NOTE]
     > [Migração de redes](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para redes usados para implantar a recuperação de Site.
     >

     ![Configurar as propriedades da máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Etapa 7: criar um plano de recuperação
Na implantação de saudação tootest ordem, você pode executar um failover de teste para uma única máquina virtual ou um plano de recuperação que contém uma ou mais máquinas virtuais. [Saiba mais](site-recovery-create-recovery-plans.md) sobre a criação de um plano de recuperação.

## <a name="step-8-test-hello-deployment"></a>Etapa 8: Testar a implantação de saudação
Há dois toorun de maneiras um tooAzure de failover de teste.

* **Failover de teste sem uma rede do Azure**— este tipo de failover de teste verifica se a máquina virtual Olá aparece corretamente no Azure. máquina virtual de saudação não será conectado tooany rede Azure após o failover.
* **Failover de teste com uma rede do Azure**— este tipo de failover verifica que Olá ambiente de replicação inteiro aparece como esperado e failover de máquinas virtuais de saudação conecta toohello rede Azure de destino especificado. Observe que para failover de teste sub-rede Olá Olá máquina de virtual de teste será descoberta com base na sub-rede de saudação do hello máquina de virtual de réplica. Isso é tooregular diferentes de replicação quando sub-rede saudação de uma máquina virtual de réplica é baseada na sub-rede de saudação do hello da máquina virtual de origem.

Se você quiser toorun um failover de teste sem especificar uma rede do Azure não é necessário tooprepare nada.

toorun um failover de teste com um destino de rede do Azure, você precisará toocreate uma nova rede Azure isolada da rede de produção do Azure (comportamento padrão quando você cria uma nova rede no Azure). Leia [Executar um failover de teste](site-recovery-failover.md) para obter mais detalhes.

toofully teste a implantação de replicação e de rede, você precisará tooset infra-estrutura Olá para que Olá replicadas toowork de máquina virtual, conforme o esperado. Uma maneira de fazer essa tootooset uma máquina virtual como um controlador de domínio com DNS e replicá-la tooAzure usando toocreate de recuperação de Site no teste de saudação de rede executando um failover de teste.  [Leia mais sobre](site-recovery-active-directory.md#test-failover-considerations) as considerações sobre failover de teste para o Active Directory.

Execute failover de teste de saudação da seguinte maneira:

> [!NOTE]
> tooget Olá melhor desempenho quando você fizer uma tooAzure de failover, certifique-se de que você tenha instalado o hello Azure agente na máquina Olá protegido. Isso ajuda na inicialização mais rápida e também no diagnóstico em caso de problemas. O agente do Linux pode ser encontrado [aqui](https://github.com/Azure/WALinuxAgent) e o agente do Windows pode ser encontrado [aqui](http://go.microsoft.com/fwlink/?LinkID=394789)
>
>

1. Em Olá **planos de recuperação** , selecione o plano de saudação e clique em **Failover de teste**.
2. Em Olá **confirmar Failover de teste** página Selecione **nenhum** ou uma rede do Azure específica.  Observe que, se você selecionar **nenhum** failover de teste de saudação verificará se a máquina virtual Olá corretamente replicados tooAzure mas não verifica sua configuração de rede de replicação.

    ![Failover de Teste](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. Em Olá **trabalhos** guia você pode acompanhar o progresso de failover. Você também deve ser toosee capaz de réplica de teste de máquina virtual Olá no hello portal do Azure. Se você estiver configurado em máquinas virtuais de tooaccess da sua rede local, você pode iniciar uma máquina virtual de toohello de conexão de área de trabalho remota.
4. Quando o failover de saudação atinge Olá **testes completos** fase, clique em **concluir teste** toofinish Olá failover de teste. Você pode fazer drill down toohello **trabalho** guia tootrack progresso de failover e o status e tooperform as ações que são necessários.
5. Após o failover será toosee capaz de réplica de teste de máquina virtual Olá no hello portal do Azure. Se você estiver configurado em máquinas virtuais de tooaccess da sua rede local, você pode iniciar uma máquina virtual de toohello de conexão de área de trabalho remota.

   1. Verifique se que máquinas virtuais de saudação foi iniciada com êxito.
   2. Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após o failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação. Você também precisará tooadd um ponto de extremidade do RDP na máquina virtual de saudação. Você pode aproveitar um [runbook de automação do Azure](site-recovery-runbook-automation.md) toodo que.
   3. Após o failover se você usar uma IP endereço tooconnect toohello virtual máquina público no Azure usando a área de trabalho remota, verifique se você não tem qualquer política de domínio que impedem a conexão de máquina virtual de tooa usando um endereço público.
6. Após a conclusão da saudação teste Olá a seguir:

   * Clique em **Olá failover de teste for concluído**. Limpar Olá power de tooautomatically do ambiente de teste e exclua Olá máquinas de virtuais de teste.
   * Clique em **notas** toorecord e salvar todas as observações associadas Olá failover de teste.
7. Quando o failover de saudação atinge Olá **testes completos** fase concluir a verificação de saudação da seguinte maneira:
   1. Exibir hello máquina de virtual de réplica no hello portal do Azure. Verifique se que a máquina virtual Olá iniciado com êxito.
   2. Se você estiver configurado em máquinas virtuais de tooaccess da sua rede local, você pode iniciar uma máquina virtual de toohello de conexão de área de trabalho remota.
   3. Clique em **teste completo Olá** toofinish-lo.
   4. Clique em **notas** toorecord e salvar todas as observações associadas Olá failover de teste.
   5. Clique em **Olá failover de teste for concluído**. Limpar Olá power de tooautomatically do ambiente de teste e exclua Olá máquina de virtual de teste.

## <a name="next-steps"></a>Próximas etapas
Depois que a implantação é configurada e está em funcionamento, [saiba mais](site-recovery-failover.md) sobre o failover.
