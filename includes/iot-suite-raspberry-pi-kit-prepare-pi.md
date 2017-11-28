## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="90e67-101">Preparar seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="90e67-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="90e67-102">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="90e67-102">Install Raspbian</span></span>

<span data-ttu-id="90e67-103">Se esta for a primeira vez que você estiver usando o Raspberry Pi, você precisa instalar o sistema operacional do Raspbian usando NOOBS no cartão SD incluído no kit.</span><span class="sxs-lookup"><span data-stu-id="90e67-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="90e67-104">O [Guia de Software do Raspberry Pi Software guia][lnk-install-raspbian] descreve como instalar um sistema operacional em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="90e67-105">Este tutorial presume que você instalou o sistema operacional Raspbian em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="90e67-106">O cartão SD incluído no [Microsoft Azure IoT Starter Kit do Raspberry Pi 3][lnk-starter-kits] já tem NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="90e67-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="90e67-107">Você pode inicializar o Raspberry Pi neste cartão e optar por instalar o sistema operacional do Raspbian.</span><span class="sxs-lookup"><span data-stu-id="90e67-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="90e67-108">Configurar o hardware</span><span class="sxs-lookup"><span data-stu-id="90e67-108">Set up the hardware</span></span>

<span data-ttu-id="90e67-109">Este tutorial usa o sensor BME280 incluído no [Microsoft Azure IoT Starter Kit do Raspberry Pi 3][lnk-starter-kits] para gerar dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="90e67-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="90e67-110">Ele usa um LED para indicar quando o Raspberry Pi processa uma invocação de método no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="90e67-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="90e67-111">Os componentes da placa universal são:</span><span class="sxs-lookup"><span data-stu-id="90e67-111">The components on the bread board are:</span></span>

- <span data-ttu-id="90e67-112">LED vermelho</span><span class="sxs-lookup"><span data-stu-id="90e67-112">Red LED</span></span>
- <span data-ttu-id="90e67-113">Resistor de 220 Ohm (vermelho, vermelho, marrom)</span><span class="sxs-lookup"><span data-stu-id="90e67-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="90e67-114">Sensor BME280</span><span class="sxs-lookup"><span data-stu-id="90e67-114">BME280 sensor</span></span>

<span data-ttu-id="90e67-115">O diagrama a seguir mostra como conectar seu hardware:</span><span class="sxs-lookup"><span data-stu-id="90e67-115">The following diagram shows how to connect your hardware:</span></span>

![Configuração de hardware para Raspberry Pi][img-connection-diagram]

<span data-ttu-id="90e67-117">A tabela a seguir resume as conexões do Raspberry Pi para os componentes na placa universal:</span><span class="sxs-lookup"><span data-stu-id="90e67-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="90e67-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="90e67-118">Raspberry Pi</span></span>            | <span data-ttu-id="90e67-119">Placa universal</span><span class="sxs-lookup"><span data-stu-id="90e67-119">Breadboard</span></span>             |<span data-ttu-id="90e67-120">Cor</span><span class="sxs-lookup"><span data-stu-id="90e67-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="90e67-121">GND (Pino 14)</span><span class="sxs-lookup"><span data-stu-id="90e67-121">GND (Pin 14)</span></span>            | <span data-ttu-id="90e67-122">Pin do LED - ve (18A)</span><span class="sxs-lookup"><span data-stu-id="90e67-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="90e67-123">Roxo</span><span class="sxs-lookup"><span data-stu-id="90e67-123">Purple</span></span>          |
| <span data-ttu-id="90e67-124">GPCLK0 (pino 7)</span><span class="sxs-lookup"><span data-stu-id="90e67-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="90e67-125">Resistor (25A)</span><span class="sxs-lookup"><span data-stu-id="90e67-125">Resistor (25A)</span></span>         | <span data-ttu-id="90e67-126">Laranja</span><span class="sxs-lookup"><span data-stu-id="90e67-126">Orange</span></span>          |
| <span data-ttu-id="90e67-127">SPI_CE0 (Pino 24)</span><span class="sxs-lookup"><span data-stu-id="90e67-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="90e67-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="90e67-128">CS (39A)</span></span>               | <span data-ttu-id="90e67-129">Azul</span><span class="sxs-lookup"><span data-stu-id="90e67-129">Blue</span></span>          |
| <span data-ttu-id="90e67-130">SPI_SCLK (Pino 23)</span><span class="sxs-lookup"><span data-stu-id="90e67-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="90e67-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="90e67-131">SCK (36A)</span></span>              | <span data-ttu-id="90e67-132">Amarelo</span><span class="sxs-lookup"><span data-stu-id="90e67-132">Yellow</span></span>        |
| <span data-ttu-id="90e67-133">SPI_MISO (Pino 21)</span><span class="sxs-lookup"><span data-stu-id="90e67-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="90e67-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="90e67-134">SDO (37A)</span></span>              | <span data-ttu-id="90e67-135">Branco</span><span class="sxs-lookup"><span data-stu-id="90e67-135">White</span></span>         |
| <span data-ttu-id="90e67-136">SPI_MOSI (Pino 19)</span><span class="sxs-lookup"><span data-stu-id="90e67-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="90e67-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="90e67-137">SDI (38A)</span></span>              | <span data-ttu-id="90e67-138">Verde</span><span class="sxs-lookup"><span data-stu-id="90e67-138">Green</span></span>         |
| <span data-ttu-id="90e67-139">GND (pino 6)</span><span class="sxs-lookup"><span data-stu-id="90e67-139">GND (Pin 6)</span></span>             | <span data-ttu-id="90e67-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="90e67-140">GND (35A)</span></span>              | <span data-ttu-id="90e67-141">Preto</span><span class="sxs-lookup"><span data-stu-id="90e67-141">Black</span></span>         |
| <span data-ttu-id="90e67-142">3.3 V (Pino 1)</span><span class="sxs-lookup"><span data-stu-id="90e67-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="90e67-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="90e67-143">3Vo (34A)</span></span>              | <span data-ttu-id="90e67-144">Vermelho</span><span class="sxs-lookup"><span data-stu-id="90e67-144">Red</span></span>           |

<span data-ttu-id="90e67-145">Para concluir a configuração de hardware, você precisa:</span><span class="sxs-lookup"><span data-stu-id="90e67-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="90e67-146">Conectar seu Raspberry Pi à fonte de alimentação incluída no kit.</span><span class="sxs-lookup"><span data-stu-id="90e67-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="90e67-147">Conectar seu Raspberry Pi à sua rede usando o cabo Ethernet incluído em seu kit.</span><span class="sxs-lookup"><span data-stu-id="90e67-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="90e67-148">Como alternativa, você pode configurar [Conectividade sem fio][lnk-pi-wireless] para o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="90e67-149">Agora você concluiu a configuração de hardware do seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="90e67-150">Entre e acesse o terminal</span><span class="sxs-lookup"><span data-stu-id="90e67-150">Sign in and access the terminal</span></span>

<span data-ttu-id="90e67-151">Você tem duas opções para acessar um ambiente de terminal no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="90e67-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="90e67-152">Se você tiver um teclado e um monitor conectado ao seu Raspberry Pi, você pode usar a GUI do Raspbian para acessar uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="90e67-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="90e67-153">Acesse a linha de comando em seu Raspberry Pi usando o SSH em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="90e67-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="90e67-154">Use uma janela de terminal na GUI</span><span class="sxs-lookup"><span data-stu-id="90e67-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="90e67-155">As credenciais padrões para Raspbian são o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="90e67-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="90e67-156">Na barra de tarefas na GUI, você pode iniciar o utilitário **Terminal** usando o ícone que se parece com um monitor.</span><span class="sxs-lookup"><span data-stu-id="90e67-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="90e67-157">Entre com o SSH</span><span class="sxs-lookup"><span data-stu-id="90e67-157">Sign in with SSH</span></span>

<span data-ttu-id="90e67-158">Você pode usar o SSH para acesso de linha de comando para o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="90e67-159">O artigo [SSH (Secure Shell)][lnk-pi-ssh] descreve como configurar SSH em seu Raspberry Pi e como conectar-se a partir do [Windows][lnk-ssh-windows] ou [Linux e Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="90e67-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="90e67-160">Entre com o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="90e67-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="90e67-161">Opcional: Compartilhar uma pasta em seu Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="90e67-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="90e67-162">Opcionalmente, você talvez queira compartilhar uma pasta em seu Raspberry Pi com seu ambiente de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="90e67-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="90e67-163">Compartilhar uma pasta permite que você use seu editor de texto preferido de área de trabalho (como [Visual Studio Code](https://code.visualstudio.com/) ou [Sublime Text](http://www.sublimetext.com/)) para editar arquivos em seu Raspberry Pi em vez de usar `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="90e67-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="90e67-164">Para compartilhar uma pasta com o Windows, configure um servidor Samba no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="90e67-165">Como alternativa, use o servidor interno [SFTP](https://www.raspberrypi.org/documentation/remote-access/) com um cliente SFTP em sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="90e67-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="90e67-166">Habilitar SPI</span><span class="sxs-lookup"><span data-stu-id="90e67-166">Enable SPI</span></span>

<span data-ttu-id="90e67-167">Antes de executar o aplicativo de exemplo, você deve habilitar o barramento Serial Peripheral Interface (SPI) no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="90e67-168">O Raspberry Pi se comunica com o dispositivo do sensor BME280 pelo barramento da SPI.</span><span class="sxs-lookup"><span data-stu-id="90e67-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="90e67-169">Abra o arquivo de configuração executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="90e67-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="90e67-170">Localize a linha:</span><span class="sxs-lookup"><span data-stu-id="90e67-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="90e67-171">Para remover os comentários da linha, exclua o `#` no início.</span><span class="sxs-lookup"><span data-stu-id="90e67-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="90e67-172">Salve suas alterações (**Ctrl-O**, **Enter**) e saia do editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="90e67-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="90e67-173">Para habilitar o SPI, reinicialize o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="90e67-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="90e67-174">Reinicializar desconecta o terminal, você precisa entrar novamente quando reinicia o Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="90e67-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

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