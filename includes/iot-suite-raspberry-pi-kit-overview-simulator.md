## <a name="overview"></a><span data-ttu-id="16183-101">Visão geral</span><span class="sxs-lookup"><span data-stu-id="16183-101">Overview</span></span>

<span data-ttu-id="16183-102">Neste tutorial, você completa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="16183-102">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="16183-103">Implantar uma instância da solução pré-configurada de monitoramento remoto em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="16183-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="16183-104">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="16183-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="16183-105">Configurar seu dispositivo para comunicação com seu computador e com a solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="16183-105">Set up your device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="16183-106">Atualizar o exemplo de código de dispositivo para conectar-se à solução de monitoramento remoto e enviar telemetria simulada, que pode ser exibida no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="16183-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16183-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="16183-107">Prerequisites</span></span>

<span data-ttu-id="16183-108">Para concluir este tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="16183-108">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="16183-109">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="16183-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="16183-110">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="16183-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="16183-111">Software necessário</span><span class="sxs-lookup"><span data-stu-id="16183-111">Required software</span></span>

<span data-ttu-id="16183-112">É necessário um cliente SSH em seu computador desktop para que você possa acessar remotamente a linha de comando no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="16183-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="16183-113">O Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="16183-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="16183-114">Recomendamos o uso de [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="16183-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="16183-115">A maioria das distribuições do Linux e Mac OS incluem o utilitário de linha de comando do SSH.</span><span class="sxs-lookup"><span data-stu-id="16183-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="16183-116">Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="16183-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="16183-117">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="16183-117">Required hardware</span></span>

<span data-ttu-id="16183-118">Um computador desktop para que você possa se conectar remotamente à linha de comando no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="16183-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="16183-119">[Microsoft IoT Starter Kit para Raspberry Pi 3][lnk-starter-kits] ou componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="16183-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="16183-120">Este tutorial usa os seguintes itens do kit:</span><span class="sxs-lookup"><span data-stu-id="16183-120">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="16183-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="16183-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="16183-122">Cartão MicroSD (com NOOBS)</span><span class="sxs-lookup"><span data-stu-id="16183-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="16183-123">Um cabo USB Mini</span><span class="sxs-lookup"><span data-stu-id="16183-123">A USB Mini cable</span></span>
- <span data-ttu-id="16183-124">Um cabo Ethernet</span><span class="sxs-lookup"><span data-stu-id="16183-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/