## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="395dd-101">Especificar o comportamento de saudação do dispositivo de IoT Olá</span><span class="sxs-lookup"><span data-stu-id="395dd-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="395dd-102">Olá biblioteca de cliente do serializador de IoT Hub usa um formato de saudação do toospecify de modelo de trocas de dispositivo de saudação de mensagens de saudação com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="395dd-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="395dd-103">Adicionar Olá declarações de variáveis a seguir após Olá `#include` instruções.</span><span class="sxs-lookup"><span data-stu-id="395dd-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="395dd-104">Substituir valores de espaço reservado de saudação [Id do dispositivo] e [chave do dispositivo] com valores anotados para seu dispositivo no painel solução de monitoramento remoto hello.</span><span class="sxs-lookup"><span data-stu-id="395dd-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="395dd-105">Use Olá Hostname de Hub IoT do hello solução painel tooreplace [nome do hub IOT].</span><span class="sxs-lookup"><span data-stu-id="395dd-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="395dd-106">Por exemplo, se o nome de host do Hub IoT for **contoso.azure-devices.net**, substitua [Nome do HubIoT] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="395dd-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="395dd-107">Adicione Olá seguindo o modelo de saudação do código toodefine que permite Olá toocommunicate de dispositivo com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="395dd-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="395dd-108">Esse modelo especifica que o dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="395dd-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="395dd-109">Pode enviar temperatura, temperatura externa, umidade e uma ID de dispositivo como telemetria.</span><span class="sxs-lookup"><span data-stu-id="395dd-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="395dd-110">Pode enviar metadados sobre Olá dispositivo tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="395dd-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="395dd-111">dispositivo Olá envia os metadados básicos em um **DeviceInfo** objeto durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="395dd-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="395dd-112">Pode enviar propriedades relatadas, toohello duas de dispositivo no IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="395dd-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="395dd-113">Essas propriedades relatadas são agrupadas em propriedades de configuração, do dispositivo e do sistema.</span><span class="sxs-lookup"><span data-stu-id="395dd-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="395dd-114">Pode receber e agir sobre as propriedades desejadas definidas em duas de dispositivo Olá no IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="395dd-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="395dd-115">Pode responder toohello **reinicializar** e **InitiateFirmwareUpdate** direcionar os métodos invocados por meio do portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="395dd-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="395dd-116">dispositivo Olá envia informações sobre métodos diretos Olá ele dá suporte ao uso de propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="395dd-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="395dd-117">Implementar o comportamento de saudação do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="395dd-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="395dd-118">Agora adicione o código que implementa o comportamento de saudação definido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="395dd-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="395dd-119">Adicione Olá funções que lidam com propriedades de saudação desejada definidas no painel de solução Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="395dd-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="395dd-120">Essas propriedades desejadas são definidas no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="395dd-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="395dd-121">Adicione Olá funções que lidam com métodos diretos de saudação invocados por meio de hub IoT de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="395dd-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="395dd-122">Esses métodos diretos são definidos no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="395dd-122">These direct methods are defined in hello model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="395dd-123">Adicione Olá função que envia uma solução de toohello pré-configurado de mensagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="395dd-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="395dd-124">Adicione Olá manipulador de retorno de chamada que é executado quando o dispositivo Olá enviou novos valores de propriedade relatado toohello pré-configurado solução a seguir:</span><span class="sxs-lookup"><span data-stu-id="395dd-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="395dd-125">Adicione Olá seguinte função tooconnect sua solução de toohello pré-configurado do dispositivo na nuvem hello e troca de dados.</span><span class="sxs-lookup"><span data-stu-id="395dd-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="395dd-126">Esta função executa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="395dd-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="395dd-127">Inicializa a plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="395dd-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="395dd-128">Registra Olá Contoso namespace com biblioteca de serialização hello.</span><span class="sxs-lookup"><span data-stu-id="395dd-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="395dd-129">Inicializa um cliente Olá com a cadeia de caracteres de conexão de dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="395dd-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="395dd-130">Criar uma instância de saudação **termostato** modelo.</span><span class="sxs-lookup"><span data-stu-id="395dd-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="395dd-131">Cria e envia os valores de propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="395dd-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="395dd-132">Envia um objeto **DeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="395dd-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="395dd-133">Cria uma telemetria de toosend loop a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="395dd-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="395dd-134">Realiza o desligamento de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="395dd-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="395dd-135">Para referência, aqui está um exemplo **telemetria** toohello mensagem enviada pré-configurado solução:</span><span class="sxs-lookup"><span data-stu-id="395dd-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```