## <a name="how-to-create-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="c186f-101">Como criar uma rede virtual usando um arquivo de configuração de rede do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c186f-101">How to create a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="c186f-102">O Azure usa um arquivo xml para definir todas as redes virtuais disponíveis para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="c186f-102">Azure uses an xml file to define all virtual networks available to a subscription.</span></span> <span data-ttu-id="c186f-103">Você pode baixar o arquivo, editá-lo para modificar ou excluir as redes virtuais existentes e criar novas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="c186f-103">You can download this file, edit it to modify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="c186f-104">Neste tutorial, você aprenderá a baixar esse arquivo, conhecido como arquivo de configuração de rede (ou netcgf) e editá-lo para criar uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c186f-104">In this tutorial, you learn how to download this file, referred to as network configuration (or netcfg) file, and edit it to create a new virtual network.</span></span> <span data-ttu-id="c186f-105">Para saber mais sobre o arquivo de configuração de rede, veja o [esquema de configuração de rede virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="c186f-105">To learn more about the network configuration file, see the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="c186f-106">Para criar uma rede virtual com um arquivo netcfg usando o PowerShell, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c186f-106">To create a virtual network with a netcfg file using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="c186f-107">Caso você nunca tenha usado o Azure PowerShell, conclua as etapas do artigo [Como instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs), então entre no Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c186f-107">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in to Azure and select your subscription.</span></span>
2. <span data-ttu-id="c186f-108">No console do Azure PowerShell, use o cmdlet **Get-AzureVnetConfig** para baixar o arquivo de configuração de rede para um diretório em seu computador ao executar o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c186f-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file to a directory on your computer by running the following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="c186f-109">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="c186f-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="c186f-110">Abra o arquivo salvo na etapa 2 usando qualquer aplicativo de editor de texto ou XML e procure o elemento **<VirtualNetworkSites>** .</span><span class="sxs-lookup"><span data-stu-id="c186f-110">Open the file you saved in step 2 using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="c186f-111">Se já tiver redes criadas, cada rede será exibida como seu próprio elemento **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="c186f-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="c186f-112">Para criar a rede virtual descrita neste cenário, adicione o seguinte XML logo abaixo do elemento **<VirtualNetworkSites>** :</span><span class="sxs-lookup"><span data-stu-id="c186f-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="c186f-113">Salve o arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="c186f-113">Save the network configuration file.</span></span>
6. <span data-ttu-id="c186f-114">No console do Azure PowerShell, use o cmdlet **Set-AzureVnetConfig** para carregar o arquivo de configuração de rede executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c186f-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="c186f-115">Saída retornada:</span><span class="sxs-lookup"><span data-stu-id="c186f-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="c186f-116">Se **OperationStatus** não tiver *Êxito* na saída retornada, verifique novamente o arquivo xml em busca de erros e conclua a etapa 6 novamente.</span><span class="sxs-lookup"><span data-stu-id="c186f-116">If **OperationStatus** is not *Succeeded* in the returned output, check the xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="c186f-117">No console do Azure PowerShell, use o cmdlet **Get-AzureVnetSite** para verificar se a nova rede foi adicionada executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c186f-117">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="c186f-118">A saída (abreviada) retornada inclui o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c186f-118">The returned (abbreviated) output includes the following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
