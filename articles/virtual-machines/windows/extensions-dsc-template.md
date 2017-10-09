---
title: "Modelo do Gerenciador de recursos de configuração de estado de aaaDesired | Microsoft Docs"
description: "Definição do modelo do Resource Manager para Configuração de Estado Desejado no Azure com exemplos e solução de problemas"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="a6dd4-103">Windows VMSS e configuração de estado desejado com modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a6dd4-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="a6dd4-104">Este artigo descreve o modelo do Gerenciador de recursos de saudação para Olá [manipulador de extensão de configuração de estado desejado](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6dd4-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="a6dd4-105">Exemplo de modelo para uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="a6dd4-105">Template example for a Windows VM</span></span>
<span data-ttu-id="a6dd4-106">Olá trecho a seguir entra em Olá seção de recursos do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="a6dd4-107">Exemplo de modelo para VMSS do Windows</span><span class="sxs-lookup"><span data-stu-id="a6dd4-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="a6dd4-108">Um nó VMSS tem uma seção de "propriedades" com hello "VirtualMachineProfile", "extensionProfile" atributo.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="a6dd4-109">O DSC é adicionado sob "extensões".</span><span class="sxs-lookup"><span data-stu-id="a6dd4-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="a6dd4-110">Informações de configuração detalhadas</span><span class="sxs-lookup"><span data-stu-id="a6dd4-110">Detailed Settings Information</span></span>
<span data-ttu-id="a6dd4-111">Olá esquema a seguir é parte de configurações Olá de saudação extensão de DSC do Azure em um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="a6dd4-112">Detalhes</span><span class="sxs-lookup"><span data-stu-id="a6dd4-112">Details</span></span>
| <span data-ttu-id="a6dd4-113">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="a6dd4-113">Property Name</span></span> | <span data-ttu-id="a6dd4-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="a6dd4-114">Type</span></span> | <span data-ttu-id="a6dd4-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="a6dd4-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6dd4-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a6dd4-116">settings.wmfVersion</span></span> |<span data-ttu-id="a6dd4-117">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-117">string</span></span> |<span data-ttu-id="a6dd4-118">Especifica a versão de saudação do hello Windows Management Framework, deve ser instalado em sua VM.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="a6dd4-119">Definir essa propriedade too'latest' instala Olá versão mais atualizada do WMF.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="a6dd4-120">Olá atual apenas os valores possíveis para essa propriedade são **'4.0', '5.0', ' 5.0PP' e 'último'**.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="a6dd4-121">Esses valores possíveis são tooupdates de assunto.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="a6dd4-122">valor padrão de saudação é 'último'.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="a6dd4-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="a6dd4-123">settings.configuration.url</span></span> |<span data-ttu-id="a6dd4-124">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-124">string</span></span> |<span data-ttu-id="a6dd4-125">Especifica o local de URL de saudação do qual toodownload seu arquivo de zip de configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="a6dd4-126">Se Olá URL fornecida exige um token SAS de acesso, será necessário tooset Olá protectedSettings.configurationUrlSasToken toohello valor da propriedade seu token SAS.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="a6dd4-127">Esta propriedade será necessária se settings.configuration.script e/ou settings.configuration.function estiverem definidas.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="a6dd4-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="a6dd4-128">settings.configuration.script</span></span> |<span data-ttu-id="a6dd4-129">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-129">string</span></span> |<span data-ttu-id="a6dd4-130">Especifica o nome do arquivo de saudação do script hello que contém a definição de saudação da sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="a6dd4-131">Este script deve estar na pasta raiz de saudação do arquivo zip de Olá baixado da URL de saudação especificado pela propriedade de configuration.url hello.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="a6dd4-132">Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.script estiverem definidas.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="a6dd4-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="a6dd4-133">settings.configuration.function</span></span> |<span data-ttu-id="a6dd4-134">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-134">string</span></span> |<span data-ttu-id="a6dd4-135">Especifica o nome de saudação da sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="a6dd4-136">configuração Olá nomeada deve estar contida no script hello definido pelo configuration.script.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="a6dd4-137">Esta propriedade será necessária se settings.configuration.script.url e/ou settings.configuration.function estiverem definidas.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="a6dd4-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a6dd4-138">settings.configurationArguments</span></span> |<span data-ttu-id="a6dd4-139">Coleção</span><span class="sxs-lookup"><span data-stu-id="a6dd4-139">Collection</span></span> |<span data-ttu-id="a6dd4-140">Define os parâmetros que você deseja que a configuração de DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="a6dd4-141">Essa propriedade não é criptografada.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="a6dd4-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="a6dd4-142">settings.configurationData.url</span></span> |<span data-ttu-id="a6dd4-143">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-143">string</span></span> |<span data-ttu-id="a6dd4-144">Especifica a URL de saudação do qual toodownload os dados de configuração (. psd1) do arquivo toouse como entrada para a sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="a6dd4-145">Se Olá URL fornecida exige um token SAS de acesso, será necessário tooset Olá protectedSettings.configurationDataUrlSasToken toohello valor da propriedade seu token SAS.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="a6dd4-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a6dd4-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="a6dd4-147">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-147">string</span></span> |<span data-ttu-id="a6dd4-148">Habilita ou desabilita a coleta de telemetria.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="a6dd4-149">Olá apenas os valores possíveis para essa propriedade são **'Habilitar', 'Disable', ', ou $null**.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="a6dd4-150">Deixar esta propriedade em branco ou nulo permite telemetria.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="a6dd4-151">valor padrão de saudação é '.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-151">hello default value is ''.</span></span> [<span data-ttu-id="a6dd4-152">Mais informações</span><span class="sxs-lookup"><span data-stu-id="a6dd4-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="a6dd4-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a6dd4-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="a6dd4-154">Coleção</span><span class="sxs-lookup"><span data-stu-id="a6dd4-154">Collection</span></span> |<span data-ttu-id="a6dd4-155">Define os locais alternativos que de quais toodownload Olá WMF.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="a6dd4-156">Mais informações</span><span class="sxs-lookup"><span data-stu-id="a6dd4-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="a6dd4-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a6dd4-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="a6dd4-158">Coleção</span><span class="sxs-lookup"><span data-stu-id="a6dd4-158">Collection</span></span> |<span data-ttu-id="a6dd4-159">Define os parâmetros que você deseja que a configuração de DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="a6dd4-160">Essa propriedade é criptografada.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-160">This property is encrypted.</span></span> |
| <span data-ttu-id="a6dd4-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a6dd4-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="a6dd4-162">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-162">string</span></span> |<span data-ttu-id="a6dd4-163">Especifica a URL do hello SAS tooaccess token Olá definido pelo configuration.url.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="a6dd4-164">Essa propriedade é criptografada.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-164">This property is encrypted.</span></span> |
| <span data-ttu-id="a6dd4-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a6dd4-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="a6dd4-166">string</span><span class="sxs-lookup"><span data-stu-id="a6dd4-166">string</span></span> |<span data-ttu-id="a6dd4-167">Especifica a URL do hello SAS tooaccess token Olá definido pelo configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="a6dd4-168">Essa propriedade é criptografada.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="a6dd4-169">Settings versus ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="a6dd4-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="a6dd4-170">Todas as configurações são salvas em um arquivo de texto de configurações no hello VM.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="a6dd4-171">Propriedades em 'Configurações' são propriedades públicas, porque eles não são criptografados no arquivo de texto de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="a6dd4-172">Propriedades em 'protectedSettings' são criptografadas com um certificado e não são mostradas em texto sem formatação neste arquivo de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="a6dd4-173">Se a configuração de saudação precisa de credenciais, elas podem ser incluídas em protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="a6dd4-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="a6dd4-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a6dd4-174">Example</span></span>
<span data-ttu-id="a6dd4-175">Hello exemplo a seguir é derivado da seção de "Introdução" hello da saudação [página Visão geral de manipulador de extensão de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6dd4-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="a6dd4-176">Este exemplo usa o recurso Gerenciador de modelos em vez da extensão de saudação toodeploy cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="a6dd4-177">Salvar a configuração de "IisInstall.ps1" Olá, colocá-lo em um. COMPACTE o arquivo e carregue o arquivo de saudação em uma URL acessível.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="a6dd4-178">Este exemplo usa o armazenamento de BLOBs do Azure, mas é possível toodownload. Arquivos ZIP de qualquer local arbitrário.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="a6dd4-179">No modelo do Azure Resource Manager hello, hello código a seguir instrui o arquivo correto do Olá Olá VM toodownload e execute função apropriada de PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="a6dd4-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="a6dd4-180">Atualizando a partir de saudação formato anterior</span><span class="sxs-lookup"><span data-stu-id="a6dd4-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="a6dd4-181">Todas as configurações no hello formato anterior (que contém as propriedades públicas de saudação ModulesUrl, ConfigurationFunction, SasToken ou propriedades) automaticamente adaptar o formato atual toohello e executam como antes.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="a6dd4-182">Olá esquema a seguir é o esquema de configurações do anterior Olá semelhante a:</span><span class="sxs-lookup"><span data-stu-id="a6dd4-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="a6dd4-183">Aqui está como formato anterior Olá adapta o formato atual toohello:</span><span class="sxs-lookup"><span data-stu-id="a6dd4-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="a6dd4-184">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="a6dd4-184">Property Name</span></span> | <span data-ttu-id="a6dd4-185">Equivalente ao esquema anterior</span><span class="sxs-lookup"><span data-stu-id="a6dd4-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="a6dd4-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a6dd4-186">settings.wmfVersion</span></span> |<span data-ttu-id="a6dd4-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a6dd4-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="a6dd4-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="a6dd4-188">settings.configuration.url</span></span> |<span data-ttu-id="a6dd4-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="a6dd4-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="a6dd4-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="a6dd4-190">settings.configuration.script</span></span> |<span data-ttu-id="a6dd4-191">Primeira parte de settings.ConfigurationFunction (antes de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="a6dd4-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="a6dd4-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="a6dd4-192">settings.configuration.function</span></span> |<span data-ttu-id="a6dd4-193">Segunda parte de settings.ConfigurationFunction (depois de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="a6dd4-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="a6dd4-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a6dd4-194">settings.configurationArguments</span></span> |<span data-ttu-id="a6dd4-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="a6dd4-195">settings.Properties</span></span> |
| <span data-ttu-id="a6dd4-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="a6dd4-196">settings.configurationData.url</span></span> |<span data-ttu-id="a6dd4-197">protectedSettings.DataBlobUri (sem token SAS)</span><span class="sxs-lookup"><span data-stu-id="a6dd4-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="a6dd4-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a6dd4-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="a6dd4-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a6dd4-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="a6dd4-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a6dd4-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="a6dd4-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a6dd4-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="a6dd4-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a6dd4-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="a6dd4-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="a6dd4-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="a6dd4-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a6dd4-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="a6dd4-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="a6dd4-205">settings.SasToken</span></span> |
| <span data-ttu-id="a6dd4-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a6dd4-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="a6dd4-207">Token SAS de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="a6dd4-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="a6dd4-208">Solução de problemas - Código de erro 1100</span><span class="sxs-lookup"><span data-stu-id="a6dd4-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="a6dd4-209">Código de erro 1100 indica que há um problema com hello extensão toohello DSC de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="a6dd4-210">texto de saudação desses erros é variável e pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="a6dd4-211">Aqui estão alguns dos erros de saudação que você pode ter e como corrigi-los.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="a6dd4-212">Valores inválidos</span><span class="sxs-lookup"><span data-stu-id="a6dd4-212">Invalid Values</span></span>
<span data-ttu-id="a6dd4-213">"Privacy.dataCollection é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="a6dd4-214">Olá apenas os valores possíveis são ', 'Habilitar' e 'Disable' ""WmfVersion é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="a6dd4-215">Únicos valores possíveis são...</span><span class="sxs-lookup"><span data-stu-id="a6dd4-215">Only possible values are …</span></span> <span data-ttu-id="a6dd4-216">e 'latest'"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-216">and 'latest'"</span></span>

<span data-ttu-id="a6dd4-217">Problema: um valor fornecido não é permitido.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="a6dd4-218">Solução: Alterar valor válido do tooa Olá valor inválido.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="a6dd4-219">Consulte a tabela de saudação na seção de detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="a6dd4-220">URL inválida</span><span class="sxs-lookup"><span data-stu-id="a6dd4-220">Invalid URL</span></span>
<span data-ttu-id="a6dd4-221">"ConfigurationData.url é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="a6dd4-222">Essa não é uma URL válida" "DataBlobUri é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="a6dd4-223">Essa não é uma URL válida" "Configuration.url é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="a6dd4-224">Essa não é uma URL válida"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-224">This is not a valid URL"</span></span>

<span data-ttu-id="a6dd4-225">Problema: uma URL fornecida não é válida.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="a6dd4-226">Solução: verifique todas as URLs fornecidas.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="a6dd4-227">Verifique se que todas as URLs resolvem toovalid locais que extensão Olá pode acessar no computador remoto hello.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="a6dd4-228">Tipo ConfigurationArgument inválido</span><span class="sxs-lookup"><span data-stu-id="a6dd4-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="a6dd4-229">"Tipo configurationArguments inválido {0}"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="a6dd4-230">Problema: Olá ConfigurationArguments propriedade não é possível resolver tooa objeto de tabela de hash.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="a6dd4-231">Solução: torne sua propriedade ConfigurationArguments uma tabela de hash.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="a6dd4-232">Segue o formato de saudação fornecido no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="a6dd4-233">Fique atento às chaves, vírgulas e aspas.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="a6dd4-234">ConfigurationArguments duplicado</span><span class="sxs-lookup"><span data-stu-id="a6dd4-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="a6dd4-235">"Argumentos '{0}' duplicados encontrados em configurationArguments públicos e protegidos"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="a6dd4-236">Problema: Olá ConfigurationArguments nas configurações do públicas e ConfigurationArguments nas configurações protegidas hello conter propriedades com hello mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="a6dd4-237">Solução: Remova uma das propriedades duplicadas hello.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="a6dd4-238">Propriedades ausentes</span><span class="sxs-lookup"><span data-stu-id="a6dd4-238">Missing Properties</span></span>
<span data-ttu-id="a6dd4-239">"Configuration.function exige que configuration.url ou configuration.module seja especificado"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="a6dd4-240">"Configuration.url exige que configuration.script seja especificado"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="a6dd4-241">"Configuration.script exige que configuration.url seja especificado"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="a6dd4-242">"Configuration.url exige que configuration.function seja especificado"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="a6dd4-243">"ConfigurationUrlSasToken exige que configuration.url seja especificado"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="a6dd4-244">"ConfigurationDataUrlSasToken exige que configurationData.url seja especificado"</span><span class="sxs-lookup"><span data-stu-id="a6dd4-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="a6dd4-245">Problema: uma propriedade definida precisa de outra propriedade que não está presente.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="a6dd4-246">Soluções:</span><span class="sxs-lookup"><span data-stu-id="a6dd4-246">Solutions:</span></span> 

* <span data-ttu-id="a6dd4-247">Forneça a propriedade ausente hello.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-247">Provide hello missing property.</span></span>
* <span data-ttu-id="a6dd4-248">Remova propriedade Olá que precisa de propriedade ausente hello.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6dd4-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6dd4-249">Next Steps</span></span>
<span data-ttu-id="a6dd4-250">Saiba mais sobre o DSC e conjuntos de escala de máquinas virtuais [usando de escala de máquina Virtual define com hello extensão de DSC do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="a6dd4-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="a6dd4-251">Encontre mais detalhes sobre [Gerenciamento de credenciais seguras do DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6dd4-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a6dd4-252">Para obter mais informações sobre o manipulador de extensão de DSC do Azure hello, consulte [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6dd4-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a6dd4-253">Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="a6dd4-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

