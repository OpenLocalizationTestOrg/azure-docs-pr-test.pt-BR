## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="5fad4-101">Preparar seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="5fad4-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="5fad4-102">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="5fad4-102">Install Raspbian</span></span>

<span data-ttu-id="5fad4-103">Se isso for Olá primeira vez que você estiver usando o Pi framboesa, é necessário tooinstall Olá Raspbian o sistema operacional usando NOOBS no cartão SD de saudação incluído no kit de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fad4-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="5fad4-104">Olá [framboesa Pi Software guia] [ lnk-install-raspbian] descreve como tooinstall um sistema operacional em seu framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="5fad4-105">Este tutorial presume que você instalou o sistema de operacional Raspbian Olá no seu framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="5fad4-106">cartão de saudação SD incluído no hello [Microsoft Azure IoT Starter Kit para framboesa Pi 3] [ lnk-starter-kits] já tem NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="5fad4-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="5fad4-107">Pode ser inicializado Olá framboesa Pi neste cartão e escolha tooinstall Olá Raspbian SO.</span><span class="sxs-lookup"><span data-stu-id="5fad4-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="5fad4-108">Configurar hardware Olá</span><span class="sxs-lookup"><span data-stu-id="5fad4-108">Set up hello hardware</span></span>

<span data-ttu-id="5fad4-109">Este tutorial usa sensor Olá BME280 incluído no hello [Microsoft Azure IoT Starter Kit para framboesa Pi 3] [ lnk-starter-kits] toogenerate os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="5fad4-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="5fad4-110">Ele usa um LED tooindicate quando Olá framboesa Pi processa uma invocação de método do painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fad4-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="5fad4-111">Olá componentes na placa de pão Olá são:</span><span class="sxs-lookup"><span data-stu-id="5fad4-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="5fad4-112">LED vermelho</span><span class="sxs-lookup"><span data-stu-id="5fad4-112">Red LED</span></span>
- <span data-ttu-id="5fad4-113">Resistor de 220 Ohm (vermelho, vermelho, marrom)</span><span class="sxs-lookup"><span data-stu-id="5fad4-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="5fad4-114">Sensor BME280</span><span class="sxs-lookup"><span data-stu-id="5fad4-114">BME280 sensor</span></span>

<span data-ttu-id="5fad4-115">diagrama a seguir Olá mostra como tooconnect seu hardware:</span><span class="sxs-lookup"><span data-stu-id="5fad4-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Configuração de hardware para Raspberry Pi][img-connection-diagram]

<span data-ttu-id="5fad4-117">Olá tabela a seguir resume conexões Olá de componentes de toohello Olá framboesa Pi no breadboard hello:</span><span class="sxs-lookup"><span data-stu-id="5fad4-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="5fad4-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="5fad4-118">Raspberry Pi</span></span>            | <span data-ttu-id="5fad4-119">Placa universal</span><span class="sxs-lookup"><span data-stu-id="5fad4-119">Breadboard</span></span>             |<span data-ttu-id="5fad4-120">Cor</span><span class="sxs-lookup"><span data-stu-id="5fad4-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="5fad4-121">GND (Pino 14)</span><span class="sxs-lookup"><span data-stu-id="5fad4-121">GND (Pin 14)</span></span>            | <span data-ttu-id="5fad4-122">Pin do LED - ve (18A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="5fad4-123">Roxo</span><span class="sxs-lookup"><span data-stu-id="5fad4-123">Purple</span></span>          |
| <span data-ttu-id="5fad4-124">GPCLK0 (pino 7)</span><span class="sxs-lookup"><span data-stu-id="5fad4-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="5fad4-125">Resistor (25A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-125">Resistor (25A)</span></span>         | <span data-ttu-id="5fad4-126">Laranja</span><span class="sxs-lookup"><span data-stu-id="5fad4-126">Orange</span></span>          |
| <span data-ttu-id="5fad4-127">SPI_CE0 (Pino 24)</span><span class="sxs-lookup"><span data-stu-id="5fad4-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="5fad4-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-128">CS (39A)</span></span>               | <span data-ttu-id="5fad4-129">Azul</span><span class="sxs-lookup"><span data-stu-id="5fad4-129">Blue</span></span>          |
| <span data-ttu-id="5fad4-130">SPI_SCLK (Pino 23)</span><span class="sxs-lookup"><span data-stu-id="5fad4-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="5fad4-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-131">SCK (36A)</span></span>              | <span data-ttu-id="5fad4-132">Amarelo</span><span class="sxs-lookup"><span data-stu-id="5fad4-132">Yellow</span></span>        |
| <span data-ttu-id="5fad4-133">SPI_MISO (Pino 21)</span><span class="sxs-lookup"><span data-stu-id="5fad4-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="5fad4-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-134">SDO (37A)</span></span>              | <span data-ttu-id="5fad4-135">Branco</span><span class="sxs-lookup"><span data-stu-id="5fad4-135">White</span></span>         |
| <span data-ttu-id="5fad4-136">SPI_MOSI (Pino 19)</span><span class="sxs-lookup"><span data-stu-id="5fad4-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="5fad4-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-137">SDI (38A)</span></span>              | <span data-ttu-id="5fad4-138">Verde</span><span class="sxs-lookup"><span data-stu-id="5fad4-138">Green</span></span>         |
| <span data-ttu-id="5fad4-139">GND (pino 6)</span><span class="sxs-lookup"><span data-stu-id="5fad4-139">GND (Pin 6)</span></span>             | <span data-ttu-id="5fad4-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-140">GND (35A)</span></span>              | <span data-ttu-id="5fad4-141">Preto</span><span class="sxs-lookup"><span data-stu-id="5fad4-141">Black</span></span>         |
| <span data-ttu-id="5fad4-142">3.3 V (Pino 1)</span><span class="sxs-lookup"><span data-stu-id="5fad4-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="5fad4-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="5fad4-143">3Vo (34A)</span></span>              | <span data-ttu-id="5fad4-144">Vermelho</span><span class="sxs-lookup"><span data-stu-id="5fad4-144">Red</span></span>           |

<span data-ttu-id="5fad4-145">configuração de hardware do toocomplete hello, você precisa:</span><span class="sxs-lookup"><span data-stu-id="5fad4-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="5fad4-146">Conecte-se a fonte de alimentação toohello framboesa Pi incluída no kit de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fad4-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="5fad4-147">Conecte a sua rede de tooyour framboesa Pi usando cabo Ethernet de saudação incluído no kit.</span><span class="sxs-lookup"><span data-stu-id="5fad4-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="5fad4-148">Como alternativa, você pode configurar [Conectividade sem fio][lnk-pi-wireless] para o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="5fad4-149">Agora você concluiu a instalação de hardware Olá de seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="5fad4-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="5fad4-150">Entrar e acessar terminal Olá</span><span class="sxs-lookup"><span data-stu-id="5fad4-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="5fad4-151">Você tem um ambiente de terminal tooaccess de duas opções com seu Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="5fad4-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="5fad4-152">Se você tiver um teclado e monitorar tooyour conectado framboesa Pi, você pode usar o hello GUI Raspbian tooaccess uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="5fad4-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="5fad4-153">Acesso a linha de comando do hello no seu Pi framboesa usando SSH em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="5fad4-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="5fad4-154">Use uma janela de terminal Olá GUI</span><span class="sxs-lookup"><span data-stu-id="5fad4-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="5fad4-155">credenciais de padrão de saudação para Raspbian são o nome de usuário **pi** e a senha **framboesa**.</span><span class="sxs-lookup"><span data-stu-id="5fad4-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="5fad4-156">Na barra de tarefas de saudação em Olá GUI, você pode iniciar Olá **Terminal** utilitário usando o ícone de saudação que se parece com um monitor.</span><span class="sxs-lookup"><span data-stu-id="5fad4-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="5fad4-157">Entre com o SSH</span><span class="sxs-lookup"><span data-stu-id="5fad4-157">Sign in with SSH</span></span>

<span data-ttu-id="5fad4-158">Você pode usar o SSH para acesso de linha de comando tooyour framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="5fad4-159">artigo Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH com o Pi framboesa e como tooconnect de [Windows] [ lnk-ssh-windows] ou [Sistema operacional Linux e Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="5fad4-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="5fad4-160">Entre com o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="5fad4-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="5fad4-161">Opcional: Compartilhar uma pasta em seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="5fad4-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="5fad4-162">Opcionalmente, talvez você queira tooshare uma pasta no seu Pi framboesa com seu ambiente de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5fad4-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="5fad4-163">Uma pasta de compartilhamento permite que você toouse seu editor de texto preferido de área de trabalho (como [código do Visual Studio](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit arquivos em seu Pi framboesa em vez de usar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="5fad4-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="5fad4-164">tooshare uma pasta com o Windows, configure um servidor do Samba no hello framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="5fad4-165">Como alternativa, usar interno de saudação [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server com um cliente SFTP na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5fad4-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="5fad4-166">Habilitar SPI</span><span class="sxs-lookup"><span data-stu-id="5fad4-166">Enable SPI</span></span>

<span data-ttu-id="5fad4-167">Antes de executar o aplicativo de exemplo hello, você deve habilitar o barramento de Interface Serial periféricos (IDA) Olá Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="5fad4-168">Olá framboesa Pi se comunica com o hello BME280 sensor sobre Olá barramento ida.</span><span class="sxs-lookup"><span data-stu-id="5fad4-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="5fad4-169">Use Olá arquivo de configuração do comando tooedit Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fad4-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="5fad4-170">Localize a linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="5fad4-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="5fad4-171">linha toouncomment Olá Olá delete `#` no início de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fad4-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="5fad4-172">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="5fad4-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="5fad4-173">tooenable ida, reinicialize Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="5fad4-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="5fad4-174">Reinicializando desconecta terminal Olá, é necessário toosign no novamente quando Olá framboesa Pi for reiniciado:</span><span class="sxs-lookup"><span data-stu-id="5fad4-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/