> [!div class="op_single_selector"]
> * [<span data-ttu-id="42107-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="42107-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="42107-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="42107-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="42107-103">C#</span><span class="sxs-lookup"><span data-stu-id="42107-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="42107-104">Java</span><span class="sxs-lookup"><span data-stu-id="42107-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="42107-105">Dispositivos gêmeos são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições).</span><span class="sxs-lookup"><span data-stu-id="42107-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="42107-106">IoT Hub mantém duas um dispositivo de cada dispositivo que se conecta tooit.</span><span class="sxs-lookup"><span data-stu-id="42107-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="42107-107">Use os dispositivos gêmeos para:</span><span class="sxs-lookup"><span data-stu-id="42107-107">Use device twins to:</span></span>

* <span data-ttu-id="42107-108">Armazene os metadados de dispositivo de seu back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="42107-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="42107-109">Relatar informações do estado atual como recursos disponíveis e condições (por exemplo, conectividade método hello usado) de seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="42107-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="42107-110">Sincronize o estado de saudação de fluxos de trabalho de longa execução (como atualizações de firmware e configuração) entre um aplicativo de dispositivo e um aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="42107-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="42107-111">Consultar os metadados, a configuração ou o estado do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="42107-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="42107-112">Dispositivos gêmeos são projetados para sincronização e para consultar condições e configurações de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="42107-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="42107-113">Para obter mais informações sobre quando toouse twins de dispositivo podem ser encontrados na [entender twins dispositivo][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="42107-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="42107-114">Dispositivos gêmeos são armazenados em um hub IoT e contêm:</span><span class="sxs-lookup"><span data-stu-id="42107-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="42107-115">*marcas*, metadados de dispositivo acessível somente por Olá solução back-end;</span><span class="sxs-lookup"><span data-stu-id="42107-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="42107-116">*propriedades desejadas*, objetos JSON pode ser modificados por solução Olá fazer final e observável pelo aplicativo de dispositivo Olá; e</span><span class="sxs-lookup"><span data-stu-id="42107-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="42107-117">*relatado propriedades*, objetos JSON modificáveis pelo aplicativo de dispositivo hello e legíveis pelo back-end de solução hello.</span><span class="sxs-lookup"><span data-stu-id="42107-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="42107-118">Marcas e propriedades não podem conter matrizes, mas objetos podem ser aninhados.</span><span class="sxs-lookup"><span data-stu-id="42107-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="42107-119">Além disso, back-end de solução Olá pode consultar twins de dispositivo com base em todos os Olá acima de dados.</span><span class="sxs-lookup"><span data-stu-id="42107-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="42107-120">Consulte também[entender twins dispositivo] [ lnk-twins] para obter mais informações sobre twins de dispositivo e toohello [linguagem de consulta de IoT Hub] [ lnk-query] referência para consultar.</span><span class="sxs-lookup"><span data-stu-id="42107-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="42107-121">Neste momento, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="42107-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="42107-122">Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="42107-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="42107-123">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="42107-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="42107-124">Criar um aplicativo de back-end que adiciona *marcas* tooa duas de dispositivo e um aplicativo de dispositivo simulado que relata a conectividade do canal como um *relatado propriedade* em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="42107-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="42107-125">Consultar dispositivos de seu aplicativo de back-end usando filtros nas marcas de saudação e propriedades criadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="42107-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md