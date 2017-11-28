## <a name="specify-the-behavior-of-the-iot-device"></a><span data-ttu-id="59396-101">Especificar o comportamento do dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="59396-101">Specify the behavior of the IoT device</span></span>

<span data-ttu-id="59396-102">A biblioteca de cliente do serializador Hub IoT usa um modelo para especificar o formato das mensagens que o dispositivo troca com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59396-102">The IoT Hub serializer client library uses a model to specify the format of the messages the device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="59396-103">Adicione as declarações de variável a seguir após as instruções `#include` .</span><span class="sxs-lookup"><span data-stu-id="59396-103">Add the following variable declarations after the `#include` statements.</span></span> <span data-ttu-id="59396-104">Substitua os valores do espaço reservado [Device Id] e [Device Key] pelos valores que você anotou para o seu dispositivo no painel da solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="59396-104">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="59396-105">Use o nome de host do Hub IoT do painel da solução para substituir [IoTHub Name].</span><span class="sxs-lookup"><span data-stu-id="59396-105">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="59396-106">Por exemplo, se o nome de host do Hub IoT for **contoso.azure-devices.net**, substitua [Nome do HubIoT] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="59396-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="59396-107">Adicione o código a seguir para definir o modelo que permite ao dispositivo se comunicar com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59396-107">Add the following code to define the model that enables the device to communicate with IoT Hub.</span></span> <span data-ttu-id="59396-108">Esse modelo especifica que o dispositivo:</span><span class="sxs-lookup"><span data-stu-id="59396-108">This model specifies that the device:</span></span>

   - <span data-ttu-id="59396-109">Pode enviar temperatura, temperatura externa, umidade e uma ID de dispositivo como telemetria.</span><span class="sxs-lookup"><span data-stu-id="59396-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="59396-110">Pode enviar metadados sobre o dispositivo para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59396-110">Can send metadata about the device to IoT Hub.</span></span> <span data-ttu-id="59396-111">O dispositivo envia metadados básicos em um objeto **DeviceInfo** durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="59396-111">The device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="59396-112">Pode enviar propriedades relatadas para o dispositivo gêmeo no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59396-112">Can send reported properties, to the device twin in IoT Hub.</span></span> <span data-ttu-id="59396-113">Essas propriedades relatadas são agrupadas em propriedades de configuração, do dispositivo e do sistema.</span><span class="sxs-lookup"><span data-stu-id="59396-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="59396-114">Pode receber e agir em propriedades desejadas definidas no dispositivo gêmeo no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59396-114">Can receive and act on desired properties set in the device twin in IoT Hub.</span></span>
   - <span data-ttu-id="59396-115">Pode responder aos métodos diretos **Reboot** e **InitiateFirmwareUpdate** invocados por meio do portal da solução.</span><span class="sxs-lookup"><span data-stu-id="59396-115">Can respond to the **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through the solution portal.</span></span> <span data-ttu-id="59396-116">O dispositivo envia informações sobre os métodos diretos aos quais ele dá suporte, usando propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="59396-116">The device sends information about the direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define the Model
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

      /* Direct methods implemented by the device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-the-behavior-of-the-device"></a><span data-ttu-id="59396-117">Implementar o comportamento do dispositivo</span><span class="sxs-lookup"><span data-stu-id="59396-117">Implement the behavior of the device</span></span>
<span data-ttu-id="59396-118">Agora adicione o código que implementa o comportamento definido no modelo.</span><span class="sxs-lookup"><span data-stu-id="59396-118">Now add code that implements the behavior defined in the model.</span></span>

1. <span data-ttu-id="59396-119">Adicione as seguintes funções que lidam com as propriedades desejadas definidas no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="59396-119">Add the following functions that handle the desired properties set in the solution dashboard.</span></span> <span data-ttu-id="59396-120">Essas propriedades desejadas são definidas no modelo:</span><span class="sxs-lookup"><span data-stu-id="59396-120">These desired properties are defined in the model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of the type of the MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of the type of the MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="59396-121">Adicione as seguintes funções que lidam com os métodos diretos invocados por meio do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59396-121">Add the following functions that handle the direct methods invoked through the IoT hub.</span></span> <span data-ttu-id="59396-122">Esses métodos diretos são definidos no modelo:</span><span class="sxs-lookup"><span data-stu-id="59396-122">These direct methods are defined in the model:</span></span>

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

1. <span data-ttu-id="59396-123">Adicione a seguinte função que envia uma mensagem para a solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="59396-123">Add the following function that sends a message to the preconfigured solution:</span></span>
   
    ```c
    /* Send data to IoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable to create a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted the message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="59396-124">Adicione o seguinte manipulador de retorno de chamada que é executado quando o dispositivo envia novos valores de propriedade relatados à solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="59396-124">Add the following callback handler that runs when the device has sent new reported property values to the preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="59396-125">Adicione a seguinte função para conectar o dispositivo à solução pré-configurada na nuvem e trocar dados.</span><span class="sxs-lookup"><span data-stu-id="59396-125">Add the following function to connect your device to the preconfigured solution in the cloud, and exchange data.</span></span> <span data-ttu-id="59396-126">Esta função realiza as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="59396-126">This function performs the following steps:</span></span>

    - <span data-ttu-id="59396-127">Inicializa a plataforma.</span><span class="sxs-lookup"><span data-stu-id="59396-127">Initializes the platform.</span></span>
    - <span data-ttu-id="59396-128">Registra o namespace da Contoso na biblioteca de serialização.</span><span class="sxs-lookup"><span data-stu-id="59396-128">Registers the Contoso namespace with the serialization library.</span></span>
    - <span data-ttu-id="59396-129">Inicializa o cliente com a cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="59396-129">Initializes the client with the device connection string.</span></span>
    - <span data-ttu-id="59396-130">Cria uma instância do modelo **Termostato**.</span><span class="sxs-lookup"><span data-stu-id="59396-130">Create an instance of the **Thermostat** model.</span></span>
    - <span data-ttu-id="59396-131">Cria e envia os valores de propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="59396-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="59396-132">Envia um objeto **DeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="59396-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="59396-133">Cria um loop para enviar telemetria a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="59396-133">Creates a loop to send telemetry every second.</span></span>
    - <span data-ttu-id="59396-134">Realiza o desligamento de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="59396-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed to initialize the platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable to SERIALIZER_REGISTER_NAMESPACE\n");
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
              // For mbed add the certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed to set option \"TrustedCerts\"\n");
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
                /* Specify the signatures of the supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot the device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file\"}";

                /* Send reported properties to IoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object to IoT Hub at startup\n");
      
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
   
    <span data-ttu-id="59396-135">Para referência, aqui está um exemplo de mensagem de **Telemetria** enviada à solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="59396-135">For reference, here is a sample **Telemetry** message sent to the preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```