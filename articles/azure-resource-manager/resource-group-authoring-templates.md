---
title: aaaAzure Gerenciador de recursos de estrutura de modelo e a sintaxe | Microsoft Docs
description: "Descreve a estrutura de saudação e propriedades de modelos do Gerenciador de recursos do Azure usando a sintaxe JSON declarativa."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Entender a estrutura de saudação e a sintaxe de modelos do Gerenciador de recursos do Azure
Este tópico descreve a estrutura de saudação de um modelo do Gerenciador de recursos do Azure. Ele apresenta seções diferentes de saudação de um modelo e hello propriedades disponíveis nessas seções. Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação. Para ver um tutorial passo a passo sobre como criar um modelo, confira [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).

## <a name="template-format"></a>Formato de modelo
Em sua estrutura mais simples, um modelo contém Olá elementos a seguir:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Nome do elemento | Obrigatório | Descrição |
|:--- |:--- |:--- |
| $schema |Sim |Local do arquivo de esquema do hello JSON que descreve a versão de saudação do idioma do modelo de saudação. Use URL Olá mostrada a saudação anterior de exemplo. |
| contentVersion |Sim |Versão do modelo de saudação (por exemplo, 1.0.0.0). Você pode fornecer qualquer valor para esse elemento. Durante a implantação de recursos usando o modelo de hello, esse valor pode ser usado toomake-se de que o modelo certo hello está sendo usado. |
| parâmetros |Não |Valores que são fornecidos quando a implantação é executado toocustomize implantação de recursos. |
| variáveis |Não |Valores que são usados como fragmentos JSON em expressões de idioma Olá modelo toosimplify modelo. |
| recursos |Sim |Tipos de recursos que são implantados ou atualizados em um grupo de recursos. |
| outputs |Não |Valores que são retornados após a implantação. |

Cada elemento contém propriedades que você pode definir. saudação de exemplo a seguir contém a sintaxe completa Olá para um modelo:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

Podemos examinar seções de saudação do modelo de saudação em maiores detalhes posteriormente neste tópico.

## <a name="expressions-and-functions"></a>Expressões e funções
sintaxe básica de saudação do modelo de saudação é JSON. No entanto, expressões e funções estendem valores JSON de saudação disponíveis no modelo de saudação.  As expressões são escritas em literais de cadeia de caracteres JSON cujo primeiro e último caracteres são colchetes Olá: `[` e `]`, respectivamente. valor de saudação da expressão de saudação é avaliado quando Olá modelo é implantado. Enquanto gravado como uma cadeia de caracteres literal, o resultado de saudação da avaliação de expressão Olá pode ser de um tipo diferente de JSON, como uma matriz ou um número inteiro, dependendo da expressão real hello.  toohave uma cadeia de caracteres literal começar com um colchete `[`, mas não que ele seja interpretado como uma expressão, adicionar uma cadeia de caracteres do colchete extra toostart Olá com `[[`.

Normalmente, você deve usar expressões com operações de tooperform de funções para a configuração de implantação de saudação. Assim como no JavaScript, as chamadas de função são formatadas como `functionName(arg1,arg2,arg3)`. Você pode referenciar propriedades usando os operadores de ponto e [index] hello.

saudação de exemplo a seguir mostra como toouse várias funções ao construir valores:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Para Olá a lista completa de funções de modelo, consulte [funções de modelo do Azure Resource Manager](resource-group-template-functions.md). 

## <a name="parameters"></a>parâmetros
Na seção de parâmetros de saudação do modelo hello, você especificar os valores que você pode inserir ao implantar Olá recursos. Esses valores de parâmetro habilite a implantação de saudação toocustomize fornecendo os valores que são adaptados para um ambiente específico (como desenvolvimento, teste e produção). Você não tem parâmetros tooprovide em seu modelo, mas sem parâmetros seu modelo sempre implanta Olá mesmos recursos com hello mesmo nomes, locais e propriedades.

Você pode definir parâmetros com hello estrutura a seguir:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Nome do elemento | Obrigatório | Descrição |
|:--- |:--- |:--- |
| parameterName |Sim |Nome do parâmetro hello. Deve ser um identificador JavaScript válido. |
| type |Sim |Tipo de valor de parâmetro hello. Consulte a lista de saudação de tipos permitidos depois desta tabela. |
| defaultValue |Não |Valor padrão para o parâmetro hello, se nenhum valor for fornecido para o parâmetro hello. |
| allowedValues |Não |Matriz de valores permitidos para Olá parâmetro toomake-se de que o valor de saudação à direita é fornecida. |
| minValue |Não |valor mínimo de saudação para parâmetros de tipo int, esse valor é inclusivo. |
| maxValue |Não |valor máximo de saudação para parâmetros de tipo int, esse valor é inclusivo. |
| minLength |Não |comprimento mínimo de saudação para parâmetros de tipo de matriz de cadeia de caracteres e secureString, esse valor é inclusivo. |
| maxLength |Não |tamanho máximo de saudação para parâmetros de tipo de matriz de cadeia de caracteres e secureString, esse valor é inclusivo. |
| description |Não |Descrição do parâmetro hello que é exibida toousers por meio do portal hello. |

Olá valores e tipos permitidos são:

* **string**
* **secureString**
* **int**
* **bool**
* **object** 
* **secureObject**
* **array**

toospecify um parâmetro como opcional, forneça um valor padrão (pode ser uma cadeia de caracteres vazia). 

Se você especificar um nome de parâmetro no modelo que corresponde a um parâmetro no modelo de Olá Olá comando toodeploy, há ambiguidade potencial sobre valores hello fornecidos por você. Gerenciador de recursos resolve essa confusão, adicionando o sufixo Olá **FromTemplate** toohello parâmetro de modelo. Por exemplo, se você incluir um parâmetro chamado **ResourceGroupName** em seu modelo, ele entra em conflito com hello **ResourceGroupName** parâmetro hello [ Novo AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet. Durante a implantação, é solicitada tooprovide um valor para **ResourceGroupNameFromTemplate**. Em geral, você deve evitar essa confusão ao não nomear parâmetros com o mesmo nome como parâmetros usados para operações de implantação de saudação.

> [!NOTE]
> Todas as senhas, chaves e outros segredos devem usar Olá **secureString** tipo. Se você passar dados confidenciais em um objeto JSON, use Olá **secureObject** tipo. Os parâmetros de modelo com o tipo secureString ou secureObject não podem ser lidos após a implantação de recursos. 
> 
> Por exemplo, hello seguinte entrada no histórico da implantação Olá mostra Olá valor para uma cadeia de caracteres e objeto, mas não para secureString e secureObject.
>
> ![mostrar valores de implantação](./media/resource-group-authoring-templates/show-parameters.png)  
>

Olá mostrado no exemplo a seguir como toodefine parâmetros:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Para como valores de parâmetro de saudação tooinput durante a implantação, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md). 

## <a name="variables"></a>variáveis
Na seção de variáveis Olá, você pode construir valores que podem ser usados em todo o modelo. Você não precisa toodefine variáveis, mas eles geralmente simplificarem seu modelo, reduzindo expressões complexas.

Você pode definir variáveis com hello estrutura a seguir:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Olá mostrado no exemplo a seguir como toodefine uma variável que é construída a partir de dois valores de parâmetro:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Olá próximo exemplo mostra uma variável que é um tipo complexo de JSON e variáveis que são construídos a partir de outras variáveis:

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Recursos
Na seção de recursos hello, você define os recursos de saudação que são implantados ou atualizados. Esta seção pode ficar complicada porque você deve entender a saudação tipos que você está implantando os valores corretos do tooprovide hello. Para Olá recurso valores específicos (apiVersion, tipo e propriedades) que você precisa tooset, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/). 

Você pode definir recursos com hello estrutura a seguir:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Nome do elemento | Obrigatório | Descrição |
|:--- |:--- |:--- |
| condition | Não | Valor booliano que indica se o recurso de saudação está implantado. |
| apiVersion |Sim |Versão do hello toouse de API REST para criar o recurso de saudação. |
| type |Sim |Tipo de recurso de saudação. Esse valor é uma combinação do namespace de saudação do provedor de recursos de saudação e o tipo de recurso de saudação (como **Microsoft.Storage/storageAccounts**). |
| name |Sim |Nome do recurso de saudação. Olá deverá seguir as restrições de componente URI definidas em RFC3986. Além disso, os serviços do Azure que expõem as partes de toooutside de nome de recurso Olá validar Olá nome toomake se ele não é uma tentativa de toospoof outra identidade. |
| location |Varia |Locais geográficos com suporte de saudação fornecido recursos. Você pode selecionar qualquer um dos locais disponíveis hello, mas geralmente faz sentido toopick aquele tooyour fechar usuários. Normalmente, isso também faz sentido tooplace recursos que interagem entre si em Olá mesmo região. A maioria dos tipos de recursos exige um local, mas alguns deles (como uma atribuição de função) não. Confira [Configure os locais dos recursos de modelos do Azure Resource Manager](resource-manager-template-location.md). |
| marcas |Não |Marcas que estão associadas a recursos de saudação. Confira [Marque recursos em modelos do Azure Resource Manager](resource-manager-template-tags.md). |
| comentários |Não |As anotações para documentar recursos Olá no modelo |
| cópia |Não |Se for necessário mais de uma instância, Olá inúmeros recursos toocreate. modo padrão de saudação é paralelo. Especifique o modo serial quando você não deseja que todos ou Olá toodeploy recursos em Olá simultaneamente. Para obter mais informações, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md). |
| dependsOn |Não |Recursos que devem ser implantados antes deste recurso. Gerenciador de recursos avalia Olá dependências entre os recursos e implanta-os na ordem correta hello. Quando os recursos não dependem uns dos outros, são implantados paralelamente. Olá valor pode ser uma lista separada por vírgulas de um recurso nomes ou identificadores exclusivos de recurso. Somente lista recursos que são implantados neste modelo. Recursos que não são definidos neste modelo já devem existir. Evite adicionar dependências desnecessárias, pois elas podem reduzir sua implantação e criar dependências circulares. Para obter orientação sobre como configurar as dependências, confira [Definir as dependências nos modelos do Azure Resource Manager](resource-group-define-dependencies.md). |
| propriedades |Não |Definições de configuração específicas do recurso. valores de saudação para propriedades de saudação são Olá mesmo como valores hello fornecer no corpo da solicitação de Olá Olá API REST operação (método PUT) toocreate Olá recurso. Você também pode especificar várias instâncias de uma propriedade de um toocreate de matriz de cópia. Para obter mais informações, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md). |
| recursos |Não |Recursos filho que dependem do recurso hello está sendo definido. Forneça somente tipos de recursos que são permitidos pelo esquema de saudação do recurso pai de saudação. Olá totalmente qualificado do tipo de recurso de filho Olá inclui tipo de recurso Olá pai como **Microsoft.Web/sites/extensions**. Dependência no recurso pai, Olá não é sugerida. Você deve definir explicitamente essa dependência. |

seção de recursos Olá contém uma matriz de saudação toodeploy de recursos. Em cada recurso, você também pode definir uma matriz de recursos filhos. Portanto, a seção de recursos pode ter uma estrutura como:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Para saber mais sobre como definir recursos filho, confira [Definir o nome e o tipo do recurso filho no modelo do Resource Manager](resource-manager-template-child-resource.md).

Olá **condição** elemento Especifica se o recurso de saudação é implantado. valor desse elemento Olá resolve tootrue ou false. Por exemplo, toospecify se uma nova conta de armazenamento é implantada, use:

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

Para obter um exemplo do uso de um recurso novo ou existente, consulte [Modelo de condição novo ou existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

toospecify se uma máquina virtual é implantada com uma senha ou chave SSH, definir duas versões da máquina virtual de saudação em seu modelo e usar **condição** toodifferentiate uso. Passe um parâmetro que especifica quais toodeploy do cenário.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Para obter um exemplo do uso de uma senha ou a máquina de virtual toodeploy chave SSH, consulte [modelo de condição de nome de usuário ou o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>outputs
Na seção de saídas hello, você deve especificar valores que são retornados da implantação. Por exemplo, você pode retornar Olá URI tooaccess um recurso implantado.

Olá, exemplo a seguir mostra a estrutura de saudação de uma definição de saída:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Nome do elemento | Obrigatório | Descrição |
|:--- |:--- |:--- |
| outputName |Sim |Nome do valor de saída de hello. Deve ser um identificador JavaScript válido. |
| type |Sim |Tipo de saudação do valor de saída. Suportam a valores de saída Olá mesmo tipos como parâmetros de entrada do modelo. |
| valor |Sim |Expressão de linguagem do modelo avaliada e retornada como valor de saída. |

Olá, exemplo a seguir mostra um valor que é retornado na seção de saídas de saudação.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Para obter mais informações sobre como trabalhar com a saída, consulte [Compartilhando o estado nos modelos do Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Limites de modelo

Limitar tamanho de saudação do seu modelo too1 MB e cada parâmetro arquivos too64 KB. limite de 1 MB de saudação se aplica a toohello o estado final do modelo de saudação depois que ela foi expandida com definições de recursos iterativo e valores para variáveis e parâmetros. 

Você também está limitado a:

* 256 parâmetros
* 256 variáveis
* 800 recursos (incluindo a contagem de cópias)
* 64 valores de saída
* 24.576 caracteres em uma expressão de modelo

Você pode exceder alguns limites de modelo usando um modelo aninhado. Para saber mais, confira [Uso de modelos vinculados ao implantar recursos do Azure](resource-group-linked-templates.md). número de saudação tooreduce de parâmetros, variáveis ou saídas, você pode combinar vários valores em um objeto. Para saber mais, veja [Objetos como parâmetros](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Próximas etapas
* modelos de tooview completa para muitos tipos diferentes de soluções, consulte Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).
* Para obter detalhes sobre as funções hello você pode usar de dentro de um modelo, consulte [funções de modelo do Gerenciador de recursos do Azure](resource-group-template-functions.md).
* toocombine vários modelos durante a implantação, consulte [usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).
* Talvez seja necessário toouse recursos existentes dentro de um grupo de recursos diferente. Essa situação é comum ao trabalhar com contas de armazenamento ou redes virtuais compartilhadas com vários grupos de recursos. Para obter mais informações, consulte Olá [função resourceId](resource-group-template-functions-resource.md#resourceid).
