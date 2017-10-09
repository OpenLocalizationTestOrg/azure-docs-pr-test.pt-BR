## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Como toocreate uma rede virtual usando uma configuração de rede do arquivo do PowerShell
O Azure usa um toodefine do arquivo xml assinatura de tooa disponíveis todas as redes virtuais. Baixar o arquivo, editá-lo toomodify ou excluir as redes virtuais existentes e criar novas redes virtuais. Neste tutorial, você aprenderá como toodownload esse arquivo, chamado tooas arquivo de configuração (ou netcfg) de rede e editá-lo toocreate uma nova rede virtual. toolearn mais sobre o arquivo de configuração de rede hello, consulte Olá [esquema de configuração de rede virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate uma rede virtual com um arquivo netcfg usando o PowerShell, Olá concluir as etapas a seguir:

1. Se você nunca usou o Azure PowerShell, Olá concluir etapas no hello [como tooInstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) artigo, em seguida, entre no tooAzure e selecione sua assinatura.
2. No console do Azure PowerShell hello, use Olá **AzureVnetConfig Get** cmdlet toodownload Olá rede arquivo tooa diretório de configuração no computador executando o comando a seguir de saudação: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Saída esperada:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Abrir o arquivo hello você salvou na etapa 2, usando qualquer aplicativo de editor XML ou texto e procure Olá  **<VirtualNetworkSites>**  elemento. Se já tiver redes criadas, cada rede será exibida como seu próprio elemento **<VirtualNetworkSite>**.
4. rede virtual do hello toocreate descrita nesse cenário, adicionar Olá XML a seguir logo abaixo Olá  **<VirtualNetworkSites>**  elemento:

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. Salve o arquivo de configuração de rede hello.
6. No console do Azure PowerShell hello, use Olá **conjunto AzureVnetConfig** arquivo de configuração de rede do cmdlet tooupload Olá executando Olá comando a seguir: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Saída retornada:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Se **OperationStatus** não é *êxito* em Olá retornado de saída, verifique o arquivo xml Olá erros e concluir a etapa 6 novamente.

7. No console do Azure PowerShell hello, use Olá **Get-AzureVnetSite** tooverify cmdlet que Olá nova rede foi adicionado executando Olá comando a seguir: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Olá retornado saída (abreviada) inclui Olá texto a seguir:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
