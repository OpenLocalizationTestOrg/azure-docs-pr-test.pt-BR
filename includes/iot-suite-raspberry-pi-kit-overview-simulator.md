## <a name="overview"></a><span data-ttu-id="a325f-101">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a325f-101">Overview</span></span>

<span data-ttu-id="a325f-102">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a325f-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="a325f-103">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a325f-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="a325f-104">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="a325f-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="a325f-105">Configure toocommunicate seu dispositivo com o computador e a solução de monitoramento remoto hello.</span><span class="sxs-lookup"><span data-stu-id="a325f-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="a325f-106">Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria simulada que você pode exibir no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="a325f-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a325f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a325f-107">Prerequisites</span></span>

<span data-ttu-id="a325f-108">toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a325f-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a325f-109">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a325f-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a325f-110">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="a325f-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="a325f-111">Software necessário</span><span class="sxs-lookup"><span data-stu-id="a325f-111">Required software</span></span>

<span data-ttu-id="a325f-112">Você precisa cliente SSH no seu tooenable computador desktop você tooremotely acesso Olá linha de comando em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="a325f-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="a325f-113">O Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="a325f-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="a325f-114">Recomendamos o uso de [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="a325f-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="a325f-115">A maioria das distribuições do Linux e Mac OS incluem o utilitário SSH de linha de comando do hello.</span><span class="sxs-lookup"><span data-stu-id="a325f-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="a325f-116">Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="a325f-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="a325f-117">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="a325f-117">Required hardware</span></span>

<span data-ttu-id="a325f-118">Um computador desktop tooenable você tooconnect remotamente toohello linha de comando em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="a325f-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="a325f-119">[Microsoft IoT Starter Kit para Raspberry Pi 3][lnk-starter-kits] ou componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="a325f-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="a325f-120">Este tutorial usa Olá itens a seguir do kit de saudação:</span><span class="sxs-lookup"><span data-stu-id="a325f-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="a325f-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a325f-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="a325f-122">Cartão MicroSD (com NOOBS)</span><span class="sxs-lookup"><span data-stu-id="a325f-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="a325f-123">Um cabo USB Mini</span><span class="sxs-lookup"><span data-stu-id="a325f-123">A USB Mini cable</span></span>
- <span data-ttu-id="a325f-124">Um cabo Ethernet</span><span class="sxs-lookup"><span data-stu-id="a325f-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/