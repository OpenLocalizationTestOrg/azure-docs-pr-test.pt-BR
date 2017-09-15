## <a name="prerequisites"></a><span data-ttu-id="56d9e-101">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56d9e-101">Prerequisites</span></span>

<span data-ttu-id="56d9e-102">Para concluir este tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="56d9e-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="56d9e-103">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="56d9e-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="56d9e-104">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="56d9e-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="56d9e-105">Software necessário</span><span class="sxs-lookup"><span data-stu-id="56d9e-105">Required software</span></span>

<span data-ttu-id="56d9e-106">É necessário um cliente SSH em seu computador desktop para que você possa acessar remotamente a linha de comando no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="56d9e-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="56d9e-107">O Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="56d9e-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="56d9e-108">Recomendamos o uso de [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="56d9e-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="56d9e-109">A maioria das distribuições do Linux e Mac OS incluem o utilitário de linha de comando do SSH.</span><span class="sxs-lookup"><span data-stu-id="56d9e-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="56d9e-110">Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="56d9e-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="56d9e-111">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="56d9e-111">Required hardware</span></span>

<span data-ttu-id="56d9e-112">Um computador desktop para que você possa se conectar remotamente à linha de comando no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="56d9e-112">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="56d9e-113">[Microsoft IoT Starter Kit para Raspberry Pi 3][lnk-starter-kits] ou componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="56d9e-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="56d9e-114">Este tutorial usa os seguintes itens do kit:</span><span class="sxs-lookup"><span data-stu-id="56d9e-114">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="56d9e-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="56d9e-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="56d9e-116">Cartão MicroSD (com NOOBS)</span><span class="sxs-lookup"><span data-stu-id="56d9e-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="56d9e-117">Um cabo USB Mini</span><span class="sxs-lookup"><span data-stu-id="56d9e-117">A USB Mini cable</span></span>
- <span data-ttu-id="56d9e-118">Um cabo Ethernet</span><span class="sxs-lookup"><span data-stu-id="56d9e-118">An Ethernet cable</span></span>
- <span data-ttu-id="56d9e-119">Sensor BME280</span><span class="sxs-lookup"><span data-stu-id="56d9e-119">BME280 sensor</span></span>
- <span data-ttu-id="56d9e-120">Placa universal</span><span class="sxs-lookup"><span data-stu-id="56d9e-120">Breadboard</span></span>
- <span data-ttu-id="56d9e-121">Cabos de jumper</span><span class="sxs-lookup"><span data-stu-id="56d9e-121">Jumper wires</span></span>
- <span data-ttu-id="56d9e-122">Resistores</span><span class="sxs-lookup"><span data-stu-id="56d9e-122">Resistors</span></span>
- <span data-ttu-id="56d9e-123">LEDs</span><span class="sxs-lookup"><span data-stu-id="56d9e-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/