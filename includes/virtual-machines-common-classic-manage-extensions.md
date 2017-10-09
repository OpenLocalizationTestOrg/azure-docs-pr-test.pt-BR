


## <a name="using-vm-extensions"></a><span data-ttu-id="45b66-101">Usando extensões de VM</span><span class="sxs-lookup"><span data-stu-id="45b66-101">Using VM Extensions</span></span>
<span data-ttu-id="45b66-102">Extensões de VM do Azure implementam comportamentos ou recursos que o ajudam a outros programas funcionam em máquinas virtuais do Azure (por exemplo, Olá **WebDeployForVSDevTest** extensão permite implantar soluções Visual Studio tooWeb em sua VM do Azure) ou fornecer Olá capacidade para que você toointeract com hello VM toosupport alguns outros comportamentos (por exemplo, você pode usar extensões de acesso da máquina virtual de saudação do PowerShell, Olá CLI do Azure e REST clientes tooreset ou modificar valores de acesso remoto em sua VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="45b66-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45b66-103">Para obter uma lista completa das extensões pelos recursos de saudação que oferecem suporte, consulte [extensões de VM do Azure e recursos](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45b66-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="45b66-104">Como cada extensão VM oferece suporte a um recurso específico, exatamente o que você pode e não pode fazer com uma extensão depende Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="45b66-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="45b66-105">Portanto, antes de modificar sua VM, verifique se que você leu documentação Olá Olá extensão de VM que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="45b66-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="45b66-106">Não há suporte para remover algumas extensões de VM; outras têm propriedades que podem ser definidas e que alteram radicalmente o comportamento da VM.</span><span class="sxs-lookup"><span data-stu-id="45b66-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="45b66-107">Olá as tarefas mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="45b66-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="45b66-108">Localizando extensões disponíveis</span><span class="sxs-lookup"><span data-stu-id="45b66-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="45b66-109">Atualizando extensões carregadas</span><span class="sxs-lookup"><span data-stu-id="45b66-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="45b66-110">Adicionando extensões</span><span class="sxs-lookup"><span data-stu-id="45b66-110">Adding Extensions</span></span>
4. <span data-ttu-id="45b66-111">Removendo extensões</span><span class="sxs-lookup"><span data-stu-id="45b66-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="45b66-112">Localizar extensões disponíveis</span><span class="sxs-lookup"><span data-stu-id="45b66-112">Find Available Extensions</span></span>
<span data-ttu-id="45b66-113">Você pode localizar a extensão e as informações estendidas usando:</span><span class="sxs-lookup"><span data-stu-id="45b66-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="45b66-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45b66-114">PowerShell</span></span>
* <span data-ttu-id="45b66-115">Interface de linha de comando da plataforma cruzada do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="45b66-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="45b66-116">API REST de gerenciamento de serviço</span><span class="sxs-lookup"><span data-stu-id="45b66-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="45b66-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="45b66-117">Azure PowerShell</span></span>
<span data-ttu-id="45b66-118">Algumas extensões têm cmdlets do PowerShell que são toothem específico, o que pode facilitar a configuração do PowerShell; mas hello cmdlets a seguir funcionam para todas as extensões VM.</span><span class="sxs-lookup"><span data-stu-id="45b66-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="45b66-119">Você pode usar o hello seguintes cmdlets tooobtain informações sobre as extensões disponíveis:</span><span class="sxs-lookup"><span data-stu-id="45b66-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="45b66-120">Para instâncias de funções web ou funções de trabalho, você pode usar o hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45b66-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="45b66-121">Para instâncias de máquinas virtuais, você pode usar o hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45b66-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="45b66-122">Por exemplo, Olá mostra exemplo de código a seguir como toolist as informações de saudação **IaaSDiagnostics** extensão usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45b66-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="45b66-123">Interface de Linha de Comando do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="45b66-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="45b66-124">Algumas extensões têm comandos de CLI do Azure que são específico toothem (Olá extensão da VM Docker é um exemplo), que podem facilitar suas configurações; mas a seguir Olá comandos funcionam para todas as extensões VM.</span><span class="sxs-lookup"><span data-stu-id="45b66-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="45b66-125">Você pode usar o hello **lista de extensões de vm do azure** tooobtain informações sobre as extensões disponíveis de comando e use Olá **–-json** opção toodisplay todas as informações disponíveis sobre uma ou mais extensões.</span><span class="sxs-lookup"><span data-stu-id="45b66-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="45b66-126">Se você não usar um nome de extensão, o comando Olá retorna uma descrição de JSON de todas as extensões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="45b66-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="45b66-127">Por exemplo, Olá exemplo de código a seguir mostra como toolist Olá informações para Olá **IaaSDiagnostics** extensão usando Olá CLI do Azure **lista de extensões de vm do azure** comando e usa Olá **–-json** opção tooreturn obter informações completas.</span><span class="sxs-lookup"><span data-stu-id="45b66-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="45b66-128">APIs REST do Gerenciamento de Serviço</span><span class="sxs-lookup"><span data-stu-id="45b66-128">Service Management REST APIs</span></span>
<span data-ttu-id="45b66-129">Você pode usar o hello seguintes APIs REST tooobtain informações sobre as extensões disponíveis:</span><span class="sxs-lookup"><span data-stu-id="45b66-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="45b66-130">Para instâncias de funções web ou funções de trabalho, você pode usar o hello [listar extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="45b66-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="45b66-131">versões de saudação toolist de extensões disponíveis, você pode usar [listar versões da extensão](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="45b66-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="45b66-132">Para instâncias de máquinas virtuais, você pode usar o hello [listar extensões de recurso](https://msdn.microsoft.com/library/dn495441.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="45b66-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="45b66-133">versões de saudação toolist de extensões disponíveis, você pode usar [listar versões da extensão de recurso](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="45b66-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="45b66-134">Adicionar, atualizar ou desabilitar extensões</span><span class="sxs-lookup"><span data-stu-id="45b66-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="45b66-135">As extensões podem ser adicionadas quando uma instância for criada ou podem ser adicionadas tooa instância em execução.</span><span class="sxs-lookup"><span data-stu-id="45b66-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="45b66-136">As Extensões podem ser atualizadas, desabilitadas ou removidas.</span><span class="sxs-lookup"><span data-stu-id="45b66-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="45b66-137">Você pode executar essas ações usando cmdlets do PowerShell do Azure ou usando operações de API de REST de gerenciamento de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="45b66-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="45b66-138">Parâmetros são necessário tooinstall e configurar algumas extensões.</span><span class="sxs-lookup"><span data-stu-id="45b66-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="45b66-139">Os parâmetros públicos e privados têm suporte para extensões.</span><span class="sxs-lookup"><span data-stu-id="45b66-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="45b66-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="45b66-140">Azure PowerShell</span></span>
<span data-ttu-id="45b66-141">Usando cmdlets do PowerShell do Azure é hello mais fácil maneira tooadd e atualizar as extensões.</span><span class="sxs-lookup"><span data-stu-id="45b66-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="45b66-142">Quando você usar os cmdlets de extensão hello, a maioria da configuração de saudação da extensão de saudação é feito para você.</span><span class="sxs-lookup"><span data-stu-id="45b66-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="45b66-143">Às vezes, talvez seja necessário tooprogrammatically adicionar uma extensão.</span><span class="sxs-lookup"><span data-stu-id="45b66-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="45b66-144">Quando você precisar toodo isso, você deve fornecer configuração de saudação da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="45b66-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="45b66-145">Você pode usar o hello tooknow cmdlets a seguir se uma extensão requer uma configuração de parâmetros públicos e privados:</span><span class="sxs-lookup"><span data-stu-id="45b66-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="45b66-146">Para instâncias de funções web ou funções de trabalho, você pode usar o hello **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45b66-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="45b66-147">Para instâncias de máquinas virtuais, você pode usar o hello **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45b66-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="45b66-148">APIs REST do Gerenciamento de Serviço</span><span class="sxs-lookup"><span data-stu-id="45b66-148">Service Management REST APIs</span></span>
<span data-ttu-id="45b66-149">Quando você recupera uma lista de extensões disponíveis usando Olá APIs REST, você receberá informações sobre como a extensão de saudação é toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="45b66-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="45b66-150">informações de saudação que são retornadas podem mostrar informações de parâmetro representadas por um esquema público e um esquema privado.</span><span class="sxs-lookup"><span data-stu-id="45b66-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="45b66-151">Valores de parâmetros públicos são retornados em consultas sobre as instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="45b66-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="45b66-152">Os valores dos parâmetros privados não são retornados.</span><span class="sxs-lookup"><span data-stu-id="45b66-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="45b66-153">Você pode usar o hello tooknow de APIs REST a seguir se uma extensão requer uma configuração de parâmetros públicos e privados:</span><span class="sxs-lookup"><span data-stu-id="45b66-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="45b66-154">Para instâncias de funções web ou funções de trabalho, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de saudação na resposta de saudação do hello [lista As extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="45b66-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="45b66-155">Para instâncias de máquinas virtuais, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de saudação na resposta de saudação do hello [lista Extensões de recurso](https://msdn.microsoft.com/library/dn495441.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="45b66-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="45b66-156">As extensões também podem usar as configurações que são definidas com JSON.</span><span class="sxs-lookup"><span data-stu-id="45b66-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="45b66-157">Quando esses tipos de extensões são usados, somente Olá **SampleConfig** elemento é usado.</span><span class="sxs-lookup"><span data-stu-id="45b66-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

