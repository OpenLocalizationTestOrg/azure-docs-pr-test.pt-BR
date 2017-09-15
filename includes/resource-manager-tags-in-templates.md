<span data-ttu-id="d6ab7-101">Para marcar um recurso durante a implantação, adicione o elemento `tags` ao recurso que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="d6ab7-102">Forneça o nome e o valor da marca.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="d6ab7-103">Aplicar um valor literal ao nome da marca</span><span class="sxs-lookup"><span data-stu-id="d6ab7-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="d6ab7-104">O exemplo a seguir mostra uma conta de armazenamento com duas marcas (`Dept` e `Environment`) que são definidas como valores literais:</span><span class="sxs-lookup"><span data-stu-id="d6ab7-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

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

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="d6ab7-105">Aplicar um objeto ao elemento da marca</span><span class="sxs-lookup"><span data-stu-id="d6ab7-105">Apply an object to the tag element</span></span>
<span data-ttu-id="d6ab7-106">Você pode definir um parâmetro de objeto que armazena várias marcas e aplicar esse objeto para o elemento de marca.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="d6ab7-107">Cada propriedade no objeto se torna uma marca separada para o recurso.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="d6ab7-108">O exemplo a seguir tem um parâmetro chamado `tagValues` que é aplicado ao elemento de marca.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

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

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="d6ab7-109">Aplicar uma cadeia de caracteres JSON ao nome da marca</span><span class="sxs-lookup"><span data-stu-id="d6ab7-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="d6ab7-110">Para armazenar diversos valores em uma única marca, aplica uma cadeia de caracteres JSON que representa os valores.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="d6ab7-111">A cadeia de caracteres JSON inteira é armazenada como uma marca que não pode exceder 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6ab7-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="d6ab7-112">O exemplo a seguir tem uma única marca denominada `CostCenter` que contém vários valores de uma cadeia de caracteres JSON:</span><span class="sxs-lookup"><span data-stu-id="d6ab7-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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