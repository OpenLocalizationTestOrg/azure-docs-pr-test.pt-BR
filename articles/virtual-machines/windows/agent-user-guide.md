---
title: "Visão geral do agente de máquina Virtual de aaaAzure | Microsoft Docs"
description: "Visão Geral do Agente de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Visão geral do Agente de Máquina Virtual do Azure

Olá agente da máquina Virtual Microsoft Azure (AM agente) é um processo seguro e leve que gerencia a interação de VM com hello controlador de malha do Azure. Olá agente de VM tem papel fundamental na habilitação e execução de extensões de máquina virtual do Azure. Extensões de VM habilitam a configuração máquinas virtuais pós-implantação, como instalação e configuração de software. Extensões de máquina virtual também habilitar os recursos de recuperação como redefinir a senha administrativa saudação de uma máquina virtual. Sem hello Azure VM Agent, extensões de máquina virtual não podem ser executadas.

Este documento fornece detalhes sobre a instalação, a detecção e a remoção de saudação agente da máquina Virtual do Azure.

## <a name="install-hello-vm-agent"></a>Instalar Olá agente de VM

### <a name="azure-gallery-image"></a>Imagem da galeria do Azure

Hello Azure VM Agent é instalado por padrão em qualquer máquina virtual do Windows implantada a partir de uma imagem da Galeria do Azure. Quando implantar uma imagem da Galeria do Azure de saudação Portal, o PowerShell, Interface de linha de comando ou um modelo do Gerenciador de recursos do Azure, hello que Azure VM Agent também é instalado. 

### <a name="manual-installation"></a>Instalação manual

Agente de VM do Windows Hello pode ser instalado manualmente usando um pacote do Windows installer. A instalação manual pode ser necessária ao criar uma imagem de máquina virtual personalizada que será implantada no Azure. toomanually saudação de instalação do agente de VM do Windows, baixar o instalador do agente de VM Olá deste local [Download do Windows Azure VM Agent](http://go.microsoft.com/fwlink/?LinkID=394789). 

Olá agente de VM pode ser instalado, clique duas vezes o arquivo de instalador do windows hello. Para uma instalação autônoma ou automatizada hello do agente de VM, execute Olá comando a seguir.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Detectar Olá agente de VM

### <a name="powershell"></a>PowerShell

módulo do PowerShell do Azure Resource Manager Olá pode ser usado tooretrieve informações sobre as máquinas virtuais do Azure. Executando `Get-AzureRmVM` retorna uma grande quantidade de informações incluindo Olá estado para hello Azure VM Agent de provisionamento.

```PowerShell
Get-AzureRmVM
```

Olá, a seguir é apenas um subconjunto de saudação `Get-AzureRmVM` saída. Saudação de aviso `ProvisionVMAgent` propriedade aninhado em `OSProfile`, essa propriedade pode ser usado toodetermine se o agente de VM Olá tiver sido implantado toohello virtual machine.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

saudação de script a seguir pode ser usado tooreturn uma lista concisa de nomes de máquina virtual e o estado de saudação do hello agente de VM.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Detecção Manual

Quando conectado tooa VM do Windows Azure, o Gerenciador de tarefas pode ser usado tooexamine processos em execução. toocheck para hello Azure VM Agent, abra o Gerenciador de tarefas > clique Olá guia de detalhes e procure um nome de processo `WindowsAzureGuestAgent.exe`. presença de Hello desse processo indica que o agente de VM hello está instalado.

## <a name="upgrade-hello-vm-agent"></a>Atualizar Olá agente de VM

Hello Azure VM Agent do Windows será atualizado automaticamente. Conforme novas máquinas virtuais são implantada tooAzure, eles recebem agente VM mais recente da saudação. Imagens VM personalizadas devem ser atualizadas manualmente tooinclude Olá novo agente de VM.
