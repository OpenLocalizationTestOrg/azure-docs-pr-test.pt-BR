---
title: "Modelo do Resource Manager para Configuração do Estado Desejado| Microsoft Docs"
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="13337-103">Windows VMSS e configuração de estado desejado com modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="13337-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="13337-104">Este artigo descreve o modelo do Resource Manager para o [manipulador de extensão da Configuração de Estado Desejado](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13337-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="13337-105">Exemplo de modelo para uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="13337-105">Template example for a Windows VM</span></span>
<span data-ttu-id="13337-106">O trecho a seguir vai na seção Recursos do modelo.</span><span class="sxs-lookup"><span data-stu-id="13337-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="13337-107">Exemplo de modelo para VMSS do Windows</span><span class="sxs-lookup"><span data-stu-id="13337-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="13337-108">Um nó VMSS tem uma seção "properties" com o atributo "VirtualMachineProfile", "extensionProfile".</span><span class="sxs-lookup"><span data-stu-id="13337-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="13337-109">O DSC é adicionado sob "extensões".</span><span class="sxs-lookup"><span data-stu-id="13337-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="13337-110">Informações de configuração detalhadas</span><span class="sxs-lookup"><span data-stu-id="13337-110">Detailed Settings Information</span></span>
<span data-ttu-id="13337-111">O esquema a seguir serve para a parte das configurações da extensão DSC do Azure em um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13337-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="13337-112">Detalhes</span><span class="sxs-lookup"><span data-stu-id="13337-112">Details</span></span>
| <span data-ttu-id="13337-113">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="13337-113">Property Name</span></span> | <span data-ttu-id="13337-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="13337-114">Type</span></span> | <span data-ttu-id="13337-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="13337-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13337-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="13337-116">settings.wmfVersion</span></span> |<span data-ttu-id="13337-117">string</span><span class="sxs-lookup"><span data-stu-id="13337-117">string</span></span> |<span data-ttu-id="13337-118">Especifica a versão do Windows Management Framework que deve ser instalada em sua VM.</span><span class="sxs-lookup"><span data-stu-id="13337-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="13337-119">Configurar essa propriedade como 'latest' instala a versão mais atualizada do WMF.</span><span class="sxs-lookup"><span data-stu-id="13337-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="13337-120">Os únicos valores possíveis no momento para essa propriedade são **'4.0', '5.0', ' 5.0PP' e 'latest'**.</span><span class="sxs-lookup"><span data-stu-id="13337-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="13337-121">Esses valores possíveis estão sujeitos a atualizações.</span><span class="sxs-lookup"><span data-stu-id="13337-121">These possible values are subject to updates.</span></span> <span data-ttu-id="13337-122">O valor padrão é 'latest'.</span><span class="sxs-lookup"><span data-stu-id="13337-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="13337-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="13337-123">settings.configuration.url</span></span> |<span data-ttu-id="13337-124">string</span><span class="sxs-lookup"><span data-stu-id="13337-124">string</span></span> |<span data-ttu-id="13337-125">Especifica o local da URL de onde baixar o arquivo zip configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="13337-126">Se a URL fornecida exigir um token SAS para acesso, será necessário definir a propriedade protectedSettings.configurationUrlSasToken como o valor do token de SAS.</span><span class="sxs-lookup"><span data-stu-id="13337-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="13337-127">Esta propriedade será necessária se settings.configuration.script e/ou settings.configuration.function estiverem definidas.</span><span class="sxs-lookup"><span data-stu-id="13337-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="13337-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="13337-128">settings.configuration.script</span></span> |<span data-ttu-id="13337-129">string</span><span class="sxs-lookup"><span data-stu-id="13337-129">string</span></span> |<span data-ttu-id="13337-130">Especifica o nome do arquivo do script que contém a definição de sua configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="13337-131">Esse script deve estar na pasta raiz do arquivo zip baixado da URL especificada pela propriedade configuration.url.</span><span class="sxs-lookup"><span data-stu-id="13337-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="13337-132">Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.script estiverem definidas.</span><span class="sxs-lookup"><span data-stu-id="13337-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="13337-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="13337-133">settings.configuration.function</span></span> |<span data-ttu-id="13337-134">string</span><span class="sxs-lookup"><span data-stu-id="13337-134">string</span></span> |<span data-ttu-id="13337-135">Especifica o nome da configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="13337-136">A configuração denominada deve estar contida no script definido por configuration.script.</span><span class="sxs-lookup"><span data-stu-id="13337-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="13337-137">Esta propriedade será necessária se settings.configuration.script.url e/ou settings.configuration.function estiverem definidas.</span><span class="sxs-lookup"><span data-stu-id="13337-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="13337-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="13337-138">settings.configurationArguments</span></span> |<span data-ttu-id="13337-139">Coleção</span><span class="sxs-lookup"><span data-stu-id="13337-139">Collection</span></span> |<span data-ttu-id="13337-140">Define os parâmetros que você deseja passar para a configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="13337-141">Essa propriedade não é criptografada.</span><span class="sxs-lookup"><span data-stu-id="13337-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="13337-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="13337-142">settings.configurationData.url</span></span> |<span data-ttu-id="13337-143">string</span><span class="sxs-lookup"><span data-stu-id="13337-143">string</span></span> |<span data-ttu-id="13337-144">Especifica a URL de onde baixar o arquivo de dados de configuração (.psd1) para usar como entrada para a sua configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="13337-145">Se a URL fornecida exigir um token SAS para acesso, será necessário definir a propriedade protectedSettings.configurationDataUrlSasToken como o valor do token de SAS.</span><span class="sxs-lookup"><span data-stu-id="13337-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="13337-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="13337-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="13337-147">string</span><span class="sxs-lookup"><span data-stu-id="13337-147">string</span></span> |<span data-ttu-id="13337-148">Habilita ou desabilita a coleta de telemetria.</span><span class="sxs-lookup"><span data-stu-id="13337-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="13337-149">Os únicos valores possíveis para essa propriedade são **'Enable', 'Disable', ou '$null'**.</span><span class="sxs-lookup"><span data-stu-id="13337-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="13337-150">Deixar esta propriedade em branco ou nulo permite telemetria.</span><span class="sxs-lookup"><span data-stu-id="13337-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="13337-151">O valor padrão é ''.</span><span class="sxs-lookup"><span data-stu-id="13337-151">The default value is ''.</span></span> [<span data-ttu-id="13337-152">Mais informações</span><span class="sxs-lookup"><span data-stu-id="13337-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="13337-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="13337-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="13337-154">Coleção</span><span class="sxs-lookup"><span data-stu-id="13337-154">Collection</span></span> |<span data-ttu-id="13337-155">Define os locais alternativos de onde baixar o WMF.</span><span class="sxs-lookup"><span data-stu-id="13337-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="13337-156">Mais informações</span><span class="sxs-lookup"><span data-stu-id="13337-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="13337-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="13337-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="13337-158">Coleção</span><span class="sxs-lookup"><span data-stu-id="13337-158">Collection</span></span> |<span data-ttu-id="13337-159">Define os parâmetros que você deseja passar para a configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="13337-160">Essa propriedade é criptografada.</span><span class="sxs-lookup"><span data-stu-id="13337-160">This property is encrypted.</span></span> |
| <span data-ttu-id="13337-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="13337-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="13337-162">string</span><span class="sxs-lookup"><span data-stu-id="13337-162">string</span></span> |<span data-ttu-id="13337-163">Especifica o token SAS para acessar a URL definida por configuration.url.</span><span class="sxs-lookup"><span data-stu-id="13337-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="13337-164">Essa propriedade é criptografada.</span><span class="sxs-lookup"><span data-stu-id="13337-164">This property is encrypted.</span></span> |
| <span data-ttu-id="13337-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="13337-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="13337-166">string</span><span class="sxs-lookup"><span data-stu-id="13337-166">string</span></span> |<span data-ttu-id="13337-167">Especifica o token SAS para acessar a URL definida por configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="13337-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="13337-168">Essa propriedade é criptografada.</span><span class="sxs-lookup"><span data-stu-id="13337-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="13337-169">Settings versus ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="13337-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="13337-170">Todas as configurações foram salvas em um arquivo de texto de configurações na VM.</span><span class="sxs-lookup"><span data-stu-id="13337-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="13337-171">Propriedades em 'settings' são propriedades públicas, pois não são criptografadas no arquivo de texto de configurações.</span><span class="sxs-lookup"><span data-stu-id="13337-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="13337-172">Propriedades em 'protectedSettings' são criptografadas com um certificado e não são mostradas em texto sem formatação neste arquivo na VM.</span><span class="sxs-lookup"><span data-stu-id="13337-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="13337-173">Se a configuração precisar de credenciais, elas poderão ser incluídas em protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="13337-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="13337-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="13337-174">Example</span></span>
<span data-ttu-id="13337-175">O exemplo a seguir é derivado da seção "Introdução" da página [Visão geral do manipulador de extensão de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13337-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="13337-176">Este exemplo usa modelos do Resource Manager, em vez de cmdlets para implantar a extensão.</span><span class="sxs-lookup"><span data-stu-id="13337-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="13337-177">Salve a configuração de "IisInstall.ps1", coloque-o em um arquivo .ZIP e carregue-o em uma URL acessível.</span><span class="sxs-lookup"><span data-stu-id="13337-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="13337-178">Este exemplo usa o Armazenamento de Blobs do Azure, mas é possível baixar os arquivos .ZIP de qualquer local aleatório.</span><span class="sxs-lookup"><span data-stu-id="13337-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="13337-179">No modelo do Azure Resource Manager, o código a seguir instrui a VM a baixar o arquivo correto e executar a função apropriada do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="13337-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="13337-180">Atualização do formato anterior</span><span class="sxs-lookup"><span data-stu-id="13337-180">Updating from the Previous Format</span></span>
<span data-ttu-id="13337-181">Todas as configurações no formato anterior (que contém as propriedades públicas ModulesUrl, ConfigurationFunction, SasToken ou Properties) serão automaticamente adaptadas ao formato atual e executadas exatamente como antes.</span><span class="sxs-lookup"><span data-stu-id="13337-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="13337-182">O esquema de configurações a seguir se parece com o esquema de configurações anterior:</span><span class="sxs-lookup"><span data-stu-id="13337-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="13337-183">Veja como formato anterior se adapta ao formato atual:</span><span class="sxs-lookup"><span data-stu-id="13337-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="13337-184">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="13337-184">Property Name</span></span> | <span data-ttu-id="13337-185">Equivalente ao esquema anterior</span><span class="sxs-lookup"><span data-stu-id="13337-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="13337-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="13337-186">settings.wmfVersion</span></span> |<span data-ttu-id="13337-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="13337-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="13337-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="13337-188">settings.configuration.url</span></span> |<span data-ttu-id="13337-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="13337-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="13337-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="13337-190">settings.configuration.script</span></span> |<span data-ttu-id="13337-191">Primeira parte de settings.ConfigurationFunction (antes de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="13337-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="13337-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="13337-192">settings.configuration.function</span></span> |<span data-ttu-id="13337-193">Segunda parte de settings.ConfigurationFunction (depois de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="13337-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="13337-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="13337-194">settings.configurationArguments</span></span> |<span data-ttu-id="13337-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="13337-195">settings.Properties</span></span> |
| <span data-ttu-id="13337-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="13337-196">settings.configurationData.url</span></span> |<span data-ttu-id="13337-197">protectedSettings.DataBlobUri (sem token SAS)</span><span class="sxs-lookup"><span data-stu-id="13337-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="13337-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="13337-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="13337-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="13337-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="13337-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="13337-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="13337-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="13337-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="13337-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="13337-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="13337-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="13337-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="13337-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="13337-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="13337-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="13337-205">settings.SasToken</span></span> |
| <span data-ttu-id="13337-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="13337-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="13337-207">Token SAS de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="13337-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="13337-208">Solução de problemas - Código de erro 1100</span><span class="sxs-lookup"><span data-stu-id="13337-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="13337-209">Código de erro 1100 indica que há um problema com a entrada do usuário para a extensão de DSC.</span><span class="sxs-lookup"><span data-stu-id="13337-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="13337-210">O texto desses erros é variável e pode mudar.</span><span class="sxs-lookup"><span data-stu-id="13337-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="13337-211">Confira alguns erros que você pode encontrar e como corrigi-los.</span><span class="sxs-lookup"><span data-stu-id="13337-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="13337-212">Valores inválidos</span><span class="sxs-lookup"><span data-stu-id="13337-212">Invalid Values</span></span>
<span data-ttu-id="13337-213">"Privacy.dataCollection é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="13337-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="13337-214">Os únicos valores possíveis são '', 'Enable' e 'Disable'" "WmfVersion é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="13337-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="13337-215">Únicos valores possíveis são...</span><span class="sxs-lookup"><span data-stu-id="13337-215">Only possible values are …</span></span> <span data-ttu-id="13337-216">e 'latest'"</span><span class="sxs-lookup"><span data-stu-id="13337-216">and 'latest'"</span></span>

<span data-ttu-id="13337-217">Problema: um valor fornecido não é permitido.</span><span class="sxs-lookup"><span data-stu-id="13337-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="13337-218">Solução: altere o valor inválido para um valor válido.</span><span class="sxs-lookup"><span data-stu-id="13337-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="13337-219">Consulte a tabela na seção Detalhes.</span><span class="sxs-lookup"><span data-stu-id="13337-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="13337-220">URL inválida</span><span class="sxs-lookup"><span data-stu-id="13337-220">Invalid URL</span></span>
<span data-ttu-id="13337-221">"ConfigurationData.url é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="13337-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="13337-222">Essa não é uma URL válida" "DataBlobUri é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="13337-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="13337-223">Essa não é uma URL válida" "Configuration.url é '{0}'.</span><span class="sxs-lookup"><span data-stu-id="13337-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="13337-224">Essa não é uma URL válida"</span><span class="sxs-lookup"><span data-stu-id="13337-224">This is not a valid URL"</span></span>

<span data-ttu-id="13337-225">Problema: uma URL fornecida não é válida.</span><span class="sxs-lookup"><span data-stu-id="13337-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="13337-226">Solução: verifique todas as URLs fornecidas.</span><span class="sxs-lookup"><span data-stu-id="13337-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="13337-227">Certifique-se de que todas as URLs resolvem para locais válidos que a extensão pode acessar no computador remoto.</span><span class="sxs-lookup"><span data-stu-id="13337-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="13337-228">Tipo ConfigurationArgument inválido</span><span class="sxs-lookup"><span data-stu-id="13337-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="13337-229">"Tipo configurationArguments inválido {0}"</span><span class="sxs-lookup"><span data-stu-id="13337-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="13337-230">Problema: a propriedade ConfigurationArguments não pode resolver um objeto Hashtable.</span><span class="sxs-lookup"><span data-stu-id="13337-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="13337-231">Solução: torne sua propriedade ConfigurationArguments uma tabela de hash.</span><span class="sxs-lookup"><span data-stu-id="13337-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="13337-232">Siga o formato fornecido no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="13337-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="13337-233">Fique atento às chaves, vírgulas e aspas.</span><span class="sxs-lookup"><span data-stu-id="13337-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="13337-234">ConfigurationArguments duplicado</span><span class="sxs-lookup"><span data-stu-id="13337-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="13337-235">"Argumentos '{0}' duplicados encontrados em configurationArguments públicos e protegidos"</span><span class="sxs-lookup"><span data-stu-id="13337-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="13337-236">Problema: ConfigurationArguments nas configurações públicas, e ConfigurationArguments nas configurações protegidas contêm propriedades com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="13337-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="13337-237">Solução: remova uma das propriedades duplicadas.</span><span class="sxs-lookup"><span data-stu-id="13337-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="13337-238">Propriedades ausentes</span><span class="sxs-lookup"><span data-stu-id="13337-238">Missing Properties</span></span>
<span data-ttu-id="13337-239">"Configuration.function exige que configuration.url ou configuration.module seja especificado"</span><span class="sxs-lookup"><span data-stu-id="13337-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="13337-240">"Configuration.url exige que configuration.script seja especificado"</span><span class="sxs-lookup"><span data-stu-id="13337-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="13337-241">"Configuration.script exige que configuration.url seja especificado"</span><span class="sxs-lookup"><span data-stu-id="13337-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="13337-242">"Configuration.url exige que configuration.function seja especificado"</span><span class="sxs-lookup"><span data-stu-id="13337-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="13337-243">"ConfigurationUrlSasToken exige que configuration.url seja especificado"</span><span class="sxs-lookup"><span data-stu-id="13337-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="13337-244">"ConfigurationDataUrlSasToken exige que configurationData.url seja especificado"</span><span class="sxs-lookup"><span data-stu-id="13337-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="13337-245">Problema: uma propriedade definida precisa de outra propriedade que não está presente.</span><span class="sxs-lookup"><span data-stu-id="13337-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="13337-246">Soluções:</span><span class="sxs-lookup"><span data-stu-id="13337-246">Solutions:</span></span> 

* <span data-ttu-id="13337-247">Forneça a propriedade ausente.</span><span class="sxs-lookup"><span data-stu-id="13337-247">Provide the missing property.</span></span>
* <span data-ttu-id="13337-248">Remova a propriedade que precisa da propriedade ausente.</span><span class="sxs-lookup"><span data-stu-id="13337-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13337-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13337-249">Next Steps</span></span>
<span data-ttu-id="13337-250">Saiba mais sobre DSC e conjuntos de escala de máquina virtual em [Uso de Conjuntos de Escala de Máquina Virtual com a Extensão de DSC do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="13337-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="13337-251">Encontre mais detalhes sobre [Gerenciamento de credenciais seguras do DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13337-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="13337-252">Para saber mais sobre o manipulador de extensões DSC do Azure, confira [Introduction to the Azure Desired State Configuration extension handler (Introdução ao manipulador de extensões Configuração de Estado Desejado do Azure)](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13337-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="13337-253">Para saber mais sobre a DSC do PowerShell, [visite o centro de documentação do PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="13337-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

