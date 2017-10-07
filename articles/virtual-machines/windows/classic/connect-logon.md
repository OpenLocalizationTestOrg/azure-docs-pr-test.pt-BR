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
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="e1bdd-103">Faça logon no tooa máquina virtual do Windows usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e1bdd-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="e1bdd-104">Olá portal do Azure, você usa Olá **conectar** botão toostart uma sessão de área de trabalho remota e logon tooa VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="e1bdd-105">Você deseja tooconnect tooa VM Linux?</span><span class="sxs-lookup"><span data-stu-id="e1bdd-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="e1bdd-106">Consulte [como toolog na máquina virtual de tooa executando o Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="e1bdd-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="e1bdd-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e1bdd-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e1bdd-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e1bdd-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e1bdd-110">Para obter informações sobre como toolog tooa VM usando Olá Gerenciador de recursos de modelo, consulte [aqui](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1bdd-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="e1bdd-111">Conecte-se a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="e1bdd-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="e1bdd-112">Entrar toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="e1bdd-113">Clique na máquina virtual de saudação que você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="e1bdd-114">Olá está listado na Olá **todos os recursos** painel.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="e1bdd-116">Clique em **conectar** na barra de comandos Olá sobre o painel de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Conecte-se o ícone para a máquina virtual de saudação](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="e1bdd-118">Faça logon na máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="e1bdd-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="e1bdd-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1bdd-119">Next steps</span></span>
* <span data-ttu-id="e1bdd-120">Se hello **conectar** estiver inativo ou se você tiver outros problemas com conexão de área de trabalho remota hello, tente redefinir a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="e1bdd-121">Clique em **redefinir o acesso remoto** do painel de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="e1bdd-123">Se houver problemas com a senha, tente redefini-la.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="e1bdd-124">Clique em **Redefinir senha** ao longo de saudação extremidade esquerda do painel de máquina virtual, em **suporte + solução de problemas**.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="e1bdd-126">Se essas dicas não funcionam ou não precisa, consulte [tooa conexões de solucionar problemas de área de trabalho remota baseado no Windows Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1bdd-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e1bdd-127">Este artigo orienta você no diagnóstico e na solução de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="e1bdd-127">This article walks you through diagnosing and resolving common problems.</span></span>
