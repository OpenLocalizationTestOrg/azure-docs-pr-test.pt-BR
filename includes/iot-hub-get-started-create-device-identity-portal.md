## <a name="create-a-device-identity"></a>Criar uma identidade do dispositivo

Nesta seção, você use Olá [portal do Azure] [ lnk-azure-portal] toocreate uma identidade de dispositivo no registro de identidade Olá em seu hub IoT. Um dispositivo não pode se conectar a tooIoT hub, a menos que ele tenha uma entrada no registro de identidade hello. Para obter mais informações, consulte a seção de "Registro de identidade" de saudação do hello [guia do desenvolvedor de IoT Hub][lnk-devguide-identity]. Olá **dispositivo Explorer** Olá o portal ajuda a você gerar uma identificação de dispositivo exclusivo e uma chave que seu dispositivo possa usar tooidentify em si, quando ele se conecta tooIoT Hub. As IDs de Dispositivo diferenciam maiúsculas de minúsculas.

1. Verifique se você está conectado no toohello [portal do Azure][lnk-azure-portal].

1. No hello Jumpbar, clique em **todos os recursos** e encontrar seu recurso de hub IoT.

    ![Navegue tooyour Iot hub][img-find-iothub]

1. Quando o recurso de hub IoT é aberto, clique em Olá **dispositivo Explorer** ferramenta e, em seguida, clique em **adicionar** na parte superior da saudação. Forneça nome Olá para o novo dispositivo, como **myDeviceId**e clique em **salvar**.

    ![Criar identidade do dispositivo no portal][img-create-device]

   Isso cria uma nova identidade do dispositivo para o Hub IoT.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. Em Olá **dispositivo Explorer**da lista de dispositivos, clique em dispositivo Olá recém-criado e anote Olá **cadeia de caracteres de Conexão---chave primária**. 

    ![Cadeia de conexão de dispositivo][img-connection-string]

> [!NOTE]
> Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable. Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual. Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo. Para saber mais, confira [Guia de Desenvolvedor do Hub IoT][lnk-devguide-identity].

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

