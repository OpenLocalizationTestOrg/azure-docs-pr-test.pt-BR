<span data-ttu-id="68436-101">Para adicionar uma marca a um grupo de recursos, use **azure group set**.</span><span class="sxs-lookup"><span data-stu-id="68436-101">To add a tag to a resource group, use **azure group set**.</span></span> <span data-ttu-id="68436-102">Se o grupo de recursos não tiver todas as marcas existentes, passe a marca.</span><span class="sxs-lookup"><span data-stu-id="68436-102">If the resource group does not have any existing tags, pass in the tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="68436-103">Marcações são atualizadas como um todo.</span><span class="sxs-lookup"><span data-stu-id="68436-103">Tags are updated as a whole.</span></span> <span data-ttu-id="68436-104">Se desejar adicionar uma marca a um grupo de recursos com marcas existentes, passe todas as marcas.</span><span class="sxs-lookup"><span data-stu-id="68436-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="68436-105">Marcas não são herdadas pelos recursos em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68436-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="68436-106">Para adicionar uma marca a um recurso, use **azure resource set**.</span><span class="sxs-lookup"><span data-stu-id="68436-106">To add a tag to a resource, use **azure resource set**.</span></span> <span data-ttu-id="68436-107">Passe o número de versão de API para o tipo de recurso ao qual você está adicionando a marca.</span><span class="sxs-lookup"><span data-stu-id="68436-107">Pass the API version number for the resource type that you are adding the tag to.</span></span> <span data-ttu-id="68436-108">Se precisa recuperar a versão de API, use o comando a seguir com o provedor de recursos para o tipo que você está configurando:</span><span class="sxs-lookup"><span data-stu-id="68436-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="68436-109">Nos resultados, procure o tipo de recurso desejado.</span><span class="sxs-lookup"><span data-stu-id="68436-109">In the results, look for the resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="68436-110">Agora, forneça essa versão de API, nome do grupo de recursos, nome do recurso, tipo de recurso e valor da marca como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="68436-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="68436-111">Marcações existem diretamente em recursos e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="68436-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="68436-112">Para ver as marcações existentes, obtenha um grupo de recursos e seus recursos com **azure group show**.</span><span class="sxs-lookup"><span data-stu-id="68436-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="68436-113">Ele retorna metadados sobre o grupo de recursos, incluindo todas as marcas aplicadas a esse grupo.</span><span class="sxs-lookup"><span data-stu-id="68436-113">Which returns metadata about the resource group, including any tags applied to it.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="68436-114">Você pode exibir as marcações de um recurso específico usando **azure resource show**.</span><span class="sxs-lookup"><span data-stu-id="68436-114">You view the tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="68436-115">Para recuperar todos os recursos com um valor de marca, use:</span><span class="sxs-lookup"><span data-stu-id="68436-115">To retrieve all the resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="68436-116">Para recuperar todos os grupos de recursos com um valor de marca, use:</span><span class="sxs-lookup"><span data-stu-id="68436-116">To retrieve all the resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="68436-117">Você pode exibir as marcas existentes em sua assinatura com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68436-117">You can view the existing tags in your subscription with the following command:</span></span>

```azurecli
azure tag list
```
