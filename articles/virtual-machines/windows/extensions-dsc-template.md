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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Windows VMSS e configuração de estado desejado com modelos do Azure Resource Manager
Este artigo descreve o modelo do Gerenciador de recursos de saudação para Olá [manipulador de extensão de configuração de estado desejado](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Exemplo de modelo para uma VM do Windows
Olá trecho a seguir entra em Olá seção de recursos do modelo de saudação.

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

## <a name="template-example-for-windows-vmss"></a>Exemplo de modelo para VMSS do Windows
Um nó VMSS tem uma seção de "propriedades" com hello "VirtualMachineProfile", "extensionProfile" atributo. O DSC é adicionado sob "extensões". 

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

## <a name="detailed-settings-information"></a>Informações de configuração detalhadas
Olá esquema a seguir é parte de configurações Olá de saudação extensão de DSC do Azure em um modelo do Gerenciador de recursos do Azure.

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

## <a name="details"></a>Detalhes
| Nome da Propriedade | Tipo | Descrição |
| --- | --- | --- |
| settings.wmfVersion |string |Especifica a versão de saudação do hello Windows Management Framework, deve ser instalado em sua VM. Definir essa propriedade too'latest' instala Olá versão mais atualizada do WMF. Olá atual apenas os valores possíveis para essa propriedade são **'4.0', '5.0', ' 5.0PP' e 'último'**. Esses valores possíveis são tooupdates de assunto. valor padrão de saudação é 'último'. |
| settings.configuration.url |string |Especifica o local de URL de saudação do qual toodownload seu arquivo de zip de configuração DSC. Se Olá URL fornecida exige um token SAS de acesso, será necessário tooset Olá protectedSettings.configurationUrlSasToken toohello valor da propriedade seu token SAS. Esta propriedade será necessária se settings.configuration.script e/ou settings.configuration.function estiverem definidas. |
| settings.configuration.script |string |Especifica o nome do arquivo de saudação do script hello que contém a definição de saudação da sua configuração de DSC. Este script deve estar na pasta raiz de saudação do arquivo zip de Olá baixado da URL de saudação especificado pela propriedade de configuration.url hello. Esta propriedade é necessária se settings.configuration.url e/ou settings.configuration.script estiverem definidas. |
| settings.configuration.function |string |Especifica o nome de saudação da sua configuração de DSC. configuração Olá nomeada deve estar contida no script hello definido pelo configuration.script. Esta propriedade será necessária se settings.configuration.script.url e/ou settings.configuration.function estiverem definidas. |
| settings.configurationArguments |Coleção |Define os parâmetros que você deseja que a configuração de DSC tooyour toopass. Essa propriedade não é criptografada. |
| settings.configurationData.url |string |Especifica a URL de saudação do qual toodownload os dados de configuração (. psd1) do arquivo toouse como entrada para a sua configuração de DSC. Se Olá URL fornecida exige um token SAS de acesso, será necessário tooset Olá protectedSettings.configurationDataUrlSasToken toohello valor da propriedade seu token SAS. |
| settings.privacy.dataEnabled |string |Habilita ou desabilita a coleta de telemetria. Olá apenas os valores possíveis para essa propriedade são **'Habilitar', 'Disable', ', ou $null**. Deixar esta propriedade em branco ou nulo permite telemetria. valor padrão de saudação é '. [Mais informações](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Coleção |Define os locais alternativos que de quais toodownload Olá WMF. [Mais informações](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Coleção |Define os parâmetros que você deseja que a configuração de DSC tooyour toopass. Essa propriedade é criptografada. |
| protectedSettings.configurationUrlSasToken |string |Especifica a URL do hello SAS tooaccess token Olá definido pelo configuration.url. Essa propriedade é criptografada. |
| protectedSettings.configurationDataUrlSasToken |string |Especifica a URL do hello SAS tooaccess token Olá definido pelo configurationData.url. Essa propriedade é criptografada. |

## <a name="settings-vs-protectedsettings"></a>Settings versus ProtectedSettings
Todas as configurações são salvas em um arquivo de texto de configurações no hello VM.
Propriedades em 'Configurações' são propriedades públicas, porque eles não são criptografados no arquivo de texto de configurações de saudação.
Propriedades em 'protectedSettings' são criptografadas com um certificado e não são mostradas em texto sem formatação neste arquivo de saudação VM.

Se a configuração de saudação precisa de credenciais, elas podem ser incluídas em protectedSettings:

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

## <a name="example"></a>Exemplo
Hello exemplo a seguir é derivado da seção de "Introdução" hello da saudação [página Visão geral de manipulador de extensão de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Este exemplo usa o recurso Gerenciador de modelos em vez da extensão de saudação toodeploy cmdlets. Salvar a configuração de "IisInstall.ps1" Olá, colocá-lo em um. COMPACTE o arquivo e carregue o arquivo de saudação em uma URL acessível. Este exemplo usa o armazenamento de BLOBs do Azure, mas é possível toodownload. Arquivos ZIP de qualquer local arbitrário.

No modelo do Azure Resource Manager hello, hello código a seguir instrui o arquivo correto do Olá Olá VM toodownload e execute função apropriada de PowerShell hello:

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

## <a name="updating-from-hello-previous-format"></a>Atualizando a partir de saudação formato anterior
Todas as configurações no hello formato anterior (que contém as propriedades públicas de saudação ModulesUrl, ConfigurationFunction, SasToken ou propriedades) automaticamente adaptar o formato atual toohello e executam como antes.

Olá esquema a seguir é o esquema de configurações do anterior Olá semelhante a:

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

Aqui está como formato anterior Olá adapta o formato atual toohello:

| Nome da Propriedade | Equivalente ao esquema anterior |
| --- | --- |
| settings.wmfVersion |settings.wmfVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |Primeira parte de settings.ConfigurationFunction (antes de '\\\\') |
| settings.configuration.function |Segunda parte de settings.ConfigurationFunction (depois de '\\\\') |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri (sem token SAS) |
| settings.privacy.dataEnabled |settings.privacy.dataEnabled |
| settings.advancedOptions.downloadMappings |settings.advancedOptions.downloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |Token SAS de protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Solução de problemas - Código de erro 1100
Código de erro 1100 indica que há um problema com hello extensão toohello DSC de entrada do usuário.
texto de saudação desses erros é variável e pode ser alterado.
Aqui estão alguns dos erros de saudação que você pode ter e como corrigi-los.

### <a name="invalid-values"></a>Valores inválidos
"Privacy.dataCollection é '{0}'. Olá apenas os valores possíveis são ', 'Habilitar' e 'Disable' ""WmfVersion é '{0}'. Únicos valores possíveis são... e 'latest'"

Problema: um valor fornecido não é permitido.

Solução: Alterar valor válido do tooa Olá valor inválido. Consulte a tabela de saudação na seção de detalhes de saudação.

### <a name="invalid-url"></a>URL inválida
"ConfigurationData.url é '{0}'. Essa não é uma URL válida" "DataBlobUri é '{0}'. Essa não é uma URL válida" "Configuration.url é '{0}'. Essa não é uma URL válida"

Problema: uma URL fornecida não é válida.

Solução: verifique todas as URLs fornecidas. Verifique se que todas as URLs resolvem toovalid locais que extensão Olá pode acessar no computador remoto hello.

### <a name="invalid-configurationargument-type"></a>Tipo ConfigurationArgument inválido
"Tipo configurationArguments inválido {0}"

Problema: Olá ConfigurationArguments propriedade não é possível resolver tooa objeto de tabela de hash. 

Solução: torne sua propriedade ConfigurationArguments uma tabela de hash. Segue o formato de saudação fornecido no exemplo anterior de saudação. Fique atento às chaves, vírgulas e aspas.

### <a name="duplicate-configurationarguments"></a>ConfigurationArguments duplicado
"Argumentos '{0}' duplicados encontrados em configurationArguments públicos e protegidos"

Problema: Olá ConfigurationArguments nas configurações do públicas e ConfigurationArguments nas configurações protegidas hello conter propriedades com hello mesmo nome.

Solução: Remova uma das propriedades duplicadas hello.

### <a name="missing-properties"></a>Propriedades ausentes
"Configuration.function exige que configuration.url ou configuration.module seja especificado"

"Configuration.url exige que configuration.script seja especificado"

"Configuration.script exige que configuration.url seja especificado"

"Configuration.url exige que configuration.function seja especificado"

"ConfigurationUrlSasToken exige que configuration.url seja especificado"

"ConfigurationDataUrlSasToken exige que configurationData.url seja especificado"

Problema: uma propriedade definida precisa de outra propriedade que não está presente.

Soluções: 

* Forneça a propriedade ausente hello.
* Remova propriedade Olá que precisa de propriedade ausente hello.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre o DSC e conjuntos de escala de máquinas virtuais [usando de escala de máquina Virtual define com hello extensão de DSC do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Encontre mais detalhes sobre [Gerenciamento de credenciais seguras do DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter mais informações sobre o manipulador de extensão de DSC do Azure hello, consulte [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview). 

