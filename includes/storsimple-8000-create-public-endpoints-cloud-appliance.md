#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="a9904-101">pontos de extremidade públicos no dispositivo de nuvem Olá toocreate</span><span class="sxs-lookup"><span data-stu-id="a9904-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="a9904-102">Entrar toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9904-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="a9904-103">Vá muito**máquinas virtuais**, selecione e clique em máquina virtual Olá que está sendo usada como o dispositivo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9904-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="a9904-104">É necessário toocreate um fluxo de saudação rede segurança grupo (NSG) regra toocontrol de tráfego dentro e fora de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9904-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="a9904-105">Execute Olá seguindo as etapas toocreate uma regra NSG.</span><span class="sxs-lookup"><span data-stu-id="a9904-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="a9904-106">Selecione **Grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="a9904-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="a9904-107">Clique em saudação padrão grupo de segurança que é apresentado.</span><span class="sxs-lookup"><span data-stu-id="a9904-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="a9904-108">Selecione **Regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="a9904-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="a9904-109">Clique em **+ adicionar** toocreate uma regra de segurança de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9904-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="a9904-110">Na folha de regra de segurança de entrada do hello adicionar:</span><span class="sxs-lookup"><span data-stu-id="a9904-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="a9904-111">Para Olá **nome**, digite o seguinte Olá nome para o ponto de extremidade de saudação: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="a9904-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="a9904-112">Para Olá **prioridade**, selecione um número menor que 1000 (que é a prioridade de saudação de regra padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="a9904-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="a9904-113">Valor mais alto do hello, prioridade inferior a saudação.</span><span class="sxs-lookup"><span data-stu-id="a9904-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="a9904-114">Saudação de conjunto **fonte** muito**qualquer**.</span><span class="sxs-lookup"><span data-stu-id="a9904-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="a9904-115">Para Olá **Service**, selecione **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="a9904-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="a9904-116">Olá **protocolo** é definida automaticamente muito**TCP** e hello **intervalo de portas** está definido muito**5986**.</span><span class="sxs-lookup"><span data-stu-id="a9904-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="a9904-117">Clique em **Okey** toocreate regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9904-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="a9904-118">A etapa final é tooassociate ao grupo de segurança da sua rede com uma sub-rede ou uma interface de rede específico.</span><span class="sxs-lookup"><span data-stu-id="a9904-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="a9904-119">Execute Olá tooassociate as etapas a seguir em seu grupo de segurança de rede com uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a9904-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="a9904-120">Vá muito**sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="a9904-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="a9904-121">Clique em **+ Associar**.</span><span class="sxs-lookup"><span data-stu-id="a9904-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="a9904-122">Selecione a rede virtual e selecione sub-rede apropriada hello.</span><span class="sxs-lookup"><span data-stu-id="a9904-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="a9904-123">Clique em **Okey** toocreate regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9904-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="a9904-124">Depois Olá regra for criada, você pode exibir seu endereço de IP Virtual público (VIP) detalhes toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="a9904-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="a9904-125">Registre esse endereço.</span><span class="sxs-lookup"><span data-stu-id="a9904-125">Record this address.</span></span>


