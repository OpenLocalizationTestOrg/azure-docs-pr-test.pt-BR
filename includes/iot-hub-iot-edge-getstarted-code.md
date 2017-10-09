## <a name="typical-output"></a>Saída típica

Olá, exemplo a seguir mostra saída Olá gravada o arquivo de log toohello pelo exemplo hello World Hello. saída de Hello é formatada para legibilidade:

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

## <a name="code-snippets"></a>Trechos de código

Esta seção discute algumas seções principais do código Olá Olá Olá\_exemplo do mundo.

### <a name="iot-edge-gateway-creation"></a>Criação do gateway do Edge IoT

Você deve implementar um *processo de gateway*. Este programa cria a infraestrutura interna da saudação (agente de saudação), carrega os módulos de borda IoT hello e configura o processo de saudação do gateway. Borda de IoT fornece Olá **Gateway\_criar\_de\_JSON** função tooenable toobootstrap um gateway de um arquivo JSON. Olá toouse **Gateway\_criar\_de\_JSON** funcionar, passá-lo Olá caminho tooa JSON arquivo Especifica Olá tooload de módulos de borda de IoT.

Você pode encontrar o código de saudação para processo de gateway de saudação em Olá *Hello World* exemplo no hello [main.c] [ lnk-main-c] arquivo. Para legibilidade, hello trecho a seguir mostra uma versão abreviada do código de saudação do processo de gateway. Este programa de exemplo cria um gateway e, em seguida, aguarda Olá Olá de toopress usuário **ENTER** antes de ele destrói o gateway de saudação da chave.

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

arquivo de configurações de JSON Olá contém uma lista de tooload de módulos IoT borda e links de saudação entre módulos hello. Cada módulo do Edge IoT deve especificar um:

* **nome**: um nome exclusivo para o módulo de saudação.
* **carregador**: um carregador que sabe como Olá tooload desejado módulo. Carregadores são um ponto de extensão para carregar os diferentes tipos de módulos. O IoT Edge fornece carregadores para uso com módulos escritos em .NET, Node.js, Java e C nativos. exemplo Hello World Olá usa apenas o carregador de C nativo Olá pois todos os módulos de saudação neste exemplo são bibliotecas dinâmicas escritas em C. Para obter mais informações sobre como módulos de borda IoT toouse escritos em idiomas diferentes, consulte Olá [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), ou [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) exemplos.
    * **nome**: nome de saudação do carregador de saudação usado módulo de saudação tooload.
    * **ponto de entrada**: biblioteca de toohello caminho Olá que contém o módulo de saudação. No Linux, essa biblioteca é um arquivo .so, no Windows, é um arquivo .dll. ponto de entrada Hello é tipo toohello específico do carregador que está sendo usado. saudação de ponto de entrada do carregador de Node. js é um arquivo. js. Olá ponto de entrada do carregador de Java é um caminho de classe e um nome de classe. Olá ponto de entrada do carregador de .NET é um nome de assembly e um nome de classe.

* **argumentos**: precisa de qualquer módulo de saudação de informações de configuração.

Olá a seguir de código mostra Olá JSON usado toodeclare todos os Olá módulos de borda IoT para exemplo de Hello World hello no Linux. Se um módulo requer argumentos depende de design de saudação do módulo de saudação. Neste exemplo, o módulo de agente de log de saudação usa um argumento que é o arquivo de saída do hello caminho toohello e Olá Olá\_módulo world não possui argumentos.

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

arquivo JSON de saudação também contém links de saudação entre módulos Olá que são passados toohello broker. Um link tem duas propriedades:

* **origem**: o nome de um módulo de saudação `modules` seção, ou `\*`.
* **coletor**: o nome de um módulo de saudação `modules` seção.

Cada link define uma rota e uma direção para as mensagens. Mensagens de saudação **fonte** são fornecidas com o módulo toohello **coletor** módulo. Você pode definir Olá **fonte** módulo muito`\*`, que indica que Olá **coletor** módulo recebe mensagens de qualquer módulo.

Olá código a seguir mostra Olá JSON usado tooconfigure links entre módulos Olá usados Olá Olá\_exemplo world no Linux. Cada mensagem produzida por Olá `hello_world` módulo é consumido por Olá `logger` módulo.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Publicação de mensagem do módulo do Hello\_World

Você pode encontrar hello código usado pelo Olá Olá\_mensagens de toopublish de módulo world em Olá ['hello_world.c'] [ lnk-helloworld-c] arquivo. Olá trecho a seguir mostra uma versão aperfeiçoada de código Olá com comentários adicionados e removido para a legibilidade do código de manipulação de erros:

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

### <a name="helloworld-module-message-processing"></a>Processamento de mensagem do módulo do Hello\_World

Olá Olá\_módulo world nunca processa mensagens de outros módulos de borda IoT publicar toohello broker. Olá, portanto, a implementação do retorno de chamada de mensagem de saudação em Olá Olá\_módulo do mundo é uma função de não-operacional.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Publicação e processamento de mensagem de módulo do agente

módulo de agente Olá recebe mensagens do agente de saudação e os grava tooa arquivo. Ele nunca publica as mensagens. Portanto, o código de saudação do módulo de agente de log de saudação chama nunca Olá **Broker_Publish** função.

Olá **Logger_Receive** função hello [logger.c] [ lnk-logger-c] arquivo é o agente de saudação do retorno de chamada hello invoca toodeliver módulo de agente de log de toohello de mensagens. Olá trecho a seguir mostra uma versão aperfeiçoada com comentários adicionados e removido para a legibilidade do código de manipulação de erros:

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

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você executou um gateway de borda IoT simple que grava o arquivo de log de tooa de mensagens. toorun um exemplo que envia mensagens tooIoT Hub, consulte [borda IoT – enviar mensagens de dispositivo para a nuvem com um dispositivo simulado usando Linux] [ lnk-gateway-simulated-linux] ou [borda IoT – enviar mensagens de dispositivo para a nuvem com um dispositivo simulado usando Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md