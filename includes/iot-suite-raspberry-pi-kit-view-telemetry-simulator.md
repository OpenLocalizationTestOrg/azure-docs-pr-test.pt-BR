## <a name="view-hello-telemetry"></a>Telemetria de saudação do modo de exibição

Olá framboesa Pi agora está enviando a solução de monitoramento remoto de toohello telemetria. Você pode exibir a telemetria de saudação no painel de solução de saudação. Você também pode enviar mensagens tooyour framboesa Pi no painel de solução de saudação.

- Navegue toohello painel de solução.
- Selecione o dispositivo em Olá **tooView dispositivo** lista suspensa.
- Telemetria de saudação do hello framboesa Pi exibe no painel de saudação.

![Telemetria de exibição de saudação framboesa Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Agir no dispositivo Olá

No painel de solução Olá, você pode chamar métodos em seu framboesa Pi. Quando Olá framboesa Pi conecta-se a solução de monitoramento remoto toohello, ele envia informações sobre métodos de saudação oferece suporte.

- No painel de solução de saudação, clique em **dispositivos** toovisit Olá **dispositivos** página. Selecione o Pi framboesa no hello **lista de dispositivos**. Depois, escolha **Métodos**:

    ![Listar dispositivos no painel][img-list-devices]

- Em Olá **invocar o método** escolha **LightBlink** em Olá **método** lista suspensa.

- Escolha **InvokeMethod**. simulador Olá imprime uma mensagem no console de saudação em Olá framboesa Pi. aplicativo Olá Olá framboesa Pi envia um painel de solução de backup toohello confirmação:

    ![Mostrar o histórico do método][img-method-history]

- Você pode alternar LED hello e desativar usando Olá **ChangeLightStatus** método com um **LightStatusValue** definido muito**1** para em ou **0** para off.

> [!WARNING]
> Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config]. Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md