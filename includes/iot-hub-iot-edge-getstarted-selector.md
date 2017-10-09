> [!div class="op_single_selector"]
> * [<span data-ttu-id="db2df-101">Linux</span><span class="sxs-lookup"><span data-stu-id="db2df-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="db2df-102">Windows</span><span class="sxs-lookup"><span data-stu-id="db2df-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="db2df-103">Este artigo fornece uma explicação detalhada de saudação [código de exemplo Hello World] [ lnk-helloworld-sample] tooillustrate componentes fundamentais do hello de saudação [Azure IoT borda] [ lnk-iot-edge] arquitetura.</span><span class="sxs-lookup"><span data-stu-id="db2df-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="db2df-104">Olá exemplo usa hello Azure IoT borda toobuild um gateway simple que registra um arquivo de tooa de mensagem "hello world" a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="db2df-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="db2df-105">Este passo a passo aborda:</span><span class="sxs-lookup"><span data-stu-id="db2df-105">This walkthrough covers:</span></span>

* <span data-ttu-id="db2df-106">**Olá arquitetura de exemplo do mundo**: descreve como [conceitos de arquitetura do Azure IoT borda] [ lnk-edge-concepts] aplicar toohello exemplo de Hello World e como os componentes de saudação se encaixam.</span><span class="sxs-lookup"><span data-stu-id="db2df-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="db2df-107">**Como toobuild Olá exemplo**: exemplo de saudação do hello etapas toobuild necessária.</span><span class="sxs-lookup"><span data-stu-id="db2df-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="db2df-108">**Como toorun Olá exemplo**: exemplo de saudação do hello etapas toorun necessária.</span><span class="sxs-lookup"><span data-stu-id="db2df-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="db2df-109">**A saída típica**: tooexpect de saída de um exemplo de hello quando você executar o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="db2df-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="db2df-110">**Trechos de código**: uma coleção de tooshow de trechos de código como o exemplo hello World Olá implementa os principais componentes do gateway de borda de IoT.</span><span class="sxs-lookup"><span data-stu-id="db2df-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="db2df-111">Arquitetura da amostra do Hello World</span><span class="sxs-lookup"><span data-stu-id="db2df-111">Hello World sample architecture</span></span>
<span data-ttu-id="db2df-112">exemplo Hello World Olá ilustra os conceitos de saudação descritos na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="db2df-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="db2df-113">exemplo Hello World Olá implementa um gateway de borda IoT que tem um pipeline composto de dois módulos de borda IoT:</span><span class="sxs-lookup"><span data-stu-id="db2df-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="db2df-114">Olá *Olá, mundo* módulo cria uma mensagem a cada cinco segundos e passa-toohello módulo de agente de log.</span><span class="sxs-lookup"><span data-stu-id="db2df-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="db2df-115">Olá *agente* mensagens de saudação do módulo gravações recebe tooa arquivo.</span><span class="sxs-lookup"><span data-stu-id="db2df-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Arquitetura de exemplo de Olá, Mundo criada com o IoT Edge do Azure][4]

<span data-ttu-id="db2df-117">Conforme descrito na seção anterior hello, Olá Olá mundo módulo não passa mensagens diretamente toohello módulo de agente de log a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="db2df-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="db2df-118">Em vez disso, ela publica um agente de mensagem toohello cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="db2df-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="db2df-119">módulo de agente Olá recebe a mensagem de saudação do agente de saudação e age em, escrevendo conteúdos de Olá Olá tooa do arquivo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="db2df-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="db2df-120">módulo de agente Olá consome somente mensagens do agente de hello, ele nunca publica o novo agente toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="db2df-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Como o agente de saudação roteia mensagens entre módulos no Azure IoT Edge][5]

<span data-ttu-id="db2df-122">Olá figura acima mostra Olá arquitetura de exemplo hello World Hello e caminhos relativos Olá toohello arquivos de origem que implementam partes diferentes do exemplo hello no hello [repositório][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="db2df-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="db2df-123">Explorar código Olá por conta própria ou usar trechos de código de saudação abaixo como guia.</span><span class="sxs-lookup"><span data-stu-id="db2df-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md