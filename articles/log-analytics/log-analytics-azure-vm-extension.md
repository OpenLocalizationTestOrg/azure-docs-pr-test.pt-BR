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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Conectar-se a análise de tooLog de máquinas virtuais do Azure com um agente de análise de Log

Para computadores Windows e Linux, Olá recomendado para coletar logs e métricas é instalar o agente de análise de Log de saudação.

Olá mais fácil maneira tooinstall Olá análise de Log agente em máquinas virtuais do Azure é por meio de Olá extensão de VM de análise de Log.  Usando a extensão de saudação simplifica o processo de instalação hello e configura automaticamente Olá agente toosend dados toohello análise de Log espaço de trabalho que você especificar. Agente de saudação também é atualizado automaticamente, garantindo que você tenha correções e recursos mais recentes de saudação.

Para máquinas virtuais do Windows, habilitar Olá *Microsoft Monitoring Agent* extensão da máquina virtual.
Para máquinas virtuais Linux, você habilita Olá *agente do OMS para Linux* extensão da máquina virtual.

Saiba mais sobre [extensões de máquina virtual do Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e hello [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Quando você usa a coleção com base em agente para dados de log, você deve configurar [fontes de dados de análise de Log](log-analytics-data-sources.md) toospecify Olá logs e métricas que você deseja toocollect.

> [!IMPORTANT]
> Se você configurar dados do log de análise de Log tooindex usando [diagnóstico do Azure](log-analytics-azure-storage.md), e configurar Olá Olá de toocollect agente mesmo logs, em seguida, Olá logs são coletados duas vezes. Você será cobrado por ambas as fontes de dados. Se você tiver Olá agente instalado, em seguida, coletar dados de log usando apenas o agente Olá - não configurar dados de log de toocollect de análise de Log de diagnóstico do Azure.
>
>

Há três maneiras de extensão da máquina virtual tooenable Olá análise de Log:

* Usando Olá portal do Azure
* Usando o Azure PowerShell
* Usando um modelo do Azure Resource Manager

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Habilitar a extensão VM Olá no hello portal do Azure
Você pode instalar o agente de saudação para análise de Log e conecte-se Olá máquina virtual do Azure que é executado usando Olá [portal do Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall Olá agente de análise de Log e conecte-se o espaço de trabalho da análise de Log tooa Olá máquina virtual
1. O logon no hello [portal do Azure](http://portal.azure.com).
2. Selecione **procurar** em Olá lado esquerdo da saudação portal e, em seguida, vá muito**Log Analytics (OMS)** e selecioná-lo.
3. Na lista de espaços de trabalho de análise de Log, selecione Olá um que você deseja toouse com hello VM do Azure.  
   ![Espaços de trabalho do OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. Em **Gerenciamento do Log Analytics**, selecione **Máquinas virtuais**.  
   ![Máquinas virtuais](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Na lista de saudação do **máquinas virtuais**, selecione Olá máquina virtual no qual você deseja que o agente de saudação tooinstall. Olá **status de conexão de OMS** para Olá VM indica que ele é **não conectado**.  
   ![VM não conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. Em detalhes Olá para sua máquina virtual, selecione **conectar**. Agente de saudação é automaticamente instalado e configurado para seu espaço de trabalho de análise de Log. Esse processo leva alguns minutos, durante esse período é Olá status de Conexão de OMS *conectando-se...*  
   ![Conectar a VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Depois de instalar e conectar-se o agente hello, Olá **conexão OMS** status será atualizado tooshow **este espaço de trabalho**.  
   ![Conectado](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Habilitar a extensão VM hello usando o PowerShell
Quando você configurar sua máquina virtual usando o PowerShell, você precisa Olá tooprovide **workspaceId** e **workspaceKey**. nomes de propriedade Olá em sua configuração de json são **diferencia maiusculas de minúsculas**.

Você pode encontrar hello Id e chave na Olá **configurações** página do portal do OMS hello, ou usando o PowerShell conforme Olá anterior de exemplo.

![ID do Espaço de Trabalho e Chave Primária](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Há comandos diferentes para máquinas virtuais clássicas do Azure e máquinas virtuais do Resource Manager. Exemplos tanto de máquinas virtuais clássicas quanto do Resource Manager são fornecidos abaixo.

Para máquinas virtuais clássicas, use Olá PowerShell de exemplo a seguir:

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

Para VMs do Linux Gerenciador de recursos usando Olá seguir CLI
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Para máquinas virtuais do Gerenciador de recursos, use Olá PowerShell de exemplo a seguir:

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


## <a name="deploy-hello-vm-extension-using-a-template"></a>Implantar a extensão VM hello usando um modelo
Usando o Gerenciador de recursos do Azure, você pode criar um modelo que define a configuração do seu aplicativo e implantação hello (no formato JSON). Este modelo é conhecido como um modelo do Gerenciador de recursos e fornece uma implantação de toodefine de forma declarativa. Usando um modelo, várias vezes você pode implantar seu aplicativo do ciclo de vida do aplicativo hello e ter certeza de que seus recursos estejam sendo implantados em um estado consistente.

Incluindo o agente de análise de Log hello como parte de seu modelo do Gerenciador de recursos, você pode garantir que cada máquina virtual é o espaço de trabalho de análise de Log de tooyour tooreport pré-configurado.

Para obter mais informações sobre os modelos do Resource Manager, veja [Criação de Modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

A seguir está um exemplo de um modelo do Gerenciador de recursos que é usado para implantar uma máquina virtual que esteja executando o Windows com hello extensão Microsoft Monitoring Agent instalado. Este modelo é um modelo de máquina virtual típica com hello adições a seguir:

* parâmetros workspaceId e workspaceName
* Seção de extensão de recurso Microsoft.EnterpriseCloud.Monitoring
* Saídas toolook workspaceId Olá e workspaceSharedKey

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

Você pode implantar um modelo usando Olá comando PowerShell a seguir:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Extensão de VM de análise de Log de saudação de solução de problemas
Normalmente, você recebe uma mensagem quando as coisas não funcionam no portal do Azure ou no Azure PowerShell.

1. O logon no hello [portal do Azure](http://portal.azure.com).
2. Localize Olá VM e abra os detalhes VM.
3. Clique em **extensões** toocheck se a extensão do OMS está habilitada ou não.

   ![Exibição da Extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Clique em Olá *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) extensão e exibir os detalhes. 

   ![Detalhes da Extensão da VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Solucionando problemas das Máquinas Virtuais do Windows
Se hello *Microsoft Monitoring Agent* extensão do agente de VM não está instalando ou relatórios, você pode executar Olá problema de saudação do tootroubleshoot as etapas a seguir.

1. Verifique se o hello Azure VM agent está instalado e as etapas de trabalho corretamente usando Olá [2965986 KB](https://support.microsoft.com/kb/2965986#mt1).
   * Você também pode analisar o arquivo de log do agente VM Olá`C:\WindowsAzure\logs\WaAppAgent.log`
   * Se o log de saudação não existir, o agente de VM Olá não está instalado.
     * [Instalar hello Azure VM Agent nas VMs clássicas](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Confirme Olá Microsoft Monitoring Agent tarefa de pulsação de extensão está em execução usando Olá etapas a seguir:
   * Faça logon na máquina virtual de toohello
   * Abra o Agendador de tarefas e localize Olá `update_azureoperationalinsight_agent_heartbeat` tarefa
   * Confirmar a tarefa hello está habilitada e está em execução a cada um minuto
   * Verifique o arquivo de log do hello pulsação na`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Arquivos de log de extensão Olá VM de agente de monitoramento da Microsoft em`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Certifique-se a máquina virtual de saudação pode executar scripts do PowerShell
5. Certificar-se de que as permissões em C:\Windows\temp não foram alteradas
6. Exibir o status Olá Olá Microsoft Monitoring Agent digitando Olá comando em uma janela elevada do PowerShell a seguir na máquina virtual de saudação`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Examine os arquivos de log de instalação Olá Microsoft Monitoring Agent em`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Para obter mais informações, consulte [Solucionando problemas em extensões do Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Solucionando Problemas em Máquinas Virtuais Linux
Se hello *agente do OMS para Linux* extensão do agente de VM não está instalando ou relatórios, você pode executar Olá problema de saudação do tootroubleshoot as etapas a seguir.

1. Se o status da extensão Olá é *desconhecido* Verifique se o agente de VM do Azure hello está instalado e funcionando corretamente, examinando o arquivo de log do agente VM Olá`/var/log/waagent.log`
   * Se o log de saudação não existir, o agente de VM Olá não está instalado.
   * [Instalar hello Azure VM Agent em VMs do Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Para outros status Íntegro, examine Olá agente do OMS para a extensão de VM do Linux arquivos de log `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Se o status da extensão hello está íntegro, mas dados não está sendo carregados examine Olá agente do OMS para Linux arquivos de log em`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Próximas etapas
* Configurar [fontes de dados de análise de Log](log-analytics-data-sources.md) toospecify Olá toocollect de logs e métricas.
* toogather dados das máquinas virtuais [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
* [Coletar dados usando o Diagnóstico do Azure](log-analytics-azure-storage.md) para outros recursos em execução no Azure.

Para computadores que não estão no Azure, você pode instalar o agente de análise de Log de saudação usando métodos Olá descritas Olá artigos a seguir:

* [Conecte-se tooLog de computadores Windows análise](log-analytics-windows-agents.md)
* [Conecte-se tooLog de computadores Linux análise](log-analytics-linux-agents.md)
