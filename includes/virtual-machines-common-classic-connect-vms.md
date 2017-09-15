

![Máquinas virtuais em um serviço de nuvem autônomo](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="b55dd-102">Ao colocar as máquinas virtuais em uma rede virtual, você pode decidir quantos serviços de nuvem deseja usar para os conjuntos de disponibilidade e o balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b55dd-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want to use for load balancing and availability sets.</span></span> <span data-ttu-id="b55dd-103">Além disso, você pode organizar as máquinas virtuais em sub-redes da mesma forma como sua rede local e conectar a rede virtual à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="b55dd-103">Additionally, you can organize the virtual machines on subnets in the same way as your on-premises network and connect the virtual network to your on-premises network.</span></span> <span data-ttu-id="b55dd-104">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="b55dd-104">Here's an example:</span></span>

![Máquinas virtuais em uma rede virtual](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="b55dd-106">As redes virtuais são a maneira recomendada para conectar máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="b55dd-106">Virtual networks are the recommended way to connect virtual machines in Azure.</span></span> <span data-ttu-id="b55dd-107">A prática recomendada é configurar cada camada do aplicativo em um serviço de nuvem separado.</span><span class="sxs-lookup"><span data-stu-id="b55dd-107">The best practice is to configure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="b55dd-108">No entanto, talvez seja necessário combinar algumas máquinas virtuais de diferentes níveis de aplicativos no mesmo serviço de nuvem para permanecer dentro do máximo de 200 serviços de nuvem por assinatura.</span><span class="sxs-lookup"><span data-stu-id="b55dd-108">However, you may need to combine some virtual machines from different application tiers into the same cloud service to remain within the maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="b55dd-109">Para verificar isso e outros limites, consulte [Assinatura do Azure e limites de serviços, cotas e restrições](../articles/azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b55dd-109">To review this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="b55dd-110">Conectar VMs em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="b55dd-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="b55dd-111">Para conectar máquinas virtuais em uma rede virtual:</span><span class="sxs-lookup"><span data-stu-id="b55dd-111">To connect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="b55dd-112">Crie a rede virtual no [portal do Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) e especifique 'implantação clássica'.</span><span class="sxs-lookup"><span data-stu-id="b55dd-112">Create the virtual network in the [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="b55dd-113">Crie o conjunto de serviços de nuvem para sua implantação de modo a refletir seu design para conjuntos de disponibilidade e balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b55dd-113">Create the set of cloud services for your deployment to reflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="b55dd-114">No portal do Azure, clique em **Novo > Computação > Serviço de nuvem** para cada serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b55dd-114">In the Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="b55dd-115">Enquanto você preenche os detalhes do serviço de nuvem, escolha o mesmo _grupo de recursos_ usado com o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b55dd-115">As you fill out the cloud service details, choose the same _resource group_ used with the virtual network.</span></span>

3. <span data-ttu-id="b55dd-116">Para criar cada nova máquina virtual, clique em **Novo > Computação** e então selecione a imagem de VM apropriada dos **Aplicativos em destaque**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-116">To create each new virtual machine, click **New > Compute**, then select the appropriate VM image from the **Featured apps**.</span></span>

  <span data-ttu-id="b55dd-117">Na folha **Noções básicas** da VM, escolha o mesmo _grupo de recursos_ usado com a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b55dd-117">In the VM **Basics** blade, choose the same _resource group_ used with the virtual network.</span></span>

  ![Folha Noções básicas da VM ao usar uma rede virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="b55dd-119">Enquanto você preenche as **Configurações** da VM, escolha o _Serviço de nuvem_ ou a _rede virtual_ correta para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b55dd-119">As you fill out the VM **Settings**, choose the correct _Cloud service_ or _virtual network_ for the VM.</span></span>

  <span data-ttu-id="b55dd-120">O Azure selecionará o outro item com base em sua seleção.</span><span class="sxs-lookup"><span data-stu-id="b55dd-120">Azure will select the other item based on your selection.</span></span>

  ![Folha Configurações da VM ao usar uma rede virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="b55dd-122">Conectar VMs em um serviço de nuvem autônomo</span><span class="sxs-lookup"><span data-stu-id="b55dd-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="b55dd-123">Para conectar máquinas virtuais em um serviço de nuvem autônomo:</span><span class="sxs-lookup"><span data-stu-id="b55dd-123">To connect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="b55dd-124">Crie o serviço de nuvem no [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b55dd-124">Create the cloud service in the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="b55dd-125">Clique em **Novo > Computação > Serviço de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="b55dd-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="b55dd-126">Ou você pode criar o serviço de nuvem para sua implantação ao criar sua primeira máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b55dd-126">Or, you can create the cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="b55dd-127">Quando você criar as máquinas virtuais, escolha o mesmo grupo de recursos usado com o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b55dd-127">When you create the virtual machines, choose the same resource group used with the cloud service.</span></span>

  ![Adicionar uma máquina virtual a um serviço de nuvem existente](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="b55dd-129">Enquanto preenche os detalhes da VM, escolha o nome do serviço de nuvem criado na primeira etapa.</span><span class="sxs-lookup"><span data-stu-id="b55dd-129">As you fill out the VM details, choose the name of cloud service created in the first step.</span></span>

  ![Selecionar um serviço de nuvem para uma máquina virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
