## <a name="build-iot-edge"></a><span data-ttu-id="eab7b-101">Criar o Edge IoT</span><span class="sxs-lookup"><span data-stu-id="eab7b-101">Build IoT Edge</span></span>

<span data-ttu-id="eab7b-102">Este tutorial usa módulos personalizados do Edge IoT para se comunicar com a solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="eab7b-102">This tutorial uses custom IoT Edge modules to communicate with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="eab7b-103">Portanto, você precisa criar os módulos do Edge IoT a partir do código-fonte personalizado.</span><span class="sxs-lookup"><span data-stu-id="eab7b-103">Therefore, you need to build the IoT Edge modules from custom source code.</span></span> <span data-ttu-id="eab7b-104">As seções a seguir descrevem como instalar o Edge IoT e criar o módulo personalizado do Edge IoT.</span><span class="sxs-lookup"><span data-stu-id="eab7b-104">The following sections describe how to install IoT Edge and build the custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="eab7b-105">Instalar o Edge IoT</span><span class="sxs-lookup"><span data-stu-id="eab7b-105">Install IoT Edge</span></span>

<span data-ttu-id="eab7b-106">As etapas a seguir descrevem como instalar o software do Edge IoT pré-compilado no Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="eab7b-106">The following steps describe how to install the pre-compiled IoT Edge software on the Intel NUC:</span></span>

1. <span data-ttu-id="eab7b-107">Configure os repositórios de pacote inteligente necessário executando os seguintes comandos no Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="eab7b-107">Configure the required smart package repositories by running the following commands on the Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="eab7b-108">Insira `y` quando o comando solicitar **Incluir este canal?**.</span><span class="sxs-lookup"><span data-stu-id="eab7b-108">Enter `y` when the command prompts you to **Include this channel?**.</span></span>

1. <span data-ttu-id="eab7b-109">Atualize o gerenciador de pacote inteligente, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="eab7b-109">Update the smart package manager by running the following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="eab7b-110">Instale o pacote do Edge IoT do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="eab7b-110">Install the Azure IoT Edge package by running the following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="eab7b-111">Verifique a instalação executando o exemplo “Olá, Mundo”.</span><span class="sxs-lookup"><span data-stu-id="eab7b-111">Verify the installation by running the "Hello world" sample.</span></span> <span data-ttu-id="eab7b-112">Este exemplo grava uma mensagem de hello world no arquivo log.txt a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="eab7b-112">This sample writes a hello world message to the log.txT file every five seconds.</span></span> <span data-ttu-id="eab7b-113">Os seguintes comandos executam o exemplo “Olá, Mundo”:</span><span class="sxs-lookup"><span data-stu-id="eab7b-113">The following commands run the "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="eab7b-114">Ignore qualquer mensagem de **argumento inválido** ao interromper o exemplo.</span><span class="sxs-lookup"><span data-stu-id="eab7b-114">Ignore any **invalid argument** messages when you stop the sample.</span></span>

    <span data-ttu-id="eab7b-115">Use o seguinte comando para exibir o conteúdo do arquivo de log:</span><span class="sxs-lookup"><span data-stu-id="eab7b-115">Use the following command to view the contents of the log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="eab7b-116">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="eab7b-116">Troubleshooting</span></span>

<span data-ttu-id="eab7b-117">Se você receber o erro “Nenhum pacote fornece o util-linux-dev”, tente reiniciar o Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eab7b-117">If you receive the error "No package provides util-linux-dev", try rebooting the Intel NUC.</span></span>
