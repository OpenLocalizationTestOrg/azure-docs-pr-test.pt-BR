## <a name="create-a-device-identity"></a><span data-ttu-id="7653e-101">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="7653e-101">Create a device identity</span></span>
<span data-ttu-id="7653e-102">Nesta seção, você deve criar um aplicativo de console .NET que cria uma identidade de dispositivo no registro de identidade Olá em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7653e-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="7653e-103">Um dispositivo não pode se conectar a tooIoT hub, a menos que ele tenha uma entrada no registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="7653e-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="7653e-104">Para obter mais informações, consulte a seção de "Registro de identidade" de saudação do hello [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="7653e-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="7653e-105">Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7653e-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="7653e-106">As IDs de Dispositivo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="7653e-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="7653e-107">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto tooa novo usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="7653e-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="7653e-108">Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7653e-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="7653e-109">Projeto de saudação do nome **CreateDeviceIdentity** e solução de saudação do nome **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="7653e-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10]
2. <span data-ttu-id="7653e-111">No Gerenciador de soluções, clique com botão direito Olá **CreateDeviceIdentity** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7653e-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="7653e-112">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="7653e-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="7653e-113">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="7653e-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][11]
4. <span data-ttu-id="7653e-115">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="7653e-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="7653e-116">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="7653e-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7653e-117">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="7653e-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="7653e-118">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="7653e-118">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="7653e-119">Esse método cria uma identidade do dispositivo com a ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="7653e-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="7653e-120">(Se esse ID de dispositivo já existe no registro de identidade Olá, código de saudação simplesmente recupera informações de dispositivo existentes hello.) aplicativo Hello, em seguida, exibe a chave primária Olá para essa identidade.</span><span class="sxs-lookup"><span data-stu-id="7653e-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="7653e-121">Você pode usar essa chave Olá simulado dispositivo aplicativo tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7653e-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="7653e-122">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="7653e-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="7653e-123">Executar este aplicativo e tome nota da chave de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7653e-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Chave de dispositivo gerado pelo aplicativo hello][12]

> [!NOTE]
> <span data-ttu-id="7653e-125">Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable.</span><span class="sxs-lookup"><span data-stu-id="7653e-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="7653e-126">Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="7653e-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="7653e-127">Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7653e-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="7653e-128">Para saber mais, confira [Guia de Desenvolvedor do Hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="7653e-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
