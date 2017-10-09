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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Como serviços de área de trabalho remota Olá tooreset ou sua senha de logon em uma VM do Windows criado usando o modelo de implantação clássico Olá
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Você também pode [executar essas etapas para máquinas virtuais criadas com o modelo de implantação do Gerenciador de recursos de saudação](../reset-rdp.md).

Se você não pode se conectar a máquina virtual do Windows tooa (VM), você pode redefinir a senha de administrador local hello ou redefinir a configuração de serviços de área de trabalho remota hello. Você pode usar qualquer extensão de acesso da máquina virtual do Azure portal ou Olá Olá na senha do Azure PowerShell tooreset hello.

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuração de tooreset maneiras ou credenciais
É possível redefinir os serviços e as credenciais de Área de Trabalho Remota de várias maneiras diferentes, dependendo de suas necessidades:

- [Redefinir usando Olá portal do Azure](#azure-portal)
- [Redefinir usando o Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portal do Azure
Você pode usar o hello [portal do Azure](https://portal.azure.com) tooreset Olá serviços de área de trabalho remota. menu tooexpand saudação do portal, clique em Olá três barras no canto superior esquerdo da saudação e, em seguida, clique em **máquinas virtuais (clássicas)**:

![Navegue até sua VM do Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

Selecione sua máquina virtual do Windows e, em seguida, clique em **redefinir remoto...** . hello seguinte caixa de diálogo é exibida tooreset configuração de área de trabalho remota de saudação:

![Página Redefinir configuração de RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

Você também pode redefinir Olá nome de usuário e a senha da conta de administrador local hello. Em sua VM, clique em **Suporte + Solução de Problemas** > **Redefinir senha**. Olá folha de redefinição de senha é exibida:

![Página Redefinir senha](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Depois de inserir Olá novo nome de usuário e senha, clique em **salvar**.

## <a name="vmaccess-extension-and-powershell"></a>Extensão VMAccess e PowerShell
Verifique se Olá que VM Agent está instalado na máquina virtual de saudação. Olá extensão VMAccess não precisa toobe instalado antes de você pode usá-lo, como Olá agente da VM está disponível. Verifique se esse Olá que VM Agent já está instalado usando o comando a seguir de saudação. (Substitua "myCloudService" e "myVM" por nomes de saudação do seu serviço de nuvem e sua VM, respectivamente. É possível conhecer esses nomes executando `Get-AzureVM` sem nenhum parâmetro).

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Se hello **write-host** comando exibe **True**, Olá VM Agent está instalado. Se ele exibe **False**, consulte instruções hello e um toohello link baixar Olá [agente de VM e extensões – parte 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) postagem no blog do Azure.

Se você criou a máquina virtual de saudação usando o portal de saudação, verifique se `$vm.GetInstance().ProvisionGuestAgent` retorna **True**. Caso contrário, você pode defini-lo usando esse comando:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Esse comando impede Olá erro a seguir quando você estiver executando o hello **Set-AzureVMExtension** comando nas etapas Avançar Olá: "Provisionar o agente convidado deve ser habilitado no objeto da VM Olá antes de configurar a extensão de acesso a VM de IaaS."

### <a name="reset-hello-local-administrator-account-password"></a>**Redefinir a senha de conta de administrador local Olá**
Criar uma credencial de logon com o nome da conta de administrador local atual do hello e uma nova senha e, em seguida, executar Olá `Set-AzureVMAccessExtension` da seguinte maneira.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Se você digitar um nome diferente de conta do atual hello, Olá extensão VMAccess renomeia a conta de administrador local hello, atribui a conta Olá senha toothat e emite uma área de trabalho remota logout. Se a conta de administrador local Olá estiver desabilitada, Olá extensão VMAccess permite.

Esses comandos também redefinem a configuração do serviço de área de trabalho remota de saudação.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Redefinir a configuração de serviços de área de trabalho remota Olá**
tooreset Olá área de trabalho remota configuração do serviço, execute Olá comando a seguir:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Olá extensão VMAccess executa dois comandos na máquina virtual de saudação:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Este comando habilita o grupo Windows Firewall interno Olá que permite que o tráfego de entrada área de trabalho remota, que usa a porta TCP 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Este comando define Olá fDenyTSConnections registro valor too0, habilitar conexões de área de trabalho remota.

## <a name="next-steps"></a>Próximas etapas
Se Olá extensão de acesso a VM do Azure não responde e senha de saudação tooreset não é possível, você pode [redefinição Olá Windows senha local offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Esse método é um processo mais avançado e exige tooconnect Olá disco rígido virtual de tooanother VM problemático Olá VM. Execute as etapas de saudação documentadas neste artigo primeiro e, em seguida, tente somente método de redefinição de senha offline hello como um último recurso.

[Recursos e extensões de VM do Azure](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Conecte-se tooan máquina virtual do Azure com RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Solucionar problemas de área de trabalho remota conexões tooa baseados no Windows Azure máquina virtual](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

