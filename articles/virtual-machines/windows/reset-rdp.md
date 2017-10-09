---
title: "aaaReset Olá senha ou a configuração de área de trabalho remota em uma VM do Windows | Microsoft Docs"
description: "Saiba como tooreset uma senha de conta ou serviços de área de trabalho remota em uma máquina virtual do Windows usando hello Azure PowerShell ou o portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="04f40-103">Como tooreset Olá serviços de área de trabalho remota ou sua senha de logon em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="04f40-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="04f40-104">Se você não pode se conectar a máquina virtual do Windows tooa (VM), você pode redefinir a senha de administrador local hello ou redefinir a configuração de serviços de área de trabalho remota hello.</span><span class="sxs-lookup"><span data-stu-id="04f40-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="04f40-105">Você pode usar qualquer extensão de acesso da máquina virtual do Azure portal ou Olá Olá na senha do Azure PowerShell tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="04f40-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="04f40-106">Se você estiver usando o PowerShell, certifique-se de que você tenha Olá [módulo PowerShell mais recente instalado e configurado](/powershell/azure/overview) e entrou tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="04f40-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="04f40-107">Você também pode [executar essas etapas para máquinas virtuais criadas com o modelo de implantação clássico Olá](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="04f40-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="04f40-108">Configuração de tooreset maneiras ou credenciais</span><span class="sxs-lookup"><span data-stu-id="04f40-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="04f40-109">É possível redefinir os serviços e as credenciais de Área de Trabalho Remota de várias maneiras diferentes, dependendo de suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="04f40-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="04f40-110">Redefinir usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04f40-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="04f40-111">Redefinir usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="04f40-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="04f40-112">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04f40-112">Azure portal</span></span>
<span data-ttu-id="04f40-113">menu tooexpand saudação do portal, clique em Olá três barras no canto superior esquerdo da saudação e, em seguida, clique em **máquinas virtuais**:</span><span class="sxs-lookup"><span data-stu-id="04f40-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Navegue até sua VM do Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="04f40-115">**Redefinir a senha de conta de administrador local Olá**</span><span class="sxs-lookup"><span data-stu-id="04f40-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="04f40-116">Selecione sua máquina virtual do Windows e clique em **Suporte + Solução de Problemas** > **Redefinir senha**.</span><span class="sxs-lookup"><span data-stu-id="04f40-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="04f40-117">Olá folha de redefinição de senha é exibida:</span><span class="sxs-lookup"><span data-stu-id="04f40-117">hello password reset blade is displayed:</span></span>

![Página Redefinir senha](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="04f40-119">Digite hello nome de usuário e uma nova senha, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="04f40-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="04f40-120">Tente se conectar tooyour VM novamente.</span><span class="sxs-lookup"><span data-stu-id="04f40-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="04f40-121">**Redefinir a configuração de serviços de área de trabalho remota Olá**</span><span class="sxs-lookup"><span data-stu-id="04f40-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="04f40-122">Selecione sua máquina virtual do Windows e clique em **Suporte + Solução de Problemas** > **Redefinir senha**.</span><span class="sxs-lookup"><span data-stu-id="04f40-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="04f40-123">Olá folha de redefinição de senha é exibida.</span><span class="sxs-lookup"><span data-stu-id="04f40-123">hello password reset blade is displayed.</span></span> 

![Redefinir configuração do RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="04f40-125">Selecione **apenas a configuração de redefinição** no menu suspenso de Olá, e clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="04f40-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="04f40-126">Tente se conectar tooyour VM novamente.</span><span class="sxs-lookup"><span data-stu-id="04f40-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="04f40-127">Extensão VMAccess e PowerShell</span><span class="sxs-lookup"><span data-stu-id="04f40-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="04f40-128">Certifique-se de que você tenha Olá [módulo PowerShell mais recente instalado e configurado](/powershell/azure/overview) e entrou tooyour assinatura do Azure com hello `Login-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="04f40-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="04f40-129">**Redefinir a senha de conta de administrador local Olá**</span><span class="sxs-lookup"><span data-stu-id="04f40-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="04f40-130">Redefinição Olá administrador senha ou nome de usuário com hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04f40-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="04f40-131">Crie as credenciais de sua conta da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="04f40-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="04f40-132">Se você digitar um nome diferente de conta de administrador local atual da saudação na sua VM, Olá extensão VMAccess renomeia a conta de administrador local hello, atribui a sua conta de toothat senha especificada e emite um evento de logoff de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="04f40-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="04f40-133">Se a conta de administrador local Olá na sua VM está desabilitada, Olá extensão VMAccess permite.</span><span class="sxs-lookup"><span data-stu-id="04f40-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="04f40-134">Olá atualizações de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup` toohello credenciais especificadas.</span><span class="sxs-lookup"><span data-stu-id="04f40-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="04f40-135">**Redefinir a configuração de serviços de área de trabalho remota Olá**</span><span class="sxs-lookup"><span data-stu-id="04f40-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="04f40-136">Redefinir o acesso remoto tooyour VM com hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04f40-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="04f40-137">Olá, exemplo a seguir redefine chamado de extensão de acesso Olá `myVMAccess` em Olá VM denominada `myVM` em Olá `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="04f40-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="04f40-138">A qualquer momento, uma VM pode ter apenas um único agente de acesso de VM.</span><span class="sxs-lookup"><span data-stu-id="04f40-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="04f40-139">Propriedades do agente tooset Olá VM acesso com êxito, Olá `-ForceRerun` opção pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="04f40-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="04f40-140">Ao usar `-ForceRerun`, certifique-se de toouse Olá o mesmo nome para o agente de acesso VM Olá conforme usado em todos os comandos anteriores.</span><span class="sxs-lookup"><span data-stu-id="04f40-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="04f40-141">Se você ainda não é possível conectar remotamente tooyour máquina virtual, consulte mais tootry etapas em [solucionar problemas de área de trabalho remota conexões tooa baseados no Windows Azure máquina virtual](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04f40-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="04f40-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04f40-142">Next steps</span></span>
<span data-ttu-id="04f40-143">Se Olá extensão de acesso a VM do Azure não responde e senha de saudação tooreset não é possível, você pode [redefinição Olá Windows senha local offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04f40-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="04f40-144">Esse método é um processo mais avançado e exige tooconnect Olá disco rígido virtual de tooanother VM problemático Olá VM.</span><span class="sxs-lookup"><span data-stu-id="04f40-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="04f40-145">Execute as etapas de saudação documentadas neste artigo primeiro e, em seguida, tente somente método de redefinição de senha offline hello como um último recurso.</span><span class="sxs-lookup"><span data-stu-id="04f40-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="04f40-146">Recursos e extensões de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="04f40-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="04f40-147">Conecte-se tooan máquina virtual do Azure com RDP ou SSH</span><span class="sxs-lookup"><span data-stu-id="04f40-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="04f40-148">Solucionar problemas de área de trabalho remota conexões tooa baseados no Windows Azure máquina virtual</span><span class="sxs-lookup"><span data-stu-id="04f40-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

