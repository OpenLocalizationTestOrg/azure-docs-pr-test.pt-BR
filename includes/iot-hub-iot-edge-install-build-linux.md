## <a name="install-the-prerequisites"></a><span data-ttu-id="b2c5d-101">Instalar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b2c5d-101">Install the prerequisites</span></span>

<span data-ttu-id="b2c5d-102">As etapas neste tutorial presumem que você esteja executando o Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-102">The steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="b2c5d-103">Abra um shell e execute os seguintes comandos para instalar os pacotes de pré-requisito:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-103">Open a shell and run the following commands to install the prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="b2c5d-104">No shell, execute o seguinte comando para clonar o repositório GitHub do Azure IoT Edge para seu computador local:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-104">In the shell, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="b2c5d-105">Como criar a amostra</span><span class="sxs-lookup"><span data-stu-id="b2c5d-105">How to build the sample</span></span>

<span data-ttu-id="b2c5d-106">Agora você pode criar os exemplos e o tempo de execução do IoT Edge em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-106">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="b2c5d-107">Abra um shell.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-107">Open a shell.</span></span>

1. <span data-ttu-id="b2c5d-108">Navegue até a pasta raiz na sua cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-108">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="b2c5d-109">Execute o script de compilação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="b2c5d-110">Esse script usa o utilitário **cmake** para criar uma pasta chamada **build** na pasta raiz da cópia local do repositório **iot-edge** e gerar um makefile.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-110">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="b2c5d-111">O script cria a solução, ignorando os testes de unidade e os testes de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-111">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="b2c5d-112">Se quiser compilar e executar os testes de unidade, adicione o parâmetro `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-112">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="b2c5d-113">Se quiser compilar e executar os testes de ponta a ponta, adicione o `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-113">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="b2c5d-114">Sempre que você executa o script **build.sh**, ele exclui e recria a pasta **build** na pasta raiz da cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-114">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>