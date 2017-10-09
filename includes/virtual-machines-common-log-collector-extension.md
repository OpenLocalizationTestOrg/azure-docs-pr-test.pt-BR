
<span data-ttu-id="e55ef-101">Diagnosticar problemas com um serviço de nuvem do Microsoft Azure requer a coleta de arquivos de log do serviço de saudação em máquinas virtuais como Olá problemas ocorrem.</span><span class="sxs-lookup"><span data-stu-id="e55ef-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="e55ef-102">Você pode usar a extensão de AzureLogCollector sob demanda de saudação tooperfom uma única coleção de logs de um ou mais VMs de serviço de nuvem (de funções web e funções de trabalho) e transferência Olá coletado arquivos tooan conta de armazenamento do Azure – tudo sem fazer logon remotamente em tooany de saudação VMs.</span><span class="sxs-lookup"><span data-stu-id="e55ef-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="e55ef-103">Descrições para a maioria das informações de saudação registrada podem ser encontradas em http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="e55ef-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="e55ef-104">Há dois modos de coleção depende de tipos de saudação do toobe arquivos coletados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="e55ef-105">Somente Logs de GA (Agente Convidado) do Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ef-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="e55ef-106">Este modo de coleção inclui todos os agentes de convidados Olá logs tooAzure relacionados e outros componentes do Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ef-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="e55ef-107">Todos os Logs (Completo).</span><span class="sxs-lookup"><span data-stu-id="e55ef-107">All Logs (Full).</span></span> <span data-ttu-id="e55ef-108">Esse modo de coleta obterá todos os arquivos do modo GA e:</span><span class="sxs-lookup"><span data-stu-id="e55ef-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="e55ef-109">logs de eventos do sistema e do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e55ef-109">system and application event logs</span></span>
  * <span data-ttu-id="e55ef-110">logs de erros de HTTP</span><span class="sxs-lookup"><span data-stu-id="e55ef-110">HTTP error logs</span></span>
  * <span data-ttu-id="e55ef-111">Logs IIS</span><span class="sxs-lookup"><span data-stu-id="e55ef-111">IIS Logs</span></span>
  * <span data-ttu-id="e55ef-112">Logs de instalação</span><span class="sxs-lookup"><span data-stu-id="e55ef-112">Setup logs</span></span>
  * <span data-ttu-id="e55ef-113">outros logs do sistema</span><span class="sxs-lookup"><span data-stu-id="e55ef-113">other system logs</span></span>

<span data-ttu-id="e55ef-114">Em ambos os modos de coleção, as pastas de coleção de dados adicionais podem ser especificadas usando uma coleção de saudação estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="e55ef-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="e55ef-115">**Nome**: nome de saudação da coleção de saudação, que será usada como nome de saudação da subpasta no toobe de arquivo zip Olá coletados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="e55ef-116">**Local**: Olá toohello pasta do caminho na máquina virtual de saudação onde os arquivos serão coletados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="e55ef-117">**SearchPattern**: padrão de saudação de nomes de saudação do toobe arquivos coletados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="e55ef-118">O padrão é “*”</span><span class="sxs-lookup"><span data-stu-id="e55ef-118">Default is “*”</span></span>
* <span data-ttu-id="e55ef-119">**Recursiva**: se arquivos hello serão coletado recursivamente sob a pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e55ef-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e55ef-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e55ef-120">Prerequisites</span></span>
* <span data-ttu-id="e55ef-121">Você precisa toohave uma conta de armazenamento para os arquivos zip com extensão toosave gerado.</span><span class="sxs-lookup"><span data-stu-id="e55ef-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="e55ef-122">Verifique se você está usando os cmdlets do Azure PowerShell V0.8.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e55ef-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="e55ef-123">Para saber mais, confira [Downloads do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e55ef-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="e55ef-124">Adicionar extensão Olá</span><span class="sxs-lookup"><span data-stu-id="e55ef-124">Add hello extension</span></span>
<span data-ttu-id="e55ef-125">Você pode usar [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets ou [APIs de REST de gerenciamento de serviço](https://msdn.microsoft.com/library/ee460799.aspx) tooadd Olá extensão AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="e55ef-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="e55ef-126">Para serviços de nuvem, Olá cmdlet do Powershell do Azure existente, **Set-AzureServiceExtension**, pode ser usado tooenable Olá extensão em instâncias de função serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e55ef-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="e55ef-127">Toda vez que essa extensão é habilitada por este cmdlet, coleta de log é disparada nas instâncias de função hello selecionado de funções selecionadas.</span><span class="sxs-lookup"><span data-stu-id="e55ef-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="e55ef-128">Para máquinas virtuais, Olá cmdlet do Powershell do Azure existente, **Set-AzureVMExtension**, pode ser usado tooenable Olá extensão em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e55ef-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="e55ef-129">Toda vez que essa extensão é habilitada por meio de cmdlets hello, coleta de log é acionada em cada instância.</span><span class="sxs-lookup"><span data-stu-id="e55ef-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="e55ef-130">Internamente, essa extensão usa hello PublicConfiguration com base em JSON e PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="e55ef-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="e55ef-131">seguir Olá é o layout de saudação de um exemplo de JSON para configuração pública e privada.</span><span class="sxs-lookup"><span data-stu-id="e55ef-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="e55ef-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="e55ef-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="e55ef-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e55ef-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="e55ef-134">Esta extensão não precisa de **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="e55ef-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="e55ef-135">Você pode apenas fornecer uma estrutura vazia para Olá **– PrivateConfiguration** argumento.</span><span class="sxs-lookup"><span data-stu-id="e55ef-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="e55ef-136">Você pode seguir uma saudação duas etapas tooadd Olá AzureLogCollector tooone ou mais instâncias de um serviço de nuvem ou máquina Virtual de funções selecionadas, os gatilhos Olá coleções em cada VM toorun e enviem arquivos de saudação coletado tooAzure conta a seguir especificado.</span><span class="sxs-lookup"><span data-stu-id="e55ef-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="e55ef-137">Adicionar como uma extensão de serviço</span><span class="sxs-lookup"><span data-stu-id="e55ef-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="e55ef-138">Execute a assinatura de tooyour Olá instruções tooconnect PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ef-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="e55ef-139">Especifique o nome do serviço hello, slot, funções e toowhich de instâncias de função você deseja tooadd e habilitar a extensão de AzureLogCollector hello.</span><span class="sxs-lookup"><span data-stu-id="e55ef-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="e55ef-140">Especifique Olá pasta de dados adicionais para o qual os arquivos serão coletados (essa etapa é opcional).</span><span class="sxs-lookup"><span data-stu-id="e55ef-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="e55ef-141">Você pode usar o token `%roleroot%` unidade toospecify Olá função raiz desde que ele não use uma unidade fixa.</span><span class="sxs-lookup"><span data-stu-id="e55ef-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="e55ef-142">Forneça o nome de conta de armazenamento do Azure hello e arquivos de chave toowhich coletado serão carregados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="e55ef-143">Chame hello SetAzureServiceLogCollector.ps1 (incluído no final de saudação do artigo Olá) como extensão de AzureLogCollector maneira tooenable Olá para um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e55ef-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="e55ef-144">Concluída a execução hello, você pode encontrar o arquivo de saudação carregado em`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="e55ef-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="e55ef-145">a seguir Olá é a definição de Olá Olá parâmetros passados toohello script.</span><span class="sxs-lookup"><span data-stu-id="e55ef-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="e55ef-146">(Isso também foi copiado abaixo.)</span><span class="sxs-lookup"><span data-stu-id="e55ef-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="e55ef-147">*ServiceName*: o nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e55ef-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="e55ef-148">*Roles*: uma lista de funções, como "FunçãoWeb1" ou "FunçãoDeTrabalho1".</span><span class="sxs-lookup"><span data-stu-id="e55ef-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="e55ef-149">*Instâncias*: uma lista de nomes de saudação de instâncias de função separados por vírgula - usar cadeia de caracteres hello curinga ("*") para todas as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="e55ef-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="e55ef-150">*Slot*: nome do slot.</span><span class="sxs-lookup"><span data-stu-id="e55ef-150">*Slot*: Slot name.</span></span> <span data-ttu-id="e55ef-151">“Produção” ou “Preparo”.</span><span class="sxs-lookup"><span data-stu-id="e55ef-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="e55ef-152">*Mode*: modo de coleta.</span><span class="sxs-lookup"><span data-stu-id="e55ef-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="e55ef-153">"Completo" ou "GA".</span><span class="sxs-lookup"><span data-stu-id="e55ef-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="e55ef-154">*StorageAccountName*: nome da conta de armazenamento do Azure para armazenar os dados coletados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="e55ef-155">*StorageAccountKey*: nome da chave de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ef-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="e55ef-156">*AdditionalDataLocationList*: uma lista de saudação estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="e55ef-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="e55ef-157">Adicionar como uma extensão de VM</span><span class="sxs-lookup"><span data-stu-id="e55ef-157">Adding as a VM Extension</span></span>
<span data-ttu-id="e55ef-158">Execute a assinatura de tooyour Olá instruções tooconnect PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ef-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="e55ef-159">Especifique o nome do serviço hello, a VM e o modo de coleta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e55ef-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="e55ef-160">Forneça o nome de conta de armazenamento do Azure hello e arquivos de chave toowhich coletado serão carregados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="e55ef-161">Chame hello os SetAzureVMLogCollector.ps1 (incluído no final de saudação do artigo Olá) como extensão de AzureLogCollector maneira tooenable Olá para um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e55ef-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="e55ef-162">Concluída a execução hello, você pode encontrar o arquivo de saudação carregado em https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="e55ef-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="e55ef-163">a seguir Olá é a definição de Olá Olá parâmetros passados toohello script.</span><span class="sxs-lookup"><span data-stu-id="e55ef-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="e55ef-164">(Isso também foi copiado abaixo.)</span><span class="sxs-lookup"><span data-stu-id="e55ef-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="e55ef-165">ServiceName: o nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e55ef-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="e55ef-166">Nome de saudação VMName da saudação VM.</span><span class="sxs-lookup"><span data-stu-id="e55ef-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="e55ef-167">Mode: modo de coleta.</span><span class="sxs-lookup"><span data-stu-id="e55ef-167">Mode: Collection mode.</span></span> <span data-ttu-id="e55ef-168">"Completo" ou "GA".</span><span class="sxs-lookup"><span data-stu-id="e55ef-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="e55ef-169">StorageAccountName: nome da conta de armazenamento do Azure para armazenar os dados coletados.</span><span class="sxs-lookup"><span data-stu-id="e55ef-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="e55ef-170">StorageAccountKey: nome da chave de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e55ef-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="e55ef-171">AdditionalDataLocationList: Uma lista de saudação estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="e55ef-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="e55ef-172">Arquivos de Script de Extensão do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e55ef-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="e55ef-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="e55ef-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="e55ef-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="e55ef-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="e55ef-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e55ef-175">Next Steps</span></span>
<span data-ttu-id="e55ef-176">Agora você pode examinar ou copiar os logs de um local muito simples.</span><span class="sxs-lookup"><span data-stu-id="e55ef-176">Now you can examine or copy your logs from one very simple location.</span></span>

