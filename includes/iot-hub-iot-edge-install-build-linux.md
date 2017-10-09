## <a name="install-hello-prerequisites"></a><span data-ttu-id="a4061-101">Instale os pré-requisitos de saudação</span><span class="sxs-lookup"><span data-stu-id="a4061-101">Install hello prerequisites</span></span>

<span data-ttu-id="a4061-102">etapas de Olá neste tutorial presumem que você estiver executando o Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="a4061-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="a4061-103">Abra um shell e execute Olá pacotes de pré-requisitos tooinstall Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4061-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="a4061-104">No shell de hello, execute Olá comando tooclone hello Azure IoT borda GitHub repositório tooyour máquina local a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4061-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="a4061-105">Como toobuild Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="a4061-105">How toobuild hello sample</span></span>

<span data-ttu-id="a4061-106">Agora você pode criar hello IoT borda exemplos e tempo de execução em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="a4061-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="a4061-107">Abra um shell.</span><span class="sxs-lookup"><span data-stu-id="a4061-107">Open a shell.</span></span>

1. <span data-ttu-id="a4061-108">Navegue a pasta raiz de toohello em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="a4061-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="a4061-109">Execute o script de compilação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a4061-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="a4061-110">Esse script usa o **cmake** toocreate utilitário uma pasta chamada **criar** na pasta raiz de saudação de sua cópia local do **iot borda** repositório e gerar um makefile.</span><span class="sxs-lookup"><span data-stu-id="a4061-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="a4061-111">script Hello, em seguida, cria a solução de hello, ignorando os testes de unidade e testes de tooend final.</span><span class="sxs-lookup"><span data-stu-id="a4061-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="a4061-112">Se você quiser toobuild e executa testes de unidade hello, adicionar Olá `--run-unittests` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a4061-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="a4061-113">Se você quiser toobuild e executa testes de tooend de término hello, adicionar Olá `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="a4061-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="a4061-114">Sempre que você executa Olá **build.sh** script, ele exclui e recria, em seguida, Olá **criar** na pasta da raiz de saudação da sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="a4061-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
