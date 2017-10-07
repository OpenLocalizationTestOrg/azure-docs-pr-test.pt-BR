---
title: " Gerenciar um servidor de processo em execução no Azure (Gerenciador de Recursos) | Microsoft Docs"
description: Este artigo descreve como tooset backup um failback processo server (Gerenciador de recursos) no Azure.
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Gerenciar um servidor de processo em execução no Azure (Gerenciador de recursos)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Clássico](./site-recovery-vmware-setup-azure-ps-classic.md)

Durante o failback, é recomendável toodeploy servidor de processo no Azure se houver alta latência entre hello rede Virtual do Azure e sua rede local. Este artigo descreve como você pode configurar, configurar e gerenciar servidores de processo Olá em execução no Azure.

> [!NOTE]
> Este artigo é toobe usado se você usou **Gerenciador de recursos** como modelo de implantação de saudação para máquinas virtuais de saudação durante o failover. Se você usou **clássico** como modelo de implantação hello, siga as etapas de saudação em [como tooset up e configurar um servidor de processo de Failback (clássico)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Implantar um servidor de processos no Azure
1. No cofre de saudação > **infra-estrutura de recuperação de Site** (sob o título de "Gerenciar" hello) > **servidores de configuração** (sob o título "Para VMware e máquinas físicas"), selecione o servidor de configuração de saudação.
2. Na página de detalhes do servidor de configuração Olá abre, clique em "+ processar servidor"

  ![Adicionar a Galeria do servidor de processo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  Em Olá **Adicionar servidor de processo** página, selecione Olá valores a seguir

  ![Adicionar item da galeria do servidor de processo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Nome do Campo**|**Valor**|
|-|-|
|Escolha onde deseja toodeploy seu servidor de processo|Selecione o valor de saudação **implantar um servidor de processo de failback no Azure** |
|Assinatura|Selecione Olá assinatura do Azure onde você fez failover máquinas virtuais de saudação|
|Grupo de recursos|Você pode criar um grupo de recursos toodeploy este servidor de processo ou escolha o servidor de processo Olá toodeploy em um grupo de recursos existente|
|Local|Selecione hello Azure Data Center em que máquinas virtuais de saudação onde failover em|
|Rede do Azure|Selecione Olá Network(VNet) Virtual do Azure que Olá máquinas virtuais em que o failover no. Se você fez failover máquinas virtuais em vários VNets do Azure, em seguida, é necessário um servidor de processo implantado por rede virtual|

4. Preencha Olá restante das propriedades Olá para o servidor de processo Olá

  ![Adicionar servidor de processo resumo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Nome do Campo**|**Valor**|
|-|-|
|Nome do Servidor|Nome de exibição < / nome de Host para sua máquina de virtual do servidor de processo|
| Nome de usuário|Um nome de usuário que se torna um administrador na máquina virtual|
|Conta de armazenamento|Nome da saudação conta de armazenamento onde é colocado saudação do disco da máquina virtual do|
|Sub-rede|subrede de máquina virtual do hello Azure VNet toowhich Olá Olá está conectado|
| Endereço IP|Endereço IP que deseja Olá tooassume de servidor de processo depois que ele é inicializado|
5. Clique em toostart do botão Okey Olá Olá máquina de virtual do servidor de processo de implantação.

> [!NOTE]
> toouse capaz de toobe este servidor de processo para failback, você precisa tooregistê-lo com o servidor de configuração local hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Registrando Olá processo servidor (em execução no Azure) tooa (executado no local) do servidor de configuração

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Atualizando Olá processo toolatest versão do servidor.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Cancelar registro do servidor de processo hello (em execução no Azure) de um servidor de configuração (executado no local)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
