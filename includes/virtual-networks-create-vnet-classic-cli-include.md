## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="2c72f-101">Como toocreate uma VNet clássica usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2c72f-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="2c72f-102">Você pode usar o hello CLI do Azure toomanage seus recursos do Azure de saudação de prompt de comando de qualquer computador que executa o Windows, Linux ou OSX.</span><span class="sxs-lookup"><span data-stu-id="2c72f-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="2c72f-103">toocreate uma rede virtual usando Olá CLI do Azure, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="2c72f-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="2c72f-104">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../articles/cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="2c72f-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="2c72f-105">Executar Olá **criar redes de rede do azure** comando toocreate uma rede virtual e uma sub-rede, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2c72f-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="2c72f-106">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="2c72f-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="2c72f-107">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="2c72f-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="2c72f-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-108">**--vnet**.</span></span> <span data-ttu-id="2c72f-109">Nome da saudação VNet toobe criado.</span><span class="sxs-lookup"><span data-stu-id="2c72f-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="2c72f-110">Para o nosso cenário, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="2c72f-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="2c72f-111">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="2c72f-112">Espaço de endereço da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2c72f-112">VNet address space.</span></span> <span data-ttu-id="2c72f-113">Para o nosso cenário, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="2c72f-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="2c72f-114">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="2c72f-115">Máscara de rede no formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="2c72f-115">Network mask in CIDR format.</span></span> <span data-ttu-id="2c72f-116">Para o nosso cenário, *16*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="2c72f-117">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="2c72f-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="2c72f-118">Nome da sub-rede primeiro hello.</span><span class="sxs-lookup"><span data-stu-id="2c72f-118">Name of hello first subnet.</span></span> <span data-ttu-id="2c72f-119">Para o nosso cenário, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="2c72f-120">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="2c72f-121">Endereço IP inicial da sub-rede ou espaço de endereço da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2c72f-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="2c72f-122">Em nosso cenário, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="2c72f-123">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="2c72f-124">Máscara de rede no formato CIDR para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2c72f-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="2c72f-125">Para o nosso cenário, *24*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="2c72f-126">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-126">**-l (or --location)**.</span></span> <span data-ttu-id="2c72f-127">Região do Azure onde Olá rede virtual será criado.</span><span class="sxs-lookup"><span data-stu-id="2c72f-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="2c72f-128">Para o nosso cenário, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="2c72f-129">Executar Olá **sub-rede da rede virtual de rede do azure criar** comando toocreate uma sub-rede, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2c72f-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="2c72f-130">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="2c72f-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="2c72f-131">Aqui está a saída Olá esperado para o comando de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="2c72f-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="2c72f-132">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="2c72f-133">Nome da saudação redes onde sub-rede Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="2c72f-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="2c72f-134">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="2c72f-135">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-135">**-n (or --name)**.</span></span> <span data-ttu-id="2c72f-136">Nome da nova subrede hello.</span><span class="sxs-lookup"><span data-stu-id="2c72f-136">Name of hello new subnet.</span></span> <span data-ttu-id="2c72f-137">Para o nosso cenário, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="2c72f-138">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="2c72f-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="2c72f-139">Bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2c72f-139">Subnet CIDR block.</span></span> <span data-ttu-id="2c72f-140">Para o nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="2c72f-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="2c72f-141">Executar Olá **Mostrar de rede virtual de rede do azure** comando tooview propriedades Olá Olá nova rede virtual, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2c72f-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="2c72f-142">Aqui está a saída Olá esperado para o comando de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="2c72f-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
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

