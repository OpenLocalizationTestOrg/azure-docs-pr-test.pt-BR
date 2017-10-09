
Diagnosticar problemas com um serviço de nuvem do Microsoft Azure requer a coleta de arquivos de log do serviço de saudação em máquinas virtuais como Olá problemas ocorrem. Você pode usar a extensão de AzureLogCollector sob demanda de saudação tooperfom uma única coleção de logs de um ou mais VMs de serviço de nuvem (de funções web e funções de trabalho) e transferência Olá coletado arquivos tooan conta de armazenamento do Azure – tudo sem fazer logon remotamente em tooany de saudação VMs.

> [!NOTE]
> Descrições para a maioria das informações de saudação registrada podem ser encontradas em http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Há dois modos de coleção depende de tipos de saudação do toobe arquivos coletados.

* Somente Logs de GA (Agente Convidado) do Azure. Este modo de coleção inclui todos os agentes de convidados Olá logs tooAzure relacionados e outros componentes do Azure.
* Todos os Logs (Completo). Esse modo de coleta obterá todos os arquivos do modo GA e:
  
  * logs de eventos do sistema e do aplicativo
  * logs de erros de HTTP
  * Logs IIS
  * Logs de instalação
  * outros logs do sistema

Em ambos os modos de coleção, as pastas de coleção de dados adicionais podem ser especificadas usando uma coleção de saudação estrutura a seguir:

* **Nome**: nome de saudação da coleção de saudação, que será usada como nome de saudação da subpasta no toobe de arquivo zip Olá coletados.
* **Local**: Olá toohello pasta do caminho na máquina virtual de saudação onde os arquivos serão coletados.
* **SearchPattern**: padrão de saudação de nomes de saudação do toobe arquivos coletados. O padrão é “*”
* **Recursiva**: se arquivos hello serão coletado recursivamente sob a pasta de saudação.

## <a name="prerequisites"></a>Pré-requisitos
* Você precisa toohave uma conta de armazenamento para os arquivos zip com extensão toosave gerado.
* Verifique se você está usando os cmdlets do Azure PowerShell V0.8.0 ou superior. Para saber mais, confira [Downloads do Azure](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Adicionar extensão Olá
Você pode usar [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets ou [APIs de REST de gerenciamento de serviço](https://msdn.microsoft.com/library/ee460799.aspx) tooadd Olá extensão AzureLogCollector.

Para serviços de nuvem, Olá cmdlet do Powershell do Azure existente, **Set-AzureServiceExtension**, pode ser usado tooenable Olá extensão em instâncias de função serviço de nuvem. Toda vez que essa extensão é habilitada por este cmdlet, coleta de log é disparada nas instâncias de função hello selecionado de funções selecionadas.

Para máquinas virtuais, Olá cmdlet do Powershell do Azure existente, **Set-AzureVMExtension**, pode ser usado tooenable Olá extensão em máquinas virtuais. Toda vez que essa extensão é habilitada por meio de cmdlets hello, coleta de log é acionada em cada instância.

Internamente, essa extensão usa hello PublicConfiguration com base em JSON e PrivateConfiguration. seguir Olá é o layout de saudação de um exemplo de JSON para configuração pública e privada.

### <a name="publicconfiguration"></a>PublicConfiguration
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

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Esta extensão não precisa de **privateConfiguration**. Você pode apenas fornecer uma estrutura vazia para Olá **– PrivateConfiguration** argumento.
> 
> 

Você pode seguir uma saudação duas etapas tooadd Olá AzureLogCollector tooone ou mais instâncias de um serviço de nuvem ou máquina Virtual de funções selecionadas, os gatilhos Olá coleções em cada VM toorun e enviem arquivos de saudação coletado tooAzure conta a seguir especificado.

## <a name="adding-as-a-service-extension"></a>Adicionar como uma extensão de serviço
1. Execute a assinatura de tooyour Olá instruções tooconnect PowerShell do Azure.
2. Especifique o nome do serviço hello, slot, funções e toowhich de instâncias de função você deseja tooadd e habilitar a extensão de AzureLogCollector hello.
   
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
3. Especifique Olá pasta de dados adicionais para o qual os arquivos serão coletados (essa etapa é opcional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > Você pode usar o token `%roleroot%` unidade toospecify Olá função raiz desde que ele não use uma unidade fixa.
   > 
   > 
4. Forneça o nome de conta de armazenamento do Azure hello e arquivos de chave toowhich coletado serão carregados.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Chame hello SetAzureServiceLogCollector.ps1 (incluído no final de saudação do artigo Olá) como extensão de AzureLogCollector maneira tooenable Olá para um serviço de nuvem. Concluída a execução hello, você pode encontrar o arquivo de saudação carregado em`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

a seguir Olá é a definição de Olá Olá parâmetros passados toohello script. (Isso também foi copiado abaixo.)

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

* *ServiceName*: o nome do serviço de nuvem.
* *Roles*: uma lista de funções, como "FunçãoWeb1" ou "FunçãoDeTrabalho1".
* *Instâncias*: uma lista de nomes de saudação de instâncias de função separados por vírgula - usar cadeia de caracteres hello curinga ("*") para todas as instâncias de função.
* *Slot*: nome do slot. “Produção” ou “Preparo”.
* *Mode*: modo de coleta. "Completo" ou "GA".
* *StorageAccountName*: nome da conta de armazenamento do Azure para armazenar os dados coletados.
* *StorageAccountKey*: nome da chave de conta de armazenamento do Azure.
* *AdditionalDataLocationList*: uma lista de saudação estrutura a seguir:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Adicionar como uma extensão de VM
Execute a assinatura de tooyour Olá instruções tooconnect PowerShell do Azure.

1. Especifique o nome do serviço hello, a VM e o modo de coleta de saudação.
   
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
2. Forneça o nome de conta de armazenamento do Azure hello e arquivos de chave toowhich coletado serão carregados.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Chame hello os SetAzureVMLogCollector.ps1 (incluído no final de saudação do artigo Olá) como extensão de AzureLogCollector maneira tooenable Olá para um serviço de nuvem. Concluída a execução hello, você pode encontrar o arquivo de saudação carregado em https://YouareStorageAccountName.blob.core.windows.net/vmlogs

a seguir Olá é a definição de Olá Olá parâmetros passados toohello script. (Isso também foi copiado abaixo.)

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

* ServiceName: o nome do serviço de nuvem.
* Nome de saudação VMName da saudação VM.
* Mode: modo de coleta. "Completo" ou "GA".
* StorageAccountName: nome da conta de armazenamento do Azure para armazenar os dados coletados.
* StorageAccountKey: nome da chave de conta de armazenamento do Azure.
* AdditionalDataLocationList: Uma lista de saudação estrutura a seguir:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Arquivos de Script de Extensão do PowerShell
SetAzureServiceLogCollector.ps1

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


SetAzureVMLogCollector.ps1

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

## <a name="next-steps"></a>Próximas etapas
Agora você pode examinar ou copiar os logs de um local muito simples.

