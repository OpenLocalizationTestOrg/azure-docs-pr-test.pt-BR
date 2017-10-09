## <a name="install-hello-prerequisites"></a>Instale os pré-requisitos de saudação

1. Instale o [Visual Studio 2015 ou 2017](https://www.visualstudio.com). Você pode usar o hello liberar Community Edition se você atende aos requisitos de licenciamento de saudação. Ser tooinclude se Visual C++ e o NuGet Package Manager.

1. Instalar [git](http://www.git-scm.com) e assegure-se de que você pode executar git.exe da linha de comando hello.

1. Instalar [CMake](https://cmake.org/download/) e assegure-se de que você pode executar cmake.exe da linha de comando hello. O CMake versão 3.7.2 ou posterior é recomendado. Olá **. msi** installer é a opção mais fácil Olá no Windows. Adicionar CMake toohello caminho para pelo menos Olá usuário atual quando Olá instalador solicita que você.

1. Instalar o [Python 2.7](https://www.python.org/downloads/release/python-27). Certifique-se de adicionar o Python tooyour `PATH` variável de ambiente no **painel de controle -> sistema -> Avançado configurações do sistema -> variáveis de ambiente**.

1. Em um prompt de comando, execute Olá comando tooclone hello Azure IoT borda GitHub repositório tooyour máquina local a seguir:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Como toobuild Olá exemplo

Agora você pode criar hello IoT borda exemplos e tempo de execução em seu computador local:

1. Abra um **Prompt de comando do desenvolvedor para VS 2015** ou **Prompt de comando do desenvolvedor para VS 2017**.

1. Navegue a pasta raiz de toohello em sua cópia local da saudação **iot borda** repositório.

1. Execute o script de compilação da seguinte maneira:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Esse script cria um arquivo de solução do Visual Studio e cria a solução de saudação. Você pode encontrar a solução do Visual Studio Olá no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório. Se você quiser toobuild e executa testes de unidade hello, adicionar Olá `--run-unittests` parâmetro. Se você quiser toobuild e executa testes de tooend de término hello, adicionar Olá `--run-e2e-tests`.

> [!NOTE]
> Sempre que você executa Olá **build.cmd** script, ele exclui e recria, em seguida, Olá **criar** na pasta da raiz de saudação da sua cópia local da saudação **iot borda** repositório.
