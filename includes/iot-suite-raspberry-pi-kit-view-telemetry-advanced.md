## <a name="view-hello-telemetry"></a>Telemetria de saudação do modo de exibição

Olá framboesa Pi agora está enviando a solução de monitoramento remoto de toohello telemetria. Você pode exibir a telemetria de saudação no painel de solução de saudação. Você também pode enviar mensagens tooyour framboesa Pi no painel de solução de saudação.

- Navegue toohello painel de solução.
- Selecione o dispositivo em Olá **tooView dispositivo** lista suspensa.
- Telemetria de saudação do hello framboesa Pi exibe no painel de saudação.

![Telemetria de exibição de saudação framboesa Pi][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Inicie a atualização de firmware Olá

processo de atualização de firmware Olá baixa e instala uma versão atualizada do aplicativo de cliente de dispositivo hello no hello framboesa Pi. Para obter mais informações sobre o processo de atualização de firmware Olá, consulte a descrição de saudação do padrão de atualização de firmware de saudação em [visão geral do gerenciamento de dispositivos com o IoT Hub][lnk-update-pattern].

Iniciar o processo de atualização de firmware Olá invocando um método no dispositivo de saudação. Esse método é assíncrono e retorna assim que o processo de atualização Olá começa. Olá dispositivo usa relatado solução de saudação toonotify propriedades sobre o progresso de saudação de atualização de saudação.

Invocar métodos em seu Pi framboesa do painel de solução de saudação. Quando Olá framboesa Pi primeiro se conecta a solução de monitoramento remoto toohello, ele envia informações sobre métodos de saudação oferece suporte. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
