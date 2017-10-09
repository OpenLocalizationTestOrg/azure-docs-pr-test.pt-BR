---
title: "aaaSet a origem de saudação e de destino para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset até a fonte de saudação e de destino quando replicar máquinas virtuais do Hyper-V toosecondary VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Etapa 6: Configurar o destino e origem da replicação Olá


Depois de criar serviços de recuperação de um cofre para o Hyper-V replicação tooa VMM site secundário com [do Azure Site Recovery](site-recovery-overview.md), use este artigo tooset fonte hello e locais de replicação de destino. 

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Instale Olá provedor Azure Site Recovery em servidores do VMM e descobrir e registrar servidores no cofre de saudação.

1. Clique em **Etapa 1: Preparar a Infraestrutura** > **Origem**.

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. Em **preparar fonte**, clique em **+ VMM** tooadd um servidor do VMM.

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. Em **Adicionar servidor**, verifique se **servidor do System Center VMM** aparece na **tipo de servidor** e servidor do VMM Olá atende Olá [pré-requisitos](#prerequisites).
4. Baixe o arquivo de instalação do provedor Azure Site Recovery hello.
5. Baixe a chave de registro de saudação. Você precisará dela quando executar a instalação. chave de saudação é válida por cinco dias depois que ele é gerado.

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Instale Olá provedor Azure Site Recovery no servidor do VMM hello. Você não precisa tooexplicitly instalar nada nos servidores de host do Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Instalar Olá provedor Azure Site Recovery

1. Execute o arquivo de instalação do provedor de saudação em cada servidor do VMM. Se o VMM for implantado em um cluster, a seguir Olá Olá primeira vez que você instala:
    -  Instalar o provedor de saudação em um nó ativo e concluir o servidor do VMM Olá instalação tooregister Olá no cofre hello.
    - Em seguida, instale Olá provedor em Olá outros nós. Nós de cluster devem todos executados Olá mesma versão do provedor de saudação.
2. A instalação executa algumas verificações de pré-requisitos e solicitações permissão toostop saudação do serviço do VMM. saudação de serviço do VMM será reiniciada automaticamente quando a instalação for concluída. Se você instalar em um cluster do VMM, você está função de Cluster Olá toostop solicitada.
3. Em **Microsoft Update**, você pode aceitar toospecify que provedor serão instaladas de acordo com a política do Microsoft Update.
4. Em **instalação**, aceite ou modifique o local de instalação padrão hello e clique em **instalar**.

    ![Local de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Após a conclusão da instalação, clique em **registrar** tooregister servidor de saudação no cofre hello.

    ![Local de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. Em **nome do cofre**, verificar nome de saudação do cofre Olá quais saudação servidor será registrado. Clique em *Avançar*.

    ![Registros do servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. Em **Conexão de Internet**, especifique como o provedor de saudação em execução no servidor do VMM Olá se conecta tooAzure.

    ![Configurações da Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Você pode especificar o provedor Olá deve se conectar diretamente toohello internet, ou por meio de um proxy.
   - Especifique as configurações de proxy, se necessário.
   - Se você usar um proxy, uma conta de RunAs VMM (DRAProxyAccount) é criada automaticamente Olá especificado, usando as credenciais do proxy. Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito. Olá configurações da conta executar como podem ser modificadas no console do VMM hello > **configurações** > **segurança** > **contas executar como**. Reinicie a alterações de tooupdate de serviço do VMM hello.
8. Em **chave de registro**, selecione chave Olá que você baixou do Azure Site Recovery e copiou toohello o servidor do VMM.
9. configuração de criptografia de saudação é usada apenas quando você estiver replicando máquinas virtuais do Hyper-V no tooAzure de nuvens do VMM. Se você estiver replicando o site secundário tooa não é usado.
10. Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello. Em uma configuração de cluster, especifique nome de função de cluster saudação do VMM.
11. Em **sincronizar metadados de nuvem**, selecione se deseja toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello. Essa ação precisa apenas toohappen uma vez em cada servidor. Se você não quiser toosynchronize todas as nuvens, deixe essa configuração desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello.
12. Clique em **próximo** toocomplete processo de saudação. Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery. saudação do servidor é exibida em Olá **servidores VMM** guia Olá **servidores** página no cofre hello.

    ![Servidor](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Depois que o servidor hello está disponível no console de recuperação de Site Olá, em **fonte** > **preparar fonte** Selecionar servidor do VMM hello e nuvem Olá selecione em quais Olá Hyper-V host está localizado. Em seguida, clique em **OK**.

Você também pode instalar o provedor Olá Olá linha de comando:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Selecione a nuvem e o servidor do VMM de destino hello:

1. Clique em **preparar infraestrutura** > **destino**e servidor do VMM de destino select Olá toouse desejado.
2. Nuvens no servidor de saudação que são sincronizadas com a recuperação de Site serão exibidas. Selecione a nuvem de destino hello.

   ![Destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 7: Configurar mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md).
