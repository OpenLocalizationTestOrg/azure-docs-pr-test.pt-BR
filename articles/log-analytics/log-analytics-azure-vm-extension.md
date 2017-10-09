---
title: "máquinas virtuais do Azure de aaaConnect tooLog análise | Microsoft Docs"
description: "Para Windows e Linux máquinas virtuais em execução no Azure, Olá recomendado maneira dos logs coletados e métricas é instalar a extensão de VM do Azure Log Analytics hello. Você pode usar o hello portal do Azure ou o PowerShell tooinstall Olá extensão de máquina virtual de análise de Log em VMs do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="48e76-104">Conectar-se a análise de tooLog de máquinas virtuais do Azure com um agente de análise de Log</span><span class="sxs-lookup"><span data-stu-id="48e76-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="48e76-105">Para computadores Windows e Linux, Olá recomendado para coletar logs e métricas é instalar o agente de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e76-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="48e76-106">Olá mais fácil maneira tooinstall Olá análise de Log agente em máquinas virtuais do Azure é por meio de Olá extensão de VM de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="48e76-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="48e76-107">Usando a extensão de saudação simplifica o processo de instalação hello e configura automaticamente Olá agente toosend dados toohello análise de Log espaço de trabalho que você especificar.</span><span class="sxs-lookup"><span data-stu-id="48e76-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="48e76-108">Agente de saudação também é atualizado automaticamente, garantindo que você tenha correções e recursos mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e76-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="48e76-109">Para máquinas virtuais do Windows, habilitar Olá *Microsoft Monitoring Agent* extensão da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="48e76-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="48e76-110">Para máquinas virtuais Linux, você habilita Olá *agente do OMS para Linux* extensão da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="48e76-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="48e76-111">Saiba mais sobre [extensões de máquina virtual do Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e hello [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48e76-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="48e76-112">Quando você usa a coleção com base em agente para dados de log, você deve configurar [fontes de dados de análise de Log](log-analytics-data-sources.md) toospecify Olá logs e métricas que você deseja toocollect.</span><span class="sxs-lookup"><span data-stu-id="48e76-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48e76-113">Se você configurar dados do log de análise de Log tooindex usando [diagnóstico do Azure](log-analytics-azure-storage.md), e configurar Olá Olá de toocollect agente mesmo logs, em seguida, Olá logs são coletados duas vezes.</span><span class="sxs-lookup"><span data-stu-id="48e76-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="48e76-114">Você será cobrado por ambas as fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="48e76-114">You are charged for both data sources.</span></span> <span data-ttu-id="48e76-115">Se você tiver Olá agente instalado, em seguida, coletar dados de log usando apenas o agente Olá - não configurar dados de log de toocollect de análise de Log de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="48e76-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="48e76-116">Há três maneiras de extensão da máquina virtual tooenable Olá análise de Log:</span><span class="sxs-lookup"><span data-stu-id="48e76-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="48e76-117">Usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="48e76-117">By using hello Azure portal</span></span>
* <span data-ttu-id="48e76-118">Usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e76-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="48e76-119">Usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48e76-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="48e76-120">Habilitar a extensão VM Olá no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="48e76-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="48e76-121">Você pode instalar o agente de saudação para análise de Log e conecte-se Olá máquina virtual do Azure que é executado usando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48e76-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="48e76-122">tooinstall Olá agente de análise de Log e conecte-se o espaço de trabalho da análise de Log tooa Olá máquina virtual</span><span class="sxs-lookup"><span data-stu-id="48e76-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="48e76-123">O logon no hello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48e76-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="48e76-124">Selecione **procurar** em Olá lado esquerdo da saudação portal e, em seguida, vá muito**Log Analytics (OMS)** e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="48e76-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="48e76-125">Na lista de espaços de trabalho de análise de Log, selecione Olá um que você deseja toouse com hello VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="48e76-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Espaços de trabalho do OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="48e76-127">Em **Gerenciamento do Log Analytics**, selecione **Máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="48e76-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="48e76-128">![Máquinas virtuais](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="48e76-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="48e76-129">Na lista de saudação do **máquinas virtuais**, selecione Olá máquina virtual no qual você deseja que o agente de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="48e76-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="48e76-130">Olá **status de conexão de OMS** para Olá VM indica que ele é **não conectado**.</span><span class="sxs-lookup"><span data-stu-id="48e76-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="48e76-131">![VM não conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="48e76-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="48e76-132">Em detalhes Olá para sua máquina virtual, selecione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="48e76-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="48e76-133">Agente de saudação é automaticamente instalado e configurado para seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="48e76-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="48e76-134">Esse processo leva alguns minutos, durante esse período é Olá status de Conexão de OMS *conectando-se...*</span><span class="sxs-lookup"><span data-stu-id="48e76-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="48e76-135">![Conectar a VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="48e76-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="48e76-136">Depois de instalar e conectar-se o agente hello, Olá **conexão OMS** status será atualizado tooshow **este espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="48e76-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="48e76-137">![Conectado](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="48e76-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="48e76-138">Habilitar a extensão VM hello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e76-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="48e76-139">Quando você configurar sua máquina virtual usando o PowerShell, você precisa Olá tooprovide **workspaceId** e **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="48e76-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="48e76-140">nomes de propriedade Olá em sua configuração de json são **diferencia maiusculas de minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="48e76-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="48e76-141">Você pode encontrar hello Id e chave na Olá **configurações** página do portal do OMS hello, ou usando o PowerShell conforme Olá anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="48e76-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![ID do Espaço de Trabalho e Chave Primária](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="48e76-143">Há comandos diferentes para máquinas virtuais clássicas do Azure e máquinas virtuais do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48e76-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="48e76-144">Exemplos tanto de máquinas virtuais clássicas quanto do Resource Manager são fornecidos abaixo.</span><span class="sxs-lookup"><span data-stu-id="48e76-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="48e76-145">Para máquinas virtuais clássicas, use Olá PowerShell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="48e76-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="48e76-146">Para VMs do Linux Gerenciador de recursos usando Olá seguir CLI</span><span class="sxs-lookup"><span data-stu-id="48e76-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="48e76-147">Para máquinas virtuais do Gerenciador de recursos, use Olá PowerShell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="48e76-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="48e76-148">Implantar a extensão VM hello usando um modelo</span><span class="sxs-lookup"><span data-stu-id="48e76-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="48e76-149">Usando o Gerenciador de recursos do Azure, você pode criar um modelo que define a configuração do seu aplicativo e implantação hello (no formato JSON).</span><span class="sxs-lookup"><span data-stu-id="48e76-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="48e76-150">Este modelo é conhecido como um modelo do Gerenciador de recursos e fornece uma implantação de toodefine de forma declarativa.</span><span class="sxs-lookup"><span data-stu-id="48e76-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="48e76-151">Usando um modelo, várias vezes você pode implantar seu aplicativo do ciclo de vida do aplicativo hello e ter certeza de que seus recursos estejam sendo implantados em um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="48e76-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="48e76-152">Incluindo o agente de análise de Log hello como parte de seu modelo do Gerenciador de recursos, você pode garantir que cada máquina virtual é o espaço de trabalho de análise de Log de tooyour tooreport pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="48e76-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="48e76-153">Para obter mais informações sobre os modelos do Resource Manager, veja [Criação de Modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="48e76-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="48e76-154">A seguir está um exemplo de um modelo do Gerenciador de recursos que é usado para implantar uma máquina virtual que esteja executando o Windows com hello extensão Microsoft Monitoring Agent instalado.</span><span class="sxs-lookup"><span data-stu-id="48e76-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="48e76-155">Este modelo é um modelo de máquina virtual típica com hello adições a seguir:</span><span class="sxs-lookup"><span data-stu-id="48e76-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="48e76-156">parâmetros workspaceId e workspaceName</span><span class="sxs-lookup"><span data-stu-id="48e76-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="48e76-157">Seção de extensão de recurso Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="48e76-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="48e76-158">Saídas toolook workspaceId Olá e workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="48e76-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="48e76-159">Você pode implantar um modelo usando Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="48e76-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="48e76-160">Extensão de VM de análise de Log de saudação de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="48e76-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="48e76-161">Normalmente, você recebe uma mensagem quando as coisas não funcionam no portal do Azure ou no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48e76-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="48e76-162">O logon no hello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48e76-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="48e76-163">Localize Olá VM e abra os detalhes VM.</span><span class="sxs-lookup"><span data-stu-id="48e76-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="48e76-164">Clique em **extensões** toocheck se a extensão do OMS está habilitada ou não.</span><span class="sxs-lookup"><span data-stu-id="48e76-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Exibição da Extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="48e76-166">Clique em Olá *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) extensão e exibir os detalhes.</span><span class="sxs-lookup"><span data-stu-id="48e76-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Detalhes da Extensão da VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="48e76-168">Solucionando problemas das Máquinas Virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="48e76-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="48e76-169">Se hello *Microsoft Monitoring Agent* extensão do agente de VM não está instalando ou relatórios, você pode executar Olá problema de saudação do tootroubleshoot as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="48e76-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="48e76-170">Verifique se o hello Azure VM agent está instalado e as etapas de trabalho corretamente usando Olá [2965986 KB](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="48e76-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="48e76-171">Você também pode analisar o arquivo de log do agente VM Olá`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="48e76-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="48e76-172">Se o log de saudação não existir, o agente de VM Olá não está instalado.</span><span class="sxs-lookup"><span data-stu-id="48e76-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="48e76-173">Instalar hello Azure VM Agent nas VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="48e76-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="48e76-174">Confirme Olá Microsoft Monitoring Agent tarefa de pulsação de extensão está em execução usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48e76-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="48e76-175">Faça logon na máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="48e76-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="48e76-176">Abra o Agendador de tarefas e localize Olá `update_azureoperationalinsight_agent_heartbeat` tarefa</span><span class="sxs-lookup"><span data-stu-id="48e76-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="48e76-177">Confirmar a tarefa hello está habilitada e está em execução a cada um minuto</span><span class="sxs-lookup"><span data-stu-id="48e76-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="48e76-178">Verifique o arquivo de log do hello pulsação na`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="48e76-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="48e76-179">Arquivos de log de extensão Olá VM de agente de monitoramento da Microsoft em`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="48e76-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="48e76-180">Certifique-se a máquina virtual de saudação pode executar scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e76-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="48e76-181">Certificar-se de que as permissões em C:\Windows\temp não foram alteradas</span><span class="sxs-lookup"><span data-stu-id="48e76-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="48e76-182">Exibir o status Olá Olá Microsoft Monitoring Agent digitando Olá comando em uma janela elevada do PowerShell a seguir na máquina virtual de saudação`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="48e76-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="48e76-183">Examine os arquivos de log de instalação Olá Microsoft Monitoring Agent em`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="48e76-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="48e76-184">Para obter mais informações, consulte [Solucionando problemas em extensões do Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48e76-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="48e76-185">Solucionando Problemas em Máquinas Virtuais Linux</span><span class="sxs-lookup"><span data-stu-id="48e76-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="48e76-186">Se hello *agente do OMS para Linux* extensão do agente de VM não está instalando ou relatórios, você pode executar Olá problema de saudação do tootroubleshoot as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="48e76-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="48e76-187">Se o status da extensão Olá é *desconhecido* Verifique se o agente de VM do Azure hello está instalado e funcionando corretamente, examinando o arquivo de log do agente VM Olá`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="48e76-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="48e76-188">Se o log de saudação não existir, o agente de VM Olá não está instalado.</span><span class="sxs-lookup"><span data-stu-id="48e76-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="48e76-189">Instalar hello Azure VM Agent em VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="48e76-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="48e76-190">Para outros status Íntegro, examine Olá agente do OMS para a extensão de VM do Linux arquivos de log `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="48e76-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="48e76-191">Se o status da extensão hello está íntegro, mas dados não está sendo carregados examine Olá agente do OMS para Linux arquivos de log em`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="48e76-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="48e76-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48e76-192">Next steps</span></span>
* <span data-ttu-id="48e76-193">Configurar [fontes de dados de análise de Log](log-analytics-data-sources.md) toospecify Olá toocollect de logs e métricas.</span><span class="sxs-lookup"><span data-stu-id="48e76-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="48e76-194">toogather dados das máquinas virtuais [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="48e76-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="48e76-195">[Coletar dados usando o Diagnóstico do Azure](log-analytics-azure-storage.md) para outros recursos em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="48e76-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="48e76-196">Para computadores que não estão no Azure, você pode instalar o agente de análise de Log de saudação usando métodos Olá descritas Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="48e76-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="48e76-197">Conecte-se tooLog de computadores Windows análise</span><span class="sxs-lookup"><span data-stu-id="48e76-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="48e76-198">Conecte-se tooLog de computadores Linux análise</span><span class="sxs-lookup"><span data-stu-id="48e76-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
