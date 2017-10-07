---
title: "aaaAzure monitoramento e máquinas virtuais do Windows | Microsoft Docs"
description: "Tutorial – Monitorar uma Máquina Virtual do Windows com o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Monitorar uma Máquina Virtual do Windows com o Azure PowerShell

Monitoramento do Azure usa a inicialização de toocollect de agentes e dados de desempenho de máquinas virtuais do Azure, armazenar esses dados no armazenamento do Azure e torná-lo acessível por meio do portal, o módulo do PowerShell do Azure hello e Olá CLI do Azure. Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Habilitar o diagnóstico de inicialização em uma VM
> * Exibir diagnóstico de inicialização
> * Exibir métricas de host VM
> * Instalar a extensão de diagnóstico Olá
> * Exibir métricas de VM
> * Criar um alerta
> * Configurar monitoramento avançado

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente. Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você. Ao trabalhar com tutorial Olá, substitua o grupo de recursos de saudação, o nome da VM e o local onde for necessário.

## <a name="view-boot-diagnostics"></a>Exibir diagnóstico de inicialização

Como máquinas virtuais do Windows é inicializado, o agente de diagnóstico de inicialização de saudação captura a saída na tela que pode ser usada para a finalidade de solução de problemas. Essa funcionalidade é habilitada por padrão. Olá capturadas tela capturas são armazenadas em uma conta de armazenamento do Azure, que também é criada por padrão. 

Você pode obter dados de diagnóstico de inicialização Olá com hello [AzureRmVMBootDiagnosticsData Get](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) comando. Olá exemplo a seguir, o diagnóstico de inicialização é raiz toohello baixado de hello * c:\* unidade. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Exibir métricas de host

Uma VM do Windows tem uma VM Host dedicada no Azure com a qual ele interage. Métricas são automaticamente coletadas para Olá Host e podem ser exibidas no portal do Azure de saudação.

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
2. Clique em **métricas** Olá folha de VM e, em seguida, selecione qualquer uma das métricas de Host de saudação em **métricas disponíveis** toosee desempenho Olá VM do Host.

    ![Exibir métricas de host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Instalar extensão de diagnóstico

métricas de host básica Olá estão disponíveis, mas toosee mais granular e métricas de VM específico, você tooneed tooinstall Olá diagnóstico do Azure extensão no hello VM. Olá extensão de diagnóstico do Azure permite o monitoramento adicional e toobe de dados de diagnóstico recuperados da saudação VM. Você pode exibir essas métricas de desempenho e criar alertas com base em como Olá VM executa. extensão de diagnóstico Olá é instalado por meio de saudação portal do Azure da seguinte maneira:

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
2. Clique em **Configurações de diagnóstico**. lista de saudação mostra que *diagnósticos de inicialização* já estão habilitados na seção anterior hello. Clique em caixa de seleção Olá *métricas básicas*.
3. Clique em Olá **habilitar o monitoramento de nível de convidado** botão.

    ![Exibir métricas de diagnóstico](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Exibir métricas de VM

Você pode exibir as métricas VM Olá no hello mesma maneira que você exibiu métricas VM do host hello:

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
2. toosee como Olá VM for executada, clique em **métricas** Olá folha de VM e, em seguida, selecione qualquer uma das métricas de diagnóstico de saudação em **métricas disponíveis**.

    ![Exibir métricas de VM](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Criar alertas

Você pode criar alertas com base em métricas de desempenho específicas. Alertas podem ser usado toonotify quando uso médio da CPU excede um determinado limite ou espaço em disco livre disponível cai abaixo de um determinado valor, por exemplo. Alertas são exibidos no portal do Azure de saudação ou podem ser enviados por email. Você também pode disparar runbooks de automação do Azure ou aplicativos do Azure lógica tooalerts de resposta que está sendo gerado.

Olá, exemplo a seguir cria um alerta para o uso médio da CPU.

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
2. Clique em **regras de alerta** na folha VM hello, em seguida, clique em **adicionar alerta métrica** na parte superior de saudação da folha de alertas de saudação.
4. Forneça um **Nome** para o alerta, como *myAlertRule*
5. tootrigger um alerta quando a porcentagem de CPU exceder 1.0 por cinco minutos, deixe Olá todos os outros padrões selecionados.
6. Opcionalmente, marque a caixa da saudação *proprietários, Contribuidores e leitores de Email* toosend notificação por email. ação de padrão de saudação é toopresent uma notificação no portal de saudação.
7. Clique em Olá **Okey** botão.

## <a name="advanced-monitoring"></a>Monitoramento avançado 

Você pode fazer um monitoramento mais avançado da sua VM usando o [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Caso ainda não tenha feito isso, você pode se inscrever para uma [avaliação gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) do Operations Management Suite.

Quando você tiver acesso toohello OMS portal, você pode encontrar o identificador de chave e o espaço de trabalho do espaço de trabalho Olá na folha de configurações de saudação. Saudação de uso [conjunto AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) toohello cmmand tootooadd Olá OMS extensão VM. Variável de saudação atualização valores em Olá abaixo tooreflect exemplo chave de espaço de trabalho do OMS e o espaço de trabalho ID.  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Depois de alguns minutos, você deverá ver Olá nova VM no espaço de trabalho do hello OMS. 

![Folha do OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você configurou e revisou VMs com a Central de Segurança do Azure. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma rede virtual
> * Criar um grupo de recursos e uma VM 
> * Habilitar o diagnóstico de inicialização em Olá VM
> * Exibir diagnóstico de inicialização
> * Exibir métricas de host
> * Instalar a extensão de diagnóstico Olá
> * Exibir métricas de VM
> * Criar um alerta
> * Configurar monitoramento avançado

Avançar toohello toolearn próximo de tutorial sobre o Centro de segurança do Azure.

> [!div class="nextstepaction"]
> [Gerenciar a segurança da VM](./tutorial-azure-security.md)