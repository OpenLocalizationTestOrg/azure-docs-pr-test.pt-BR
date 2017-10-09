## <a name="create-a-device-identity"></a>Criar uma identidade do dispositivo
Nesta seção, você deve criar um aplicativo de console .NET que cria uma identidade de dispositivo no registro de identidade Olá em seu hub IoT. Um dispositivo não pode se conectar a tooIoT hub, a menos que ele tenha uma entrada no registro de identidade hello. Para obter mais informações, consulte a seção de "Registro de identidade" de saudação do hello [guia do desenvolvedor de IoT Hub][lnk-devguide-identity]. Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub. As IDs de Dispositivo diferenciam maiúsculas de minúsculas.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto tooa novo usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior. Projeto de saudação do nome **CreateDeviceIdentity** e solução de saudação do nome **IoTHubGetStarted**.
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10]
2. No Gerenciador de soluções, clique com botão direito Olá **CreateDeviceIdentity** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
3. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.
   
    ![Janela do Gerenciador de Pacotes NuGet][11]
4. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Adicionar Olá após o método toohello **programa** classe:
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    Esse método cria uma identidade do dispositivo com a ID **myFirstDevice**. (Se esse ID de dispositivo já existe no registro de identidade Olá, código de saudação simplesmente recupera informações de dispositivo existentes hello.) aplicativo Hello, em seguida, exibe a chave primária Olá para essa identidade. Você pode usar essa chave Olá simulado dispositivo aplicativo tooconnect tooyour IoT hub.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Executar este aplicativo e tome nota da chave de dispositivo de saudação.
   
    ![Chave de dispositivo gerado pelo aplicativo hello][12]

> [!NOTE]
> Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable. Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual. Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo. Para saber mais, confira [Guia de Desenvolvedor do Hub IoT][lnk-devguide-identity].
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
