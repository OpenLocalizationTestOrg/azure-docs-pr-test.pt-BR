---
title: "aaaSet a origem de saudação e de destino para VMware tooAzure de replicação com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de máquinas virtuais do VMware tooAzure armazenamento com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Etapa 8: Configurar a origem de saudação e de destino para VMware tooAzure de replicação

Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de máquinas virtuais VMware, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar o servidor de configuração de hello, registrá-lo no cofre hello e descobrir máquinas virtuais.

1. Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.
2. Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.
3. Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.
4. Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.
5. Baixe a chave de registro de cofre hello. Você precisará dela quando executar a Configuração Unificada. chave de saudação é válida por cinco dias depois que ele é gerado.

   ![Configurar origem](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Registrar o servidor de configuração de saudação no cofre Olá

Seguinte Olá antes de iniciar, em seguida executar instalação unificado tooinstall Olá configuração server, Olá processo server e o servidor de destino mestre hello.
    - Obter uma rápida visão geral em vídeo

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - No servidor de configuração de saudação VM, certifique-se de que o relógio do sistema hello está sincronizado com um [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Ele deve ser correspondente. Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.
    - Execute a instalação como Administrador Local no servidor de configuração de saudação VM.
    - Certifique-se de que TLS 1.0 está ativado Olá VM.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> também pode ser instalado o servidor de configuração de saudação [da linha de comando Olá](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>Conectar servidores tooVMware

tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente local, você precisará tooconnect o VMware vCenter Server ou hosts de ESXi vSphere com a recuperação de Site. Observe o seguinte Olá antes de começar:

- Se você adicionar o servidor do vCenter hello ou vSphere hosts tooSite recuperação com uma conta sem privilégios de administrador no servidor de saudação, conta de Olá precisa desses privilégios habilitados:
    - Datacenter, Repositório de Dados, Pasta, Host, Rede, Recurso, Máquina Virtual, vSphere Distributed Switch.
    - servidor do vCenter Olá precisa de permissões de exibições de armazenamento.
- Quando você adiciona servidores de VMware tooSite recuperação, pode levar 15 minutos ou mais para que eles tooappear no portal de saudação.

### <a name="add-hello-account-for-automatic-discovery"></a>Adicionar conta Olá para descoberta automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Configurar uma conexão

Conecte-se tooservers da seguinte maneira:

1. Selecione **+ vCenter** toostart conectando um VMware vCenter server ou um host do VMware vSphere ESXi.
2. Em **adicionar vCenter**, especifique um nome amigável para o servidor de host ou vCenter vSphere hello e em seguida, especifique o endereço IP hello ou FQDN do servidor de saudação.
3. Deixe a porta hello como 443, a menos que os servidores do VMware são toolisten configurada para solicitações em uma porta diferente. Selecione a conta Olá tooconnect toohello VMware vCenter ou vSphere ESXi server. Clique em **OK**.
4. Recuperação de site se conecta a servidores tooVMware usar Olá especificado as configurações e descobre máquinas virtuais.

> [!NOTE]
> Se você estiver adicionando um servidor ou host com uma conta que não tem privilégios de administrador no servidor de host ou vCenter Olá, certifique-se de que conta Olá tem esses privilégios habilitados: Datacenter repositório de dados, pasta, Host, rede, o recurso de máquina Virtual, e vSphere comutador distribuída. Além disso, Olá VMware vCenter server precisa de exibições de armazenamento Olá privilégio habilitado.


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Antes de configurar o ambiente de destino hello, verifique se que você tem uma conta de armazenamento do Azure e a configuração da rede virtual.

1. Clique em **preparar infraestrutura** > **destino**, e selecione Olá assinatura do Azure que você deseja toouse.
2. Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.
3. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

   ![Destino](./media/vmware-walkthrough-source-target/gs-target.png)
4. Se você não tiver criado uma conta de armazenamento ou de rede, clique em **+ conta de armazenamento** ou **+ rede**, toocreate embutido de rede ou a conta de um Gerenciador de recursos.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 9: configurar uma política de replicação](vmware-walkthrough-replication.md)
