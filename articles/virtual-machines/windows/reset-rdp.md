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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Como tooreset Olá serviços de área de trabalho remota ou sua senha de logon em uma VM do Windows
Se você não pode se conectar a máquina virtual do Windows tooa (VM), você pode redefinir a senha de administrador local hello ou redefinir a configuração de serviços de área de trabalho remota hello. Você pode usar qualquer extensão de acesso da máquina virtual do Azure portal ou Olá Olá na senha do Azure PowerShell tooreset hello. Se você estiver usando o PowerShell, certifique-se de que você tenha Olá [módulo PowerShell mais recente instalado e configurado](/powershell/azure/overview) e entrou tooyour assinatura do Azure. Você também pode [executar essas etapas para máquinas virtuais criadas com o modelo de implantação clássico Olá](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuração de tooreset maneiras ou credenciais
É possível redefinir os serviços e as credenciais de Área de Trabalho Remota de várias maneiras diferentes, dependendo de suas necessidades:

- [Redefinir usando Olá portal do Azure](#azure-portal)
- [Redefinir usando o Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portal do Azure
menu tooexpand saudação do portal, clique em Olá três barras no canto superior esquerdo da saudação e, em seguida, clique em **máquinas virtuais**:

![Navegue até sua VM do Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Redefinir a senha de conta de administrador local Olá**

Selecione sua máquina virtual do Windows e clique em **Suporte + Solução de Problemas** > **Redefinir senha**. Olá folha de redefinição de senha é exibida:

![Página Redefinir senha](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Digite hello nome de usuário e uma nova senha, clique em **atualização**. Tente se conectar tooyour VM novamente.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Redefinir a configuração de serviços de área de trabalho remota Olá**

Selecione sua máquina virtual do Windows e clique em **Suporte + Solução de Problemas** > **Redefinir senha**. Olá folha de redefinição de senha é exibida. 

![Redefinir configuração do RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Selecione **apenas a configuração de redefinição** no menu suspenso de Olá, e clique em **atualização**. Tente se conectar tooyour VM novamente.


## <a name="vmaccess-extension-and-powershell"></a>Extensão VMAccess e PowerShell
Certifique-se de que você tenha Olá [módulo PowerShell mais recente instalado e configurado](/powershell/azure/overview) e entrou tooyour assinatura do Azure com hello `Login-AzureRmAccount` cmdlet.

### <a name="reset-hello-local-administrator-account-password"></a>**Redefinir a senha de conta de administrador local Olá**
Redefinição Olá administrador senha ou nome de usuário com hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet do PowerShell. Crie as credenciais de sua conta da seguinte maneira:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Se você digitar um nome diferente de conta de administrador local atual da saudação na sua VM, Olá extensão VMAccess renomeia a conta de administrador local hello, atribui a sua conta de toothat senha especificada e emite um evento de logoff de área de trabalho remota. Se a conta de administrador local Olá na sua VM está desabilitada, Olá extensão VMAccess permite.

Olá atualizações de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup` toohello credenciais especificadas.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Redefinir a configuração de serviços de área de trabalho remota Olá**
Redefinir o acesso remoto tooyour VM com hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet do PowerShell. Olá, exemplo a seguir redefine chamado de extensão de acesso Olá `myVMAccess` em Olá VM denominada `myVM` em Olá `myResourceGroup` grupo de recursos:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> A qualquer momento, uma VM pode ter apenas um único agente de acesso de VM. Propriedades do agente tooset Olá VM acesso com êxito, Olá `-ForceRerun` opção pode ser usada. Ao usar `-ForceRerun`, certifique-se de toouse Olá o mesmo nome para o agente de acesso VM Olá conforme usado em todos os comandos anteriores.

Se você ainda não é possível conectar remotamente tooyour máquina virtual, consulte mais tootry etapas em [solucionar problemas de área de trabalho remota conexões tooa baseados no Windows Azure máquina virtual](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Próximas etapas
Se Olá extensão de acesso a VM do Azure não responde e senha de saudação tooreset não é possível, você pode [redefinição Olá Windows senha local offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Esse método é um processo mais avançado e exige tooconnect Olá disco rígido virtual de tooanother VM problemático Olá VM. Execute as etapas de saudação documentadas neste artigo primeiro e, em seguida, tente somente método de redefinição de senha offline hello como um último recurso.

[Recursos e extensões de VM do Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Conecte-se tooan máquina virtual do Azure com RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Solucionar problemas de área de trabalho remota conexões tooa baseados no Windows Azure máquina virtual](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

