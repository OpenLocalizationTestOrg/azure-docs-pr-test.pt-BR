---
title: " Gerenciar um servidor de processo em execução em Azure(Classic) | Microsoft Docs"
description: Este artigo descreve como tooset backup um failback Server(Classic) do processo no Azure.
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Gerenciar um servidor de processo em execução no Azure (clássico)
> [!div class="op_single_selector"]
> * [Azure Clássico ](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Gerenciador de Recursos](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Durante o failback, é recomendável toodeploy servidor de processo no Azure se houver alta latência entre hello rede Virtual do Azure e sua rede local. Este artigo descreve como você pode configurar, configurar e gerenciar servidores de processo Olá em execução no Azure.

> [!NOTE]
> Este artigo é toobe usado se você usou clássico como modelo de implantação de saudação para máquinas virtuais de saudação durante o failover. Se você usou o Gerenciador de recursos como Olá implantação modelo siga Olá etapas [como tooset up e configurar um servidor de processo de Failback (Gerenciador de recursos)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Implantar um Servidor de Processos no Azure

1. No Azure Marketplace, criar uma máquina virtual usando Olá **V2 de servidor do Microsoft Azure Site Recovery processo** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Certifique-se de que você selecione o modelo de implantação hello como **clássico** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. No Assistente de máquina virtual de criar hello > configurações básicas, certifique-se de selecionar Olá toowhere assinatura e local de failover de máquinas virtuais de saudação.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Certifique-se de que a máquina virtual hello está conectada Olá de toowhich de rede Virtual do Azure toohello failover da máquina virtual está conectado.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Depois que a máquina de virtual do servidor de processo Olá é provisionada, você precisa toolog no e registrá-lo com hello servidor de configuração.

> [!NOTE]
> toouse capaz de toobe este servidor de processo para failback, você precisa tooregistê-lo com o servidor de configuração local hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Saudação (em execução no Azure) do servidor de processo tooa (executado no local) do servidor de configuração de registro

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Saudação do servidor em processo toolatest a versão da atualização.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Olá Cancelando o registro do servidor de processo (em execução no Azure) de um servidor de configuração (executado no local)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
