## <a name="install-the-prerequisites"></a><span data-ttu-id="25fa7-101">Instalar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25fa7-101">Install the prerequisites</span></span>

1. <span data-ttu-id="25fa7-102">Instale o [Visual Studio 2015 ou 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="25fa7-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="25fa7-103">Você poderá usar a Community Edition gratuita se atender aos requisitos de licenciamento.</span><span class="sxs-lookup"><span data-stu-id="25fa7-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="25fa7-104">Inclua o Visual C++ e o Gerenciador de Pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="25fa7-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="25fa7-105">Instale o [git](http://www.git-scm.com) e assegure-se de que você pode executar git.exe da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="25fa7-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="25fa7-106">Instale o [CMake](https://cmake.org/download/) e assegure-se de que você pode executar cmake.exe da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="25fa7-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="25fa7-107">O CMake versão 3.7.2 ou posterior é recomendado.</span><span class="sxs-lookup"><span data-stu-id="25fa7-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="25fa7-108">O instalador **.msi** é a opção mais fácil no Windows.</span><span class="sxs-lookup"><span data-stu-id="25fa7-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="25fa7-109">Adicione CMake ao PATH para pelo menos o usuário atual quando o instalador solicitar.</span><span class="sxs-lookup"><span data-stu-id="25fa7-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="25fa7-110">Instalar o [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="25fa7-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="25fa7-111">Verifique se você adicionou o Python à sua variável do ambiente do `PATH` em **Painel de Controle -> Sistema -> Configurações avançadas do sistema -> Variáveis do Ambiente**.</span><span class="sxs-lookup"><span data-stu-id="25fa7-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="25fa7-112">Em um prompt de comando, execute o seguinte comando para clonar o repositório GitHub do Azure IoT Edge para seu computador local:</span><span class="sxs-lookup"><span data-stu-id="25fa7-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="25fa7-113">Como criar a amostra</span><span class="sxs-lookup"><span data-stu-id="25fa7-113">How to build the sample</span></span>

<span data-ttu-id="25fa7-114">Agora você pode criar os exemplos e o tempo de execução do IoT Edge em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="25fa7-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="25fa7-115">Abra um **Prompt de comando do desenvolvedor para VS 2015** ou **Prompt de comando do desenvolvedor para VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="25fa7-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="25fa7-116">Navegue até a pasta raiz na sua cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="25fa7-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="25fa7-117">Execute o script de compilação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="25fa7-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="25fa7-118">Este script cria um arquivo de solução do Visual Studio e compila a solução.</span><span class="sxs-lookup"><span data-stu-id="25fa7-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="25fa7-119">É possível encontrar a solução do Visual Studio na pasta **build** na cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="25fa7-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="25fa7-120">Se quiser compilar e executar os testes de unidade, adicione o parâmetro `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="25fa7-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="25fa7-121">Se quiser compilar e executar os testes de ponta a ponta, adicione o `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="25fa7-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="25fa7-122">Sempre que você executa o script **build.cmd**, ele exclui e recria a pasta **build** na pasta raiz da cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="25fa7-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>