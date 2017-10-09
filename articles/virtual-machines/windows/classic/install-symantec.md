---
title: aaaInstall Symantec Endpoint Protection em uma VM do Windows Azure | Microsoft Docs
description: "Saiba como tooinstall e configurar a extensão de segurança Olá Symantec Endpoint Protection em um novo ou existente VM do Azure criado com o modelo de implantação clássico Olá."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Como tooinstall e configurar o Symantec Endpoint Protection em uma VM do Windows
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Este artigo mostra como tooinstall e configurar o cliente do hello Symantec Endpoint Protection em uma máquina virtual existente (VM) executando o Windows Server. Este cliente completo inclui serviços como proteção contra vírus e spyware, firewall e prevenção contra intrusão. cliente de saudação é instalado como uma extensão de segurança usando Olá agente de VM.

Se você tiver uma assinatura existente da Symantec para uma solução local, você pode usá-lo tooprotect suas máquinas virtuais do Azure. Se ainda não for cliente, você poderá se inscrever em uma assinatura de avaliação. Para obter mais informações sobre essa solução, consulte [Symantec Endpoint Protection na plataforma Azure da Microsoft][Symantec]. Essa página também contém informações de toolicensing links e instruções para instalar o cliente de saudação se você já é um cliente do Symantec.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Instalar o Symantec Endpoint Protection em uma VM existente
Antes de começar, você precisa seguir hello:

* módulo do PowerShell do Azure Hello, versão 0.8.2 ou posterior, no computador do trabalho. Você pode verificar a versão de saudação do PowerShell do Azure que você instalou com hello **azure Get-Module | versão de formato de tabela** comando. Para obter instruções e uma versão mais recente do link toohello, consulte [como tooInstall e configurar o Azure PowerShell][PS]. Faça logon tooyour assinatura do Azure usando `Add-AzureAccount`.
* Olá Olá de agente de VM em execução em Máquina Virtual do Azure.

Primeiro, verifique se esse Olá que VM Agent já está instalado na máquina virtual de saudação. Preencha o nome de serviço de nuvem hello e nome da máquina virtual e execute Olá comandos em um prompt de comando do PowerShell do Azure de nível de administrador a seguir. Substitua tudo entre aspas hello, incluindo hello < e > caracteres.

> [!TIP]
> Se você não souber o serviço de nuvem hello e nomes de máquina virtual, execute **Get-AzureVM** nomes de saudação toolist para todas as máquinas virtuais em sua assinatura atual.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Se hello **write-host** comando exibe **True**, Olá VM Agent está instalado. Se ele exibe **False**, consulte as instruções de saudação e um toohello link baixar Olá postagem no blog do Azure [agente de VM e extensões – parte 2][Agent].

Se Olá agente de VM é instalado, execute agente de Symantec Endpoint Protection esses comandos tooinstall hello.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify que Olá Symantec extensão de segurança foi instalado e é atualizado:

1. Faça logon na máquina virtual de toohello. Para obter instruções, consulte [como tooLog no tooa Máquina Virtual executando o Windows Server][Logon].
2. Para Windows Server 2008 R2, clique em **Iniciar > Symantec Endpoint Protection**. Para o Windows Server 2012 ou Windows Server 2012 R2, na tela de início do hello, digite **Symantec**e, em seguida, clique em **Symantec Endpoint Protection**.
3. De saudação **Status** guia da saudação **Status Symantec Endpoint Protection** janela, aplicar atualizações ou reinicie se necessário.

## <a name="additional-resources"></a>Recursos adicionais
[Como tooLog no tooa Máquina Virtual executando o Windows Server][Logon]

[Recursos e Extensões de VM do Azure][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
