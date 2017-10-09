## <a name="customize-and-extend-hello-device-management-actions"></a>Personalizar e estender ações de gerenciamento de dispositivo Olá

Suas soluções IoT podem expandir Olá definido pelo conjunto de padrões de gerenciamento de dispositivo ou habilite padrões personalizados usando duas de dispositivo hello e primitivos de método de nuvem para dispositivo. Outros exemplos de ações de gerenciamento do dispositivo incluem a redefinição de fábrica, atualização do firmware, atualização do software, gerenciamento de energia, gerenciamento da rede e da conectividade, e criptografia dos dados.

## <a name="device-maintenance-windows"></a>Janelas de manutenção do dispositivo

Normalmente, configure as ações de tooperform de dispositivos em um horário que minimiza interrupções e tempo de inatividade. Janelas de manutenção do dispositivo são um tempo de saudação toodefine padrão usadas quando um dispositivo deve atualizar sua configuração. As soluções de back-end podem usar propriedades de saudação desejada de saudação dispositivo duas toodefine e ativar uma política em seu dispositivo que permite que uma janela de manutenção. Quando um dispositivo recebe a política de janela de manutenção hello, ele pode usar Olá relatado propriedade Olá status do dispositivo duas tooreport Olá da política de saudação. aplicativo de back-end Olá pode usar dispositivo duas consultas tooattest toocompliance de dispositivos e de cada política.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você usou um método direto de tootrigger uma reinicialização remota em um dispositivo. Você Olá usadas propriedades relatado tooreport Olá reinicializar última hora do dispositivo hello e saudação do hello consultado dispositivo duas toodiscover reinicializar última hora do dispositivo de saudação da nuvem de saudação.

toocontinue guia de Introdução ao IoT Hub e padrões de gerenciamento de dispositivo como remoto pela atualização de firmware de ar hello, consulte:

[Tutorial: Como toodo um atualização do firmware][lnk-fwupdate]

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

toocontinue guia de Introdução ao IoT Hub, consulte [guia de Introdução com borda IoT][lnk-iot-edge].

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md