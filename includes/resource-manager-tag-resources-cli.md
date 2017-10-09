<span data-ttu-id="2801c-101">tooadd um grupo de recursos de tooa de marca, use **conjunto de grupos do azure**.</span><span class="sxs-lookup"><span data-stu-id="2801c-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="2801c-102">Se o grupo de recursos de saudação não tem marcas existentes, passe na marca de saudação.</span><span class="sxs-lookup"><span data-stu-id="2801c-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="2801c-103">Marcações são atualizadas como um todo.</span><span class="sxs-lookup"><span data-stu-id="2801c-103">Tags are updated as a whole.</span></span> <span data-ttu-id="2801c-104">Se você quiser tooadd um grupo de recursos de tooa marca que tem marcas existentes, passe todas as marcas de saudação.</span><span class="sxs-lookup"><span data-stu-id="2801c-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="2801c-105">Marcas não são herdadas pelos recursos em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2801c-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="2801c-106">tooadd um recurso de tooa de marca, use **conjunto de recursos do azure**.</span><span class="sxs-lookup"><span data-stu-id="2801c-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="2801c-107">Passe Olá número de versão de API Olá tipo de recurso que você está adicionando marca hello.</span><span class="sxs-lookup"><span data-stu-id="2801c-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="2801c-108">Se você precisar de versão de API de saudação tooretrieve, use Olá comando com o provedor de recursos Olá para o tipo de saudação que você está definindo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2801c-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="2801c-109">Nos resultados de hello, procure por tipo de recurso de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="2801c-109">In hello results, look for hello resource type you want.</span></span>

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

<span data-ttu-id="2801c-110">Agora, forneça essa versão de API, nome do grupo de recursos, nome do recurso, tipo de recurso e valor da marca como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="2801c-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="2801c-111">Marcações existem diretamente em recursos e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="2801c-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="2801c-112">marcas existentes do toosee hello, obter um grupo de recursos e seus recursos com **Mostrar de grupo do azure**.</span><span class="sxs-lookup"><span data-stu-id="2801c-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="2801c-113">Que retorna metadados sobre o grupo de recursos hello, incluindo qualquer tooit marcas aplicadas.</span><span class="sxs-lookup"><span data-stu-id="2801c-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

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

<span data-ttu-id="2801c-114">Exibir marcas Olá para um recurso específico usando **Mostrar recurso do azure**.</span><span class="sxs-lookup"><span data-stu-id="2801c-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="2801c-115">tooretrieve todos os recursos de saudação com um valor de marca, use:</span><span class="sxs-lookup"><span data-stu-id="2801c-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="2801c-116">tooretrieve todos os grupos de recursos de saudação com um valor de marca, use:</span><span class="sxs-lookup"><span data-stu-id="2801c-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="2801c-117">Você pode exibir as marcas existentes Olá em sua assinatura com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2801c-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
