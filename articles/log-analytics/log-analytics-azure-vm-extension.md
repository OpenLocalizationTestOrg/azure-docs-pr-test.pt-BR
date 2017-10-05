---
title: "Conectar máquinas virtuais do Azure ao Log Analytics | Microsoft Docs"
description: "Para máquinas virtuais Windows e Linux em execução no Azure, a maneira recomendada de coletar métricas e logs é instalando a extensão de VM do Azure do Log Analytics. Você pode usar o portal do Azure ou o PowerShell para instalar a extensão da máquina virtual do Log Analytics em VMs do Azure."
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
ms.openlocfilehash: cdae291b546fef4d7fdb8b067c8e4f4c9708d43f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="6286c-104">Conectar máquinas virtuais do Azure ao Log Analytics com um agente do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6286c-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="6286c-105">Para computadores Windows e Linux, o método recomendado para coletar métricas e logs é instalando o agente do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6286c-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="6286c-106">A maneira mais fácil de instalar o agente do Log Analytics em máquinas virtuais do Azure é por meio da Extensão de VM do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6286c-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="6286c-107">Usar a extensão simplifica o processo de instalação e configura automaticamente o agente para enviar dados para o espaço de trabalho do Log Analytics que você especificar.</span><span class="sxs-lookup"><span data-stu-id="6286c-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="6286c-108">O agente também será automaticamente atualizado, garantindo que você disponha dos recursos e correções mais recentes.</span><span class="sxs-lookup"><span data-stu-id="6286c-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="6286c-109">Para máquinas virtuais do Windows, você deve habilitar a extensão de máquina virtual *Microsoft Monitoring Agent*.</span><span class="sxs-lookup"><span data-stu-id="6286c-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="6286c-110">Para máquinas virtuais do Linux, você deve habilitar a extensão de máquina virtual *Agente do OMS para Linux*.</span><span class="sxs-lookup"><span data-stu-id="6286c-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="6286c-111">Saiba mais sobre [extensões de máquina virtual do Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e o [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6286c-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6286c-112">Ao usar a coleta com base em agente para dados de log, você deve configurar [fontes de dados no Log Analytics](log-analytics-data-sources.md) para especificar os logs e métricas a coletar.</span><span class="sxs-lookup"><span data-stu-id="6286c-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6286c-113">Se você configurar o Log Analytics para indexar dados de log usando o [diagnóstico do Azure](log-analytics-azure-storage.md) e se você configurar o agente para coletar os mesmos logs, eles serão coletados duas vezes.</span><span class="sxs-lookup"><span data-stu-id="6286c-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="6286c-114">Você será cobrado por ambas as fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="6286c-114">You are charged for both data sources.</span></span> <span data-ttu-id="6286c-115">Se tiver o agente instalado, você coletará dados de log usando apenas o agente – não configure o Log Analytics para coletar dados de log do Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6286c-115">If you have the agent installed, then collect log data by using only the agent - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="6286c-116">Há três maneiras fáceis de habilitar a extensão da máquina virtual do Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="6286c-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="6286c-117">Usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6286c-117">By using the Azure portal</span></span>
* <span data-ttu-id="6286c-118">Usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6286c-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="6286c-119">Usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6286c-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="6286c-120">Habilitar a extensão de VM no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6286c-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="6286c-121">Você pode instalar o agente para o Log Analytics e conectar a máquina virtual do Azure na qual ele é executado usando o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6286c-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="6286c-122">Para instalar o agente do Log Analytics e conectar a máquina virtual a um espaço de trabalho do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6286c-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="6286c-123">Faça logon no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6286c-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="6286c-124">Selecione **Procurar** no lado esquerdo do portal e, em seguida, vá para **Log Analytics (OMS)** e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="6286c-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="6286c-125">Em sua lista de espaços de trabalho do Log Analytics, selecione aquele que você deseja utilizar com a VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="6286c-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![Espaços de trabalho do OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="6286c-127">Em **Gerenciamento do Log Analytics**, selecione **Máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="6286c-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="6286c-128">![Máquinas virtuais](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="6286c-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="6286c-129">Na lista de **Máquinas virtuais**, selecione a máquina virtual em que deseja instalar o agente.</span><span class="sxs-lookup"><span data-stu-id="6286c-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="6286c-130">O **status de conexão do OMS** para a VM indicará que ela **Não está conectada**.</span><span class="sxs-lookup"><span data-stu-id="6286c-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="6286c-131">![VM não conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="6286c-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="6286c-132">Nos detalhes de sua máquina virtual, selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="6286c-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="6286c-133">O agente é automaticamente instalado e configurado para o seu espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6286c-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="6286c-134">Esse processo leva alguns minutos, período durante o qual o status da conexão do OMS é *Conectando-se...*</span><span class="sxs-lookup"><span data-stu-id="6286c-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="6286c-135">![Conectar a VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="6286c-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="6286c-136">Quando o agente estiver instalado e conectado, o status da **Conexão do OMS** será atualizado para mostrar **Este espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6286c-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="6286c-137">![Conectado](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="6286c-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="6286c-138">Habilitar a extensão de VM usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6286c-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="6286c-139">Ao configurar sua máquina virtual usando o PowerShell, você precisa fornecer o **workspaceId** e o **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="6286c-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="6286c-140">Os nomes de propriedade em sua configuração de json **diferenciam maiúsculas de minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="6286c-140">The property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="6286c-141">É possível encontrar a ID e a chave na página **Configurações** do portal do OMS, ou então usando o PowerShell como mostrado no exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="6286c-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![ID do Espaço de Trabalho e Chave Primária](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="6286c-143">Há comandos diferentes para máquinas virtuais clássicas do Azure e máquinas virtuais do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6286c-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="6286c-144">Exemplos tanto de máquinas virtuais clássicas quanto do Resource Manager são fornecidos abaixo.</span><span class="sxs-lookup"><span data-stu-id="6286c-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="6286c-145">Para máquinas virtuais clássicas, use o seguinte exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6286c-145">For classic virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="6286c-146">Para VMs Linux do Gerenciador de Recursos que usam a CLI a seguir</span><span class="sxs-lookup"><span data-stu-id="6286c-146">For Resource Manager Linux VMs using the following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="6286c-147">Para máquinas virtuais do Resource Manager, use o seguinte exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6286c-147">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="6286c-148">Implantar a extensão de VM usando um modelo</span><span class="sxs-lookup"><span data-stu-id="6286c-148">Deploy the VM extension using a template</span></span>
<span data-ttu-id="6286c-149">Usando o Azure Resource Manager, você pode criar um modelo (no formato JSON) que define a implantação e a configuração do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6286c-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="6286c-150">Esse modelo é conhecido como um modelo do Gerenciador de Recursos e fornece uma forma declarativa de definir a implantação.</span><span class="sxs-lookup"><span data-stu-id="6286c-150">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="6286c-151">Usando um modelo, você pode implantar seu aplicativo em todo seu ciclo de vida repetidamente e com a confiança que seus recursos estão sendo implantados em um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="6286c-151">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="6286c-152">Ao incluir o agente do Log Analytics como parte do seu modelo do Resource Manager, você pode assegurar que cada máquina virtual seja pré-configurada para gerar relatórios para seu espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6286c-152">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="6286c-153">Para obter mais informações sobre os modelos do Resource Manager, veja [Criação de Modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6286c-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6286c-154">A seguir está um exemplo de um modelo do Resource Manager que é usado para implantar uma máquina virtual que esteja executando o Windows com a extensão Microsoft Monitoring Agent instalada.</span><span class="sxs-lookup"><span data-stu-id="6286c-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="6286c-155">Este é um modelo de máquina virtual típico, com as seguintes adições:</span><span class="sxs-lookup"><span data-stu-id="6286c-155">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="6286c-156">parâmetros workspaceId e workspaceName</span><span class="sxs-lookup"><span data-stu-id="6286c-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="6286c-157">Seção de extensão de recurso Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="6286c-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="6286c-158">Saídas para pesquisar o workspaceId e o workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="6286c-158">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
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
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
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

<span data-ttu-id="6286c-159">Você pode implantar um modelo usando o comando do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="6286c-159">You can deploy a template by using the following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="6286c-160">Solução de problemas da extensão de VM de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6286c-160">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="6286c-161">Normalmente, você recebe uma mensagem quando as coisas não funcionam no portal do Azure ou no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6286c-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="6286c-162">Faça logon no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6286c-162">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="6286c-163">Localize a VM e abra os detalhes da VM.</span><span class="sxs-lookup"><span data-stu-id="6286c-163">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="6286c-164">Clique em **Extensões** para verificar se a extensão do OMS está habilitada ou não.</span><span class="sxs-lookup"><span data-stu-id="6286c-164">Click **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![Exibição da Extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="6286c-166">Clique na extensão *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) e exiba os detalhes.</span><span class="sxs-lookup"><span data-stu-id="6286c-166">Click the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Detalhes da Extensão da VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="6286c-168">Solucionando problemas das Máquinas Virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="6286c-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="6286c-169">Se a extensão do agente de VM *Microsoft Monitoring Agent* não está instalando ou reportando, você pode executar as etapas a seguir para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="6286c-169">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="6286c-170">Verifique se o agente de VM do Azure está instalado e funcionando corretamente usando as etapas em [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="6286c-170">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="6286c-171">Você também pode examinar o arquivo de log do agente de VM `C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="6286c-171">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="6286c-172">Se o log não existir, isso significará que o agente de VM não está instalado.</span><span class="sxs-lookup"><span data-stu-id="6286c-172">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="6286c-173">Instalar o Agente de VM do Azure em VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="6286c-173">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="6286c-174">Confirme que a tarefa de pulsação da extensão do Microsoft Monitoring Agent está em execução usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6286c-174">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="6286c-175">Fazer logon na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6286c-175">Log in to the virtual machine</span></span>
   * <span data-ttu-id="6286c-176">Abrir o agendador de tarefas e localizar a tarefa `update_azureoperationalinsight_agent_heartbeat`</span><span class="sxs-lookup"><span data-stu-id="6286c-176">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="6286c-177">Confirmar que a tarefa está habilitada e está executando a cada minuto</span><span class="sxs-lookup"><span data-stu-id="6286c-177">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="6286c-178">Verificar o arquivo de log de pulsação em `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="6286c-178">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="6286c-179">Examinar os arquivos de log de extensão de VM do Microsoft Monitoring Agent em `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="6286c-179">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="6286c-180">Certificar-se de que a máquina virtual pode executar scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6286c-180">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="6286c-181">Certificar-se de que as permissões em C:\Windows\temp não foram alteradas</span><span class="sxs-lookup"><span data-stu-id="6286c-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="6286c-182">Exibir o status do Microsoft Monitoring Agent, digitando o seguinte comando em uma janela do PowerShell com privilégios elevados na máquina virtual `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="6286c-182">View the status of the Microsoft Monitoring Agent by typing the following command in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="6286c-183">Examinar os arquivos de log de instalação do Microsoft Monitoring Agent em `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="6286c-183">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="6286c-184">Para obter mais informações, consulte [Solucionando problemas em extensões do Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6286c-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="6286c-185">Solucionando Problemas em Máquinas Virtuais Linux</span><span class="sxs-lookup"><span data-stu-id="6286c-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="6286c-186">Se a extensão do agente de VM *Agente do OMS para Linux* não estiver instalando ou reportando, você pode executar as etapas a seguir para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="6286c-186">If the *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="6286c-187">Se o status da extensão for *Desconhecido*, verifique se o agente de VM do Azure está instalado e funcionando corretamente, examinando o arquivo de log do agente de VM `/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="6286c-187">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="6286c-188">Se o log não existir, isso significará que o agente de VM não está instalado.</span><span class="sxs-lookup"><span data-stu-id="6286c-188">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="6286c-189">Instalar o Agente de VM do Azure em VMs Linux</span><span class="sxs-lookup"><span data-stu-id="6286c-189">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="6286c-190">Para outros status não íntegros, examine o Agente do OMS para arquivos de log de extensão de VMs do Linux em `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="6286c-190">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="6286c-191">Se o status da extensão estiver íntegro mas os dados não estiverem sendo carregados, examine o Agente do OMS para arquivos de log do Linux em `/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="6286c-191">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="6286c-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6286c-192">Next steps</span></span>
* <span data-ttu-id="6286c-193">Configurar [fontes de dados no Log Analytics](log-analytics-data-sources.md) para especificar os logs e as métricas a coletar.</span><span class="sxs-lookup"><span data-stu-id="6286c-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="6286c-194">[Adicionar soluções do Log Analytics da Galeria de Soluções](log-analytics-add-solutions.md) para coletar dados de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6286c-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="6286c-195">[Coletar dados usando o Diagnóstico do Azure](log-analytics-azure-storage.md) para outros recursos em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="6286c-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="6286c-196">Para computadores que não estão no Azure, você pode instalar o agente do Log Analytics usando os métodos descritos nos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="6286c-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="6286c-197">Conectar computadores Windows ao Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6286c-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="6286c-198">Conectar computadores Linux ao Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6286c-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)
