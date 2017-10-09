<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a><span data-ttu-id="027f4-101">toocable de alimentação do seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="027f4-101">toocable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="027f4-102">Ambos os compartimentos no seu dispositivo StorSimple incluem PCMs redundantes.</span><span class="sxs-lookup"><span data-stu-id="027f4-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="027f4-103">Para cada compartimento, Olá PCMs deve ser instalado e conectado toodifferent power fontes tooensure alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="027f4-103">For each enclosure, hello PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="027f4-104">Verifique se Olá interruptores em todos os PCMs de saudação estão na posição do hello OFF.</span><span class="sxs-lookup"><span data-stu-id="027f4-104">Make sure that hello power switches on all hello PCMs are in hello OFF position.</span></span>
2. <span data-ttu-id="027f4-105">No compartimento principal do hello, conecte-se tooboth cabos de alimentação Olá PCMs.</span><span class="sxs-lookup"><span data-stu-id="027f4-105">On hello primary enclosure, connect hello power cords tooboth PCMs.</span></span> <span data-ttu-id="027f4-106">Olá cabos de alimentação são identificados em vermelho na alimentação Olá cabeamento diagrama abaixo.</span><span class="sxs-lookup"><span data-stu-id="027f4-106">hello power cords are identified in red in hello power cabling diagram, below.</span></span>
3. <span data-ttu-id="027f4-107">Certifique-se de que Olá dois PCMs no hello compartimento principal usam separado fontes de alimentação.</span><span class="sxs-lookup"><span data-stu-id="027f4-107">Make sure that hello two PCMs on hello primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="027f4-108">Anexe Olá power cabos toohello power em unidades de distribuição do rack Olá conforme mostrado no diagrama de cabeamento de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="027f4-108">Attach hello power cords toohello power on hello rack distribution units as shown in hello power cabling diagram.</span></span>
5. <span data-ttu-id="027f4-109">Repita as etapas 2 a 4 para Olá compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="027f4-109">Repeat steps 2 through 4 for hello EBOD enclosure.</span></span>
6. <span data-ttu-id="027f4-110">Ative o compartimento do EBOD Olá colocando o interruptor de energia Olá em cada toohello na posição ligado PCM.</span><span class="sxs-lookup"><span data-stu-id="027f4-110">Turn on hello EBOD enclosure by flipping hello power switch on each PCM toohello ON position.</span></span>
7. <span data-ttu-id="027f4-111">Verifique se que Olá compartimento EBOD está ligado observando que LEDs Olá verde Olá parte posterior do controlador do EBOD Olá estão ligados.</span><span class="sxs-lookup"><span data-stu-id="027f4-111">Verify that hello EBOD enclosure is turned on by checking that hello green LEDs on hello back of hello EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="027f4-112">Ative o compartimento principal Olá colocando cada comutador toohello na posição ligado PCM.</span><span class="sxs-lookup"><span data-stu-id="027f4-112">Turn on hello primary enclosure by flipping each PCM switch toohello ON position.</span></span>
9. <span data-ttu-id="027f4-113">Verifique se sistema Olá em assegurando o controlador do dispositivo Olá que LEDs tem ativado.</span><span class="sxs-lookup"><span data-stu-id="027f4-113">Verify that hello system is on by ensuring hello device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="027f4-114">Certifique-se de que conexão Olá entre o controlador do EBOD hello e controlador do dispositivo Olá está ativa verificando que Olá quatro LEDs próxima toohello porta SAS no controlador do EBOD Olá estão verdes.</span><span class="sxs-lookup"><span data-stu-id="027f4-114">Make sure that hello connection between hello EBOD controller and hello device controller is active by verifying that hello four LEDs next toohello SAS port on hello EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="027f4-115">tooensure alta disponibilidade para seu sistema, recomendamos que siga estritamente toohello mostrado no diagrama a seguir de saudação do esquema de cabeamento de alimentação.</span><span class="sxs-lookup"><span data-stu-id="027f4-115">tooensure high availability for your system, we recommend that you strictly adhere toohello power cabling scheme shown in hello following diagram.</span></span>
    > 
    > 
    
    ![Cabeamento do dispositivo 4U para alimentação](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="027f4-117">**Cabeamento de energia**</span><span class="sxs-lookup"><span data-stu-id="027f4-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="027f4-118">Rótulo</span><span class="sxs-lookup"><span data-stu-id="027f4-118">Label</span></span> | <span data-ttu-id="027f4-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="027f4-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="027f4-120">1</span><span class="sxs-lookup"><span data-stu-id="027f4-120">1</span></span> |<span data-ttu-id="027f4-121">Compartimento principal</span><span class="sxs-lookup"><span data-stu-id="027f4-121">Primary enclosure</span></span> |
    | <span data-ttu-id="027f4-122">2</span><span class="sxs-lookup"><span data-stu-id="027f4-122">2</span></span> |<span data-ttu-id="027f4-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="027f4-123">PCM 0</span></span> |
    | <span data-ttu-id="027f4-124">3</span><span class="sxs-lookup"><span data-stu-id="027f4-124">3</span></span> |<span data-ttu-id="027f4-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="027f4-125">PCM 1</span></span> |
    | <span data-ttu-id="027f4-126">4</span><span class="sxs-lookup"><span data-stu-id="027f4-126">4</span></span> |<span data-ttu-id="027f4-127">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="027f4-127">Controller 0</span></span> |
    | <span data-ttu-id="027f4-128">5</span><span class="sxs-lookup"><span data-stu-id="027f4-128">5</span></span> |<span data-ttu-id="027f4-129">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="027f4-129">Controller 1</span></span> |
    | <span data-ttu-id="027f4-130">6</span><span class="sxs-lookup"><span data-stu-id="027f4-130">6</span></span> |<span data-ttu-id="027f4-131">Controlador 0 do EBOD</span><span class="sxs-lookup"><span data-stu-id="027f4-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="027f4-132">7</span><span class="sxs-lookup"><span data-stu-id="027f4-132">7</span></span> |<span data-ttu-id="027f4-133">Controlador 1 do EBOD</span><span class="sxs-lookup"><span data-stu-id="027f4-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="027f4-134">8</span><span class="sxs-lookup"><span data-stu-id="027f4-134">8</span></span> |<span data-ttu-id="027f4-135">Compartimento EBOD</span><span class="sxs-lookup"><span data-stu-id="027f4-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="027f4-136">9</span><span class="sxs-lookup"><span data-stu-id="027f4-136">9</span></span> |<span data-ttu-id="027f4-137">PDUs</span><span class="sxs-lookup"><span data-stu-id="027f4-137">PDUs</span></span> |

