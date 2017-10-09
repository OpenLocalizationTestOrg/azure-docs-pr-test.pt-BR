<span data-ttu-id="9b42f-101">A versão 3.0 do módulo de AzureRm.Resources Olá incluídas alterações significativas para trabalhar com marcas.</span><span class="sxs-lookup"><span data-stu-id="9b42f-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="9b42f-102">Antes de prosseguir, verifique sua versão:</span><span class="sxs-lookup"><span data-stu-id="9b42f-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="9b42f-103">Se os resultados mostram uma versão 3.0 ou posterior, exemplos neste tópico Olá trabalharem com seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9b42f-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="9b42f-104">Se você não tiver a versão 3.0 ou posterior, [atualize sua versão](/powershell/azureps-cmdlets-docs/) usando a Galeria do PowerShell ou o Web Platform Installer antes de avançar com este tópico.</span><span class="sxs-lookup"><span data-stu-id="9b42f-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="9b42f-105">toosee Olá marcas existentes para um *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="9b42f-106">Esse script retorna Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b42f-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="9b42f-107">toosee Olá marcas existentes para um *recurso que tem uma ID de recurso especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="9b42f-108">Ou, toosee Olá marcas existentes para um *recurso que tem um grupo de recursos e o nome especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="9b42f-109">tooget *grupos de recursos que têm uma marca específica*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="9b42f-110">tooget *recursos que têm uma marca específica*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="9b42f-111">Quando você aplica marcas tooa recurso ou um grupo de recursos, você pode substituir as marcas existentes Olá nesse recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b42f-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="9b42f-112">Portanto, você deve usar uma abordagem diferente com base em se o recurso de saudação ou grupo de recursos tem marcas existentes.</span><span class="sxs-lookup"><span data-stu-id="9b42f-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="9b42f-113">tooadd marcas tooa *grupo de recursos sem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="9b42f-114">tooadd marcas tooa *grupo de recursos que tem marcas existentes*, recuperar marcas existentes hello, adicionar Olá nova marca e reaplicar Olá marcas:</span><span class="sxs-lookup"><span data-stu-id="9b42f-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="9b42f-115">tooadd marcas tooa *recurso sem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="9b42f-116">tooadd marcas tooa *recurso que tem marcas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="9b42f-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="9b42f-117">tooapply todas as marcas de recursos do tooits um grupo de recursos, e *não reter marcas existentes nos recursos de saudação*, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b42f-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="9b42f-118">tooapply todas as marcas de recursos do tooits um grupo de recursos, e *reter marcas existentes em recursos que não sejam duplicatas*, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b42f-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="9b42f-119">tooremove todas as marcas, passe uma tabela de hash vazio:</span><span class="sxs-lookup"><span data-stu-id="9b42f-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



