---
title: "aaaAutoscale conjuntos de escala de máquinas virtuais do Windows | Microsoft Docs"
description: "Configurar o dimensionamento automático para um conjunto de escala de máquina virtual do Windows usando o Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a>Dimensionar automaticamente máquinas em um conjunto de escala de máquina virtual
Conjuntos de escala de máquinas virtuais tornam mais fácil para você toodeploy e gerenciam máquinas virtuais idênticas como um conjunto. Os conjuntos de dimensionamento fornecem uma camada de computação altamente escalonável e personalizável para aplicativos de hiperescala e suporte a imagens da plataforma Windows, imagens da plataforma Linux, imagens personalizadas e extensões. Para obter mais informações sobre conjuntos de dimensionamento, confira [Conjuntos de Dimensionamento de Máquina Virtual](virtual-machine-scale-sets-overview.md).

Este tutorial mostra como definir toocreate um conjunto de escala de máquinas virtuais do Windows e automaticamente escala máquinas Olá Olá. Você cria escala Olá definir e configurar o dimensionamento criando um modelo do Gerenciador de recursos do Azure e implantá-lo usando o PowerShell do Azure. Para obter mais informações sobre modelos, confira [Criação de modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md). toolearn mais sobre o dimensionamento automático de conjuntos de escala, consulte [o dimensionamento automático e conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-autoscale-overview.md).

Neste artigo, você implanta a seguir Olá recursos e extensões:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Para obter mais informações sobre os recursos do Resource Manager, consulte [Azure Resource Manager versus implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="step-1-install-azure-powershell"></a>Etapa 1: instalar o PowerShell do Azure
Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecionando a sua assinatura e entrar no tooAzure.

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a>Etapa 2: Criar um grupo de recursos e uma conta de armazenamento
1. **Criar um grupo de recursos** – todos os recursos devem ser implantado tooa grupo de recursos. Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate um grupo de recursos denominado **vmsstestrg1**.
2. **Criar uma conta de armazenamento** – esta conta de armazenamento é onde o modelo de saudação é armazenado. Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate uma conta de armazenamento denominada **vmsstestsa**.

## <a name="step-3-create-hello-template"></a>Etapa 3: Criar o modelo de saudação
Um modelo do Gerenciador de recursos do Azure possibilita que você toodeploy e gerenciar recursos do Azure juntos usando uma descrição de JSON dos recursos de saudação e parâmetros de implantação associados.

1. Em seu editor favorito, crie o arquivo de Olá C:\VMSSTemplate.json e adicione a saudação inicial JSON toosupport Olá modelo de estrutura.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Parâmetros não são sempre obrigatórias, mas eles fornecem uma maneira tooinput valores quando Olá modelo é implantado. Adicione esses parâmetros no elemento de pai do hello parâmetros que você adicionou toohello modelo.

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * Um nome para Olá outra máquina virtual que é usado tooaccess Olá máquinas no conjunto de escala de saudação.
    * nome de Olá Olá da conta de armazenamento onde o modelo de saudação é armazenado.
    * número de saudação de máquinas virtuais tooinitially criar no conjunto de escala de saudação.
    * nome de Hello e a senha da conta de administrador de saudação em máquinas virtuais de saudação.
    * Um prefixo de nome para recursos de saudação que são criados a escala de saudação toosupport definido.

3. Variáveis podem ser usadas em valores de toospecify um modelo que podem ser alterados com frequência ou valores que precisam de toobe criadas de uma combinação de valores de parâmetro. Adicione essas variáveis no elemento de pai do hello variáveis que você adicionou toohello modelo.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * Nomes DNS que são usados por Olá interfaces de rede.

        * nomes de endereços IP Hello e prefixos de rede virtual hello e sub-redes.
        * Olá nomes e identificadores de rede virtual do hello, balanceador de carga e interfaces de rede.
        * Nomes de conta de armazenamento para contas de saudação associadas máquinas Olá no conjunto de escala de saudação.
        * Configurações de extensão de diagnóstico está instalado em máquinas virtuais de saudação do hello. Para obter mais informações sobre Olá extensão de diagnóstico, consulte [criar uma máquina Virtual do Windows com o monitoramento e diagnóstico usando o modelo do Gerenciador de recursos do Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Adicione o recurso de conta de armazenamento Olá sob o elemento de pai do hello recursos que você adicionou toohello modelo. Este modelo usa uma saudação de toocreate loop recomendada cinco contas de armazenamento onde os discos do sistema operacional hello e dados de diagnóstico são armazenados. Esse conjunto de contas pode dar suporte a backup de máquinas virtuais de too100 em um conjunto de escala, que é o máximo de saudação atual. Cada conta de armazenamento é nomeada com um designador que foi definido em variáveis de saudação combinados com o prefixo de Olá que você fornece parâmetros Olá para o modelo de saudação.

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. Adicione recursos de rede virtual hello. Confira [Provedor de Recurso de Rede](../virtual-network/resource-groups-networking.md)para obter mais informações.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Adicione Olá públicos recursos de endereço IP que são usados por Olá balanceador de carga e interface de rede.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Adicione o recurso de Balanceador de carga de saudação que é usado pelo conjunto de escala de saudação. Para obter mais informações, confira [Suporte do Gerenciador de Recursos do Azure para Balanceador de Carga](../load-balancer/load-balancer-arm.md).

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. Adicione recurso Olá de interface de rede que é usado pela máquina virtual separada de saudação. Como máquinas em um conjunto de escala não são acessíveis por meio de um endereço IP público, uma outra máquina virtual é criada no hello mesmo virtual tooremotely máquinas de saudação de acesso de rede.

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Adicione máquina virtual separada de saudação em Olá mesma rede como conjunto de escala de saudação.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
        }
      }
    },
    ```

10. Adicionar recursos do conjunto de escala de máquinas virtuais hello e especifique a extensão de diagnóstico de saudação que é instalado em todas as máquinas virtuais no conjunto de escala de saudação. Muitas das configurações de saudação do recurso são semelhantes com o recurso de máquina virtual de saudação. Olá principais diferenças são o elemento de capacidade de saudação que especifica o número de saudação de máquinas virtuais no conjunto de escala hello e upgradePolicy que especifica como as atualizações são feitas toovirtual máquinas. Olá conjunto de escala não é criado até que todas as contas de armazenamento Olá são criadas conforme especificado com o elemento de dependsOn hello.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Adicione Olá autoscaleSettings recurso que define como o conjunto de escala Olá ajusta com base no uso do processador Olá nas máquinas Olá Olá conjunto de escala.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    Para este tutorial, estes valores são importantes:
    
    * **metricName**  
    Esse valor é Olá mesmo que o contador de desempenho de saudação que definimos na variável de wadperfcounter hello. Usando essa variável, Olá extensão de diagnóstico coleta Olá **( total)\% tempo processador** contador.
    
    * **metricResourceUri**  
    Esse valor é o identificador de recurso de saudação do conjunto de escala de máquinas virtuais de saudação.
    
    * **timeGrain**  
    Esse valor é a granularidade de saudação de métricas de saudação que são coletadas. Neste modelo, ele é definido tooone minuto.
    
    * **statistic**  
    Esse valor determina como as métricas de saudação são combinados tooaccommodate Olá automática de ação de dimensionamento. Olá os valores possíveis são: média, Mín, máx. Neste modelo, Olá médio total da CPU de máquinas virtuais de saudação é coletada.
    
    * **timeWindow**  
    Esse valor é Olá intervalo de tempo no qual os dados de instância são coletados. Deve estar entre 5 minutos e 12 horas.
    
    * **timeAggregation**  
    o valor determina como os dados de saudação que são coletados devem ser combinados ao longo do tempo. valor padrão de saudação é média. Olá os valores possíveis são: média, mínimo, máximo, último, Total, contagem.
    
    * **operator**  
    Esse valor é o operador Olá toocompare usado Olá métrica dados e hello limite. Olá os valores possíveis são: igual a, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **threshold**  
    Esse valor será Olá que dispara a ação de escala de saudação. Neste modelo, as máquinas são adicionadas toohello escala definida quando o uso médio de CPU Olá entre as máquinas no conjunto de saudação é acima de 50%.
    
    * **direction**  
    Esse valor determina a ação de saudação que é obtida quando o valor de limite de saudação é obtida. Olá possíveis valores são aumento ou diminuição. Neste modelo, hello número de máquinas virtuais no conjunto de escala de saudação é aumentado se o limite de saudação é acima de 50% na janela de tempo de saudação definida.
    
    * **tipo**  
    Esse valor é o tipo de saudação de ação que deve ocorrer e deve ser definido como tooChangeCount.
    
    * **valor**  
    Esse valor é o número de saudação de máquinas virtuais que são adicionados ou removidos do conjunto de escala de saudação. Este valor deve ser 1 ou maior. valor padrão de saudação é 1. Neste modelo, número de saudação de máquinas em escala Olá conjunto aumenta por 1 quando Olá limite é atingido.
    
    * **cooldown**  
    Esse valor é Olá toowait tempo desde a última ação de escala Olá antes da próxima ação de saudação. Esse valor deve estar entre um minuto e uma semana.

12. Salve o arquivo de modelo de saudação.    

## <a name="step-4-upload-hello-template-toostorage"></a>Etapa 4: Carregar Olá modelo toostorage
modelo de saudação pode ser carregado desde que saiba o nome de saudação e a chave primária Olá da conta de armazenamento que você criou na etapa 1.

1. Na janela do Microsoft Azure PowerShell hello, defina uma variável que especifica o nome de Olá Olá da conta de armazenamento que você criou na etapa 1.
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. Defina uma variável que especifica a chave primária Olá Olá da conta de armazenamento.
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   Você pode obter essa chave clicando o ícone de chave Olá ao exibir o recurso de conta de armazenamento Olá no hello portal do Azure.
3. Crie objeto contexto de conta de armazenamento de saudação que é usado toovalidate operações com conta de armazenamento de saudação.
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. Crie contêiner Olá para armazenar o modelo de saudação.

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. Carregar Olá modelo arquivo toohello novo contêiner.

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a>Etapa 5: Implantar o modelo de saudação
Agora que você criou o modelo de hello, você pode iniciar a implantação recursos hello. Use esse processo de saudação do comando toostart:

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

Quando você pressiona insira, são solicitadas tooprovide valores variáveis de Olá atribuída. Forneça esses valores:

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

Ele deve levar cerca de 15 minutos para todos os toosuccessfully de recursos de saudação ser implantada.

> [!NOTE]
> Você também pode usar os recursos de saudação do portal Olá capacidade toodeploy. Use este link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"
> 
> 

## <a name="step-6-monitor-resources"></a>Etapa 6: Monitorar recursos
Você pode obter informações sobre os conjuntos de dimensionamento de máquina virtual usando estes métodos:

* Olá portal do Azure - no momento você pode obter uma quantidade limitada de informações usando o portal de saudação.
* Olá [Gerenciador de recursos do Azure](https://resources.azure.com/) -essa ferramenta é hello melhor para explorar o estado atual de saudação do seu conjunto de escala. Siga este caminho e você deverá ver a exibição de instância de saudação de escala Olá definido que você criou:
  
    subscriptions > {sua assinatura} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines

* PowerShell do Azure - Use esse comando tooget algumas informações:

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  Ou
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* Conecte-se a máquina virtual separada de toohello exatamente como faria com qualquer outro computador e, em seguida, você pode acessar remotamente máquinas virtuais Olá Olá escala conjunto toomonitor individuais processos.

> [!NOTE]
> Uma API REST completa para obter informações sobre conjuntos de dimensionamento podem ser encontradas nos [Conjuntos de Dimensionamento de Máquina Virtual](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-7-remove-hello-resources"></a>Etapa 7: Remover recursos Olá
Como você é cobrado pelos recursos usados no Azure, sempre é um recurso de toodelete de práticas recomendadas que não é mais necessários. Você não precisa toodelete cada recurso separadamente de um grupo de recursos. Você pode excluir o grupo de recursos de saudação e todos os seus recursos são excluídos automaticamente.

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

Se você quiser tookeep seu grupo de recursos, você pode excluir escala Olá definida apenas.

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a>Próximas etapas
* Gerenciar o conjunto de escala de saudação que você acabou criada usando as informações de saudação em [gerenciar máquinas virtuais em um conjunto de escala de máquinas virtuais](virtual-machine-scale-sets-windows-manage.md).
* Saiba mais sobre a escala vertical revisando [Dimensionamento vertical automático com conjuntos de escala de máquina virtual](virtual-machine-scale-sets-vertical-scale-reprovision.md)
* Encontre exemplos de recursos de monitoramento do Azure Monitor nos [Exemplos de início rápido do Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)
* Saiba mais sobre os recursos de notificação no [usar AutoEscala ações toosend email e webhook notificações de alerta no Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Saiba como muito[notificações de alerta de e-mail e webhook toosend os logs de auditoria de uso no Monitor do Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

