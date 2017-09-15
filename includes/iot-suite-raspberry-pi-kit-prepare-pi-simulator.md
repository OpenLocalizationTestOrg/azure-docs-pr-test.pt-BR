## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="0188b-101">Preparar seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="0188b-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="0188b-102">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="0188b-102">Install Raspbian</span></span>

<span data-ttu-id="0188b-103">Se esta for a primeira vez que você estiver usando o Raspberry Pi, você precisa instalar o sistema operacional do Raspbian usando NOOBS no cartão SD incluído no kit.</span><span class="sxs-lookup"><span data-stu-id="0188b-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="0188b-104">O [Guia de Software do Raspberry Pi Software guia][lnk-install-raspbian] descreve como instalar um sistema operacional em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0188b-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="0188b-105">Este tutorial presume que você instalou o sistema operacional Raspbian em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0188b-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="0188b-106">O cartão SD incluído no [Microsoft Azure IoT Starter Kit do Raspberry Pi 3][lnk-starter-kits] já tem NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="0188b-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="0188b-107">Você pode inicializar o Raspberry Pi neste cartão e optar por instalar o sistema operacional do Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0188b-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

<span data-ttu-id="0188b-108">Para concluir a configuração de hardware, você precisa:</span><span class="sxs-lookup"><span data-stu-id="0188b-108">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="0188b-109">Conectar seu Raspberry Pi à fonte de alimentação incluída no kit.</span><span class="sxs-lookup"><span data-stu-id="0188b-109">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="0188b-110">Conectar seu Raspberry Pi à sua rede usando o cabo Ethernet incluído em seu kit.</span><span class="sxs-lookup"><span data-stu-id="0188b-110">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="0188b-111">Como alternativa, você pode configurar [Conectividade sem fio][lnk-pi-wireless] para o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0188b-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="0188b-112">Agora você concluiu a configuração de hardware do seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0188b-112">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="0188b-113">Entre e acesse o terminal</span><span class="sxs-lookup"><span data-stu-id="0188b-113">Sign in and access the terminal</span></span>

<span data-ttu-id="0188b-114">Você tem duas opções para acessar um ambiente de terminal no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0188b-114">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="0188b-115">Se você tiver um teclado e um monitor conectado ao seu Raspberry Pi, você pode usar a GUI do Raspbian para acessar uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="0188b-115">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="0188b-116">Acesse a linha de comando em seu Raspberry Pi usando o SSH em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="0188b-116">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="0188b-117">Use uma janela de terminal na GUI</span><span class="sxs-lookup"><span data-stu-id="0188b-117">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="0188b-118">As credenciais padrões para Raspbian são o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="0188b-118">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="0188b-119">Na barra de tarefas na GUI, você pode iniciar o utilitário **Terminal** usando o ícone que se parece com um monitor.</span><span class="sxs-lookup"><span data-stu-id="0188b-119">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="0188b-120">Entre com o SSH</span><span class="sxs-lookup"><span data-stu-id="0188b-120">Sign in with SSH</span></span>

<span data-ttu-id="0188b-121">Você pode usar o SSH para acesso de linha de comando para o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0188b-121">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="0188b-122">O artigo [SSH (Secure Shell)][lnk-pi-ssh] descreve como configurar SSH em seu Raspberry Pi e como conectar-se a partir do [Windows][lnk-ssh-windows] ou [Linux e Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="0188b-122">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="0188b-123">Entre com o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="0188b-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="0188b-124">Opcional: Compartilhar uma pasta em seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="0188b-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="0188b-125">Opcionalmente, você talvez queira compartilhar uma pasta em seu Raspberry Pi com seu ambiente de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0188b-125">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="0188b-126">Compartilhar uma pasta permite que você use seu editor de texto preferido de área de trabalho (como [Visual Studio Code](https://code.visualstudio.com/) ou [Sublime Text](http://www.sublimetext.com/)) para editar arquivos em seu Raspberry Pi em vez de usar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="0188b-126">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="0188b-127">Para compartilhar uma pasta com o Windows, configure um servidor Samba no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0188b-127">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="0188b-128">Como alternativa, use o servidor interno [SFTP](https://www.raspberrypi.org/documentation/remote-access/) com um cliente SFTP em sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0188b-128">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/