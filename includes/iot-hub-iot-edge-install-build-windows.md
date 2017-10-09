## <a name="install-hello-prerequisites"></a><span data-ttu-id="bfc00-101">Instale os pré-requisitos de saudação</span><span class="sxs-lookup"><span data-stu-id="bfc00-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="bfc00-102">Instale o [Visual Studio 2015 ou 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="bfc00-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="bfc00-103">Você pode usar o hello liberar Community Edition se você atende aos requisitos de licenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfc00-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="bfc00-104">Ser tooinclude se Visual C++ e o NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="bfc00-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="bfc00-105">Instalar [git](http://www.git-scm.com) e assegure-se de que você pode executar git.exe da linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="bfc00-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="bfc00-106">Instalar [CMake](https://cmake.org/download/) e assegure-se de que você pode executar cmake.exe da linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="bfc00-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="bfc00-107">O CMake versão 3.7.2 ou posterior é recomendado.</span><span class="sxs-lookup"><span data-stu-id="bfc00-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="bfc00-108">Olá **. msi** installer é a opção mais fácil Olá no Windows.</span><span class="sxs-lookup"><span data-stu-id="bfc00-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="bfc00-109">Adicionar CMake toohello caminho para pelo menos Olá usuário atual quando Olá instalador solicita que você.</span><span class="sxs-lookup"><span data-stu-id="bfc00-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="bfc00-110">Instalar o [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="bfc00-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="bfc00-111">Certifique-se de adicionar o Python tooyour `PATH` variável de ambiente no **painel de controle -> sistema -> Avançado configurações do sistema -> variáveis de ambiente**.</span><span class="sxs-lookup"><span data-stu-id="bfc00-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="bfc00-112">Em um prompt de comando, execute Olá comando tooclone hello Azure IoT borda GitHub repositório tooyour máquina local a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfc00-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="bfc00-113">Como toobuild Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="bfc00-113">How toobuild hello sample</span></span>

<span data-ttu-id="bfc00-114">Agora você pode criar hello IoT borda exemplos e tempo de execução em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="bfc00-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="bfc00-115">Abra um **Prompt de comando do desenvolvedor para VS 2015** ou **Prompt de comando do desenvolvedor para VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="bfc00-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="bfc00-116">Navegue a pasta raiz de toohello em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="bfc00-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="bfc00-117">Execute o script de compilação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bfc00-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="bfc00-118">Esse script cria um arquivo de solução do Visual Studio e cria a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfc00-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="bfc00-119">Você pode encontrar a solução do Visual Studio Olá no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="bfc00-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="bfc00-120">Se você quiser toobuild e executa testes de unidade hello, adicionar Olá `--run-unittests` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="bfc00-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="bfc00-121">Se você quiser toobuild e executa testes de tooend de término hello, adicionar Olá `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="bfc00-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="bfc00-122">Sempre que você executa Olá **build.cmd** script, ele exclui e recria, em seguida, Olá **criar** na pasta da raiz de saudação da sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="bfc00-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
