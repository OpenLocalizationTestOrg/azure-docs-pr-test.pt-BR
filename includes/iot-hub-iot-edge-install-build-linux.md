## <a name="install-hello-prerequisites"></a>Instale os pré-requisitos de saudação

etapas de Olá neste tutorial presumem que você estiver executando o Ubuntu Linux.

Abra um shell e execute Olá pacotes de pré-requisitos tooinstall Olá comandos a seguir:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

No shell de hello, execute Olá comando tooclone hello Azure IoT borda GitHub repositório tooyour máquina local a seguir:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Como toobuild Olá exemplo

Agora você pode criar hello IoT borda exemplos e tempo de execução em seu computador local:

1. Abra um shell.

1. Navegue a pasta raiz de toohello em sua cópia local da saudação **iot borda** repositório.

1. Execute o script de compilação da seguinte maneira:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Esse script usa o **cmake** toocreate utilitário uma pasta chamada **criar** na pasta raiz de saudação de sua cópia local do **iot borda** repositório e gerar um makefile. script Hello, em seguida, cria a solução de hello, ignorando os testes de unidade e testes de tooend final. Se você quiser toobuild e executa testes de unidade hello, adicionar Olá `--run-unittests` parâmetro. Se você quiser toobuild e executa testes de tooend de término hello, adicionar Olá `--run-e2e-tests`.

> [!NOTE]
> Sempre que você executa Olá **build.sh** script, ele exclui e recria, em seguida, Olá **criar** na pasta da raiz de saudação da sua cópia local da saudação **iot borda** repositório.
