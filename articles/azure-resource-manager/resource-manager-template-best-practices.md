---
title: "práticas recomendadas de aaaBest para criar modelos do Gerenciador de recursos | Microsoft Docs"
description: Diretrizes para simplificar seus modelos do Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Práticas recomendadas para criação de modelos do Azure Resource Manager
Essas diretrizes podem ajudar você a criar modelos do Azure Resource Manager toouse fácil e confiável. diretrizes de saudação são apenas sugestões. Elas não são requisitos, exceto onde apontadas. O cenário pode exigir uma variação de uma saudação abordagens ou exemplos a seguir.

## <a name="resource-names"></a>Nomes de recurso
Normalmente, você trabalha com três tipos de nome de recurso no Resource Manager:

* Os nomes de recurso devem ser exclusivos.
* Nomes de recursos que não são necessárias toobe exclusivo, mas escolha tooprovide um nome que pode ajudá-lo a identificar um recurso com base no contexto.
* Nomes de recursos que podem ser genéricos.

 Para obter informações sobre restrições de nome de recurso, confira [Recursos recomendados de convenções de nomenclatura do Azure](../guidance/guidance-naming-conventions.md).

### <a name="unique-resource-names"></a>Nomes de recurso exclusivos
Você deve fornecer um nome de recurso exclusivo para qualquer tipo de recurso que tenha um ponto de extremidade de acesso de dados. Entre os tipos comuns de recurso que exigem um nome exclusivo estão:

* Armazenamento do Azure<sup>1</sup> 
* Recurso de Aplicativos Web do Serviço de Aplicativo do Azure
* SQL Server
* Cofre da Chave do Azure
* Cache Redis do Azure
* Lote do Azure
* Gerenciador de Tráfego do Azure
* Pesquisa do Azure
* Azure HDInsight

<sup>1</sup> Os nomes de conta de armazenamento devem estar em letras minúsculas, ter até 24 caracteres e não incluir hifens.

Se você fornecer um parâmetro de nome de um recurso, você deve fornecer um nome exclusivo quando você implanta o recurso de saudação. Opcionalmente, você pode criar uma variável que usa Olá [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate um nome de função. 

Você também pode ser desejável tooadd um prefixo ou sufixo toohello **uniqueString** resultados. Modificando nome exclusivo de saudação pode ajudá-lo mais facilmente identificar o tipo de recurso de saudação do nome de saudação. Por exemplo, você pode gerar um nome exclusivo para uma conta de armazenamento usando Olá variável a seguir:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Nomes de recurso para identificação
Alguns tipos de recursos que talvez você queira tooname, mas seus nomes não tem toobe exclusivo. Para esses tipos de recurso, você pode fornecer um nome que identifica o contexto do recurso hello e o tipo de recurso de saudação. Forneça um nome descritivo que ajudará você a identificar o recurso de saudação em uma lista de recursos. Se você precisar toouse um nome de recurso diferente para diferentes implantações, você pode usar um parâmetro para o nome da saudação:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Se você não precisar toopass em um nome durante a implantação, você pode usar uma variável: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

Também é possível usar um valor embutido em código:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Nomes de recurso genéricos
Tipos de recursos que você acessa principalmente por meio de um recurso diferente, você pode usar um nome genérico que é embutido no modelo de saudação. Por exemplo, você pode definir um nome genérico padrão para regras de firewall em um servidor SQL:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>parâmetros
Olá informações a seguir podem ser útil ao trabalhar com parâmetros:

* Minimize o uso de parâmetros. Sempre que possível, use uma variável ou um valor literal. Use parâmetros somente para estes cenários:
   
   * Configurações que você deseja toouse variações de acordo com tooenvironment (SKU, tamanho, capacidade).
   * Nomes de recurso que você deseja toospecify para facilitar sua identificação.
   * Valores que você utiliza com frequência toocomplete outras tarefas (como um nome de usuário de administrador).
   * Segredos (como senhas).
   * número de saudação ou matriz de valores toouse quando você criar várias instâncias de um tipo de recurso.
* Use minúsculas concatenadas para nomes de parâmetro.
* Forneça uma descrição de cada parâmetro na Olá metadados:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Defina valores padrão para parâmetros (exceto senhas e chaves SSH):
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Use **SecureString** para todos os segredos e senhas: 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Sempre que possível, não use um local de toospecify do parâmetro. Em vez disso, use Olá **local** propriedade saudação do grupo de recursos. Usando Olá **resourceGroup () .location** expressão de todos os seus recursos, os recursos no modelo de saudação são implantados em Olá mesmo local que o grupo de recursos de saudação:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Se um tipo de recurso é suportado em apenas um número limitado de locais, você poderá toospecify um local válido diretamente no modelo de saudação. Se você deve usar um **local** parâmetro, compartilhar esse valor de parâmetro tanto quanto possível com recursos que são provavelmente toobe em Olá mesmo local. Isso minimiza o número de saudação de vezes que os usuários são solicitados tooprovide informações de localização.
* Evite usar um parâmetro ou variável para a versão da API Olá para um tipo de recurso. Os valores e propriedades do recurso podem variar de acordo com o número de versão. IntelliSense em um editor de código não é possível determinar o esquema correto hello quando a versão da API Olá é definida tooa parâmetro ou variável. Em vez disso, codificar Olá versão de API no modelo de saudação.

## <a name="variables"></a>variáveis
Olá informações a seguir podem ser útil ao trabalhar com variáveis:

* Use variáveis para valores que você precisa toouse mais de uma vez em um modelo. Se um valor é usado apenas uma vez, um valor embutido faz seu tooread mais fácil de modelo.
* Você não pode usar o hello [referência](resource-group-template-functions-resource.md#reference) função hello **variáveis** seção Olá modelo. Olá **referência** função deriva seu valor de estado de tempo de execução do recurso hello. No entanto, variáveis são resolvidas durante a saudação inicial de análise do modelo de saudação. Construir valores que precisam de saudação **referência** função diretamente no hello **recursos** ou **gera** seção Olá modelo.
* Inclua variáveis em nomes de recurso que devem ser exclusivos, conforme descrito em [Nomes de recurso](#resource-names).
* Você pode agrupar variáveis em objetos complexos. Saudação de uso **variable.subentry** tooreference um valor de um objeto complexo de formato. O agrupamento de variáveis pode ajudar a rastrear variáveis relacionadas. Isso também melhora a legibilidade do modelo de saudação. Aqui está um exemplo:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Um objeto complexo não pode conter uma expressão que faça referência a um valor de um objeto complexo. Defina uma variável separada para essa finalidade.
   > 
   > 
   
     Para obter exemplos avançados de como usar objetos complexos como variáveis, confira [Compartilhar estado nos modelos do Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="resources"></a>Recursos
Olá informações a seguir podem ser útil ao trabalhar com recursos:

* toohelp outros colaboradores entender a finalidade de saudação do recurso de saudação, especifique **comentários** para cada recurso no modelo de saudação:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* Você pode usar marcas tooadd metadados tooresources. Use metadados tooadd informações sobre os recursos. Por exemplo, você pode adicionar detalhes de cobrança toorecord metadados para um recurso. Para obter mais informações, consulte [usando marcas tooorganize seus recursos do Azure](resource-group-using-tags.md).
* Se você usar um *ponto de extremidade público* no modelo (como um Blob do Azure storage ponto de extremidade público), *faça não embutir* Olá namespace. Saudação de uso **referência** função toodynamically recuperar Olá namespace. Você pode usar ambientes com namespace pública essa abordagem toodeploy Olá modelo toodifferent sem alterar manualmente o ponto de extremidade Olá no modelo de saudação. Definir Olá API versão toohello mesma versão que você está usando para a conta de armazenamento Olá no modelo:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Se conta de armazenamento Olá for implantada em Olá mesmo modelo que você está criando, você não precisa namespace do provedor Olá toospecify ao fazer referência a recursos de saudação. Esta é a sintaxe de saudação simplificada:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Se você tiver outros valores em seu modelo que são configurado toouse um espaço para nome público, alterar esses valores tooreflect Olá mesmo **referência** função. Por exemplo, você pode definir Olá **storageUri** propriedade do perfil de diagnóstico de máquina virtual hello:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Você também pode fazer referência a uma conta de armazenamento existente que esteja em um grupo de recursos diferente:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Atribua pública tooa de endereços IP máquina virtual somente quando um aplicativo exija isso. tooconnect tooa máquina virtual (VM) para a depuração, ou para fins administrativos, ou gerenciamento usar regras de NAT de entrada, um gateway de rede virtual ou um jumpbox.
   
     Para obter mais informações sobre como se conectar a máquinas de toovirtual, consulte:
   
   * [Executar VMs para uma arquitetura de N camadas no Azure](../guidance/guidance-compute-n-tier-vm.md)
   * [Configurar acesso WinRM para VMs no Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Permitir o acesso externo tooyour VM usando Olá portal do Azure](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Permitir o acesso externo tooyour VM usando o PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Permitir o acesso externo tooyour VM do Linux usando a CLI do Azure](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Olá **domainNameLabel** propriedade para endereços IP públicos deve ser exclusiva. Olá **domainNameLabel** valor deve ter entre 3 e 63 caracteres e seguem as regras de saudação especificadas por essa expressão regular: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Porque Olá **uniqueString** função gera uma cadeia de caracteres que é 13 caracteres hello **dnsPrefixString** parâmetro é limitado too50 caracteres:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Quando você adiciona uma extensão de script personalizado tooa senha, use Olá **commandToExecute** propriedade Olá **protectedSettings** propriedade:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure os segredos são criptografados quando eles são passados como parâmetros tooVMs e extensões, use Olá **protectedSettings** propriedade das extensões de saudação relevantes.
   > 
   > 

## <a name="outputs"></a>outputs
Se você usar um modelo toocreate os endereços IP públicos, inclua um **gera** seção que retorna detalhes do endereço IP de saudação e nome de domínio totalmente qualificado da saudação (FQDN). Você pode usar a saída valores tooeasily recuperar detalhes sobre os FQDNs e endereços IP públicos após a implantação. Ao fazer referência a recursos hello, use a versão de hello API que você usou toocreate-lo: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Modelo único vs. modelos aninhados
toodeploy sua solução, você pode usar um único modelo ou um modelo principal com vários modelos aninhados. Os modelos aninhados são comuns em cenários mais avançados. Usando um oferece modelo aninhado você Olá vantagens a seguir:

* Você pode dividir uma solução em componentes direcionados.
* Você pode reutilizar modelos aninhados com diferentes modelos principais.

Se você escolher modelos toouse aninhado, Olá diretrizes a seguir pode ajudá-lo a padronizar o design do modelo. Essas diretrizes se baseiam nos [padrões de design para modelos do Azure Resource Manager](best-practices-resource-manager-design-templates.md). Recomendamos um design que tem Olá modelos a seguir:

* **Modelo principal** (azuredeploy.json). Uso de parâmetros de entrada hello.
* **Modelo de recursos compartilhados**. Use toodeploy os recursos que usam todos os outros recursos compartilhados (por exemplo, virtual de rede e disponibilidade conjuntos). Saudação de uso **dependsOn** tooensure de expressão que esse modelo é implantado antes de outros modelos.
* **Modelo de recursos opcionais**. Use tooconditionally implantar recursos com base em um parâmetro (por exemplo, um jumpbox).
* **Modelo de recursos de membro**. Cada tipo de instância dentro de uma camada de aplicativo tem sua própria configuração. Dentro de uma camada, você pode definir tipos diferentes de instância. (Por exemplo, Olá instância primeiro cria um cluster, e instâncias adicionais são adicionadas cluster existente toohello.) Cada tipo de instância tem seu próprio modelo de implantação.
* **Scripts**. Scripts amplamente reutilizáveis são aplicáveis a cada tipo de instância (por exemplo, inicializar e formatar discos adicionais). Os scripts personalizados que você cria para uma finalidade específica de personalização forem diferentes, com base no tipo de instância de saudação.

![Modelo aninhado](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Para saber mais, confira [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Vincular condicionalmente toonested modelos
Você pode usar modelos de toonested de parâmetro tooconditionally link. parâmetro Hello se torna parte da saudação URI para o modelo de saudação:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Formato de modelo
É uma boa prática toopass seu modelo por meio de um validador JSON. Um validador pode ajudar a remover vírgulas, parênteses e colchetes irrelevantes que podem gerar um erro durante a implantação. Experimente o [JSONLint](http://jsonlint.com/) ou um pacote linter para seu ambiente de edição favorito (Visual Studio Code, Atom, Sublime Text, Visual Studio).

Também é uma boa ideia tooformat o JSON para melhor legibilidade. Você pode usar um pacote de formatador JSON para seu editor local. No Visual Studio, o documento de saudação tooformat, pressione **Ctrl + K, Ctrl + D**. No Visual Studio Code, pressione **Alt + Shift + F**. Se seu editor de local não Formatar documento hello, você pode usar um [formatador online](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Próximas etapas
* Para obter diretrizes sobre a arquitetura de sua solução para máquinas virtuais, confira [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) (Executar uma VM Windows no Azure) e [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md) (Executar uma VM Linux no Azure).
* Para obter orientação sobre como configurar uma conta de armazenamento, confira [Lista de verificação de desempenho e escalabilidade do armazenamento do Azure](../storage/common/storage-performance-checklist.md).
* toolearn sobre como uma empresa pode usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold Azure enterprise: controle de assinatura prescritivas](resource-manager-subscription-governance.md).

