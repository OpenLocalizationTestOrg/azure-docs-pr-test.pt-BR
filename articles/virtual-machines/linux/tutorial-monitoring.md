---
title: "Monitorar máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Saiba como monitorar o diagnóstico de inicialização e as métricas de desempenho em uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 3fe8390e88e609b57a462e066f972346f8e8730e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="4ea4b-103">Como monitorar uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="4ea4b-103">How to monitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="4ea4b-104">Para garantir que suas VMs (máquinas virtuais) no Azure estejam sendo executadas corretamente, examine o diagnóstico de inicialização e as métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-104">To ensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="4ea4b-105">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ea4b-106">Habilitar o diagnóstico de inicialização na VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-106">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="4ea4b-107">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="4ea4b-107">View boot diagnostics</span></span>
> * <span data-ttu-id="4ea4b-108">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="4ea4b-108">View host metrics</span></span>
> * <span data-ttu-id="4ea4b-109">Habilitar a extensão de diagnóstico na VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-109">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="4ea4b-110">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-110">View VM metrics</span></span>
> * <span data-ttu-id="4ea4b-111">Criar alertas com base nas métricas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4ea4b-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="4ea4b-112">Configurar monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="4ea4b-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4ea4b-113">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4ea4b-114">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="4ea4b-115">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="4ea4b-116">Criar VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-116">Create VM</span></span>

<span data-ttu-id="4ea4b-117">Para ver os diagnósticos e as métricas em ação, você precisa de uma VM.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-117">To see diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="4ea4b-118">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4ea4b-119">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroupMonitor* no local *eastus*.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-119">The following example creates a resource group named *myResourceGroupMonitor* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="4ea4b-120">Agora, crie uma VM com [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="4ea4b-121">O exemplo a seguir cria uma VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-121">The following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="4ea4b-122">Habilitar o diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="4ea4b-122">Enable boot diagnostics</span></span>

<span data-ttu-id="4ea4b-123">Durante a inicialização das VMs do Linux, a extensão de diagnóstico de inicialização captura a saída de inicialização e a armazena no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-123">As Linux VMs boot, the boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="4ea4b-124">Esses dados podem ser usados para solucionar problemas de inicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-124">This data can be used to troubleshoot VM boot issues.</span></span> <span data-ttu-id="4ea4b-125">Os diagnósticos de inicialização não são habilitados automaticamente quando você cria uma VM do Linux usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-125">Boot diagnostics are not automatically enabled when you create a Linux VM using the Azure CLI.</span></span>

<span data-ttu-id="4ea4b-126">Antes de habilitar o diagnóstico de inicialização, é necessário criar uma conta de armazenamento para armazenar os logs de inicialização.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-126">Before enabling boot diagnostics, a storage account needs to be created for storing boot logs.</span></span> <span data-ttu-id="4ea4b-127">As contas de armazenamento devem ter um nome exclusivo globalmente, com três a 24 caracteres e conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="4ea4b-128">Crie uma conta de armazenamento com o comando [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-128">Create a storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="4ea4b-129">Neste exemplo, uma cadeia de caracteres aleatória é usada para criar um nome de conta de armazenamento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-129">In this example, a random string is used to create a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="4ea4b-130">Ao habilitar o diagnóstico de inicialização, o URI do contêiner de armazenamento de blobs é exigido.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-130">When enabling boot diagnostics, the URI to the blob storage container is needed.</span></span> <span data-ttu-id="4ea4b-131">O comando a seguir consulta a conta de armazenamento para retornar esse URI.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-131">The following command queries the storage account to return this URI.</span></span> <span data-ttu-id="4ea4b-132">O valor do URI é armazenado em uma variável chamada *bloburi*, que é usada na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-132">The URI value is stored in a variable names *bloburi*, which is used in the next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="4ea4b-133">Agora, habilite o diagnóstico de inicialização com [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="4ea4b-134">O valor `--storage` é o URI do blob coletado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-134">The `--storage` value is the blob URI collected in the previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="4ea4b-135">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="4ea4b-135">View boot diagnostics</span></span>

<span data-ttu-id="4ea4b-136">Quando o diagnóstico de inicialização for habilitado, sempre que você parar e iniciar a VM, as informações sobre o processo de inicialização serão gravadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-136">When boot diagnostics are enabled, each time you stop and start the VM, information about the boot process is written to a log file.</span></span> <span data-ttu-id="4ea4b-137">Para este exemplo, primeiro desaloque a VM com o comando [az vm deallocate](/cli/azure/vm#deallocate) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-137">For this example, first deallocate the VM with the [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="4ea4b-138">Agora, inicie a VM com o comando [az vm start]( /cli/azure/vm#stop) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-138">Now start the VM with the [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="4ea4b-139">Você pode obter os dados de diagnóstico de inicialização para *myVM* com o comando [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-139">You can get the boot diagnostic data for *myVM* with the [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="4ea4b-140">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="4ea4b-140">View host metrics</span></span>

<span data-ttu-id="4ea4b-141">Uma VM do Linux tem um host dedicado no Azure com o qual ela interage.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="4ea4b-142">As métricas são coletadas automaticamente para o host e podem ser exibidas no Portal do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-142">Metrics are automatically collected for the host and can be viewed in the Azure portal as follows:</span></span>

1. <span data-ttu-id="4ea4b-143">No Portal do Azure, clique em **Grupos de Recursos**, selecione **myResourceGroupMonitor** e, em seguida, selecione **myVM** na lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-143">In the Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="4ea4b-144">Para ver como está o desempenho da VM do host, clique em **Métricas** na folha da VM e, em seguida, selecione qualquer uma das métricas de *Host* em **Métricas disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-144">To see how the host VM is performing, click **Metrics** on the VM blade, then select any of the *[Host]* metrics under **Available metrics**.</span></span>

    ![Exibir métricas de host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="4ea4b-146">Instalar extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4ea4b-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ea4b-147">Este documento descreve a versão 2.3 da Extensão de Diagnóstico do Linux, a qual está preterida.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-147">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="4ea4b-148">A versão 2.3 será suportada até 30 de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="4ea4b-149">A versão 3.0 da Extensão de Diagnóstico do Linux pode ser ativada em vez disso.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-149">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="4ea4b-150">Para obter mais informações, consulte a [documentação](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-150">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="4ea4b-151">As métricas de host básicas estão disponíveis, mas para ver métricas mais granulares e específicas de VM, você precisa instalar a extensão de Diagnóstico do Azure na VM.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-151">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="4ea4b-152">A extensão de Diagnóstico do Azure permite que dados de monitoramento e diagnóstico adicionais sejam recuperados da VM.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-152">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="4ea4b-153">Você pode exibir essas métricas de desempenho e criar alertas com base no desempenho de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-153">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="4ea4b-154">A extensão de diagnóstico é instalada por meio do Portal do Azure, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-154">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="4ea4b-155">No Portal do Azure, clique em **Grupos de Recursos**, selecione **myResourceGroup** e, em seguida, selecione **myVM** na lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-155">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="4ea4b-156">Clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="4ea4b-157">A lista mostra que o *Diagnóstico de inicialização* já está habilitado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-157">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="4ea4b-158">Clique na caixa de seleção para as *Métricas básicas*.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-158">Click the check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="4ea4b-159">Na seção *Conta de armazenamento*, navegue até a conta *mydiagdata[1234]* criada na seção anterior e selecione-a.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-159">In the *Storage account* section, browse to and select the *mydiagdata[1234]* account created in the previous section.</span></span>
1. <span data-ttu-id="4ea4b-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4ea4b-160">Click the **Save** button.</span></span>

    ![Exibir métricas de diagnóstico](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="4ea4b-162">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-162">View VM metrics</span></span>

<span data-ttu-id="4ea4b-163">Você pode exibir as métricas da VM da mesma maneira que você exibiu as métricas da VM host:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-163">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="4ea4b-164">No Portal do Azure, clique em **Grupos de Recursos**, selecione **myResourceGroup** e, em seguida, selecione **myVM** na lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-164">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="4ea4b-165">Para ver como está o desempenho da VM do Host, clique em **Métricas** na folha da VM e, em seguida, selecione qualquer uma das métricas de diagnóstico em **Métricas disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-165">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Exibir métricas de VM](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="4ea4b-167">Criar alertas</span><span class="sxs-lookup"><span data-stu-id="4ea4b-167">Create alerts</span></span>

<span data-ttu-id="4ea4b-168">Você pode criar alertas com base em métricas de desempenho específicas.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="4ea4b-169">Alertas podem ser usados para lhe notificar quando uso médio da CPU excede um determinado limite ou o espaço em disco livre disponível cai abaixo de um determinado valor, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-169">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="4ea4b-170">Os alertas são exibidos no Portal do Azure, ou podem ser enviados por email.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-170">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="4ea4b-171">Você também pode disparar Runbooks da Automação do Azure ou Aplicativos Lógicos do Azure em resposta à geração de alertas.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="4ea4b-172">O exemplo a seguir cria um alerta para uso médio da CPU.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-172">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="4ea4b-173">No Portal do Azure, clique em **Grupos de Recursos**, selecione **myResourceGroup** e, em seguida, selecione **myVM** na lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-173">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="4ea4b-174">Clique em **Regras de alerta** na folha da VM e, em seguida, clique em **Adicionar alerta de métrica** na parte superior da folha de alertas.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-174">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="4ea4b-175">Forneça um **Nome** para o alerta, como *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="4ea4b-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="4ea4b-176">Para disparar um alerta quando o percentual de CPU excede 1.0 por cinco minutos, deixe todos os outros padrões selecionados.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-176">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="4ea4b-177">Opcionalmente, marque a caixa de *Proprietários, colaboradores e leitores de email* para enviar uma notificação por email.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-177">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="4ea4b-178">A ação padrão é apresentar uma notificação no portal.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-178">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="4ea4b-179">Clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-179">Click the **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="4ea4b-180">Monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="4ea4b-180">Advanced monitoring</span></span> 

<span data-ttu-id="4ea4b-181">Você pode fazer um monitoramento mais avançado da sua VM usando o [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="4ea4b-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="4ea4b-182">Caso ainda não tenha feito isso, você pode se inscrever para uma [avaliação gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="4ea4b-183">Quando você tem acesso ao portal do OMS, você pode encontrar a chave e o identificador de espaço de trabalho na folha Configurações.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-183">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="4ea4b-184">Substitua <workspace-key> e <workspace-id> pelos valores de seu espaço de trabalho OMS e, em seguida, use **az vm extension set** para adicionar a extensão do OMS à VM:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-184">Replace <workspace-key> and <workspace-id> with the values for from your OMS workspace and then you can use **az vm extension set** to add the OMS extension to the VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="4ea4b-185">Na folha Pesquisa de Logsdo portal do OMS, você deve ver *myVM*, como mostra a figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-185">On the Log Search blade of the OMS portal, you should see *myVM* such as what is shown in the following picture:</span></span>

![Folha do OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="4ea4b-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ea4b-187">Next steps</span></span>

<span data-ttu-id="4ea4b-188">Neste tutorial, você configurou e revisou VMs com a Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="4ea4b-189">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="4ea4b-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ea4b-190">Habilitar o diagnóstico de inicialização na VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-190">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="4ea4b-191">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="4ea4b-191">View boot diagnostics</span></span>
> * <span data-ttu-id="4ea4b-192">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="4ea4b-192">View host metrics</span></span>
> * <span data-ttu-id="4ea4b-193">Habilitar a extensão de diagnóstico na VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-193">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="4ea4b-194">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-194">View VM metrics</span></span>
> * <span data-ttu-id="4ea4b-195">Criar alertas com base nas métricas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4ea4b-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="4ea4b-196">Configurar monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="4ea4b-196">Set up advanced monitoring</span></span>

<span data-ttu-id="4ea4b-197">Avance para o próximo tutorial para saber mais sobre a Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea4b-197">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ea4b-198">Gerenciar a segurança da VM</span><span class="sxs-lookup"><span data-stu-id="4ea4b-198">Manage VM security</span></span>](./tutorial-azure-security.md)