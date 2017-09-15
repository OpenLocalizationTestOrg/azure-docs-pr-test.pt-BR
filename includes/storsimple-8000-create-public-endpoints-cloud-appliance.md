#### <a name="to-create-public-endpoints-on-the-cloud-appliance"></a><span data-ttu-id="9832b-101">Para criar pontos de extremidade públicos no dispositivo de nuvem</span><span class="sxs-lookup"><span data-stu-id="9832b-101">To create public endpoints on the cloud appliance</span></span>

1. <span data-ttu-id="9832b-102">Entre no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9832b-102">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="9832b-103">Acesse **Máquinas Virtuais** e selecione a máquina virtual que está sendo usada como seu dispositivo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9832b-103">Go to **Virtual Machines**, and then select and click the virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="9832b-104">Você precisa criar uma regra de NSG (grupo de segurança de rede) para controlar o fluxo de entrada e saída de tráfego de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9832b-104">You need to create a network security group (NSG) rule to control the flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="9832b-105">Execute as etapas a seguir para criar uma regra de NSG.</span><span class="sxs-lookup"><span data-stu-id="9832b-105">Perform the following steps to create an NSG rule.</span></span>
    1. <span data-ttu-id="9832b-106">Selecione **Grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="9832b-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="9832b-107">Clique no grupo de segurança de rede padrão apresentado.</span><span class="sxs-lookup"><span data-stu-id="9832b-107">Click the default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="9832b-108">Selecione **Regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="9832b-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="9832b-109">Clique em **+ Adicionar** para criar uma regra de segurança de entrada.</span><span class="sxs-lookup"><span data-stu-id="9832b-109">Click **+ Add** to create an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="9832b-110">Na folha Adicionar regra de segurança de entrada:</span><span class="sxs-lookup"><span data-stu-id="9832b-110">In the Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="9832b-111">Para o **Nome**, digite o seguinte nome para o ponto de extremidade: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="9832b-111">For the **Name**, type the following name for the endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="9832b-112">Para a **Prioridade**, selecione um número menor do que 1000 (que é a prioridade para a regra padrão).</span><span class="sxs-lookup"><span data-stu-id="9832b-112">For the **Priority**, select a number lesser than 1000 (which is the priority for the default rule).</span></span> <span data-ttu-id="9832b-113">Quanto maior o valor, menor a prioridade.</span><span class="sxs-lookup"><span data-stu-id="9832b-113">Higher the value, lower the priority.</span></span>

        3. <span data-ttu-id="9832b-114">Defina **Fonte** como **Qualquer**.</span><span class="sxs-lookup"><span data-stu-id="9832b-114">Set the **Source** to **Any**.</span></span>

        4. <span data-ttu-id="9832b-115">Para **Serviço**, selecione **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="9832b-115">For the **Service**, select **WinRM**.</span></span> <span data-ttu-id="9832b-116">O **Protocolo** é definido automaticamente como **TCP**, e **Intervalo de portas** é definido como **5986**.</span><span class="sxs-lookup"><span data-stu-id="9832b-116">The **Protocol** is automatically set to **TCP** and the **Port range** is set to **5986**.</span></span>

        5. <span data-ttu-id="9832b-117">Clique em **OK** para criar a regra.</span><span class="sxs-lookup"><span data-stu-id="9832b-117">Click **OK** to create the rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="9832b-118">A etapa final é associar o grupo de segurança de rede com uma sub-rede ou uma interface de rede específica.</span><span class="sxs-lookup"><span data-stu-id="9832b-118">Your final step is to associate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="9832b-119">Execute as seguintes etapas para associar o grupo de segurança de rede a uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9832b-119">Perform the following steps to associate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="9832b-120">Acesse **Sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="9832b-120">Go to **Subnets**.</span></span>
    2. <span data-ttu-id="9832b-121">Clique em **+ Associar**.</span><span class="sxs-lookup"><span data-stu-id="9832b-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="9832b-122">Selecione sua rede virtual e selecione a sub-rede apropriada.</span><span class="sxs-lookup"><span data-stu-id="9832b-122">Select your virtual network, and then select the appropriate subnet.</span></span>
    4. <span data-ttu-id="9832b-123">Clique em **OK** para criar a regra.</span><span class="sxs-lookup"><span data-stu-id="9832b-123">Click **OK** to create the rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="9832b-124">Após a criação da regra, você poderá exibir seus detalhes para determinar o endereço VIP (IP Virtual Público).</span><span class="sxs-lookup"><span data-stu-id="9832b-124">After the rule is created, you can view its details to determine the Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="9832b-125">Registre esse endereço.</span><span class="sxs-lookup"><span data-stu-id="9832b-125">Record this address.</span></span>


