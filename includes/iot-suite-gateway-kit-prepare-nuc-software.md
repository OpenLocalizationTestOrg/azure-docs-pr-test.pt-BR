## <a name="build-iot-edge"></a>Criar o Edge IoT

Este tutorial usa toocommunicate de módulos personalizado IoT borda com hello solução pré-configurada de monitoramento remoto. Portanto, você precisa toobuild módulos de borda IoT saudação do código-fonte personalizada. Olá seções a seguir descreve como tooinstall IoT borda e compilação Olá módulo personalizado de borda de IoT.

### <a name="install-iot-edge"></a>Instalar o Edge IoT

Olá etapas a seguir descrevem como tooinstall Olá pré-compilado software IoT borda Olá Intel NUC:

1. Configure repositórios de pacote inteligente Olá necessário executando Olá comandos a seguir no hello Intel NUC:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Digite `y` quando Olá comando solicita a você muito**incluir esse canal?**.

1. Atualize Gerenciador de pacote inteligente Olá executando Olá comando a seguir:

    ```bash
    smart update
    ```

1. Instale pacote do Azure IoT borda Olá executando Olá comando a seguir:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Verificar a instalação de saudação pelo exemplo de "Hello world" hello em execução. Este exemplo grava um arquivo de log. txt hello world mensagem toohello a cada cinco segundos. Olá, comandos a seguir executam hello "Hello world" exemplo:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Ignorar todas **argumento inválido** mensagens quando você interrompe o exemplo hello.

    Use Olá conteúdo de saudação do comando tooview saudação do arquivo de log a seguir:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Solucionar problemas

Se você receber o erro hello "nenhum pacote fornece util-linux-dev", tente reiniciar Olá NUC Intel.
