


## <a name="using-vm-extensions"></a>Usando extensões de VM
Extensões de VM do Azure implementam comportamentos ou recursos que o ajudam a outros programas funcionam em máquinas virtuais do Azure (por exemplo, Olá **WebDeployForVSDevTest** extensão permite implantar soluções Visual Studio tooWeb em sua VM do Azure) ou fornecer Olá capacidade para que você toointeract com hello VM toosupport alguns outros comportamentos (por exemplo, você pode usar extensões de acesso da máquina virtual de saudação do PowerShell, Olá CLI do Azure e REST clientes tooreset ou modificar valores de acesso remoto em sua VM do Azure).

> [!IMPORTANT]
> Para obter uma lista completa das extensões pelos recursos de saudação que oferecem suporte, consulte [extensões de VM do Azure e recursos](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Como cada extensão VM oferece suporte a um recurso específico, exatamente o que você pode e não pode fazer com uma extensão depende Olá extensão. Portanto, antes de modificar sua VM, verifique se que você leu documentação Olá Olá extensão de VM que você deseja toouse. Não há suporte para remover algumas extensões de VM; outras têm propriedades que podem ser definidas e que alteram radicalmente o comportamento da VM.
> 
> 

Olá as tarefas mais comuns são:

1. Localizando extensões disponíveis
2. Atualizando extensões carregadas
3. Adicionando extensões
4. Removendo extensões

## <a name="find-available-extensions"></a>Localizar extensões disponíveis
Você pode localizar a extensão e as informações estendidas usando:

* PowerShell
* Interface de linha de comando da plataforma cruzada do Azure (CLI do Azure)
* API REST de gerenciamento de serviço

### <a name="azure-powershell"></a>Azure PowerShell
Algumas extensões têm cmdlets do PowerShell que são toothem específico, o que pode facilitar a configuração do PowerShell; mas hello cmdlets a seguir funcionam para todas as extensões VM.

Você pode usar o hello seguintes cmdlets tooobtain informações sobre as extensões disponíveis:

* Para instâncias de funções web ou funções de trabalho, você pode usar o hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.
* Para instâncias de máquinas virtuais, você pode usar o hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.
  
   Por exemplo, Olá mostra exemplo de código a seguir como toolist as informações de saudação **IaaSDiagnostics** extensão usando o PowerShell.
  
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

### <a name="azure-command-line-interface-azure-cli"></a>Interface de Linha de Comando do Azure (CLI do Azure)
Algumas extensões têm comandos de CLI do Azure que são específico toothem (Olá extensão da VM Docker é um exemplo), que podem facilitar suas configurações; mas a seguir Olá comandos funcionam para todas as extensões VM.

Você pode usar o hello **lista de extensões de vm do azure** tooobtain informações sobre as extensões disponíveis de comando e use Olá **–-json** opção toodisplay todas as informações disponíveis sobre uma ou mais extensões. Se você não usar um nome de extensão, o comando Olá retorna uma descrição de JSON de todas as extensões disponíveis.

Por exemplo, Olá exemplo de código a seguir mostra como toolist Olá informações para Olá **IaaSDiagnostics** extensão usando Olá CLI do Azure **lista de extensões de vm do azure** comando e usa Olá **–-json** opção tooreturn obter informações completas.

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



### <a name="service-management-rest-apis"></a>APIs REST do Gerenciamento de Serviço
Você pode usar o hello seguintes APIs REST tooobtain informações sobre as extensões disponíveis:

* Para instâncias de funções web ou funções de trabalho, você pode usar o hello [listar extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) operação. versões de saudação toolist de extensões disponíveis, você pode usar [listar versões da extensão](https://msdn.microsoft.com/library/dn495437.aspx).
* Para instâncias de máquinas virtuais, você pode usar o hello [listar extensões de recurso](https://msdn.microsoft.com/library/dn495441.aspx) operação. versões de saudação toolist de extensões disponíveis, você pode usar [listar versões da extensão de recurso](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Adicionar, atualizar ou desabilitar extensões
As extensões podem ser adicionadas quando uma instância for criada ou podem ser adicionadas tooa instância em execução. As Extensões podem ser atualizadas, desabilitadas ou removidas. Você pode executar essas ações usando cmdlets do PowerShell do Azure ou usando operações de API de REST de gerenciamento de serviços de saudação. Parâmetros são necessário tooinstall e configurar algumas extensões. Os parâmetros públicos e privados têm suporte para extensões.

### <a name="azure-powershell"></a>Azure PowerShell
Usando cmdlets do PowerShell do Azure é hello mais fácil maneira tooadd e atualizar as extensões. Quando você usar os cmdlets de extensão hello, a maioria da configuração de saudação da extensão de saudação é feito para você. Às vezes, talvez seja necessário tooprogrammatically adicionar uma extensão. Quando você precisar toodo isso, você deve fornecer configuração de saudação da extensão de saudação.

Você pode usar o hello tooknow cmdlets a seguir se uma extensão requer uma configuração de parâmetros públicos e privados:

* Para instâncias de funções web ou funções de trabalho, você pode usar o hello **Get-AzureServiceAvailableExtension** cmdlet.
* Para instâncias de máquinas virtuais, você pode usar o hello **Get-AzureVMAvailableExtension** cmdlet.

### <a name="service-management-rest-apis"></a>APIs REST do Gerenciamento de Serviço
Quando você recupera uma lista de extensões disponíveis usando Olá APIs REST, você receberá informações sobre como a extensão de saudação é toobe configurado. informações de saudação que são retornadas podem mostrar informações de parâmetro representadas por um esquema público e um esquema privado. Valores de parâmetros públicos são retornados em consultas sobre as instâncias de saudação. Os valores dos parâmetros privados não são retornados.

Você pode usar o hello tooknow de APIs REST a seguir se uma extensão requer uma configuração de parâmetros públicos e privados:

* Para instâncias de funções web ou funções de trabalho, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de saudação na resposta de saudação do hello [lista As extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) operação.
* Para instâncias de máquinas virtuais, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de saudação na resposta de saudação do hello [lista Extensões de recurso](https://msdn.microsoft.com/library/dn495441.aspx) operação.

> [!NOTE]
> As extensões também podem usar as configurações que são definidas com JSON. Quando esses tipos de extensões são usados, somente Olá **SampleConfig** elemento é usado.
> 
> 

