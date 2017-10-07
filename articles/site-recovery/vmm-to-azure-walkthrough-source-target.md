---
title: "aaaSet a origem de saudação e de destino para tooAzure de replicação do Hyper-V (com o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de máquinas virtuais do Hyper-V no armazenamento de tooAzure de nuvens do VMM com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Etapa 8: Configurar a origem de saudação e de destino para tooAzure de replicação do Hyper-V (com o VMM)

Depois de [criar um cofre](vmm-to-azure-walkthrough-create-vault.md) e especificar o que você deseja tooreplicate, usar esta fonte de tooconfigure de artigo e configurações de destino durante a replicação de máquinas virtuais de Hyper-V no local no System Center Virtual Machine Manager (VMM) tooAzure de nuvens, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

S1. Clique em **Preparar a Infraestrutura** > **Origem**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. Em **preparar fonte**, clique em **+ VMM** tooadd um servidor do VMM.

    ![Configurar origem](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. Em **Adicionar servidor**, verifique se **servidor do System Center VMM** aparece na **tipo de servidor** e servidor do VMM Olá atende Olá [pré-requisitos e URL requisitos de](#prerequisites).
4. Baixe o arquivo de instalação do provedor Azure Site Recovery hello.
5. Baixe a chave de registro de saudação. Você precisará dela quando executar a instalação. chave de saudação é válida por cinco dias depois que ele é gerado.

    ![Configurar origem](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Instalar Olá provedor no servidor do VMM Olá

1. Execute o arquivo de instalação do provedor Olá no servidor do VMM hello.
2. No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.
3. Em **instalação**, aceite ou modifique o local de instalação do provedor de padrão de saudação e clique em **instalar**.

    ![Local de instalação](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Quando a instalação for concluída, clique em **registrar** servidor do VMM Olá tooregister no cofre hello.
5. Em Olá **as configurações do cofre** , clique em **procurar** tooselect arquivo de chave do Cofre de saudação. Especifique a assinatura do Azure Site Recovery hello e nome do cofre hello.

    ![Registros do servidor](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. Em **Conexão de Internet**, especifique como Olá provedor em execução no servidor do VMM Olá conectará tooSite recuperação sobre Olá da internet.

   * Se você desejar Olá provedor tooconnect diretamente, selecione **se conectar diretamente tooAzure recuperação de Site sem um proxy**.
   * Se o proxy existente exige autenticação ou deseja toouse um proxy personalizado, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.
   * Se você usar um proxy personalizado, especifique as credenciais, porta e endereço de saudação.
   * Se você estiver usando um proxy, você deve ter já Olá URLs permitidas descritos em [pré-requisitos](#on-premises-prerequisites).
   * Se você usar um proxy personalizado, uma conta de RunAs VMM (DRAProxyAccount) será criada automaticamente Olá especificado, usando as credenciais do proxy. Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito. configurações de conta de RunAs VMM Olá podem ser modificadas no console do VMM hello. Em **configurações**, expanda **segurança** > **contas executar como**e, em seguida, modificar a senha Olá para DRAProxyAccount. O serviço VMM toorestart hello, será necessário para que essa configuração tenha efeito.

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Aceite ou modifique o local de saudação de um certificado SSL que é gerado automaticamente para a criptografia de dados. Este certificado será usado se você habilitar a criptografia de dados para uma nuvem protegida pelo Azure no portal do Azure Site Recovery hello. Mantenha esse certificado protegido. Quando você executa um failover tooAzure você precisará dele toodecrypt, se a criptografia de dados está habilitada.
8. Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello. Em uma configuração de cluster, especifique o nome de função de cluster saudação do VMM.
9. Habilitar **sincronizar metadados de nuvem**, se você quiser toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello. Essa ação precisa apenas toohappen uma vez em cada servidor. Se você não quiser toosynchronize todas as nuvens, você pode deixar essa configuração está desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello. Clique em **registrar** toocomplete processo de saudação.

    ![Registros do servidor](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. O registro é iniciado. Após a conclusão do registro, o servidor de saudação é exibido na **infra-estrutura de recuperação de Site** > **servidores VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Instalar o agente de serviços de recuperação do Azure Olá nos hosts Hyper-V

1. Depois de configurar Olá provedor, você precisa arquivo de instalação toodownload Olá para agente de serviços de recuperação do Azure hello. Execute a instalação em cada servidor Hyper-V Olá nuvem do VMM.

    ![Sites do Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. Em **Verificação de Pré-requisitos**, clique em **Avançar**. Quaisquer pré-requisitos faltantes serão instalados automaticamente.

    ![Agente de Serviços de Recuperação de Pré-requisitos](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. Em **configurações de instalação**, aceite ou modifique o local de instalação hello e Olá cache local. Você pode configurar o cache de saudação em uma unidade que tenha pelo menos 5 GB de armazenamento disponível, mas é recomendável uma unidade de cache com 600 GB ou mais de espaço livre. Em seguida, clique em **Instalar**.
4. Após a conclusão da instalação, clique em **fechar** toofinish.

    ![Registrar o Agente MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Instalação de linha de comando
Você pode instalar Olá Microsoft Azure Recovery Services Agent na linha de comando usando o comando a seguir de saudação:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurar tooSite de acesso de proxy de internet recuperação a partir de hosts Hyper-V

Agente de serviços de recuperação de saudação em execução em hosts do Hyper-V precisa tooAzure de acesso à internet para replicação de VM. Se você estiver acessando Olá internet através de um proxy, configurá-lo da seguinte maneira:

1. Abra o snap-in MMC do Backup do Microsoft Azure de saudação no host do Hyper-V hello. Por padrão, um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Olá snap-in, clique em **alterar propriedades**.
3. Em Olá **configuração de Proxy** especifique as informações do servidor proxy.

    ![Registrar o Agente MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Verifique que o agente Olá pode alcançar Olá URLs descritos em Olá [pré-requisitos](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá
Especifique Olá toobe de conta de armazenamento do Azure usado para replicação e Olá toowhich de rede do Azure VMs do Azure irão se conectar após o failover.

1. Clique em **preparar infraestrutura** > **destino**, selecione a assinatura hello e Olá onde você deseja toocreate Olá failover de máquinas virtuais do grupo de recursos. Escolha o modelo de implantação de saudação que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá máquinas virtuais com failover.

    ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

    ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Se você não tiver criado uma conta de armazenamento, e você desejar toocreate um usando o Gerenciador de recursos, clique em **+ conta de armazenamento** toodo que embutido.  Em Olá **criar conta de armazenamento** folha especificar um nome de conta, tipo, assinatura e local. Olá conta deve ser no hello Cofre de serviços de recuperação do mesmo local que hello.

   ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Se você quiser toocreate uma conta de armazenamento usando o modelo clássico hello, use Olá portal do Azure. [Saiba mais](../storage/common/storage-create-storage-account.md)
   * Se você estiver usando uma conta de armazenamento premium para os dados replicados, configure uma conta de armazenamento padrão, os logs de replicação toostore capturam alterações contínuas tooon de dados locais.
5. Se você não tiver criado uma rede do Azure, e você desejar toocreate um usando o Gerenciador de recursos, clique em **+ rede** toodo que embutido. Em Olá **criar rede virtual** folha especificar um nome de rede, intervalo de endereços, detalhes de sub-rede, assinatura e local. rede Olá deve estar no hello Cofre de serviços de recuperação do mesmo local que hello.

   ![Rede](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Se você quiser toocreate uma rede usando o modelo clássico hello, use Olá portal do Azure. [Saiba mais](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 9: Configurar mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md)
