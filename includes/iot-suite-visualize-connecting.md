## <a name="view-device-telemetry-in-hello-dashboard"></a>Telemetria de dispositivo de exibição no painel de saudação
Painel de saudação em Olá habilita solução telemetria Olá tooview seus dispositivos enviam tooIoT Hub de monitoramento remoto.

1. No navegador, toohello retorno remoto solução painel de monitoramento, clique em **dispositivos** em Olá painel esquerdo toonavigate toohello **lista de dispositivos**.
2. Em Olá **lista de dispositivos**, você verá que o status de saudação do dispositivo é **executando**. Se não estiver, clique em **Ativar dispositivo** em Olá **detalhes do dispositivo** painel.
   
    ![Exibir status do dispositivo][18]
3. Clique em **painel** tooreturn toohello painel, selecione seu dispositivo no hello **tooView dispositivo** suspensa tooview sua telemetria. Telemetria de saudação do aplicativo de exemplo hello é 50 unidades de temperatura interna, 55 unidades de temperatura externa e 50 unidades para umidade.
   
    ![Exibir telemetria de dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Invocar um método no seu dispositivo
painel Olá na solução de monitoramento remoto Olá permite tooinvoke métodos em seus dispositivos por meio de IoT Hub. Por exemplo, no hello solução de monitoramento remoto, você pode invocar toosimulate um método que a reinicialização de um dispositivo.

1. Olá remoto monitoramento solução painel, clique em **dispositivos** em Olá painel esquerdo toonavigate toohello **lista de dispositivos**.
2. Clique em **ID do dispositivo** para seu dispositivo no hello **lista de dispositivos**.
3. Em Olá **detalhes do dispositivo** do painel, clique em **métodos**.
   
    ![Métodos do dispositivo][13]
4. Em Olá **método** lista suspensa, selecione **InitiateFirmwareUpdate**e, em seguida, em **FWPACKAGEURI** insira uma URL fictícia. Clique em **invocar o método** toocall método hello dispositivo hello.
   
    ![Invocar um método do dispositivo][14]
   

5. Você verá uma mensagem no console de saudação executar o código do dispositivo quando o dispositivo Olá manipula método hello. resultados de saudação do método hello são adicionados toohello histórico no portal de solução de saudação:

    ![Exibir o histórico do método][img-method-history]

## <a name="next-steps"></a>Próximas etapas
artigo Olá [soluções pré-configuradas de personalização] [ lnk-customize] descreve algumas maneiras que você pode estender esse exemplo. Extensões possíveis incluem usar sensores reais e implementar comandos adicionais.

Você pode aprender mais sobre Olá [permissões no site do hello azureiotsuite.com][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
