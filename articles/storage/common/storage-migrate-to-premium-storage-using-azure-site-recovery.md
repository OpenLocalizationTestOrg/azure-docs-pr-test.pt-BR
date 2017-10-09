---
title: "aaaMigrating tooAzure armazenamento Premium usando o Azure Site Recovery (discos não gerenciados) | Microsoft Docs"
description: "Migre seu tooAzure de máquinas virtuais existentes armazenamento Premium usando o Site Recovery (discos não gerenciados)."
services: storage
documentationcenter: 
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: luywang
ms.openlocfilehash: 2c82fffaa38baeeb4a676748125bd85d6e0500f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery-unmanaged-disks"></a>Migrando tooPremium armazenamento usando o Azure Site Recovery (discos não gerenciados)

O [Armazenamento Premium do Azure](storage-premium-storage.md) dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais (VMs) que estão executando cargas de trabalho intensivas para entradas e saídas. Olá finalidade deste guia é toohelp usuários migrar seus discos VM de uma conta de armazenamento padrão tooa conta de armazenamento Premium usando [do Azure Site Recovery](../../site-recovery/site-recovery-overview.md).

Recuperação de site é um serviço do Azure que contribui tooyour continuidade de negócios e Olá a estratégia de recuperação de desastres ao orquestrar a replicação de servidores físicos locais e VMs toohello nuvem (Azure) ou o datacenter secundário tooa. Quando ocorrem paralisações do local primário, você failover toohello aplicativos de tookeep de local secundário e cargas de trabalho disponíveis. Você não local primário tooyour voltar ao retornar toonormal operação. Recuperação de site fornece recuperação de desastre toosupport failovers de teste sem afetar os ambientes de produção. É possível executar failovers com perda mínima de dados (dependendo da frequência de replicação) para desastres inesperados. No cenário de saudação do migrando tooPremium armazenamento, você pode usar o hello [Failover na recuperação de Site](../../site-recovery/site-recovery-failover.md) no tooa de discos de destino do Azure Site Recovery toomigrate conta de armazenamento Premium.

É recomendável migrar tooPremium armazenamento usando a recuperação de Site porque essa opção fornece o tempo de inatividade mínimo e evita a execução manual de saudação de copiar os discos e criar novas VMs. O Site Recovery vai copiar os discos sistematicamente e criar novas VMs durante o failover. O Site Recovery oferece suporte a vários tipos de failover com pouco ou nenhum tempo de inatividade. tooplan seu tempo de inatividade e a estimativa de perda de dados, consulte Olá [tipos de failover](../../site-recovery/site-recovery-failover.md) tabela na recuperação de Site. Se você [preparar tooconnect tooAzure VMs após o failover](../../site-recovery/vmware-walkthrough-overview.md), você deve ser capaz de tooconnect toohello VM do Azure usando o RDP após o failover.

![][1]

## <a name="azure-site-recovery-components"></a>Componentes do Azure Site Recovery

Esses são componentes do Site Recovery Olá que são relevantes toothis cenário de migração.

* O **servidor de configuração** é uma VM do Azure que coordena a comunicação e gerencia os processos de recuperação e replicação de dados. Essa VM, você executará um servidor de configuração única instalação arquivos tooinstall hello e um componente adicional, chamado de servidor de processo, como um gateway de replicação. Leia sobre os [pré-requisitos do servidor de configuração](../../site-recovery/vmware-walkthrough-overview.md). Servidor de configuração só precisa toobe configurado uma vez e pode ser usado para todos os toohello de migrações mesma região.

* **Servidor de processo** é um gateway de replicação que recebe dados de replicação de origem VMs otimiza os dados de saudação com cache, a compactação e criptografia e o envia tooa conta de armazenamento. Também gerencia a instalação por push de toosource de serviço de mobilidade Olá VMs e executa a descoberta automática de máquinas virtuais de origem. servidor de processo saudação padrão está instalado no servidor de configuração de saudação. Você pode implantar autônomo adicionais processo servidores tooscale sua implantação. Leia sobre [práticas recomendadas para implantação de servidor de processo](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) e [implantação de servidores de processo adicionais](../../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Servidor de processo só precisa toobe configurado uma vez e pode ser usado para todos os toohello de migrações mesma região.

* **Serviço de mobilidade** é um componente que é implantado em cada máquina virtual padrão que você deseja tooreplicate. Captura gravações de dados Olá VM padrão e encaminha-toohello do servidor em processo. Leia sobre [Pré-requisitos de computadores replicados](../../site-recovery/vmware-walkthrough-overview.md).

Este gráfico mostra como esses componentes interagem.

![][15]

> [!NOTE]
> Recuperação de site não oferece suporte a migração de saudação de discos de espaços de armazenamento.

Para obter componentes adicionais para outros cenários, consulte muito[arquitetura de cenário](../../site-recovery/vmware-walkthrough-overview.md).

## <a name="azure-essentials"></a>Conceitos básicos do Azure

Esses são Olá requisitos do Azure para este cenário de migração.

* Uma assinatura do Azure
* Dados replicados de um toostore de conta de armazenamento do Azure Premium
* Uma rede virtual do Azure (VNet) de toowhich VMs se conectará quando eles são criados no failover. Olá VNet do Azure deve estar no hello mesma região como Olá um no qual Olá executa recuperação de Site
* Uma conta de armazenamento do Azure padrão nos logs de replicação que toostore. Isso pode ser Olá a mesma conta de armazenamento como discos de saudação VM que está sendo migrado

## <a name="prerequisites"></a>Pré-requisitos

* Entender componentes de cenário de migração relevantes Olá em Olá anterior seção
* Planejar o tempo de inatividade aprendendo sobre Olá [Failover na recuperação de Site](../../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Etapas de configuração e migração

Você pode usar a recuperação de Site toomigrate VMs Azure IaaS entre regiões ou na mesma região. Olá instruções a seguir foram todos adaptadas para este cenário de migração de artigo Olá [replicar máquinas virtuais do VMware ou servidores físicos tooAzure](../../site-recovery/vmware-walkthrough-overview.md). Siga os links de saudação para obter etapas detalhadas adicionais toohello instruções neste artigo.

1. **Crie um cofre de Serviços de Recuperação**. Criar e gerenciar Cofre de recuperação de Site Olá por meio de saudação [portal do Azure](https://portal.azure.com). Clique em **Novo** > **Backup** > **de Gerenciamento** e **Site Recovery (OMS)**. Como alternativa, você pode clicar em **Procurar** > **Cofres dos Serviços de Recuperação** > **Adicionar**. Máquinas virtuais serão replicadas toohello região que você especificar nesta etapa. Para fins de saudação de migração no hello mesma região, região hello selecione onde suas VMs de origem e contas de armazenamento de origem são. 

2. Olá etapas a seguir ajudam **escolha suas metas de proteção**.

    2a. No hello VM onde você deseja que o servidor de configuração tooinstall hello, abra Olá [portal do Azure](https://portal.azure.com). Vá muito**os cofres de serviços de recuperação** > **configurações**. Em **Configurações**, selecione **Site Recovery**. Em **Site Recovery**, selecione **Etapa 1: Preparar infraestrutura**. Em **Preparar infraestrutura**, selecione **Objetivo de proteção**.

    ![][2]

    2b. Em **objetivo de proteção**, no hello primeira lista suspensa, selecione **tooAzure**. Na lista suspensa da segunda hello, selecione **não virtualizados / outros**e, em seguida, clique em **Okey**.

    ![][3]

3. Olá etapas a seguir ajudam **configurar o ambiente de origem da saudação (servidor de configuração)**.

    3a. Baixar Olá **instalação unificado do Azure Site Recovery** e hello **chave de registro de cofre** por vai toohello **preparar infraestrutura**  >  **Origem preparar** > **Adicionar servidor** folha. Você precisará Olá configuração de Olá unificado de toorun chave de registro de cofre. chave de saudação é válida por 5 dias depois que ele é gerado.

    ![][4]

    3b. Adicionar servidor de configuração no hello **Adicionar servidor** folha.

    ![][5]

    3c. No hello VM que você está usando como servidor de configuração de Olá, execute o servidor de configuração do Unified instalação tooinstall hello e servidor de processo de saudação. Você pode percorrer capturas de tela de saudação [aqui](../../site-recovery/vmware-walkthrough-overview.md) toocomplete instalação de saudação. Você pode consultar toohello capturas de tela de etapas especificadas para esse cenário de migração a seguir.

    Em **antes de começar a**, selecione **instalar o servidor de configuração de saudação e servidor de processo**.

    ![][6]

    3d. Em **registro**, navegue e selecione a chave de registro de saudação baixado do cofre hello.

    ![][7]

    3e. Em **detalhes do ambiente**, selecione se você vai tooreplicate VMware VMs. Para esse cenário de migração, escolha **Não**.

    ![][8]

    3f. Após a conclusão da instalação hello, você verá Olá **o servidor de configuração do Microsoft Azure Site Recovery** janela. Use Olá **gerenciar contas** guia conta Olá toocreate recuperação de Site pode usar para a descoberta automática. (Cenário Olá sobre como proteger máquinas físicas, configurando Olá conta não é relevante, mas você precisa de pelo menos uma conta tooenable um de saudação etapas a seguir. Nesse caso, você pode nomear conta hello e a senha como qualquer.) Saudação de uso **registro do cofre** o arquivo de credencial de cofre do guia tooupload hello.

    ![][9]

4. **Configurar o ambiente de destino Olá**. Clique em **preparar infraestrutura** > **destino**e especifique o modelo de implantação de saudação desejar toouse para máquinas virtuais depois do failover. Você pode escolher **Clássico** ou **Gerenciador de recursos**, dependendo do cenário.

    ![][10]

    A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis. Observe que, se você estiver usando uma conta de armazenamento Premium para os dados replicados, você precisa tooset backup uma replicação toostore da conta de armazenamento padrão logs.

5. **Defina as configurações de replicação**. Siga [definir as configurações de replicação](../../site-recovery/vmware-walkthrough-overview.md) tooverify que seu servidor de configuração está associado com a política de replicação Olá criar com êxito.

6. **Planejamento de capacidade**. Saudação de uso [Planejador de capacidade](../../site-recovery/site-recovery-capacity-planner.md) tooaccurately largura de banda de rede de estimativa, armazenamento e outros requisitos toomeet as necessidades de sua replicação. Quando terminar, selecione **Sim** em **Você concluiu o planejamento da capacidade?**.

    ![][11]

7. Olá etapas a seguir ajudam **instalar serviço de mobilidade e habilitar a replicação**.

    7a. Você pode escolher muito[instalação por push](../../site-recovery/vmware-walkthrough-overview.md) tooyour fonte VMs ou muito[instalar manualmente o serviço de mobilidade](../../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) em sua fonte de VMs. Você pode encontrar o requisito de saudação da instalação de envio e o caminho de saudação do instalador manual Olá Olá link fornecido. Se você estiver fazendo uma instalação manual, talvez seja necessário toouse um IP endereço toofind Olá configuração servidor interno.

    ![][12]

    Olá failover VM terá dois discos temporários: um do hello primário VM e hello outros criado durante a saudação provisionamento de VM na região de recuperação hello. tooexclude Olá temporário em disco antes da replicação, instale o serviço de mobilidade de saudação antes de habilitar a replicação. toolearn mais informações sobre como tooexclude Olá disco temporário, consulte muito[excluir discos de replicação](../../site-recovery/vmware-walkthrough-overview.md).

    7b. Agora habilite a replicação da seguinte maneira:
      * Clique em **Replicar aplicativo** > **Origem**. Depois de habilitar a replicação para Olá primeira vez, clique em + replicar em replicação de tooenable Olá cofre para outras máquinas.
      * Na etapa 1, configure Fonte como o servidor de processo.
      * Na etapa 2, especifique o modelo de implantação do hello após o failover, um toomigrate de conta de armazenamento Premium para, logs de toosave de uma conta de armazenamento padrão e toofail uma rede virtual para.
      * Na etapa 3, adicionar as VMs protegidas pelo endereço IP (talvez seja necessário um toofind de endereço IP interno-los).
      * Na etapa 4, configure propriedades Olá selecionando contas Olá configurado anteriormente no servidor de processo hello.
      * Na etapa 5, escolha a política de replicação Olá criado anteriormente, definir as configurações de replicação.
      Clique em **OK** e habilite a replicação.

    > [!NOTE]
    > Quando uma VM do Azure é desalocada e iniciada novamente, não há nenhuma garantia de que ele receberá Olá mesmo endereço IP. Se o endereço IP de saudação do servidor de processo do servidor de configuração de saudação ou Olá protegido alteração de VMs do Azure, replicação Olá esse cenário pode não funcionar corretamente.

    ![][13]

    Ao criar seu ambiente de Armazenamento do Azure, é recomendável usar contas de armazenamento separadas para cada VM em um conjunto de disponibilidade. É recomendável que você siga a prática recomendada Olá Olá camada de armazenamento muito[usar várias contas de armazenamento para cada conjunto de disponibilidade](../../virtual-machines/windows/manage-availability.md). Distribuição de contas de armazenamento de toomultiple de discos VM ajuda a disponibilidade de armazenamento tooimprove e distribui hello e/s na infra-estrutura de armazenamento do Azure de saudação. Se suas VMs estiverem em um conjunto de disponibilidade, em vez de replicar discos de todas as VMs em uma conta de armazenamento, é altamente recomendável migrar várias VMs várias vezes, para que Olá de Olá VMs no mesmo conjunto de disponibilidade não compartilham uma única conta de armazenamento. Saudação de uso **habilitar replicação** tooset folha uma conta de armazenamento de destino para cada VM, um de cada vez. Você pode escolher um modelo de implantação após o failover de acordo com a necessidade de tooyour. Se você escolher o Gerenciador de recursos (RM) como seu modelo de implantação após o failover, você pode fazer failover tooan uma VM do RM RM VM ou failover um tooan VM clássico RM VM.

8. **Execute um teste de failover**. toocheck se a replicação for concluída, clique em seu Site de recuperação e, em seguida, clique em **configurações** > **itens duplicados**. Você verá o status de saudação e a porcentagem de seu processo de replicação. Após a replicação inicial é concluída, execute toovalidate de Failover de teste sua estratégia de replicação. Para obter etapas detalhadas de failover de teste, consulte muito[executar um failover de teste na recuperação de Site](../../site-recovery/vmware-walkthrough-overview.md). Você pode ver o status de saudação do failover de teste em **configurações** > **trabalhos** > **YOUR_FAILOVER_PLAN_NAME**. Na folha de saudação, você verá uma análise das etapas de saudação e resultados de êxito/falha. Se o failover de teste de Olá falhar em qualquer etapa, clique em mensagem de erro Olá etapa toocheck hello. Certifique-se de que sua estratégia de replicação e VMs atende aos requisitos de saudação antes de executar um failover. Leitura [tooAzure de Failover de teste na recuperação de Site](../../site-recovery/site-recovery-test-failover-to-azure.md) para obter mais informações e instruções de failover de teste.

9. **Executar um failover**. Após a conclusão do failover de teste Olá, execute um failover toomigrate tooPremium seus discos armazenamento e replicar as instâncias VM hello. Siga Olá detalhadas etapas [executar um failover](../../site-recovery/site-recovery-failover.md#run-a-failover). Verifique se você selecionou **desligar máquinas virtuais e sincronize os dados mais recentes Olá** toospecify que recuperação de Site deve tente tooshut para baixo VMs Olá protegido e sincronizar dados de saudação para que hello versão mais recente dos dados hello será submetida a failover. Se você não selecionar essa opção ou Olá tentativa não for bem-sucedida Olá failover serão do hello mais recente ponto de recuperação disponível para Olá VM. Recuperação de site irá criar uma instância de VM cujo tipo é hello iguais ou semelhante tooa VM compatíveis com armazenamento Premium. Você pode verificar o desempenho de saudação e o preço de várias instâncias VM indo muito[preços de máquinas virtuais do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) ou [preços de máquinas virtuais Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Etapas pós-migração

1. **Configurar a disponibilidade de toohello VMs replicada definida se aplicável**. Recuperação de site não oferece suporte para migração de VMs junto com o conjunto de disponibilidade de saudação. Dependendo da implantação de saudação da VM replicada, siga um destes procedimentos hello:
  * Para uma máquina virtual criada usando o modelo de implantação clássico Olá: Adicionar Olá VM toohello conjunto de disponibilidade no hello portal do Azure. Para obter etapas detalhadas, consulte muito[adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](../../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Para o modelo de implantação do Gerenciador de recursos de saudação: salvar sua configuração de saudação VM e, em seguida, exclua e crie novamente o hello VMs no conjunto de disponibilidade de saudação. toodo assim, use o script hello em [definida do Azure Resource Manager VM conjunto de disponibilidade](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Verifique a limitação de saudação do script e planejar o tempo de inatividade antes de executar o script hello.

2. **Exclua VMs e discos antigos**. Antes de excluir esses, verifique se os discos de Premium Olá são consistentes com os discos de origem e hello que novas VMs executam Olá mesmo funcionar como fonte de saudação VMs. No modelo de implantação do Gerenciador de recursos (RM) hello, exclua Olá VM e excluir discos Olá de suas contas de armazenamento de origem no hello portal do Azure. No modelo de implantação clássico Olá, você pode excluir hello VM e discos no portal clássico do hello ou o portal do Azure. Se houver um problema no qual Olá disco não será excluído mesmo que você excluiu Olá VM, consulte [solucionar problemas de erros quando você excluir VHDs](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Infraestrutura do Azure Site Recovery Olá limpa**. Se a recuperação de Site não é mais necessário, você poderá limpar sua infraestrutura de excluindo itens replicados, servidor de configuração de saudação e Olá diretiva de recuperação e, em seguida, excluir o cofre do Azure Site Recovery hello.

## <a name="troubleshooting"></a>Solucionar problemas

* [Monitorar e solucionar problemas de proteção para máquinas virtuais e sites físicos](../../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Fórum do Microsoft Azure Site Recovery](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Próximas etapas

Consulte Olá recursos para cenários específicos para migrar máquinas virtuais a seguir:

* [Migrar Máquinas Virtuais do Azure entre as Contas de Armazenamento](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Criar e carregar um VHD do Windows Server tooAzure.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migração de máquinas virtuais do Amazon AWS tooMicrosoft do Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Além disso, consulte Olá recursos toolearn mais sobre o armazenamento do Azure e máquinas virtuais do Azure a seguir:

* [Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Máquinas Virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
