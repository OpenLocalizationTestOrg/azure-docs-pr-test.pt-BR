> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c455-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c455-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="1c455-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="1c455-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="1c455-103">C#</span><span class="sxs-lookup"><span data-stu-id="1c455-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="1c455-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="1c455-104">Introduction</span></span>

<span data-ttu-id="1c455-105">Em [começar com twins de dispositivo do IoT Hub][lnk-twin-tutorial], você aprendeu como tooset metadados do dispositivo de volta a sua solução final usando *marcas*, reporte as condições de dispositivo de um aplicativo de dispositivo usando *relatado propriedades*e consultar essas informações usando uma linguagem SQL.</span><span class="sxs-lookup"><span data-stu-id="1c455-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="1c455-106">Neste tutorial, você aprenderá como toouse Olá do duas do dispositivo Olá *propriedades desejadas* juntamente com *relatado propriedades*, tooremotely configurar aplicativos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1c455-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="1c455-107">Mais especificamente, este tutorial mostra como uma duas de dispositivo relatado e propriedades desejadas habilite uma configuração de várias etapa de um aplicativo de dispositivo e fornecem Olá visibilidade toohello solução back-end de status Olá dessa operação em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1c455-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="1c455-108">Você pode encontrar mais informações sobre a função hello das configurações de dispositivo em [visão geral do gerenciamento de dispositivos com o IoT Hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="1c455-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="1c455-109">Em um nível alto, usar twins dispositivo habilita Olá solução back-end toospecify Olá desejado configuração para dispositivos Olá gerenciado, em vez de enviar comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="1c455-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="1c455-110">Isso coloca o dispositivo Olá responsável por configurar Olá melhor maneira tooupdate sua configuração (muito importante em cenários de IoT onde as condições de dispositivo específico afetam Olá capacidade tooimmediately executadas comandos específicos), ao relatar continuamente toohello solução novamente terminar o estado atual da saudação e possíveis condições de erro do processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c455-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="1c455-111">Esse padrão é toohello fundamental para o gerenciamento de grandes conjuntos de dispositivos, pois permite Olá solução back-end toohave visibilidade total do estado de saudação do processo de configuração de saudação em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1c455-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="1c455-112">Em cenários em que os dispositivos são controlados de forma mais interativa (ativar um ventilador por meio de um aplicativo controlado pelo usuário), considere usar [métodos diretos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="1c455-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="1c455-113">Neste tutorial, alterações de back-end de solução de saudação configuração de telemetria de saudação de um dispositivo de destino e, como resultado que, o aplicativo de dispositivo Olá segue um processo de várias etapas de tooapply uma configuração de atualização (por exemplo, que requerem a reinicialização de módulo de software, que esse tutorial simula com um atraso simple).</span><span class="sxs-lookup"><span data-stu-id="1c455-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="1c455-114">back-end de solução Olá armazena a configuração de saudação nas propriedades desejada do duas do dispositivo Olá Olá maneira a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c455-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="1c455-115">Como as configurações podem ser objetos complexos, elas geralmente são atribuídas ids exclusivas (hashes ou [GUIDs][lnk-guid]) toosimplify seus comparações.</span><span class="sxs-lookup"><span data-stu-id="1c455-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="1c455-116">aplicativo de dispositivo Hello relatórios sua configuração atual de espelhamento propriedade Olá desejado **telemetryConfig** no hello reportada propriedades:</span><span class="sxs-lookup"><span data-stu-id="1c455-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="1c455-117">Observe como Olá relatadas **telemetryConfig** tem uma propriedade adicional **status**, usado tooreport estado de saudação do processo de atualização de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c455-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="1c455-118">Quando uma nova configuração desejada é recebida, aplicativo de dispositivo Olá relata uma configuração pendente alterando Olá informações:</span><span class="sxs-lookup"><span data-stu-id="1c455-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="1c455-119">Em seguida, posteriormente, Olá dispositivo aplicativo será relatar Olá êxito ou falha dessa operação atualizando Olá acima de propriedade.</span><span class="sxs-lookup"><span data-stu-id="1c455-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="1c455-120">Observe como solução Olá back-end é a capacidade, a qualquer momento, o status de saudação tooquery do processo de configuração de saudação em todos os dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c455-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="1c455-121">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="1c455-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="1c455-122">Criar um aplicativo de dispositivo simulado que recebe atualizações de configuração de back-end de solução hello e relatórios de várias atualizações como *relatado propriedades* na configuração de saudação o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="1c455-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="1c455-123">Crie um aplicativo de back-end que atualizações Olá configuração desejada de um dispositivo e, em seguida, consultas Olá o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="1c455-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
