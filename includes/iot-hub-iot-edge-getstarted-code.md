## <a name="typical-output"></a><span data-ttu-id="07297-101">Saída típica</span><span class="sxs-lookup"><span data-stu-id="07297-101">Typical output</span></span>

<span data-ttu-id="07297-102">Olá, exemplo a seguir mostra saída Olá gravada o arquivo de log toohello pelo exemplo hello World Hello.</span><span class="sxs-lookup"><span data-stu-id="07297-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="07297-103">saída de Hello é formatada para legibilidade:</span><span class="sxs-lookup"><span data-stu-id="07297-103">hello output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="07297-104">Trechos de código</span><span class="sxs-lookup"><span data-stu-id="07297-104">Code snippets</span></span>

<span data-ttu-id="07297-105">Esta seção discute algumas seções principais do código Olá Olá Olá\_exemplo do mundo.</span><span class="sxs-lookup"><span data-stu-id="07297-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="07297-106">Criação do gateway do Edge IoT</span><span class="sxs-lookup"><span data-stu-id="07297-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="07297-107">Você deve implementar um *processo de gateway*.</span><span class="sxs-lookup"><span data-stu-id="07297-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="07297-108">Este programa cria a infraestrutura interna da saudação (agente de saudação), carrega os módulos de borda IoT hello e configura o processo de saudação do gateway.</span><span class="sxs-lookup"><span data-stu-id="07297-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="07297-109">Borda de IoT fornece Olá **Gateway\_criar\_de\_JSON** função tooenable toobootstrap um gateway de um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="07297-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="07297-110">Olá toouse **Gateway\_criar\_de\_JSON** funcionar, passá-lo Olá caminho tooa JSON arquivo Especifica Olá tooload de módulos de borda de IoT.</span><span class="sxs-lookup"><span data-stu-id="07297-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="07297-111">Você pode encontrar o código de saudação para processo de gateway de saudação em Olá *Hello World* exemplo no hello [main.c] [ lnk-main-c] arquivo.</span><span class="sxs-lookup"><span data-stu-id="07297-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="07297-112">Para legibilidade, hello trecho a seguir mostra uma versão abreviada do código de saudação do processo de gateway.</span><span class="sxs-lookup"><span data-stu-id="07297-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="07297-113">Este programa de exemplo cria um gateway e, em seguida, aguarda Olá Olá de toopress usuário **ENTER** antes de ele destrói o gateway de saudação da chave.</span><span class="sxs-lookup"><span data-stu-id="07297-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="07297-114">arquivo de configurações de JSON Olá contém uma lista de tooload de módulos IoT borda e links de saudação entre módulos hello.</span><span class="sxs-lookup"><span data-stu-id="07297-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="07297-115">Cada módulo do Edge IoT deve especificar um:</span><span class="sxs-lookup"><span data-stu-id="07297-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="07297-116">**nome**: um nome exclusivo para o módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="07297-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="07297-117">**carregador**: um carregador que sabe como Olá tooload desejado módulo.</span><span class="sxs-lookup"><span data-stu-id="07297-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="07297-118">Carregadores são um ponto de extensão para carregar os diferentes tipos de módulos.</span><span class="sxs-lookup"><span data-stu-id="07297-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="07297-119">O IoT Edge fornece carregadores para uso com módulos escritos em .NET, Node.js, Java e C nativos.</span><span class="sxs-lookup"><span data-stu-id="07297-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="07297-120">exemplo Hello World Olá usa apenas o carregador de C nativo Olá pois todos os módulos de saudação neste exemplo são bibliotecas dinâmicas escritas em C. Para obter mais informações sobre como módulos de borda IoT toouse escritos em idiomas diferentes, consulte Olá [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), ou [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) exemplos.</span><span class="sxs-lookup"><span data-stu-id="07297-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="07297-121">**nome**: nome de saudação do carregador de saudação usado módulo de saudação tooload.</span><span class="sxs-lookup"><span data-stu-id="07297-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="07297-122">**ponto de entrada**: biblioteca de toohello caminho Olá que contém o módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="07297-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="07297-123">No Linux, essa biblioteca é um arquivo .so, no Windows, é um arquivo .dll.</span><span class="sxs-lookup"><span data-stu-id="07297-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="07297-124">ponto de entrada Hello é tipo toohello específico do carregador que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="07297-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="07297-125">saudação de ponto de entrada do carregador de Node. js é um arquivo. js.</span><span class="sxs-lookup"><span data-stu-id="07297-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="07297-126">Olá ponto de entrada do carregador de Java é um caminho de classe e um nome de classe.</span><span class="sxs-lookup"><span data-stu-id="07297-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="07297-127">Olá ponto de entrada do carregador de .NET é um nome de assembly e um nome de classe.</span><span class="sxs-lookup"><span data-stu-id="07297-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="07297-128">**argumentos**: precisa de qualquer módulo de saudação de informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="07297-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="07297-129">Olá a seguir de código mostra Olá JSON usado toodeclare todos os Olá módulos de borda IoT para exemplo de Hello World hello no Linux.</span><span class="sxs-lookup"><span data-stu-id="07297-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="07297-130">Se um módulo requer argumentos depende de design de saudação do módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="07297-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="07297-131">Neste exemplo, o módulo de agente de log de saudação usa um argumento que é o arquivo de saída do hello caminho toohello e Olá Olá\_módulo world não possui argumentos.</span><span class="sxs-lookup"><span data-stu-id="07297-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="07297-132">arquivo JSON de saudação também contém links de saudação entre módulos Olá que são passados toohello broker.</span><span class="sxs-lookup"><span data-stu-id="07297-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="07297-133">Um link tem duas propriedades:</span><span class="sxs-lookup"><span data-stu-id="07297-133">A link has two properties:</span></span>

* <span data-ttu-id="07297-134">**origem**: o nome de um módulo de saudação `modules` seção, ou `\*`.</span><span class="sxs-lookup"><span data-stu-id="07297-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="07297-135">**coletor**: o nome de um módulo de saudação `modules` seção.</span><span class="sxs-lookup"><span data-stu-id="07297-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="07297-136">Cada link define uma rota e uma direção para as mensagens.</span><span class="sxs-lookup"><span data-stu-id="07297-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="07297-137">Mensagens de saudação **fonte** são fornecidas com o módulo toohello **coletor** módulo.</span><span class="sxs-lookup"><span data-stu-id="07297-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="07297-138">Você pode definir Olá **fonte** módulo muito`\*`, que indica que Olá **coletor** módulo recebe mensagens de qualquer módulo.</span><span class="sxs-lookup"><span data-stu-id="07297-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="07297-139">Olá código a seguir mostra Olá JSON usado tooconfigure links entre módulos Olá usados Olá Olá\_exemplo world no Linux.</span><span class="sxs-lookup"><span data-stu-id="07297-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="07297-140">Cada mensagem produzida por Olá `hello_world` módulo é consumido por Olá `logger` módulo.</span><span class="sxs-lookup"><span data-stu-id="07297-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="07297-141">Publicação de mensagem do módulo do Hello\_World</span><span class="sxs-lookup"><span data-stu-id="07297-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="07297-142">Você pode encontrar hello código usado pelo Olá Olá\_mensagens de toopublish de módulo world em Olá ['hello_world.c'] [ lnk-helloworld-c] arquivo.</span><span class="sxs-lookup"><span data-stu-id="07297-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="07297-143">Olá trecho a seguir mostra uma versão aperfeiçoada de código Olá com comentários adicionados e removido para a legibilidade do código de manipulação de erros:</span><span class="sxs-lookup"><span data-stu-id="07297-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="07297-144">Processamento de mensagem do módulo do Hello\_World</span><span class="sxs-lookup"><span data-stu-id="07297-144">Hello\_world module message processing</span></span>

<span data-ttu-id="07297-145">Olá Olá\_módulo world nunca processa mensagens de outros módulos de borda IoT publicar toohello broker.</span><span class="sxs-lookup"><span data-stu-id="07297-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="07297-146">Olá, portanto, a implementação do retorno de chamada de mensagem de saudação em Olá Olá\_módulo do mundo é uma função de não-operacional.</span><span class="sxs-lookup"><span data-stu-id="07297-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="07297-147">Publicação e processamento de mensagem de módulo do agente</span><span class="sxs-lookup"><span data-stu-id="07297-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="07297-148">módulo de agente Olá recebe mensagens do agente de saudação e os grava tooa arquivo.</span><span class="sxs-lookup"><span data-stu-id="07297-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="07297-149">Ele nunca publica as mensagens.</span><span class="sxs-lookup"><span data-stu-id="07297-149">It never publishes any messages.</span></span> <span data-ttu-id="07297-150">Portanto, o código de saudação do módulo de agente de log de saudação chama nunca Olá **Broker_Publish** função.</span><span class="sxs-lookup"><span data-stu-id="07297-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="07297-151">Olá **Logger_Receive** função hello [logger.c] [ lnk-logger-c] arquivo é o agente de saudação do retorno de chamada hello invoca toodeliver módulo de agente de log de toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="07297-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="07297-152">Olá trecho a seguir mostra uma versão aperfeiçoada com comentários adicionados e removido para a legibilidade do código de manipulação de erros:</span><span class="sxs-lookup"><span data-stu-id="07297-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="07297-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07297-153">Next steps</span></span>

<span data-ttu-id="07297-154">Neste artigo, você executou um gateway de borda IoT simple que grava o arquivo de log de tooa de mensagens.</span><span class="sxs-lookup"><span data-stu-id="07297-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="07297-155">toorun um exemplo que envia mensagens tooIoT Hub, consulte [borda IoT – enviar mensagens de dispositivo para a nuvem com um dispositivo simulado usando Linux] [ lnk-gateway-simulated-linux] ou [borda IoT – enviar mensagens de dispositivo para a nuvem com um dispositivo simulado usando Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="07297-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md