## <a name="overview"></a><span data-ttu-id="0feb8-101">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0feb8-101">Overview</span></span>
<span data-ttu-id="0feb8-102">Quando você cria uma nova máquina virtual (VM) em um grupo de recursos ao implantar uma imagem de [Azure Marketplace](https://azure.microsoft.com/marketplace/), unidade de sistema operacional saudação padrão será de 127 GB.</span><span class="sxs-lookup"><span data-stu-id="0feb8-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="0feb8-103">Mesmo que é possível tooadd dados discos toohello VM (dependendo de quantos dos Olá SKU que você escolheu) e Além disso é recomendado tooinstall aplicativos e cargas de trabalho intensivas nesses discos adendo da CPU, muitas vezes, os clientes precisam tooexpand Olá SO unidade toosupport determinados cenários, como a seguir:</span><span class="sxs-lookup"><span data-stu-id="0feb8-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="0feb8-104">Suporte a aplicativos herdados que instalam componentes na unidade do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="0feb8-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="0feb8-105">Migração de um PC físico ou máquina virtual local com uma unidade do sistema operacional maior.</span><span class="sxs-lookup"><span data-stu-id="0feb8-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0feb8-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="0feb8-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="0feb8-107">Este artigo aborda usando o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0feb8-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="0feb8-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0feb8-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="0feb8-109">Redimensionar a unidade Olá SO</span><span class="sxs-lookup"><span data-stu-id="0feb8-109">Resize hello OS drive</span></span>
<span data-ttu-id="0feb8-110">Neste artigo é vai realizar tarefa de saudação do redimensionamento unidade Olá SO usando módulos de Gerenciador de recursos de [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="0feb8-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="0feb8-111">Abra o ISE do Powershell ou a janela do Powershell no modo de administrador e execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="0feb8-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="0feb8-112">Tooyour entrar no Microsoft Azure da conta no modo de gerenciamento de recursos e selecione sua assinatura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0feb8-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="0feb8-113">Defina o nome do grupo de recursos e o nome da VM como se segue:</span><span class="sxs-lookup"><span data-stu-id="0feb8-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="0feb8-114">Obter uma referência tooyour VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0feb8-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="0feb8-115">Pare Olá VM antes de redimensionar o disco de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0feb8-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="0feb8-116">E aqui vai momento Olá que você estava esperando!</span><span class="sxs-lookup"><span data-stu-id="0feb8-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="0feb8-117">Definir tamanho de saudação do valor do hello OS disco toohello desejado e atualizar Olá VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0feb8-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="0feb8-118">Olá novo tamanho deve ser maior que o tamanho de disco existente hello.</span><span class="sxs-lookup"><span data-stu-id="0feb8-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="0feb8-119">Olá máximo permitido é de 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="0feb8-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="0feb8-120">Olá atualização VM pode levar alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="0feb8-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="0feb8-121">Depois que o comando Olá conclui a execução, reinicie Olá VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0feb8-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="0feb8-122">É isso.</span><span class="sxs-lookup"><span data-stu-id="0feb8-122">And that’s it!</span></span> <span data-ttu-id="0feb8-123">Agora RDP em Olá VM, abra o gerenciamento do computador (ou o gerenciamento de disco) e expanda a unidade hello usando Olá espaço recentemente alocado.</span><span class="sxs-lookup"><span data-stu-id="0feb8-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="0feb8-124">Resumo</span><span class="sxs-lookup"><span data-stu-id="0feb8-124">Summary</span></span>
<span data-ttu-id="0feb8-125">Neste artigo, usamos o Azure Resource Manager módulos do Powershell tooexpand Olá unidade do sistema operacional de uma máquina virtual IaaS.</span><span class="sxs-lookup"><span data-stu-id="0feb8-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="0feb8-126">Reproduzida abaixo é o script completo a saudação para referência:</span><span class="sxs-lookup"><span data-stu-id="0feb8-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="0feb8-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0feb8-127">Next Steps</span></span>
<span data-ttu-id="0feb8-128">Embora neste artigo, nos concentramos principalmente nos expandir disco Olá SO da VM de saudação, hello desenvolvido script também pode ser usado para expandir Olá dados discos anexados toohello VM alterando uma única linha de código.</span><span class="sxs-lookup"><span data-stu-id="0feb8-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="0feb8-129">Por exemplo, tooexpand Olá primeiramente os dados anexado toohello VM de disco, substitua Olá ```OSDisk``` objeto do ```StorageProfile``` com ```DataDisks``` de matriz e usar um índice numérico de tooobtain um disco de dados anexados referência toofirst, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="0feb8-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="0feb8-130">Da mesma forma, você pode fazer referência a outros dados discos anexados toohello VM, usando um índice, como mostrado acima ou Olá ```Name``` Olá disco conforme ilustrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="0feb8-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="0feb8-131">Se você quiser toofind out como tooattach discos tooan VM do Azure Resource Manager, verifique isso [artigo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0feb8-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

