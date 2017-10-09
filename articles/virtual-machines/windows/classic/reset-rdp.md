---
title: "aaaReset Olá senha ou a configuração de área de trabalho remota em uma VM do Windows Azure | Microsoft Docs"
description: "Saiba como tooreset uma senha ou conta de serviços de área de trabalho remota em uma VM do Windows criado usando a implantação do modelo usando o hello clássico hello Azure PowerShell ou o portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="96eb4-103">Como serviços de área de trabalho remota Olá tooreset ou sua senha de logon em uma VM do Windows criado usando o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="96eb4-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="96eb4-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="96eb4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="96eb4-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="96eb4-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="96eb4-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="96eb4-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="96eb4-107">Você também pode [executar essas etapas para máquinas virtuais criadas com o modelo de implantação do Gerenciador de recursos de saudação](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="96eb4-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="96eb4-108">Se você não pode se conectar a máquina virtual do Windows tooa (VM), você pode redefinir a senha de administrador local hello ou redefinir a configuração de serviços de área de trabalho remota hello.</span><span class="sxs-lookup"><span data-stu-id="96eb4-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="96eb4-109">Você pode usar qualquer extensão de acesso da máquina virtual do Azure portal ou Olá Olá na senha do Azure PowerShell tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="96eb4-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="96eb4-110">Configuração de tooreset maneiras ou credenciais</span><span class="sxs-lookup"><span data-stu-id="96eb4-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="96eb4-111">É possível redefinir os serviços e as credenciais de Área de Trabalho Remota de várias maneiras diferentes, dependendo de suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="96eb4-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="96eb4-112">Redefinir usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="96eb4-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="96eb4-113">Redefinir usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="96eb4-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="96eb4-114">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="96eb4-114">Azure portal</span></span>
<span data-ttu-id="96eb4-115">Você pode usar o hello [portal do Azure](https://portal.azure.com) tooreset Olá serviços de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="96eb4-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="96eb4-116">menu tooexpand saudação do portal, clique em Olá três barras no canto superior esquerdo da saudação e, em seguida, clique em **máquinas virtuais (clássicas)**:</span><span class="sxs-lookup"><span data-stu-id="96eb4-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Navegue até sua VM do Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="96eb4-118">Selecione sua máquina virtual do Windows e, em seguida, clique em **redefinir remoto...** . hello seguinte caixa de diálogo é exibida tooreset configuração de área de trabalho remota de saudação:</span><span class="sxs-lookup"><span data-stu-id="96eb4-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Página Redefinir configuração de RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="96eb4-120">Você também pode redefinir Olá nome de usuário e a senha da conta de administrador local hello.</span><span class="sxs-lookup"><span data-stu-id="96eb4-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="96eb4-121">Em sua VM, clique em **Suporte + Solução de Problemas** > **Redefinir senha**.</span><span class="sxs-lookup"><span data-stu-id="96eb4-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="96eb4-122">Olá folha de redefinição de senha é exibida:</span><span class="sxs-lookup"><span data-stu-id="96eb4-122">hello password reset blade is displayed:</span></span>

![Página Redefinir senha](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="96eb4-124">Depois de inserir Olá novo nome de usuário e senha, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="96eb4-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="96eb4-125">Extensão VMAccess e PowerShell</span><span class="sxs-lookup"><span data-stu-id="96eb4-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="96eb4-126">Verifique se Olá que VM Agent está instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="96eb4-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="96eb4-127">Olá extensão VMAccess não precisa toobe instalado antes de você pode usá-lo, como Olá agente da VM está disponível.</span><span class="sxs-lookup"><span data-stu-id="96eb4-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="96eb4-128">Verifique se esse Olá que VM Agent já está instalado usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="96eb4-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="96eb4-129">(Substitua "myCloudService" e "myVM" por nomes de saudação do seu serviço de nuvem e sua VM, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="96eb4-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="96eb4-130">É possível conhecer esses nomes executando `Get-AzureVM` sem nenhum parâmetro).</span><span class="sxs-lookup"><span data-stu-id="96eb4-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="96eb4-131">Se hello **write-host** comando exibe **True**, Olá VM Agent está instalado.</span><span class="sxs-lookup"><span data-stu-id="96eb4-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="96eb4-132">Se ele exibe **False**, consulte instruções hello e um toohello link baixar Olá [agente de VM e extensões – parte 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) postagem no blog do Azure.</span><span class="sxs-lookup"><span data-stu-id="96eb4-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="96eb4-133">Se você criou a máquina virtual de saudação usando o portal de saudação, verifique se `$vm.GetInstance().ProvisionGuestAgent` retorna **True**.</span><span class="sxs-lookup"><span data-stu-id="96eb4-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="96eb4-134">Caso contrário, você pode defini-lo usando esse comando:</span><span class="sxs-lookup"><span data-stu-id="96eb4-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="96eb4-135">Esse comando impede Olá erro a seguir quando você estiver executando o hello **Set-AzureVMExtension** comando nas etapas Avançar Olá: "Provisionar o agente convidado deve ser habilitado no objeto da VM Olá antes de configurar a extensão de acesso a VM de IaaS."</span><span class="sxs-lookup"><span data-stu-id="96eb4-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="96eb4-136">**Redefinir a senha de conta de administrador local Olá**</span><span class="sxs-lookup"><span data-stu-id="96eb4-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="96eb4-137">Criar uma credencial de logon com o nome da conta de administrador local atual do hello e uma nova senha e, em seguida, executar Olá `Set-AzureVMAccessExtension` da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="96eb4-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="96eb4-138">Se você digitar um nome diferente de conta do atual hello, Olá extensão VMAccess renomeia a conta de administrador local hello, atribui a conta Olá senha toothat e emite uma área de trabalho remota logout. Se a conta de administrador local Olá estiver desabilitada, Olá extensão VMAccess permite.</span><span class="sxs-lookup"><span data-stu-id="96eb4-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="96eb4-139">Esses comandos também redefinem a configuração do serviço de área de trabalho remota de saudação.</span><span class="sxs-lookup"><span data-stu-id="96eb4-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="96eb4-140">**Redefinir a configuração de serviços de área de trabalho remota Olá**</span><span class="sxs-lookup"><span data-stu-id="96eb4-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="96eb4-141">tooreset Olá área de trabalho remota configuração do serviço, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="96eb4-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="96eb4-142">Olá extensão VMAccess executa dois comandos na máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="96eb4-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="96eb4-143">Este comando habilita o grupo Windows Firewall interno Olá que permite que o tráfego de entrada área de trabalho remota, que usa a porta TCP 3389.</span><span class="sxs-lookup"><span data-stu-id="96eb4-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="96eb4-144">Este comando define Olá fDenyTSConnections registro valor too0, habilitar conexões de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="96eb4-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96eb4-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96eb4-145">Next steps</span></span>
<span data-ttu-id="96eb4-146">Se Olá extensão de acesso a VM do Azure não responde e senha de saudação tooreset não é possível, você pode [redefinição Olá Windows senha local offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96eb4-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="96eb4-147">Esse método é um processo mais avançado e exige tooconnect Olá disco rígido virtual de tooanother VM problemático Olá VM.</span><span class="sxs-lookup"><span data-stu-id="96eb4-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="96eb4-148">Execute as etapas de saudação documentadas neste artigo primeiro e, em seguida, tente somente método de redefinição de senha offline hello como um último recurso.</span><span class="sxs-lookup"><span data-stu-id="96eb4-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="96eb4-149">Recursos e extensões de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="96eb4-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="96eb4-150">Conecte-se tooan máquina virtual do Azure com RDP ou SSH</span><span class="sxs-lookup"><span data-stu-id="96eb4-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="96eb4-151">Solucionar problemas de área de trabalho remota conexões tooa baseados no Windows Azure máquina virtual</span><span class="sxs-lookup"><span data-stu-id="96eb4-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

