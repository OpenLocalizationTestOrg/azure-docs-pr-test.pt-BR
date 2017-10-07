---
title: "aaaLog em tooa clássico VM do Azure | Microsoft Docs"
description: "Use Olá toolog portal do Azure na máquina virtual do Windows tooa criada com o modelo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Faça logon no tooa máquina virtual do Windows usando Olá portal do Azure
Olá portal do Azure, você usa Olá **conectar** botão toostart uma sessão de área de trabalho remota e logon tooa VM do Windows.

Você deseja tooconnect tooa VM Linux? Consulte [como toolog na máquina virtual de tooa executando o Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações sobre como toolog tooa VM usando Olá Gerenciador de recursos de modelo, consulte [aqui](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Conecte-se a máquina virtual de toohello
1. Entrar toohello portal do Azure.
2. Clique na máquina virtual de saudação que você deseja tooaccess. Olá está listado na Olá **todos os recursos** painel.

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. Clique em **conectar** na barra de comandos Olá sobre o painel de máquina virtual de saudação.

    ![Conecte-se o ícone para a máquina virtual de saudação](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Faça logon na máquina virtual de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Próximas etapas
* Se hello **conectar** estiver inativo ou se você tiver outros problemas com conexão de área de trabalho remota hello, tente redefinir a configuração de saudação. Clique em **redefinir o acesso remoto** do painel de máquina virtual de saudação.

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Se houver problemas com a senha, tente redefini-la. Clique em **Redefinir senha** ao longo de saudação extremidade esquerda do painel de máquina virtual, em **suporte + solução de problemas**.

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Se essas dicas não funcionam ou não precisa, consulte [tooa conexões de solucionar problemas de área de trabalho remota baseado no Windows Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Este artigo orienta você no diagnóstico e na solução de problemas comuns.
