A versão 3.0 do módulo de AzureRm.Resources Olá incluídas alterações significativas para trabalhar com marcas. Antes de prosseguir, verifique sua versão:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Se os resultados mostram uma versão 3.0 ou posterior, exemplos neste tópico Olá trabalharem com seu ambiente. Se você não tiver a versão 3.0 ou posterior, [atualize sua versão](/powershell/azureps-cmdlets-docs/) usando a Galeria do PowerShell ou o Web Platform Installer antes de avançar com este tópico.

```powershell
Version
-------
3.5.0
```

toosee Olá marcas existentes para um *grupo de recursos*, use:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Esse script retorna Olá formato a seguir:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee Olá marcas existentes para um *recurso que tem uma ID de recurso especificado*, use:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Ou, toosee Olá marcas existentes para um *recurso que tem um grupo de recursos e o nome especificado*, use:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *grupos de recursos que têm uma marca específica*, use:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *recursos que têm uma marca específica*, use:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Quando você aplica marcas tooa recurso ou um grupo de recursos, você pode substituir as marcas existentes Olá nesse recurso ou grupo de recursos. Portanto, você deve usar uma abordagem diferente com base em se o recurso de saudação ou grupo de recursos tem marcas existentes. 

tooadd marcas tooa *grupo de recursos sem marcas existentes*, use:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd marcas tooa *grupo de recursos que tem marcas existentes*, recuperar marcas existentes hello, adicionar Olá nova marca e reaplicar Olá marcas:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd marcas tooa *recurso sem marcas existentes*, use:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd marcas tooa *recurso que tem marcas existentes*, use:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply todas as marcas de recursos do tooits um grupo de recursos, e *não reter marcas existentes nos recursos de saudação*, use Olá script a seguir:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply todas as marcas de recursos do tooits um grupo de recursos, e *reter marcas existentes em recursos que não sejam duplicatas*, use Olá script a seguir:

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

tooremove todas as marcas, passe uma tabela de hash vazio:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



