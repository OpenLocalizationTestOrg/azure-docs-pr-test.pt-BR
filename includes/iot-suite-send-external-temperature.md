## <a name="configure-hello-nodejs-simulated-device"></a>Configurar dispositivo simulado do hello Node. js
1. No painel de monitoramento remoto de saudação, clique em **+ adicionar um dispositivo** e, em seguida, adicione um *personalizadas de dispositivo*. Anote Olá IoT Hub hostname, a id de dispositivo e a chave do dispositivo. Você precisa-los posteriormente neste tutorial ao preparar o aplicativo de cliente de dispositivo de remote_monitoring.js hello.
2. Certifique-se de que o Node.js versão 0.12.x ou posterior esteja instalado no computador de desenvolvimento. Executar `node --version` em um prompt de comando ou em uma versão de saudação do shell toocheck. Para obter informações sobre como usar um Gerenciador de pacote tooinstall Node. js no Linux, consulte [Node. js instalando por meio do Gerenciador de pacote][node-linux].
3. Quando você tiver instalado o Node. js, clonar a versão mais recente de saudação do hello [azure iot-sdk-nó] [ lnk-github-repo] máquina de desenvolvimento tooyour de repositório. Sempre use Olá **mestre** ramificação para a versão mais recente Olá das bibliotecas de saudação e exemplos.
4. A cópia local da saudação de [azure iot-sdk-nó] [ lnk-github-repo] repositório, Olá cópia seguir dois arquivos de saudação exemplos/de dispositivo de nó tooan vazio pasta no computador de desenvolvimento:
   
   * packages.json
   * remote_monitoring.js
5. Abra o arquivo de remote_monitoring.js hello e procure Olá após a definição da variável:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Substitua a **[cadeia de conexão de dispositivo do Hub IoT]** pela cadeia de conexão do seu dispositivo. Use valores de saudação para o nome de host IoT Hub, id do dispositivo e a chave do dispositivo que você tenha um anotado na etapa 1. Uma cadeia de caracteres de conexão do dispositivo tem Olá formato a seguir:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Se o nome de host do IoT Hub é **contoso** e a id do dispositivo é **meudispositivo**, sua cadeia de caracteres de conexão parece Olá trecho de código a seguir:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Salve o arquivo hello. Execute Olá comandos em um shell ou o prompt de comando na pasta Olá que contém os pacotes necessários do tooinstall Olá esses arquivos a seguir e, em seguida, execute o aplicativo de exemplo hello:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Observe a telemetria dinâmica em ação
painel Olá mostra a telemetria de temperatura e umidade Olá de dispositivos simuladas existentes de saudação:

![Painel de padrão de saudação][image1]

Se você selecionar dispositivo simulado do Node. js Olá que você executou na seção anterior hello, consulte temperatura, umidade e telemetria temperatura externa:

![Adicionar painel de toohello temperatura externa][image2]

solução de monitoramento remoto Olá automaticamente detecta Olá adicionais temperatura externa telemetria tipo e o adiciona toohello gráfico no painel de saudação.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png