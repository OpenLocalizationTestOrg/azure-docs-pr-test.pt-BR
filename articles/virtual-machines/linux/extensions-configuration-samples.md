---
title: "Exemplo de configuração de extensões de VM do Linux | Microsoft Docs"
description: "Configuração de exemplo para criação de modelos com extensões para VMs do Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f50e6b2-fce0-41ef-823d-df433957601a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/13/2016
ms.author: kundanap
ms.openlocfilehash: 7bdc28328f29005ae48cc281a05fce7067c96556
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="linux-vm-extension-configuration-samples"></a><span data-ttu-id="77e22-103">Exemplos de configuração de extensão de VM Linux.</span><span class="sxs-lookup"><span data-stu-id="77e22-103">Linux VM extension configuration samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77e22-104">PowerShell – modelo</span><span class="sxs-lookup"><span data-stu-id="77e22-104">PowerShell - Template</span></span>](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="77e22-105">CLI - Modelo</span><span class="sxs-lookup"><span data-stu-id="77e22-105">CLI - Template</span></span>](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="77e22-106">Este artigo fornece um exemplo de configuração para configurar extensões de VM do Azure para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="77e22-106">This article provides sample configuration for configuring Azure VM extensions for Linux VMs.</span></span>

<span data-ttu-id="77e22-107">Para saber mais sobre estas extensões, clique aqui: [Visão geral de extensões de VM do Azure.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="77e22-107">To learn more about these extensions click here : [Azure VM Extensions Overview.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="77e22-108">Para saber mais sobre a criação de modelos de extensão, clique aqui: [Criando modelos de extensão.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="77e22-108">To learn more about authoring extension templates click here : [Authoring Extension Templates.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="77e22-109">Este artigo lista os valores de configuração esperados para algumas das Extensões do Linux.</span><span class="sxs-lookup"><span data-stu-id="77e22-109">This article lists expected configuration values for some of the Linux Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="77e22-110">Trecho do exemplo de modelo para Extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="77e22-110">Sample template snippet for VM Extensions.</span></span>
<span data-ttu-id="77e22-111">O trecho do modelo para Implantação de extensões tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="77e22-111">The template snippet for Deploying extensions looks as following:</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="77e22-112">Trecho de código do modelo de exemplo para extensões de VM com Conjuntos de Escala de VM.</span><span class="sxs-lookup"><span data-stu-id="77e22-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
          {
           "type":"Microsoft.Compute/virtualMachineScaleSets",
          ....
                 "extensionProfile":{
                 "extensions":[
                   {
                     "name":"extension Name",
                     "properties":{
                       "publisher":"Publisher Namespace",
                       "type":"extension Name",
                       "typeHandlerVersion":"extension version",
                       "autoUpgradeMinorVersion":true,
                       "settings":{
                       // Extension specific configuration goes in here.
                       }
                     }
                    }
                  }
                }

<span data-ttu-id="77e22-113">Antes de implantar a extensão, verifique a versão mais recente da extensão e substitua "typeHandlerVersion" pela versão mais recente atual.</span><span class="sxs-lookup"><span data-stu-id="77e22-113">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

<span data-ttu-id="77e22-114">O restante do artigo fornece exemplos de configurações para extensões de VM Linux.</span><span class="sxs-lookup"><span data-stu-id="77e22-114">Rest of the article provides sample configurations for Linux VM Extensions.</span></span>

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="77e22-115">Agente CloudLink SecureVM</span><span class="sxs-lookup"><span data-stu-id="77e22-115">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMLinuxAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN to CloudLinkCenter"
            }
          }

### <a name="customscript-extension-for-linux"></a><span data-ttu-id="77e22-116">Extensão CustomScript para Linux.</span><span class="sxs-lookup"><span data-stu-id="77e22-116">CustomScript Extension for Linux.</span></span>
    {
        "publisher": " Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
            ],
            "commandToExecute": "powershell.exe-ExecutionPolicyUnrestricted-Filestart.ps1"
        }
    }


### <a name="datadog-agent"></a><span data-ttu-id="77e22-117">Agente Datadog</span><span class="sxs-lookup"><span data-stu-id="77e22-117">Datadog Agent</span></span>
        {
          "publisher": "Datadog.Agent",
          "type": "DatadogLinuxAgent",
          "typeHandlerVersion": "0.4",
          "settings": {
            "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
          }
        }

### <a name="chef-agent"></a><span data-ttu-id="77e22-118">Agente Chef</span><span class="sxs-lookup"><span data-stu-id="77e22-118">Chef Agent</span></span>
        {
          "publisher": "Chef.Bootstrap.WindowsAzure",
          "type": "CentosChefClient|LinuxChefClient",
          "typeHandlerVersion": "1210.12",
          "settings": {
            "validation_key" : " Validation key",
            "client_rb" : "client_rb file",
            "runlist" : "Optional runlist"
          }
        }

### <a name="vm-access-extension-password-reset"></a><span data-ttu-id="77e22-119">Extensão de acesso a VM (redefinição de senha)</span><span class="sxs-lookup"><span data-stu-id="77e22-119">VM Access Extension (Password Reset)</span></span>
<span data-ttu-id="77e22-120">Para obter o esquema atualizado, consulte a [Documentação do VMAccessForLinux](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)</span><span class="sxs-lookup"><span data-stu-id="77e22-120">For updated schema refer to the [VMAccessForLinux Documentation](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)</span></span>

        {
          "publisher": "Microsoft.OSTCExtensions",
          "type": "VMAccessForLinux",
          "typeHandlerVersion": "1.2",
          "protectedSettings": {
            "username": "(required, string) the name of the user",
            "password": "(optional, string) the password of the user",
            "reset_ssh": "(optional, boolean) whether or not reset the ssh",
            "ssh_key": "(optional, string) the public key of the user, base64 encoded pem",
            "remove_user": "(optional, string) the user name to remove"
          }
        }

### <a name="os-patching"></a><span data-ttu-id="77e22-121">Aplicação de patches de SO</span><span class="sxs-lookup"><span data-stu-id="77e22-121">OS Patching</span></span>
<span data-ttu-id="77e22-122">Para obter o esquema atualizado, consulte a [Documentação do OSPatching](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)</span><span class="sxs-lookup"><span data-stu-id="77e22-122">For updated schema refer to the [OSPatching Documentation](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)</span></span>

        {
        "publisher": "Microsoft.OSTCExtensions",
        "type": "OSPatchingForLinux",
        "typeHandlerVersion": "2.9",
        "Settings": {
          "disabled": false,
          "stop": false,
          "rebootAfterPatch": "RebootIfNeed|Required|NotRequired|Auto",
          "category": "Important|ImportantAndRecommended",
          "installDuration": "<hr:min>",
          "oneoff": false,
          "intervalOfWeeks": "<number>",
          "dayOfWeek": "Sunday|Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Everyday",
          "startTime": "<hr:min>",
          "vmStatusTest": {
              "local": false,
              "idleTestScript": "<path_to_idletestscript>",
              "healthyTestScript": "<path_to_healthytestscript>"
          }
        }
        }

### <a name="docker-extension"></a><span data-ttu-id="77e22-123">Extensão do Docker</span><span class="sxs-lookup"><span data-stu-id="77e22-123">Docker Extension</span></span>
<span data-ttu-id="77e22-124">Para obter o esquema atualizado, consulte [Documentação de extensão do Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)</span><span class="sxs-lookup"><span data-stu-id="77e22-124">For updated schema refer to the [Docker Extension Documentation](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)</span></span>

        {
          "publisher": "Microsoft.Azure.Extensions ",
          "type": "DockerExtension ",
          "typeHandlerVersion": "1.0",
          "Settings": {
            "docker":{
                "port": "2376",
                "options": ["-D", "--dns=8.8.8.8"]
            },
            "compose": {
                "cache" : {
                    "image" : "memcached",
                    "ports" : ["11211:11211"]
                },
                "blog": {
                    "image": "ghost",
                    "ports": ["80:2368"]
                }
            }
            }
        }

        ### Linux Diagnostics Extension
        {
        "storageAccountName": "storage account to receive data",
        "storageAccountKey": "key of the account",
        "perfCfg": [
        {
            "query": "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
            "table": "LinuxMemory"
        }
        ],
        "fileCfg": [
        {
            "file": "/var/log/mysql.err",
            "table": "mysqlerr"
        }
        ]
        }

<span data-ttu-id="77e22-125">Nos exemplos acima, substitua o número de versão pelo número de versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="77e22-125">In the examples above, replace the version number with the latest version number.</span></span>

<span data-ttu-id="77e22-126">Veja abaixo um modelo de VM completo para a criação de uma VM do Linux com uma extensão:</span><span class="sxs-lookup"><span data-stu-id="77e22-126">Here is a full VM template for creating a Linux VM with an extension:</span></span>

[<span data-ttu-id="77e22-127">Extensão de script personalizado em uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="77e22-127">Custom Script Extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

