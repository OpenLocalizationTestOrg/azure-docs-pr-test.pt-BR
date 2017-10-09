---
title: "aaaSet a origem de saudação e de destino para tooAzure de replicação do Hyper-V (sem o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de armazenamento de tooAzure de VMs Hyper-V com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Etapa 8: Configurar a origem de saudação e de destino para tooAzure de replicação do Hyper-V

Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de máquinas virtuais (sem o System Center VMM) do Hyper-V, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar site Olá Hyper-V, instale hello provedor Azure Site Recovery e o agente de serviços de recuperação do Azure Olá nos hosts Hyper-V e registrar site Olá no cofre de saudação.

1. Em **Preparar a infraestrutura**, clique em **Origem**. Clique em um novo site de Hyper-V como um contêiner para seus hosts Hyper-V ou clusters de tooadd **+ Site Hyper-V**.

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. Em **site Hyper-V criar**, especifique um nome para o site de saudação. Em seguida, clique em **OK**. Agora, selecione o site Olá você criou e clique em **+ servidor Hyper-V** tooadd um site de toohello do servidor.

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. Em **Adicionar Servidor** > **Tipo de servidor**, verifique se **Servidor Hyper-V** é exibido.

    - Verifique se o servidor Olá Hyper-V você deseja tooadd está em conformidade com hello [pré-requisitos](#on-premises-prerequisites), e é capaz de tooaccess Olá URLs especificadas.
    - Baixe o arquivo de instalação do provedor Azure Site Recovery hello. Executar este Olá tooinstall do arquivo provedor e Olá agente de serviços de recuperação em cada host Hyper-V.

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Instalar hello provedor e agente

1. Execute o arquivo de instalação do provedor de saudação em cada host que você adicionou site toohello Hyper-V. Se você estiver instalando em um cluster do Hyper-V, execute a instalação em cada nó de cluster. Instalar e registrar cada nó de cluster do Hyper-V garante que as VMs estarão protegidas, mesmo se migrarem entre nós.
2. No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.
3. Em **instalação**, aceite ou modifique o local de instalação do provedor de padrão de saudação e clique em **instalar**.
4. Em **as configurações do cofre**, clique em **procurar** tooselect Olá cofre arquivo de chave que você baixou. Especifique a assinatura do Azure Site Recovery Olá, nome do cofre Olá, e Olá Hyper-V site toowhich Olá Hyper-V servidor pertence.

    ![Registros do servidor](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. Em **as configurações de Proxy**, especifique como Olá tooAzure recuperação de Site se conecta de provedor em execução em hosts Hyper-V em Olá da internet.

    * Se você quiser Olá provedor tooconnect diretamente selecione **se conectar diretamente tooAzure recuperação de Site sem um proxy**.
    * Se o proxy existente exige autenticação ou deseja toouse um proxy personalizado para conexão de provedor hello, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.
    * Se você usar um proxy:
        - Especificar credenciais, porta e endereço Olá
        - Criar URLs de saudação se descrito em Olá [pré-requisitos](#prerequisites) são permitidas por meio do proxy de saudação.

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Após a conclusão da instalação, clique em **registrar** tooregister servidor de saudação no cofre hello.

    ![Local de instalação](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Após a conclusão do registro, os metadados do servidor de saudação Hyper-V são recuperados pelo Azure Site Recovery e saudação do servidor é exibida no **infra-estrutura de recuperação de Site** > **Hosts Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Especifique a conta de armazenamento do Azure Olá para replicação e Olá toowhich de rede do Azure VMs do Azure irão se conectar após o failover.

1. Clique em **Preparar a Infraestrutura** > **Destino**.
2. Selecione a assinatura de saudação e grupo de recursos de saudação no qual você deseja toocreate Olá VMs do Azure após o failover. Escolha deployment Olá modelo que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá VMs.

3. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

    - Se você não tiver uma conta de armazenamento, clique em **+ armazenamento** toocreate embutido uma conta baseada no Gerenciador de recursos. 
    - Se você não tiver uma rede do Azure, clique em **+ rede** toocreate embutido um Gerenciador de recursos de rede.






## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 9: configurar uma política de replicação](hyper-v-site-walkthrough-replication.md)
