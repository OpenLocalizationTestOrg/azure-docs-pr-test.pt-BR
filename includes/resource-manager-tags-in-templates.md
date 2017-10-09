<span data-ttu-id="9d66a-101">tootag um recurso durante a implantação, adicionar Olá `tags` recurso de toohello do elemento está implantando.</span><span class="sxs-lookup"><span data-stu-id="9d66a-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="9d66a-102">Fornece o valor e o nome da marca hello.</span><span class="sxs-lookup"><span data-stu-id="9d66a-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="9d66a-103">Aplicar um nome de marca do valor literal toohello</span><span class="sxs-lookup"><span data-stu-id="9d66a-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="9d66a-104">Olá, exemplo a seguir mostra uma conta de armazenamento com duas marcas (`Dept` e `Environment`) que são definidos valores tooliteral:</span><span class="sxs-lookup"><span data-stu-id="9d66a-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

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

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="9d66a-105">Aplique um elemento de marca do objeto toohello</span><span class="sxs-lookup"><span data-stu-id="9d66a-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="9d66a-106">Você pode definir um parâmetro de objeto que armazena várias marcas e aplicar esse elemento de marca do objeto toohello.</span><span class="sxs-lookup"><span data-stu-id="9d66a-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="9d66a-107">Cada propriedade no objeto Olá se torna uma marca separada para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d66a-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="9d66a-108">Olá, exemplo a seguir tem um parâmetro chamado `tagValues` que é o elemento de marca toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="9d66a-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

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

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="9d66a-109">Aplicar um nome de marca de toohello de cadeia de caracteres JSON</span><span class="sxs-lookup"><span data-stu-id="9d66a-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="9d66a-110">toostore muitos valores em uma única marca, aplicar uma cadeia de caracteres JSON que representa valores hello.</span><span class="sxs-lookup"><span data-stu-id="9d66a-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="9d66a-111">cadeia de caracteres Hello de inteira JSON é armazenada como uma marca que não pode exceder 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9d66a-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="9d66a-112">Olá, exemplo a seguir tem uma única marca nomeada `CostCenter` que contém vários valores de uma cadeia de caracteres JSON:</span><span class="sxs-lookup"><span data-stu-id="9d66a-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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