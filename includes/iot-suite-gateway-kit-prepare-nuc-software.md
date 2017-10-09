## <a name="build-iot-edge"></a><span data-ttu-id="d203d-101">Criar o Edge IoT</span><span class="sxs-lookup"><span data-stu-id="d203d-101">Build IoT Edge</span></span>

<span data-ttu-id="d203d-102">Este tutorial usa toocommunicate de módulos personalizado IoT borda com hello solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="d203d-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="d203d-103">Portanto, você precisa toobuild módulos de borda IoT saudação do código-fonte personalizada.</span><span class="sxs-lookup"><span data-stu-id="d203d-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="d203d-104">Olá seções a seguir descreve como tooinstall IoT borda e compilação Olá módulo personalizado de borda de IoT.</span><span class="sxs-lookup"><span data-stu-id="d203d-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="d203d-105">Instalar o Edge IoT</span><span class="sxs-lookup"><span data-stu-id="d203d-105">Install IoT Edge</span></span>

<span data-ttu-id="d203d-106">Olá etapas a seguir descrevem como tooinstall Olá pré-compilado software IoT borda Olá Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="d203d-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="d203d-107">Configure repositórios de pacote inteligente Olá necessário executando Olá comandos a seguir no hello Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="d203d-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="d203d-108">Digite `y` quando Olá comando solicita a você muito**incluir esse canal?**.</span><span class="sxs-lookup"><span data-stu-id="d203d-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="d203d-109">Atualize Gerenciador de pacote inteligente Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d203d-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="d203d-110">Instale pacote do Azure IoT borda Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d203d-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="d203d-111">Verificar a instalação de saudação pelo exemplo de "Hello world" hello em execução.</span><span class="sxs-lookup"><span data-stu-id="d203d-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="d203d-112">Este exemplo grava um arquivo de log. txt hello world mensagem toohello a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="d203d-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="d203d-113">Olá, comandos a seguir executam hello "Hello world" exemplo:</span><span class="sxs-lookup"><span data-stu-id="d203d-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="d203d-114">Ignorar todas **argumento inválido** mensagens quando você interrompe o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="d203d-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="d203d-115">Use Olá conteúdo de saudação do comando tooview saudação do arquivo de log a seguir:</span><span class="sxs-lookup"><span data-stu-id="d203d-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="d203d-116">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d203d-116">Troubleshooting</span></span>

<span data-ttu-id="d203d-117">Se você receber o erro hello "nenhum pacote fornece util-linux-dev", tente reiniciar Olá NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="d203d-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
