> [!div class="op_single_selector"]
> * [<span data-ttu-id="939d3-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="939d3-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="939d3-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="939d3-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="939d3-103">C#</span><span class="sxs-lookup"><span data-stu-id="939d3-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="939d3-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="939d3-104">Introduction</span></span>

<span data-ttu-id="939d3-105">Em [Introdução a dispositivos gêmeos do Hub IoT][lnk-twin-tutorial], você aprendeu a definir metadados de dispositivo do back-end de solução usando *marcas*, relatar as condições de dispositivo de um aplicativo de dispositivo usando *propriedades relatadas* e consultar essas informações usando uma linguagem semelhante a SQL.</span><span class="sxs-lookup"><span data-stu-id="939d3-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how to set device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="939d3-106">Neste tutorial, você aprenderá a usar as *propriedades desejadas* do dispositivo gêmeo juntamente com as *propriedades relatadas*, para configurar os remotamente os aplicativos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="939d3-106">In this tutorial, you will learn how to use the the device twin's *desired properties* along with *reported properties*, to remotely configure device apps.</span></span> <span data-ttu-id="939d3-107">Mais especificamente, este tutorial mostra como as propriedades relatadas e desejadas de um dispositivo gêmeo habilitam uma configuração de várias etapas de um aplicativo de dispositivo e fornecem a visibilidade para o back-end de solução do status da operação em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="939d3-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide the visibility to the solution back end of the status of this operation across all devices.</span></span> <span data-ttu-id="939d3-108">Você pode encontrar mais informações sobre a função das configurações do dispositivo em [Visão geral do gerenciamento de dispositivos com o Hub IoT][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="939d3-108">You can find more information regarding the role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="939d3-109">Em um nível elevado, usar dispositivos gêmeos permite que o back-end de solução especifique as configurações desejadas para os dispositivos gerenciados, em vez de enviar comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="939d3-109">At a high level, using device twins enables the solution back end to specify the desired configuration for the managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="939d3-110">Isso faz com que o dispositivo seja responsável por definir a melhor maneira de atualizar sua configuração (muito importante em cenários de IoT em que condições específicas de dispositivo afetam a capacidade de executar imediatamente comandos específicos), enquanto relata continuamente para o back-end da solução o estado atual e possíveis condições de erro do processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="939d3-110">This puts the device in charge of setting up the best way to update its configuration (very important in IoT scenarios where specific device conditions affect the ability to immediately carry out specific commands), while continually reporting to the solution back end the current state and potential error conditions of the update process.</span></span> <span data-ttu-id="939d3-111">Esse padrão é fundamental para o gerenciamento de grandes conjuntos de dispositivos, pois ele permite que o back-end da solução tenha visibilidade total do estado do processo de configuração em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="939d3-111">This pattern is instrumental to the management of large sets of devices, as it enables the solution back end to have full visibility of the state of the configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="939d3-112">Em cenários em que os dispositivos são controlados de forma mais interativa (ativar um ventilador por meio de um aplicativo controlado pelo usuário), considere usar [métodos diretos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="939d3-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="939d3-113">Neste tutorial, o back-end de solução altera a configuração de telemetria de um dispositivo de destino e, como resultado disso, o aplicativo do dispositivo segue um processo de várias etapas para aplicar uma atualização de configuração (por exemplo, exigir a reinicialização de um módulo de software, que este tutorial simula com um atraso simples).</span><span class="sxs-lookup"><span data-stu-id="939d3-113">In this tutorial, the solution back end changes the telemetry configuration of a target device and, as a result of that, the device app follows a multi-step process to apply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="939d3-114">O back-end de solução armazena a configuração nas propriedades desejadas do gêmeo do dispositivo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="939d3-114">The solution back end stores the configuration in the device twin's desired properties in the following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of the configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="939d3-115">Como as configurações podem ser objetos complexos, geralmente são atribuídos a IDs exclusivas (hashes ou [GUIDs][lnk-guid]) para simplificar suas comparações.</span><span class="sxs-lookup"><span data-stu-id="939d3-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) to simplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="939d3-116">O aplicativo do dispositivo relata sua configuração atual espelhando a propriedade desejada **telemetryConfig** nas propriedades relatadas:</span><span class="sxs-lookup"><span data-stu-id="939d3-116">The device app reports its current configuration mirroring the desired property **telemetryConfig** in the reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="939d3-117">Observe como o relatório **telemetryConfig** tem uma propriedade adicional **status**, usada para relatar o estado do processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="939d3-117">Note how the reported **telemetryConfig** has an additional property **status**, used to report the state of the configuration update process.</span></span>

<span data-ttu-id="939d3-118">Quando uma nova configuração desejada é recebida, o aplicativo de dispositivo relata uma configuração pendente alterando as informações:</span><span class="sxs-lookup"><span data-stu-id="939d3-118">When a new desired configuration is received, the device app reports a pending configuration by changing the information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of the pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="939d3-119">Em seguida, posteriormente, o aplicativo do dispositivo relatará o sucesso ou a falha dessa operação atualizando a propriedade acima.</span><span class="sxs-lookup"><span data-stu-id="939d3-119">Then, at some later time, the device app will report the success or failure of this operation by updating the above property.</span></span>
<span data-ttu-id="939d3-120">Observe como o back-end da solução é capaz de, a qualquer momento, consultar o status do processo de configuração em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="939d3-120">Note how the solution back end is able, at any time, to query the status of the configuration process across all the devices.</span></span>

<span data-ttu-id="939d3-121">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="939d3-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="939d3-122">Criar um aplicativo de dispositivo simulado que recebe atualizações de configuração de back-end da solução e relata várias atualizações como *propriedades relatadas* no processo de atualização da configuração.</span><span class="sxs-lookup"><span data-stu-id="939d3-122">Create a simulated device app that receives configuration updates from the solution back end, and reports multiple updates as *reported properties* on the configuration update process.</span></span>
* <span data-ttu-id="939d3-123">Crie um aplicativo de back-end que atualiza a configuração desejada de um dispositivo e consulta o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="939d3-123">Create a back-end app that updates the desired configuration of a device, and then queries the configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
