---
title: "Configurar o ambiente de origem da saudação (VMware tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooset o seu toostart do ambiente local replicando o VMware virtual máquinas tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Configurar o ambiente de origem da saudação (tooAzure VMware)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-set-up-physical-to-azure.md)

Este artigo descreve como tooset o seu toostart do ambiente local replicando virtual máquinas em execução no VMware tooAzure.

## <a name="prerequisites"></a>Pré-requisitos

artigo de saudação pressupõe que você já tenha criado:
- Um cofre de serviços de recuperação Olá [portal do Azure](http://portal.azure.com "portal do Azure").
- Uma conta dedicada no seu VMware vCenter que pode ser usada para [descoberta automática](./site-recovery-vmware-to-azure.md).
- Uma máquina virtual no qual servidor de configuração de saudação tooinstall.

## <a name="configuration-server-minimum-requirements"></a>Requisitos mínimos do servidor de configuração
software de servidor de configuração de saudação deve ser implantado em uma máquina virtual de VMware altamente disponível. Olá a tabela a seguir lista o hardware mínimo hello, software e requisitos de rede para um servidor de configuração.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Servidores proxy baseado em HTTPS não são suportados pelo servidor de configuração de saudação.

## <a name="choose-your-protection-goals"></a>Escolher as metas de proteção

1. No portal do Azure de Olá, vá toohello **dos serviços de recuperação** cofre folha e selecione seu cofre.
2. No menu de recursos de saudação do cofre hello, ir muito**Introdução** > **recuperação de Site** > **etapa 1: preparar a infraestrutura**  >  **Objetivo de proteção**.

    ![Escolher metas](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. Em **objetivo de proteção**, selecione **tooAzure**e escolha **Sim, com VMware vSphere hipervisor**. Em seguida, clique em **OK**.

    ![Escolher metas](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá
Configurando o ambiente de origem Olá envolve duas atividades principais:

- Instalar e registrar um servidor de configuração com o Site Recovery.
- Descobrir máquinas virtuais locais conectando o Site Recovery tooyour local VMware vCenter ou vSphere EXSi hosts.

### <a name="step-1-install-and-register-a-configuration-server"></a>Etapa 1: Instalar e registrar um servidor de configuração

1. Clique em **Etapa 1: Preparar a Infraestrutura** > **Origem**. Em **preparar fonte**, se você não tiver um servidor de configuração, clique em **+ servidor de configuração** tooadd um.

    ![Configurar origem](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. Em Olá **Adicionar servidor** folha, verifique se **servidor de configuração** aparece na **tipo de servidor**.
4. Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.
5. Baixe a chave de registro de cofre hello. Você precisa chave de registro de hello quando você executa a instalação unificado. chave de saudação é válida por cinco dias depois que ele é gerado.

    ![Configurar origem](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. No computador de saudação estiver usando como o servidor de configuração hello, execute **instalação unificado do Azure Site Recovery** mestre de Olá, servidor de processo Olá e servidor de configuração de saudação tooinstall o servidor de destino.

#### <a name="run-azure-site-recovery-unified-setup"></a>Executar a Configuração Unificada do Azure Site Recovery

> [!TIP]
> Registro do servidor de configuração falhará se o tempo de saudação no relógio do sistema do computador difere da hora local em mais de cinco minutos. Sincronizar o relógio do sistema com uma [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de saudação.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> servidor de configuração de saudação pode ser instalado por meio da linha de comando. Para obter mais informações, consulte [instalar servidor de configuração de saudação usando as ferramentas de linha de comando](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Adicionar conta de VMware Olá para descoberta automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Etapa 2: Adicionar um vCenter
tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente local, você precisará tooconnect o VMware vCenter Server ou hosts de ESXi vSphere com a recuperação de Site.

Selecione **+ vCenter** toostart conectando um VMware vCenter server ou um host do VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Problemas comuns
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Próximas etapas
[Configurar o ambiente de destino](./site-recovery-prepare-target-vmware-to-azure.md) no Azure.
