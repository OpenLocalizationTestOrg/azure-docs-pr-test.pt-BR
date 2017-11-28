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
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="da500-103">Monitorar uma Máquina Virtual do Windows com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="da500-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="da500-104">Monitoramento do Azure usa a inicialização de toocollect de agentes e dados de desempenho de máquinas virtuais do Azure, armazenar esses dados no armazenamento do Azure e torná-lo acessível por meio do portal, o módulo do PowerShell do Azure hello e Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="da500-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="da500-105">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="da500-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="da500-106">Habilitar o diagnóstico de inicialização em uma VM</span><span class="sxs-lookup"><span data-stu-id="da500-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="da500-107">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="da500-107">View boot diagnostics</span></span>
> * <span data-ttu-id="da500-108">Exibir métricas de host VM</span><span class="sxs-lookup"><span data-stu-id="da500-108">View VM host metrics</span></span>
> * <span data-ttu-id="da500-109">Instalar a extensão de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="da500-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="da500-110">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="da500-110">View VM metrics</span></span>
> * <span data-ttu-id="da500-111">Criar um alerta</span><span class="sxs-lookup"><span data-stu-id="da500-111">Create an alert</span></span>
> * <span data-ttu-id="da500-112">Configurar monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="da500-112">Set up advanced monitoring</span></span>

<span data-ttu-id="da500-113">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="da500-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="da500-114">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="da500-115">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="da500-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="da500-116">exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="da500-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="da500-117">Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você.</span><span class="sxs-lookup"><span data-stu-id="da500-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="da500-118">Ao trabalhar com tutorial Olá, substitua o grupo de recursos de saudação, o nome da VM e o local onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="da500-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="da500-119">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="da500-119">View boot diagnostics</span></span>

<span data-ttu-id="da500-120">Como máquinas virtuais do Windows é inicializado, o agente de diagnóstico de inicialização de saudação captura a saída na tela que pode ser usada para a finalidade de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="da500-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="da500-121">Essa funcionalidade é habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="da500-121">This capability is enabled by default.</span></span> <span data-ttu-id="da500-122">Olá capturadas tela capturas são armazenadas em uma conta de armazenamento do Azure, que também é criada por padrão.</span><span class="sxs-lookup"><span data-stu-id="da500-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="da500-123">Você pode obter dados de diagnóstico de inicialização Olá com hello [AzureRmVMBootDiagnosticsData Get](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) comando.</span><span class="sxs-lookup"><span data-stu-id="da500-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="da500-124">Olá exemplo a seguir, o diagnóstico de inicialização é raiz toohello baixado de hello * c:\* unidade.</span><span class="sxs-lookup"><span data-stu-id="da500-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="da500-125">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="da500-125">View host metrics</span></span>

<span data-ttu-id="da500-126">Uma VM do Windows tem uma VM Host dedicada no Azure com a qual ele interage.</span><span class="sxs-lookup"><span data-stu-id="da500-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="da500-127">Métricas são automaticamente coletadas para Olá Host e podem ser exibidas no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="da500-128">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="da500-129">Clique em **métricas** Olá folha de VM e, em seguida, selecione qualquer uma das métricas de Host de saudação em **métricas disponíveis** toosee desempenho Olá VM do Host.</span><span class="sxs-lookup"><span data-stu-id="da500-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Exibir métricas de host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="da500-131">Instalar extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="da500-131">Install diagnostics extension</span></span>

<span data-ttu-id="da500-132">métricas de host básica Olá estão disponíveis, mas toosee mais granular e métricas de VM específico, você tooneed tooinstall Olá diagnóstico do Azure extensão no hello VM.</span><span class="sxs-lookup"><span data-stu-id="da500-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="da500-133">Olá extensão de diagnóstico do Azure permite o monitoramento adicional e toobe de dados de diagnóstico recuperados da saudação VM.</span><span class="sxs-lookup"><span data-stu-id="da500-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="da500-134">Você pode exibir essas métricas de desempenho e criar alertas com base em como Olá VM executa.</span><span class="sxs-lookup"><span data-stu-id="da500-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="da500-135">extensão de diagnóstico Olá é instalado por meio de saudação portal do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="da500-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="da500-136">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="da500-137">Clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="da500-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="da500-138">lista de saudação mostra que *diagnósticos de inicialização* já estão habilitados na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="da500-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="da500-139">Clique em caixa de seleção Olá *métricas básicas*.</span><span class="sxs-lookup"><span data-stu-id="da500-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="da500-140">Clique em Olá **habilitar o monitoramento de nível de convidado** botão.</span><span class="sxs-lookup"><span data-stu-id="da500-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Exibir métricas de diagnóstico](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="da500-142">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="da500-142">View VM metrics</span></span>

<span data-ttu-id="da500-143">Você pode exibir as métricas VM Olá no hello mesma maneira que você exibiu métricas VM do host hello:</span><span class="sxs-lookup"><span data-stu-id="da500-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="da500-144">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="da500-145">toosee como Olá VM for executada, clique em **métricas** Olá folha de VM e, em seguida, selecione qualquer uma das métricas de diagnóstico de saudação em **métricas disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="da500-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Exibir métricas de VM](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="da500-147">Criar alertas</span><span class="sxs-lookup"><span data-stu-id="da500-147">Create alerts</span></span>

<span data-ttu-id="da500-148">Você pode criar alertas com base em métricas de desempenho específicas.</span><span class="sxs-lookup"><span data-stu-id="da500-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="da500-149">Alertas podem ser usado toonotify quando uso médio da CPU excede um determinado limite ou espaço em disco livre disponível cai abaixo de um determinado valor, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="da500-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="da500-150">Alertas são exibidos no portal do Azure de saudação ou podem ser enviados por email.</span><span class="sxs-lookup"><span data-stu-id="da500-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="da500-151">Você também pode disparar runbooks de automação do Azure ou aplicativos do Azure lógica tooalerts de resposta que está sendo gerado.</span><span class="sxs-lookup"><span data-stu-id="da500-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="da500-152">Olá, exemplo a seguir cria um alerta para o uso médio da CPU.</span><span class="sxs-lookup"><span data-stu-id="da500-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="da500-153">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="da500-154">Clique em **regras de alerta** na folha VM hello, em seguida, clique em **adicionar alerta métrica** na parte superior de saudação da folha de alertas de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="da500-155">Forneça um **Nome** para o alerta, como *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="da500-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="da500-156">tootrigger um alerta quando a porcentagem de CPU exceder 1.0 por cinco minutos, deixe Olá todos os outros padrões selecionados.</span><span class="sxs-lookup"><span data-stu-id="da500-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="da500-157">Opcionalmente, marque a caixa da saudação *proprietários, Contribuidores e leitores de Email* toosend notificação por email.</span><span class="sxs-lookup"><span data-stu-id="da500-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="da500-158">ação de padrão de saudação é toopresent uma notificação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="da500-159">Clique em Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="da500-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="da500-160">Monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="da500-160">Advanced monitoring</span></span> 

<span data-ttu-id="da500-161">Você pode fazer um monitoramento mais avançado da sua VM usando o [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="da500-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="da500-162">Caso ainda não tenha feito isso, você pode se inscrever para uma [avaliação gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="da500-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="da500-163">Quando você tiver acesso toohello OMS portal, você pode encontrar o identificador de chave e o espaço de trabalho do espaço de trabalho Olá na folha de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="da500-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="da500-164">Saudação de uso [conjunto AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) toohello cmmand tootooadd Olá OMS extensão VM.</span><span class="sxs-lookup"><span data-stu-id="da500-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="da500-165">Variável de saudação atualização valores em Olá abaixo tooreflect exemplo chave de espaço de trabalho do OMS e o espaço de trabalho ID.</span><span class="sxs-lookup"><span data-stu-id="da500-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

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

<span data-ttu-id="da500-166">Depois de alguns minutos, você deverá ver Olá nova VM no espaço de trabalho do hello OMS.</span><span class="sxs-lookup"><span data-stu-id="da500-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![Folha do OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="da500-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da500-168">Next steps</span></span>
<span data-ttu-id="da500-169">Neste tutorial, você configurou e revisou VMs com a Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="da500-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="da500-170">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="da500-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="da500-171">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="da500-171">Create a virtual network</span></span>
> * <span data-ttu-id="da500-172">Criar um grupo de recursos e uma VM</span><span class="sxs-lookup"><span data-stu-id="da500-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="da500-173">Habilitar o diagnóstico de inicialização em Olá VM</span><span class="sxs-lookup"><span data-stu-id="da500-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="da500-174">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="da500-174">View boot diagnostics</span></span>
> * <span data-ttu-id="da500-175">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="da500-175">View host metrics</span></span>
> * <span data-ttu-id="da500-176">Instalar a extensão de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="da500-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="da500-177">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="da500-177">View VM metrics</span></span>
> * <span data-ttu-id="da500-178">Criar um alerta</span><span class="sxs-lookup"><span data-stu-id="da500-178">Create an alert</span></span>
> * <span data-ttu-id="da500-179">Configurar monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="da500-179">Set up advanced monitoring</span></span>

<span data-ttu-id="da500-180">Avançar toohello toolearn próximo de tutorial sobre o Centro de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="da500-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="da500-181">Gerenciar a segurança da VM</span><span class="sxs-lookup"><span data-stu-id="da500-181">Manage VM security</span></span>](./tutorial-azure-security.md)