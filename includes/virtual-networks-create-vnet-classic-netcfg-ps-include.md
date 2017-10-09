## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="b9df6-101">Como toocreate uma rede virtual usando uma configuração de rede do arquivo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9df6-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="b9df6-102">O Azure usa um toodefine do arquivo xml assinatura de tooa disponíveis todas as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="b9df6-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="b9df6-103">Baixar o arquivo, editá-lo toomodify ou excluir as redes virtuais existentes e criar novas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="b9df6-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="b9df6-104">Neste tutorial, você aprenderá como toodownload esse arquivo, chamado tooas arquivo de configuração (ou netcfg) de rede e editá-lo toocreate uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b9df6-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="b9df6-105">toolearn mais sobre o arquivo de configuração de rede hello, consulte Olá [esquema de configuração de rede virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9df6-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="b9df6-106">toocreate uma rede virtual com um arquivo netcfg usando o PowerShell, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9df6-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="b9df6-107">Se você nunca usou o Azure PowerShell, Olá concluir etapas no hello [como tooInstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) artigo, em seguida, entre no tooAzure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b9df6-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="b9df6-108">No console do Azure PowerShell hello, use Olá **AzureVnetConfig Get** cmdlet toodownload Olá rede arquivo tooa diretório de configuração no computador executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b9df6-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="b9df6-109">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b9df6-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="b9df6-110">Abrir o arquivo hello você salvou na etapa 2, usando qualquer aplicativo de editor XML ou texto e procure Olá  **<VirtualNetworkSites>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="b9df6-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="b9df6-111">Se já tiver redes criadas, cada rede será exibida como seu próprio elemento **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="b9df6-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="b9df6-112">rede virtual do hello toocreate descrita nesse cenário, adicionar Olá XML a seguir logo abaixo Olá  **<VirtualNetworkSites>**  elemento:</span><span class="sxs-lookup"><span data-stu-id="b9df6-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="b9df6-113">Salve o arquivo de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="b9df6-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="b9df6-114">No console do Azure PowerShell hello, use Olá **conjunto AzureVnetConfig** arquivo de configuração de rede do cmdlet tooupload Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9df6-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="b9df6-115">Saída retornada:</span><span class="sxs-lookup"><span data-stu-id="b9df6-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="b9df6-116">Se **OperationStatus** não é *êxito* em Olá retornado de saída, verifique o arquivo xml Olá erros e concluir a etapa 6 novamente.</span><span class="sxs-lookup"><span data-stu-id="b9df6-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="b9df6-117">No console do Azure PowerShell hello, use Olá **Get-AzureVnetSite** tooverify cmdlet que Olá nova rede foi adicionado executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9df6-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="b9df6-118">Olá retornado saída (abreviada) inclui Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9df6-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
