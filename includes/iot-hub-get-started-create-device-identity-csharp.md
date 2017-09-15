## <a name="create-a-device-identity"></a><span data-ttu-id="27b24-101">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="27b24-101">Create a device identity</span></span>
<span data-ttu-id="27b24-102">Nesta seção, você cria um aplicativo do console do .NET que cria uma identidade do dispositivo no registro de identidade em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27b24-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="27b24-103">Um dispositivo não pode se conectar ao Hub IoT, a menos que ele tenha uma entrada no Registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="27b24-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="27b24-104">Para obter mais informações, consulte a seção "Registro de identidade" do [Guia do Desenvolvedor do Hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="27b24-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="27b24-105">Quando você executar esse aplicativo de console, ele irá gerar uma ID e chave do dispositivo exclusivas com as quais seu dispositivo poderá identificar-se ao enviar mensagens entre o dispositivo e a nuvem para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27b24-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="27b24-106">As IDs de Dispositivo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="27b24-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="27b24-107">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# a uma nova solução usando o modelo de projeto **Aplicativo do Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="27b24-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="27b24-108">Verifique se a versão do .NET Framework é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="27b24-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="27b24-109">Nomeie o projeto **CreateDeviceIdentity** e a solução **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="27b24-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10]
2. <span data-ttu-id="27b24-111">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **CreateDeviceIdentity** e clique em **Gerenciar Pacotes Nuget**.</span><span class="sxs-lookup"><span data-stu-id="27b24-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="27b24-112">Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="27b24-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="27b24-113">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="27b24-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][11]
4. <span data-ttu-id="27b24-115">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="27b24-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="27b24-116">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="27b24-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="27b24-117">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="27b24-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="27b24-118">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="27b24-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="27b24-119">Esse método cria uma identidade do dispositivo com a ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="27b24-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="27b24-120">(se essa ID do dispositivo já existir no registro de identidade, o código simplesmente irá recuperar as informações do dispositivo existentes.) Em seguida, o aplicativo exibe a chave primária dessa identidade.</span><span class="sxs-lookup"><span data-stu-id="27b24-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="27b24-121">Você usa essa chave no aplicativo de dispositivo simulado para se conectar ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27b24-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="27b24-122">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="27b24-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="27b24-123">Execute este aplicativo e anote a chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27b24-123">Run this application, and make a note of the device key.</span></span>
   
    ![Chave do dispositivo gerada pelo aplicativo][12]

> [!NOTE]
> <span data-ttu-id="27b24-125">O Registro de identidade do Hub IoT armazena apenas as identidades de dispositivo para habilitar o acesso seguro ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27b24-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="27b24-126">Ele armazena as IDs e as chaves do dispositivo a usar como credenciais de segurança e um sinalizador habilitado/desabilitado que você poderá usar para desabilitar o acesso de um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="27b24-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="27b24-127">Se seu aplicativo precisar armazenar outros metadados específicos do dispositivo, ele deverá usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27b24-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="27b24-128">Para saber mais, confira [Guia de Desenvolvedor do Hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="27b24-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
