---
title: "aaaInstall Trend Micro Deep Security em uma máquina virtual | Microsoft Docs"
description: "Este artigo descreve como tooinstall e configurar a segurança de Trend Micro em uma máquina virtual criada com o modelo de implantação clássico Olá no Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Como tooinstall e configurar o Trend Micro Deep Security como um serviço em uma VM do Windows
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Este artigo mostra como tooinstall e configurar o Trend Micro Deep Security como um serviço em um novo ou existente máquina virtual (VM executando o Windows Server). O Deep Security as a Service inclui proteção anti-malware, firewall, sistema de prevenção de intrusões e monitoramento de integridade.

Olá cliente é instalado como uma extensão de segurança por meio de saudação agente de VM. Em uma nova máquina virtual, instale Olá Deep Security Agent, como Olá que agente VM é criada automaticamente pelo Olá portal do Azure.

Uma VM existente criada usando o portal clássico do hello, Olá CLI do Azure ou o PowerShell não pode ter um agente VM. Para uma máquina virtual existente que não tenha Olá agente de VM, você precisa toodownload e instalá-lo primeiro. Este artigo aborda ambas as situações.

Se você tiver uma assinatura atual da Trend Micro para uma solução local, você pode usá-lo toohelp proteger suas máquinas virtuais do Azure. Se ainda não for cliente, você poderá se inscrever em uma assinatura de avaliação. Para obter mais informações sobre esta solução, consulte Olá Trend Micro postagem de blog [Microsoft Azure VM Agent extensão para Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Instalar Olá Deep Security Agent em uma nova VM

Olá [portal do Azure](http://portal.azure.com) permite que você instale a extensão de segurança Trend Micro hello quando você usar uma imagem de saudação **Marketplace** toocreate Olá VM. Se você estiver criando uma única máquina virtual, usando o portal de saudação é uma proteção de tooadd de maneira fácil de Trend Micro.

Usando uma entrada de saudação **Marketplace** abre um assistente que ajuda você a configurar a máquina virtual de saudação. Use Olá **configurações** folha, o terceiro painel saudação do assistente hello, Olá tooinstall extensão de segurança Trend Micro.  Para obter instruções gerais, consulte [criar uma máquina virtual executando o Windows hello portal do Azure](tutorial.md).

Quando você obtém toohello **configurações** folha do Assistente de Olá Olá seguintes etapas:

1. Clique em **extensões**, em seguida, clique em **Adicionar extensão** no próximo painel de saudação.

   ![Começar a adicionar a extensão de saudação][1]

2. Selecione **Deep Security Agent** em Olá **novo recurso** painel. No painel de Deep Security Agent hello, clique em **criar**.

   ![Identificar o Deep Security Agent][2]

3. Digite hello **identificador do locatário** e **senha de ativação do locatário** para extensão de saudação. Opcionalmente, você pode inserir um **Identificador de Política de Segurança**. Em seguida, clique em **Okey** tooadd cliente de saudação.

   ![Fornecer detalhes da extensão][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Instalar Olá Deep Security Agent em uma VM existente
Agente de saudação tooinstall em uma VM existente, você precisa Olá itens a seguir:

* módulo do PowerShell do Azure Hello, versão 0.8.2 ou mais recente, instalado no computador local. Você pode verificar a versão de saudação do PowerShell do Azure que você instalou usando Olá **azure Get-Module | versão de formato de tabela** comando. Para obter instruções e uma versão mais recente do link toohello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Faça logon tooyour assinatura do Azure usando `Add-AzureAccount`.
* saudação do agente de VM instalado na máquina de virtual de destino hello.

Primeiro, verifique se esse Olá que VM Agent já está instalado. Preencha o nome de serviço de nuvem hello e nome da máquina virtual e execute Olá comandos em um prompt de comando do PowerShell do Azure de nível de administrador a seguir. Substitua tudo entre aspas hello, incluindo hello < e > caracteres.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Se você não souber o nome da máquina virtual e serviço de nuvem hello, execute **Get-AzureVM** toodisplay informações para todos os Olá máquinas virtuais em sua assinatura atual.

Se hello **write-host** comando retorna **True**, Olá VM Agent está instalado. Se ele retorna **False**, consulte as instruções de saudação e um toohello link baixar Olá postagem no blog do Azure [agente de VM e extensões – parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Se Olá agente VM é instalado, execute estes comandos.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Próximas etapas
Leva alguns minutos para Olá toostart de agente em execução quando ele está instalado. Depois disso, você precisa tooactivate segurança profunda na máquina virtual de saudação para que ele possa ser gerenciado por um Gerenciador de segurança profunda. Consulte Olá artigos para obter instruções adicionais a seguir:

* Artigo de tendência sobre essa solução, [Segurança na nuvem Instant-On do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* Um [script do Windows PowerShell de exemplo](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure Olá VM
* [Instruções](http://go.microsoft.com/fwlink/?LinkId=404099) para exemplo hello

## <a name="additional-resources"></a>Recursos adicionais
[Como toolog na máquina virtual de tooa executando o Windows Server]

[Recursos e extensões de VM do Azure]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Como toolog na máquina virtual de tooa executando o Windows Server]:connect-logon.md
[Recursos e extensões de VM do Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
