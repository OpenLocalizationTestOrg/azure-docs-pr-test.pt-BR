tootag um recurso durante a implantação, adicionar Olá `tags` recurso de toohello do elemento está implantando. Fornece o valor e o nome da marca hello.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Aplicar um nome de marca do valor literal toohello
Olá, exemplo a seguir mostra uma conta de armazenamento com duas marcas (`Dept` e `Environment`) que são definidos valores tooliteral:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a>Aplique um elemento de marca do objeto toohello
Você pode definir um parâmetro de objeto que armazena várias marcas e aplicar esse elemento de marca do objeto toohello. Cada propriedade no objeto Olá se torna uma marca separada para o recurso de saudação. Olá, exemplo a seguir tem um parâmetro chamado `tagValues` que é o elemento de marca toohello aplicado.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a>Aplicar um nome de marca de toohello de cadeia de caracteres JSON

toostore muitos valores em uma única marca, aplicar uma cadeia de caracteres JSON que representa valores hello. cadeia de caracteres Hello de inteira JSON é armazenada como uma marca que não pode exceder 256 caracteres. Olá, exemplo a seguir tem uma única marca nomeada `CostCenter` que contém vários valores de uma cadeia de caracteres JSON:  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```