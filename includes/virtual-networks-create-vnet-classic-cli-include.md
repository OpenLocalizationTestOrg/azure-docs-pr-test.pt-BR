## <a name="how-to-create-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="a8655-101">Como criar uma rede virtual clássica usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a8655-101">How to create a classic VNet using Azure CLI</span></span>
<span data-ttu-id="a8655-102">Você pode usar a CLI do Azure para gerenciar os recursos do Azure no prompt de comando de qualquer computador com Windows, Linux ou OSX.</span><span class="sxs-lookup"><span data-stu-id="a8655-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="a8655-103">Para criar uma rede virtual usando a CLI do Azure, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="a8655-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="a8655-104">Se você nunca usou a CLI do Azure, consulte [Instalar e configurar a CLI do Azure](../articles/cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8655-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a8655-105">Execute o comando **azure network vnet create** para criar uma rede virtual e uma sub-rede, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a8655-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="a8655-106">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="a8655-106">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="a8655-107">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="a8655-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="a8655-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="a8655-108">**--vnet**.</span></span> <span data-ttu-id="a8655-109">Nome da rede virtual a ser criada.</span><span class="sxs-lookup"><span data-stu-id="a8655-109">Name of the VNet to be created.</span></span> <span data-ttu-id="a8655-110">Para o nosso cenário, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="a8655-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="a8655-111">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="a8655-112">Espaço de endereço da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a8655-112">VNet address space.</span></span> <span data-ttu-id="a8655-113">Para o nosso cenário, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="a8655-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="a8655-114">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="a8655-115">Máscara de rede no formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="a8655-115">Network mask in CIDR format.</span></span> <span data-ttu-id="a8655-116">Para o nosso cenário, *16*.</span><span class="sxs-lookup"><span data-stu-id="a8655-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="a8655-117">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="a8655-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="a8655-118">Nome da primeira sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a8655-118">Name of the first subnet.</span></span> <span data-ttu-id="a8655-119">Para o nosso cenário, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a8655-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="a8655-120">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="a8655-121">Endereço IP inicial da sub-rede ou espaço de endereço da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a8655-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="a8655-122">Em nosso cenário, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="a8655-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="a8655-123">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="a8655-124">Máscara de rede no formato CIDR para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a8655-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="a8655-125">Para o nosso cenário, *24*.</span><span class="sxs-lookup"><span data-stu-id="a8655-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="a8655-126">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-126">**-l (or --location)**.</span></span> <span data-ttu-id="a8655-127">Região do Azure em que a rede virtual será criada.</span><span class="sxs-lookup"><span data-stu-id="a8655-127">Azure region where the VNet will be created.</span></span> <span data-ttu-id="a8655-128">Para o nosso cenário, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="a8655-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="a8655-129">Execute o comando **azure network vnet subnet create** para criar uma sub-rede, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a8655-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="a8655-130">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="a8655-130">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="a8655-131">Este é o resultado esperado para o comando descrito acima:</span><span class="sxs-lookup"><span data-stu-id="a8655-131">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="a8655-132">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="a8655-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="a8655-133">Nome da rede virtual onde a sub-rede será criada.</span><span class="sxs-lookup"><span data-stu-id="a8655-133">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="a8655-134">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="a8655-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="a8655-135">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-135">**-n (or --name)**.</span></span> <span data-ttu-id="a8655-136">Nome da nova sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a8655-136">Name of the new subnet.</span></span> <span data-ttu-id="a8655-137">Para o nosso cenário, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="a8655-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="a8655-138">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="a8655-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="a8655-139">Bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a8655-139">Subnet CIDR block.</span></span> <span data-ttu-id="a8655-140">Para o nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a8655-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="a8655-141">Execute o comando **azure network vnet show** para exibir as propriedades da nova rede virtual, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a8655-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="a8655-142">Este é o resultado esperado para o comando descrito acima:</span><span class="sxs-lookup"><span data-stu-id="a8655-142">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

