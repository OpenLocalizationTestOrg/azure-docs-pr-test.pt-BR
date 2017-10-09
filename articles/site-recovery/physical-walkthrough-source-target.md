---
title: "aaaSet a origem de saudação e de destino para tooAzure de replicação de servidor físico com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de armazenamento de tooAzure servidores físicos com hello serviço Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Etapa 7: Configurar a origem de saudação e de destino para tooAzure de replicação de servidor físico

Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de servidores físicos, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar o servidor de configuração de hello, registrá-lo no cofre hello e descobrir máquinas.

1. Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.
2. Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.
3. Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.
4. Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.
5. Baixe a chave de registro de cofre hello. Você precisará dela quando executar a Configuração Unificada. chave de saudação é válida por cinco dias depois que ele é gerado.

   ![Configurar origem](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Registrar o servidor de configuração de saudação no cofre Olá

Seguinte Olá antes de iniciar, em seguida executar instalação unificado tooinstall Olá configuração server, Olá processo server e o servidor de destino mestre hello. Olá vídeo descreve como configurar componentes Olá para replicação de tooAzure de VM do VMware. No entanto, hello mesmo processo é válido para a replicação tooAzure servidor físico.

- No servidor de configuração de saudação VM, certifique-se de que o relógio do sistema hello está sincronizado com um [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Ele deve ser correspondente. Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.
- Execute a instalação como um administrador Local no computador do servidor de configuração de saudação.
- Certifique-se de que TLS 1.0 está ativado Olá VM.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> também pode ser instalado o servidor de configuração de saudação [da linha de comando Olá](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Antes de configurar o ambiente de destino hello, verifique se que você tem uma conta de armazenamento do Azure e a configuração da rede virtual.

1. Clique em **preparar infraestrutura** > **destino**, e selecione Olá assinatura do Azure que você deseja toouse.
2. Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.
3. A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

   ![Destino](./media/physical-walkthrough-source-target/gs-target.png)

4. Se você não tiver criado uma conta de armazenamento ou de rede, clique em **+ conta de armazenamento** ou **+ rede**, toocreate embutido de rede ou a conta de um Gerenciador de recursos.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 8: configurar uma política de replicação](physical-walkthrough-replication.md)
