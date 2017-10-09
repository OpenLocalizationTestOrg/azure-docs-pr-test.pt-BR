## <a name="prerequisites"></a><span data-ttu-id="e72e9-101">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e72e9-101">Prerequisites</span></span>

<span data-ttu-id="e72e9-102">toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e72e9-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e72e9-103">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e72e9-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e72e9-104">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="e72e9-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="e72e9-105">Software necessário</span><span class="sxs-lookup"><span data-stu-id="e72e9-105">Required software</span></span>

<span data-ttu-id="e72e9-106">Você precisa cliente SSH no seu tooenable computador desktop você tooremotely acesso Olá linha de comando em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="e72e9-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="e72e9-107">O Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="e72e9-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="e72e9-108">Recomendamos o uso de [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="e72e9-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="e72e9-109">A maioria das distribuições do Linux e Mac OS incluem o utilitário SSH de linha de comando do hello.</span><span class="sxs-lookup"><span data-stu-id="e72e9-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="e72e9-110">Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="e72e9-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="e72e9-111">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="e72e9-111">Required hardware</span></span>

<span data-ttu-id="e72e9-112">Um computador desktop tooenable você tooconnect remotamente toohello linha de comando em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="e72e9-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="e72e9-113">[Microsoft IoT Starter Kit para Raspberry Pi 3][lnk-starter-kits] ou componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="e72e9-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="e72e9-114">Este tutorial usa Olá itens a seguir do kit de saudação:</span><span class="sxs-lookup"><span data-stu-id="e72e9-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="e72e9-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="e72e9-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="e72e9-116">Cartão MicroSD (com NOOBS)</span><span class="sxs-lookup"><span data-stu-id="e72e9-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="e72e9-117">Um cabo USB Mini</span><span class="sxs-lookup"><span data-stu-id="e72e9-117">A USB Mini cable</span></span>
- <span data-ttu-id="e72e9-118">Um cabo Ethernet</span><span class="sxs-lookup"><span data-stu-id="e72e9-118">An Ethernet cable</span></span>
- <span data-ttu-id="e72e9-119">Sensor BME280</span><span class="sxs-lookup"><span data-stu-id="e72e9-119">BME280 sensor</span></span>
- <span data-ttu-id="e72e9-120">Placa universal</span><span class="sxs-lookup"><span data-stu-id="e72e9-120">Breadboard</span></span>
- <span data-ttu-id="e72e9-121">Cabos de jumper</span><span class="sxs-lookup"><span data-stu-id="e72e9-121">Jumper wires</span></span>
- <span data-ttu-id="e72e9-122">Resistores</span><span class="sxs-lookup"><span data-stu-id="e72e9-122">Resistors</span></span>
- <span data-ttu-id="e72e9-123">LEDs</span><span class="sxs-lookup"><span data-stu-id="e72e9-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/