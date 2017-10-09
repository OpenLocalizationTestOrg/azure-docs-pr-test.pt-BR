> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Este artigo fornece uma explicação detalhada de saudação [código de exemplo Hello World] [ lnk-helloworld-sample] tooillustrate componentes fundamentais do hello de saudação [Azure IoT borda] [ lnk-iot-edge] arquitetura. Olá exemplo usa hello Azure IoT borda toobuild um gateway simple que registra um arquivo de tooa de mensagem "hello world" a cada cinco segundos.

Este passo a passo aborda:

* **Olá arquitetura de exemplo do mundo**: descreve como [conceitos de arquitetura do Azure IoT borda] [ lnk-edge-concepts] aplicar toohello exemplo de Hello World e como os componentes de saudação se encaixam.
* **Como toobuild Olá exemplo**: exemplo de saudação do hello etapas toobuild necessária.
* **Como toorun Olá exemplo**: exemplo de saudação do hello etapas toorun necessária. 
* **A saída típica**: tooexpect de saída de um exemplo de hello quando você executar o exemplo hello.
* **Trechos de código**: uma coleção de tooshow de trechos de código como o exemplo hello World Olá implementa os principais componentes do gateway de borda de IoT.


## <a name="hello-world-sample-architecture"></a>Arquitetura da amostra do Hello World
exemplo Hello World Olá ilustra os conceitos de saudação descritos na seção anterior hello. exemplo Hello World Olá implementa um gateway de borda IoT que tem um pipeline composto de dois módulos de borda IoT:

* Olá *Olá, mundo* módulo cria uma mensagem a cada cinco segundos e passa-toohello módulo de agente de log.
* Olá *agente* mensagens de saudação do módulo gravações recebe tooa arquivo.

![Arquitetura de exemplo de Olá, Mundo criada com o IoT Edge do Azure][4]

Conforme descrito na seção anterior hello, Olá Olá mundo módulo não passa mensagens diretamente toohello módulo de agente de log a cada cinco segundos. Em vez disso, ela publica um agente de mensagem toohello cada cinco segundos.

módulo de agente Olá recebe a mensagem de saudação do agente de saudação e age em, escrevendo conteúdos de Olá Olá tooa do arquivo da mensagem.

módulo de agente Olá consome somente mensagens do agente de hello, ele nunca publica o novo agente toohello de mensagens.

![Como o agente de saudação roteia mensagens entre módulos no Azure IoT Edge][5]

Olá figura acima mostra Olá arquitetura de exemplo hello World Hello e caminhos relativos Olá toohello arquivos de origem que implementam partes diferentes do exemplo hello no hello [repositório][lnk-iot-edge]. Explorar código Olá por conta própria ou usar trechos de código de saudação abaixo como guia.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md