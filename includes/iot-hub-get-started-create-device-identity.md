## <a name="create-a-device-identity"></a>Criar uma identidade do dispositivo

Nesta seção, você usar uma ferramenta de Node.js chamada [Gerenciador de Hub IOT] [ iot-hub-explorer] toocreate uma identidade de dispositivo para este tutorial. As IDs de Dispositivo diferenciam maiúsculas de minúsculas.

1. Execute o seguinte de saudação em seu ambiente de linha de comando:

    `npm install -g iothub-explorer@latest`

1. Em seguida, execute Olá hub do comando toologin tooyour a seguir. Substituir `{iot hub connection string}` com hello cadeia de caracteres de conexão de IoT Hub copiou anteriormente:

    `iothub-explorer login "{iot hub connection string}"`

1. Finalmente, crie uma nova identidade de dispositivo chamada `myDeviceId` com o comando hello:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Anote uma cadeia de caracteres de conexão de dispositivo a saudação do resultado de saudação. Essa cadeia de caracteres de conexão do dispositivo é usada pelo Olá dispositivo aplicativo tooconnect tooyour IoT Hub como um dispositivo.

![][img-identity]

Consulte também[guia de Introdução ao IoT Hub] [ lnk-getstarted] tooprogrammatically criar identidades de dispositivo.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
