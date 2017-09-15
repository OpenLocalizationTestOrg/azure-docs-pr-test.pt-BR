


## <a name="using-vm-extensions"></a><span data-ttu-id="f4fa3-101">Usando extensões de VM</span><span class="sxs-lookup"><span data-stu-id="f4fa3-101">Using VM Extensions</span></span>
<span data-ttu-id="f4fa3-102">As Extensões de VM do Azure implementam comportamentos ou recursos que ajudam outros programas a funcionar em VMs do Azure (por exemplo, a extensão **WebDeployForVSDevTest** permite o Visual Studio para soluções de implantação da Web em sua VM do Azure) ou fornecem a capacidade de interagir com a máquina virtual para dar suporte a alguns outros comportamentos (por exemplo, você pode usar as extensões de acesso da máquina virtual do Powershell, a CLI do Azure e clientes REST para redefinir ou modificar os valores de acesso remoto na sua VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4fa3-103">Para obter uma lista completa das extensões pelos recursos aos quais elas dão suporte, consulte [Extensões e recursos de VM do Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f4fa3-104">Como cada extensão de VM dá suporte a um recurso específico, exatamente o que você pode e não pode fazer com uma extensão depende da extensão.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="f4fa3-105">Portanto, antes de modificar a sua VM, verifique se que você leu a documentação para a extensão de VM que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="f4fa3-106">Não há suporte para remover algumas extensões de VM; outras têm propriedades que podem ser definidas e que alteram radicalmente o comportamento da VM.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="f4fa3-107">As tarefas mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-107">The most common tasks are:</span></span>

1. <span data-ttu-id="f4fa3-108">Localizando extensões disponíveis</span><span class="sxs-lookup"><span data-stu-id="f4fa3-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="f4fa3-109">Atualizando extensões carregadas</span><span class="sxs-lookup"><span data-stu-id="f4fa3-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="f4fa3-110">Adicionando extensões</span><span class="sxs-lookup"><span data-stu-id="f4fa3-110">Adding Extensions</span></span>
4. <span data-ttu-id="f4fa3-111">Removendo extensões</span><span class="sxs-lookup"><span data-stu-id="f4fa3-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="f4fa3-112">Localizar extensões disponíveis</span><span class="sxs-lookup"><span data-stu-id="f4fa3-112">Find Available Extensions</span></span>
<span data-ttu-id="f4fa3-113">Você pode localizar a extensão e as informações estendidas usando:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="f4fa3-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4fa3-114">PowerShell</span></span>
* <span data-ttu-id="f4fa3-115">Interface de linha de comando da plataforma cruzada do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="f4fa3-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="f4fa3-116">API REST de gerenciamento de serviço</span><span class="sxs-lookup"><span data-stu-id="f4fa3-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="f4fa3-117">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="f4fa3-117">Azure PowerShell</span></span>
<span data-ttu-id="f4fa3-118">Algumas extensões têm cmdlets do Powershell que são específicos delas, que podem facilitar suas configurações do PowerShell; mas os seguintes cmdlets funcionam para todas as extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="f4fa3-119">Você pode usar os cmdlets a seguir para obter informações sobre as extensões disponíveis:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="f4fa3-120">Para instâncias de funções web ou funções de trabalho, você pode usar o cmdlet [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f4fa3-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="f4fa3-121">Para instâncias de máquinas virtuais, você pode usar o cmdlet [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f4fa3-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="f4fa3-122">Por exemplo, o exemplo de código a seguir mostra como listar as informações para a extensão **IaaSDiagnostics** usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="f4fa3-123">Interface de Linha de Comando do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="f4fa3-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="f4fa3-124">Algumas extensões têm os comandos da CLI do Azure específicos a elas (a Extensão de VM do Docker é um exemplo), que podem facilitar suas configurações; mas os comandos a seguir funcionam para todas as extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="f4fa3-125">Você pode usar o comando **azure vm extension list** para obter informações sobre as extensões disponíveis e usar a opção **–-json** para exibir todas as informações disponíveis sobre uma ou mais extensões.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="f4fa3-126">Se você não usar um nome de extensão, o comando retorna uma descrição JSON de todas as extensões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="f4fa3-127">Por exemplo, o exemplo de código a seguir mostra como listar as informações para a extensão **IaaSDiagnostics** usando o comando **azure vm extension list** da CLI do Azure e usa a opção **–-json** para retornar informações completas.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="f4fa3-128">APIs REST do Gerenciamento de Serviço</span><span class="sxs-lookup"><span data-stu-id="f4fa3-128">Service Management REST APIs</span></span>
<span data-ttu-id="f4fa3-129">Você pode usar as APIs REST a seguir para obter informações sobre as extensões disponíveis:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="f4fa3-130">Para instâncias de funções web ou funções de trabalho, você pode usar a operação [Listar extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f4fa3-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="f4fa3-131">Para listar as versões de extensões disponíveis, você pode usar [Listar versões da extensão](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="f4fa3-132">Para instâncias de máquinas virtuais, você pode usar a operação [Listar extensões de recurso](https://msdn.microsoft.com/library/dn495441.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f4fa3-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="f4fa3-133">Para listar as versões de extensões disponíveis, você pode usar [Listar versões da extensão de recurso](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="f4fa3-134">Adicionar, atualizar ou desabilitar extensões</span><span class="sxs-lookup"><span data-stu-id="f4fa3-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="f4fa3-135">As extensões podem ser adicionadas quando uma instância for criada ou podem ser adicionadas a uma instância em execução.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="f4fa3-136">As Extensões podem ser atualizadas, desabilitadas ou removidas.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="f4fa3-137">Você pode executar essas ações usando cmdlets do Azure PowerShell ou usando as operações de API de REST do Gerenciamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="f4fa3-138">São necessários parâmetros para instalar e configurar algumas extensões.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="f4fa3-139">Os parâmetros públicos e privados têm suporte para extensões.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="f4fa3-140">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="f4fa3-140">Azure PowerShell</span></span>
<span data-ttu-id="f4fa3-141">Usar cmdlets do Azure PowerShell é a maneira mais fácil de adicionar e atualizar extensões.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="f4fa3-142">Quando você usa os cmdlets de extensão, a maioria da configuração da extensão é feita para você.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="f4fa3-143">Às vezes, talvez seja necessário adicionar programaticamente uma extensão.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="f4fa3-144">Quando precisar fazer isso, você deverá fornecer a configuração da extensão.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="f4fa3-145">Você pode usar os cmdlets a seguir para saber se uma extensão requer uma configuração de parâmetros públicos e privados:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="f4fa3-146">Para instâncias de funções web ou funções de trabalho, você pode usar o cmdlet **Get-AzureServiceAvailableExtension** .</span><span class="sxs-lookup"><span data-stu-id="f4fa3-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="f4fa3-147">Para instâncias de máquinas virtuais, você pode usar o cmdlet **Get-AzureVMAvailableExtension** .</span><span class="sxs-lookup"><span data-stu-id="f4fa3-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="f4fa3-148">APIs REST do Gerenciamento de Serviço</span><span class="sxs-lookup"><span data-stu-id="f4fa3-148">Service Management REST APIs</span></span>
<span data-ttu-id="f4fa3-149">Ao recuperar uma lista de extensões disponíveis usando as APIs REST, você receberá informações sobre como a extensão deve ser configurada.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="f4fa3-150">As informações retornadas podem mostrar informações de parâmetro representadas por um esquema público e um esquema privado.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="f4fa3-151">Os valores de parâmetros públicos são retornados em consultas sobre as instâncias.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="f4fa3-152">Os valores dos parâmetros privados não são retornados.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="f4fa3-153">Você pode usar as APIs REST a seguir para saber se uma extensão requer uma configuração de parâmetros públicos e privados:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="f4fa3-154">Para instâncias de funções Web ou funções de trabalho, os elementos **PublicConfigurationSchema** e **PrivateConfigurationSchema** contêm as informações na resposta da operação [Listar Extensões Disponíveis](https://msdn.microsoft.com/library/dn169559.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="f4fa3-155">Para instâncias de Máquinas Virtuais, os elementos **PublicConfigurationSchema** e **PrivateConfigurationSchema** contêm as informações na resposta da operação [Listar Extensões de Recurso](https://msdn.microsoft.com/library/dn495441.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="f4fa3-156">As extensões também podem usar as configurações que são definidas com JSON.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="f4fa3-157">Quando esses tipos de extensões são usados, apenas o elemento **SampleConfig** é usado.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

