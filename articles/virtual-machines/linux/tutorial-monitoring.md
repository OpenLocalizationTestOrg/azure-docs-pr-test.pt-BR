---
title: "máquinas virtuais do aaaMonitor Linux no Azure | Microsoft Docs"
description: "Saiba como toomonitor de inicialização de diagnóstico e métricas de desempenho em uma máquina virtual do Linux no Azure"
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
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="30432-103">Como toomonitor uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="30432-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="30432-104">tooensure que suas máquinas virtuais (VMs) no Azure estão sendo executados corretamente, você pode examinar o diagnóstico de inicialização e métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="30432-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="30432-105">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="30432-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30432-106">Habilitar o diagnóstico de inicialização em Olá VM</span><span class="sxs-lookup"><span data-stu-id="30432-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="30432-107">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="30432-107">View boot diagnostics</span></span>
> * <span data-ttu-id="30432-108">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="30432-108">View host metrics</span></span>
> * <span data-ttu-id="30432-109">Habilitar a extensão de diagnóstico em Olá VM</span><span class="sxs-lookup"><span data-stu-id="30432-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="30432-110">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="30432-110">View VM metrics</span></span>
> * <span data-ttu-id="30432-111">Criar alertas com base nas métricas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="30432-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="30432-112">Configurar monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="30432-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="30432-113">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="30432-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="30432-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="30432-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30432-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="30432-116">Criar VM</span><span class="sxs-lookup"><span data-stu-id="30432-116">Create VM</span></span>

<span data-ttu-id="30432-117">toosee diagnósticos e métricas em ação, você precisa de uma VM.</span><span class="sxs-lookup"><span data-stu-id="30432-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="30432-118">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="30432-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="30432-119">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupMonitor* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="30432-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="30432-120">Agora, crie uma VM com [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="30432-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="30432-121">Olá, exemplo a seguir cria uma VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="30432-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="30432-122">Habilitar o diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="30432-122">Enable boot diagnostics</span></span>

<span data-ttu-id="30432-123">Como inicializar as VMs do Linux, extensão de diagnóstico de inicialização de saudação captura a saída de inicialização e os armazena no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="30432-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="30432-124">Esses dados podem ser usados tootroubleshoot problemas de inicialização VM.</span><span class="sxs-lookup"><span data-stu-id="30432-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="30432-125">O diagnóstico de inicialização não é habilitado automaticamente quando você criar uma VM do Linux usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="30432-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="30432-126">Antes de habilitar o diagnóstico de inicialização, uma conta de armazenamento precisa toobe criado para armazenar logs de inicialização.</span><span class="sxs-lookup"><span data-stu-id="30432-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="30432-127">As contas de armazenamento devem ter um nome exclusivo globalmente, com três a 24 caracteres e conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="30432-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="30432-128">Criar uma conta de armazenamento com hello [criar conta de armazenamento az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="30432-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="30432-129">Neste exemplo, uma cadeia de caracteres aleatória é toocreate usado um nome de conta de armazenamento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="30432-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="30432-130">Ao habilitar o diagnóstico de inicialização, o contêiner de armazenamento de blob do hello URI toohello é necessária.</span><span class="sxs-lookup"><span data-stu-id="30432-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="30432-131">Olá consultas a seguir comando Olá tooreturn da conta de armazenamento esse URI.</span><span class="sxs-lookup"><span data-stu-id="30432-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="30432-132">Olá valor URI é armazenado em uma variável nomes *bloburi*, que é usada na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="30432-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="30432-133">Agora, habilite o diagnóstico de inicialização com [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="30432-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="30432-134">Olá `--storage` valor é blob Olá URI coletado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="30432-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="30432-135">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="30432-135">View boot diagnostics</span></span>

<span data-ttu-id="30432-136">Quando o diagnóstico de inicialização está habilitado, cada vez que você parar e iniciar Olá VM, o processo de inicialização hello serão gravadas informações sobre tooa arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="30432-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="30432-137">Neste exemplo, primeiro desalocar Olá VM com hello [az vm desalocar](/cli/azure/vm#deallocate) comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="30432-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="30432-138">Iniciar agora Olá VM com hello [início de vm az]( /cli/azure/vm#stop) comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="30432-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="30432-139">Você pode obter dados de diagnóstico de inicialização Olá para *myVM* com hello [az vm diagnóstico de inicialização get-inicialização-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="30432-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="30432-140">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="30432-140">View host metrics</span></span>

<span data-ttu-id="30432-141">Uma VM do Linux tem um host dedicado no Azure com o qual ela interage.</span><span class="sxs-lookup"><span data-stu-id="30432-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="30432-142">Métricas são automaticamente coletadas para o host de saudação e podem ser exibidas no portal do Azure de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="30432-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="30432-143">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroupMonitor**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="30432-144">toosee como VM do host hello está sendo executado, clique em **métricas** na folha VM hello, em seguida, selecione qualquer uma das Olá *[Host]* métricas em **métricas disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="30432-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Exibir métricas de host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="30432-146">Instalar extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="30432-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30432-147">Este documento descreve a versão 2.3 Olá extensão de diagnóstico do Linux, que foi preterido.</span><span class="sxs-lookup"><span data-stu-id="30432-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="30432-148">A versão 2.3 será suportada até 30 de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="30432-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="30432-149">A versão 3.0 do hello extensão de diagnóstico do Linux pode ser habilitada em vez disso.</span><span class="sxs-lookup"><span data-stu-id="30432-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="30432-150">Para obter mais informações, consulte [Olá documentação](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="30432-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="30432-151">métricas de host básica Olá estão disponíveis, mas toosee mais granular e métricas de VM específico, você tooneed tooinstall Olá diagnóstico do Azure extensão no hello VM.</span><span class="sxs-lookup"><span data-stu-id="30432-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="30432-152">Olá extensão de diagnóstico do Azure permite o monitoramento adicional e toobe de dados de diagnóstico recuperados da saudação VM.</span><span class="sxs-lookup"><span data-stu-id="30432-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="30432-153">Você pode exibir essas métricas de desempenho e criar alertas com base em como Olá VM executa.</span><span class="sxs-lookup"><span data-stu-id="30432-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="30432-154">extensão de diagnóstico Olá é instalado por meio de saudação portal do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="30432-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="30432-155">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="30432-156">Clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="30432-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="30432-157">lista de saudação mostra que *diagnósticos de inicialização* já estão habilitados na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="30432-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="30432-158">Clique em caixa de seleção Olá *métricas básicas*.</span><span class="sxs-lookup"><span data-stu-id="30432-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="30432-159">Em Olá *conta de armazenamento* seção, procurar Olá selecione tooand *mydiagdata [1234]* conta criada na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="30432-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="30432-160">Clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="30432-160">Click hello **Save** button.</span></span>

    ![Exibir métricas de diagnóstico](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="30432-162">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="30432-162">View VM metrics</span></span>

<span data-ttu-id="30432-163">Você pode exibir as métricas VM Olá no hello mesma maneira que você exibiu métricas VM do host hello:</span><span class="sxs-lookup"><span data-stu-id="30432-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="30432-164">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="30432-165">toosee como Olá VM for executada, clique em **métricas** Olá folha de VM e, em seguida, selecione qualquer uma das métricas de diagnóstico de saudação em **métricas disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="30432-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Exibir métricas de VM](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="30432-167">Criar alertas</span><span class="sxs-lookup"><span data-stu-id="30432-167">Create alerts</span></span>

<span data-ttu-id="30432-168">Você pode criar alertas com base em métricas de desempenho específicas.</span><span class="sxs-lookup"><span data-stu-id="30432-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="30432-169">Alertas podem ser usado toonotify quando uso médio da CPU excede um determinado limite ou espaço em disco livre disponível cai abaixo de um determinado valor, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="30432-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="30432-170">Alertas são exibidos no portal do Azure de saudação ou podem ser enviados por email.</span><span class="sxs-lookup"><span data-stu-id="30432-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="30432-171">Você também pode disparar runbooks de automação do Azure ou aplicativos do Azure lógica tooalerts de resposta que está sendo gerado.</span><span class="sxs-lookup"><span data-stu-id="30432-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="30432-172">Olá, exemplo a seguir cria um alerta para o uso médio da CPU.</span><span class="sxs-lookup"><span data-stu-id="30432-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="30432-173">No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="30432-174">Clique em **regras de alerta** na folha VM hello, em seguida, clique em **adicionar alerta métrica** na parte superior de saudação da folha de alertas de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="30432-175">Forneça um **Nome** para o alerta, como *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="30432-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="30432-176">tootrigger um alerta quando a porcentagem de CPU exceder 1.0 por cinco minutos, deixe Olá todos os outros padrões selecionados.</span><span class="sxs-lookup"><span data-stu-id="30432-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="30432-177">Opcionalmente, marque a caixa da saudação *proprietários, Contribuidores e leitores de Email* toosend notificação por email.</span><span class="sxs-lookup"><span data-stu-id="30432-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="30432-178">ação de padrão de saudação é toopresent uma notificação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="30432-179">Clique em Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="30432-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="30432-180">Monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="30432-180">Advanced monitoring</span></span> 

<span data-ttu-id="30432-181">Você pode fazer um monitoramento mais avançado da sua VM usando o [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="30432-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="30432-182">Caso ainda não tenha feito isso, você pode se inscrever para uma [avaliação gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="30432-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="30432-183">Quando você tiver acesso toohello OMS portal, você pode encontrar o identificador de chave e o espaço de trabalho do espaço de trabalho Olá na folha de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="30432-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="30432-184">Substitua < chave do espaço de trabalho > e < id do espaço de trabalho > com valores de saudação para do seu OMS espaço de trabalho e, em seguida, você pode usar **conjunto de extensão de vm az** tooadd Olá OMS extensão toohello VM:</span><span class="sxs-lookup"><span data-stu-id="30432-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

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

<span data-ttu-id="30432-185">Na folha de pesquisa de Log de saudação do portal do OMS hello, você deve ver *myVM* como o mostrado na figura abaixo de saudação:</span><span class="sxs-lookup"><span data-stu-id="30432-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![Folha do OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="30432-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30432-187">Next steps</span></span>

<span data-ttu-id="30432-188">Neste tutorial, você configurou e revisou VMs com a Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="30432-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="30432-189">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="30432-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30432-190">Habilitar o diagnóstico de inicialização em Olá VM</span><span class="sxs-lookup"><span data-stu-id="30432-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="30432-191">Exibir diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="30432-191">View boot diagnostics</span></span>
> * <span data-ttu-id="30432-192">Exibir métricas de host</span><span class="sxs-lookup"><span data-stu-id="30432-192">View host metrics</span></span>
> * <span data-ttu-id="30432-193">Habilitar a extensão de diagnóstico em Olá VM</span><span class="sxs-lookup"><span data-stu-id="30432-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="30432-194">Exibir métricas de VM</span><span class="sxs-lookup"><span data-stu-id="30432-194">View VM metrics</span></span>
> * <span data-ttu-id="30432-195">Criar alertas com base nas métricas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="30432-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="30432-196">Configurar monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="30432-196">Set up advanced monitoring</span></span>

<span data-ttu-id="30432-197">Avançar toohello toolearn próximo de tutorial sobre o Centro de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="30432-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30432-198">Gerenciar a segurança da VM</span><span class="sxs-lookup"><span data-stu-id="30432-198">Manage VM security</span></span>](./tutorial-azure-security.md)