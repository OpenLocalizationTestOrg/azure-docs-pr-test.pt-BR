## <a name="create-a-device-identity"></a><span data-ttu-id="fa7e5-101">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="fa7e5-101">Create a device identity</span></span>

<span data-ttu-id="fa7e5-102">Nesta seção, você usar uma ferramenta de Node.js chamada [Gerenciador de Hub IOT] [ iot-hub-explorer] toocreate uma identidade de dispositivo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fa7e5-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="fa7e5-103">As IDs de Dispositivo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fa7e5-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="fa7e5-104">Execute o seguinte de saudação em seu ambiente de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="fa7e5-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="fa7e5-105">Em seguida, execute Olá hub do comando toologin tooyour a seguir.</span><span class="sxs-lookup"><span data-stu-id="fa7e5-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="fa7e5-106">Substituir `{iot hub connection string}` com hello cadeia de caracteres de conexão de IoT Hub copiou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="fa7e5-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="fa7e5-107">Finalmente, crie uma nova identidade de dispositivo chamada `myDeviceId` com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="fa7e5-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="fa7e5-108">Anote uma cadeia de caracteres de conexão de dispositivo a saudação do resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa7e5-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="fa7e5-109">Essa cadeia de caracteres de conexão do dispositivo é usada pelo Olá dispositivo aplicativo tooconnect tooyour IoT Hub como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fa7e5-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="fa7e5-110">Consulte também[guia de Introdução ao IoT Hub] [ lnk-getstarted] tooprogrammatically criar identidades de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fa7e5-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
