---
title: "aaaDeploy o Azure IoT Suite conectado gateway fábrica | Microsoft Docs"
description: "Como toodeploy um gateway no Windows ou Linux toohello de conectividade tooenable conectadas fábrica pré-configurado a solução."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Implantar um gateway no Windows ou Linux para solução de fábrica pré-configurado Olá conectado

Olá software necessário toodeploy um gateway para a solução de fábrica pré-configurado Olá conectado tem dois componentes:

* Olá *OPC Proxy* estabelece uma conexão tooIoT Hub. Olá *OPC Proxy* , em seguida, aguarda o comando e controle de mensagens de saudação integrado OPC navegador que é executado no portal de solução de fábrica conectado hello.
* Olá *OPC publicador* conecta tooexisting local OPC UA servidores e encaminha mensagens de telemetria deles tooIoT Hub.

Ambos os componentes são de código livre e estão disponíveis como origem no GitHub e nos contêineres do Docker:

| GitHub | DockerHub |
| ------ | --------- |
| [Publicador OPC][lnk-publisher-github] | [Publicador OPC][lnk-publisher-docker] |
| [Proxy OPC][lnk-proxy-github] | [Proxy OPC][lnk-proxy-docker] |

Nenhum endereço IP de público ou falhas no firewall do gateway Olá são necessárias para o componente. Olá OPC Proxy e o publicador de OPC usam somente saídas portas 443, 5671 e 8883.

Olá etapas neste artigo mostram como toodeploy um gateway usando o Docker [Windows](#windows-deployment) ou [Linux](#linux-deployment). gateway de Olá permite que a solução de fábrica pré-configurado conectividade toohello conectado.

> [!NOTE]
> Olá gateway software que é executado no contêiner do Docker Olá [Azure IoT borda].

## <a name="windows-deployment"></a>Implantação no Windows

> [!NOTE]
> Se você ainda não tem um dispositivo de gateway, a Microsoft aconselha a comprar um gateway comercial de um de nossos parceiros. Visite Olá [catálogo de dispositivo IoT do Azure] para obter uma lista de dispositivos de gateway compatíveis com hello conectado a solução de fábrica. Siga as instruções de saudação que vêm com hello dispositivo tooset o gateway de saudação. Como alternativa, use Olá seguindo as instruções toomanually definir um dos seus gateways existentes.

### <a name="install-docker"></a>Instalar o Docker

Instale o [Docker para Windows] no seu dispositivo de gateway baseado no Windows. Durante a instalação do Windows Docker, selecione uma unidade no seu tooshare da máquina de host com o Docker. Olá captura de tela mostra a unidade Olá D no seu sistema Windows de compartilhamento a seguir:

![Instalar o Docker][img-install-docker]

Em seguida, crie uma pasta chamada **docker** na raiz de saudação da saudação unidade compartilhada.
Você também pode executar essa etapa depois de instalar o docker Olá **configurações** menu.

### <a name="configure-hello-gateway"></a>Configurar o gateway de saudação

1. Você precisa Olá **iothubowner** cadeia de caracteres de conexão de seu Azure IoT Suite conectado fábrica implantação toocomplete Olá gateway implantação. Em Olá [portal do Azure], navegar tooyour IoT Hub no grupo de recursos de saudação criado quando você implantou a solução de fábrica Olá conectado. Clique em **políticas de acesso compartilhado** tooaccess Olá **iothubowner** cadeia de caracteres de conexão:

    ![Localize Olá cadeia de caracteres de conexão de IoT Hub][img-hub-connection]

    Saudação de cópia **cadeia de caracteres de Conexão - chave primária** valor.

1. Configurar o gateway de saudação para o IoT Hub executando módulos de gateway Olá dois **quando** em um prompt de comando com:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  é Olá nome toogive tooyour OPC UA publicador em formato de saudação **publisher.&lt; o nome de domínio totalmente qualificado&gt;**. Por exemplo, se sua rede de fábrica é chamado **myfactorynetwork.com**, Olá **ApplicationName** valor é **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  é hello **iothubowner** cadeia de caracteres de conexão que você copiou na etapa anterior hello. Essa cadeia de conexão só é usada nesta etapa, ele não é necessário no hello etapas a seguir:

    Você usa Olá mapeado d:\\pasta docker (Olá `-v` argumento) toopersist posterior Olá dois certificados x. 509 que usam módulos de gateway de saudação.

### <a name="run-hello-gateway"></a>Executar Olá gateway

1. Reinicie o gateway hello usando Olá comandos a seguir:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Por motivos de segurança, certificados x. 509 de saudação dois persistentes no hello d:\\pasta docker contém a chave privada Olá. Limitar acesso toothis pasta toohello credenciais (normalmente **administradores**) use o contêiner do Docker toorun hello. Com o botão direito Olá d:\\pasta docker, escolha **propriedades**, em seguida, **segurança**e, em seguida, **editar**. Dê aos **Administradores** controle total e remova todas as outras pessoas:

    ![Compartilhamento de tooDocker conceder permissões][img-docker-share]

1. Verifique a conectividade de rede. Em um prompt de comando, digite o comando de saudação `ping publisher.<your fully qualified domain name>` tooping seu gateway. Se o destino de saudação está inacessível, adicione o endereço IP de saudação e nome do seu arquivo de hosts do gateway toohello no gateway. arquivo de hosts de saudação está localizado em Olá **Windows\\System32\\drivers\\etc** pasta.

1. Em seguida, tente tooconnect toohello publisher usando um cliente OPC UA local em execução no gateway de saudação. Olá ponto de extremidade de OPC UA URL é `opc.tcp://publisher.<your fully qualified domain name>:62222`. Caso não tenha um cliente OPC UA, você poderá baixar e usar um [cliente OPC UA de software livre].

1. Quando esses testes locais foi concluído com êxito, procure toohello **conectar seu próprio servidor de UA OPC** página no portal de solução de fábrica conectado hello. Insira a URL de ponto de extremidade do publicador hello (`tcp://publisher.<your fully qualified domain name>:62222`) e clique em **conectar**. Você recebe um aviso de certificado. Clique em **Continuar.** Em seguida você receber um erro que Olá publisher não confia Olá UA Web cliente. tooresolve este erro, a saudação de cópia **UA Web cliente** certificado da saudação **unidade d:\\docker\\certificados rejeitadas\\certificados** pasta toohello **Unidade d:\\docker\\UA aplicativos\\certificados** pasta no gateway hello. Não é necessário toorestart do gateway de saudação. Repita esta etapa. Agora você pode conectar o gateway toohello da nuvem hello e você está pronto tooadd solução de toohello servidores OPC UA.

### <a name="add-your-opc-ua-servers"></a>Adicionar os servidores OPC UA

1. Procurar toohello **conectar seu próprio servidor de UA OPC** página no portal de solução de fábrica conectado hello. Siga as mesmas etapas Olá anterior tooestablish seção confiança entre Olá portal fábrica conectado e Olá servidor OPC UA de saudação. Essa etapa estabelece uma relação de confiança mútua de certificados de saudação do hello conectado o portal de fábrica e hello servidor OPC UA e cria uma conexão.

1. Procurar Olá árvore de nós de OPC UA do seu servidor de OPC UA, nós OPC hello e selecione **publicar**. Para publicação toowork dessa maneira, Olá servidor OPC UA e Olá publicador deve ser em Olá mesma rede. Em outras palavras, se Olá totalmente qualificado nome de domínio do publicador Olá for **publisher.mydomain.com** e nome de domínio totalmente qualificado de saudação da saudação OPC UA servidor deve ser, por exemplo, **myopcuaserver.mydomain.com**. Se sua configuração for diferente, você pode adicionar manualmente arquivos de publishesnodes.json toohello de nós encontrado no hello **unidade d:\\docker** pasta. Olá publishesnodes.json arquivo é gerado automaticamente em Olá primeiro bem-sucedida de publicação de um nó OPC.

1. Telemetria agora flui de dispositivo de gateway de saudação. Você pode exibir a telemetria Olá no hello **locais de fábrica** exibir do portal de fábrica conectado Olá em **nova fábrica**.

## <a name="linux-deployment"></a>Implantação no Linux

> [!NOTE]
> Se você ainda não tem um dispositivo de gateway, a Microsoft aconselha a comprar um gateway comercial de um de nossos parceiros. Visite Olá [catálogo de dispositivo IoT do Azure] para obter uma lista de dispositivos de gateway compatíveis com hello conectado a solução de fábrica. Siga as instruções de saudação que vêm com hello dispositivo tooset o gateway de saudação. Como alternativa, use Olá seguindo as instruções toomanually definir um dos seus gateways existentes.

[Instale o Docker] em seu dispositivo de gateway Linux.

### <a name="configure-hello-gateway"></a>Configurar o gateway de saudação

1. Você precisa Olá **iothubowner** cadeia de caracteres de conexão de seu Azure IoT Suite conectado fábrica implantação toocomplete Olá gateway implantação. Em Olá [portal do Azure], navegar tooyour IoT Hub no grupo de recursos de saudação criado quando você implantou a solução de fábrica Olá conectado. Clique em **políticas de acesso compartilhado** tooaccess Olá **iothubowner** cadeia de caracteres de conexão:

    ![Localize Olá cadeia de caracteres de conexão de IoT Hub][img-hub-connection]

    Saudação de cópia **cadeia de caracteres de Conexão - chave primária** valor.

1. Configurar o gateway de saudação para o IoT Hub executando módulos de gateway Olá dois **quando** de um shell com:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  é Olá nome de gateway do OPC UA aplicativo hello cria no formato de saudação do hello **publisher.&lt; o nome de domínio totalmente qualificado&gt;**. Por exemplo, **publicador.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  é hello **iothubowner** cadeia de caracteres de conexão que você copiou na etapa anterior hello. Essa cadeia de conexão só é usada nesta etapa, ele não é necessário no hello etapas a seguir:

    Use Olá **/ compartilhado** pasta (Olá `-v` argumento) toopersist posterior Olá dois certificados x. 509 que usam módulos de gateway hello.

### <a name="run-hello-gateway"></a>Executar Olá gateway

1. Reinicie o gateway hello usando Olá comandos a seguir:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Por motivos de segurança, certificados x. 509 de saudação dois persistentes no hello **/ compartilhado** pasta contém a chave privada hello. Limitar acesso toothis pasta toohello credenciais usadas toorun Olá contêiner do Docker. permissões de saudação tooset para **raiz** apenas, use Olá `chmod` shell de comando na pasta hello.

1. Verifique a conectividade de rede. Em um shell, digite o comando de saudação `ping publisher.<your fully qualified domain name>` tooping seu gateway. Se o destino de saudação está inacessível, adicione o endereço IP de saudação e nome do seu arquivo de hosts do gateway tooyour no gateway. arquivo de hosts de saudação está localizado em Olá **/etc** pasta.

1. Em seguida, tente tooconnect toohello publisher usando um cliente OPC UA local em execução no gateway de saudação. Olá ponto de extremidade de OPC UA URL é `opc.tcp://publisher.<your fully qualified domain name>:62222`. Caso não tenha um cliente OPC UA, você poderá baixar e usar um [cliente OPC UA de software livre].

1. Quando esses testes locais foi concluído com êxito, procure toohello **conectar seu próprio servidor de UA OPC** página no portal de solução de fábrica conectado hello. Insira a URL de ponto de extremidade do publicador hello (`tcp://publisher.<your fully qualified domain name>:62222`) e clique em **conectar**. Você recebe um aviso de certificado. Clique em **Continuar.** Em seguida você receber um erro que Olá publisher não confia Olá UA Web cliente. tooresolve este erro, a saudação de cópia **UA Web cliente** certificado da saudação **compartilhados/rejeitado certificados/certificados** pasta toohello **/shared/UA aplicativos/certificados** pasta no gateway hello. Não é necessário toorestart do gateway de saudação. Repita esta etapa. Agora você pode conectar o gateway toohello da nuvem hello e você está pronto tooadd solução de toohello servidores OPC UA.

### <a name="add-your-opc-ua-servers"></a>Adicionar os servidores OPC UA

1. Procurar toohello **conectar seu próprio servidor de UA OPC** página no portal de solução de fábrica conectado hello. Siga as mesmas etapas Olá anterior tooestablish seção confiança entre Olá portal fábrica conectado e Olá servidor OPC UA de saudação. Essa etapa estabelece uma relação de confiança mútua de certificados de saudação do hello conectado o portal de fábrica e hello servidor OPC UA e cria uma conexão.

1. Procurar Olá árvore de nós de OPC UA do seu servidor de OPC UA, nós OPC hello e selecione **publicar**. Para publicação toowork dessa maneira, Olá servidor OPC UA e Olá publicador deve ser em Olá mesma rede. Em outras palavras, se Olá totalmente qualificado nome de domínio do publicador Olá for **publisher.mydomain.com** e nome de domínio totalmente qualificado de saudação da saudação OPC UA servidor deve ser, por exemplo, **myopcuaserver.mydomain.com**. Se sua configuração for diferente, você pode adicionar manualmente arquivos de publishesnodes.json toohello de nós encontrado no hello **/ compartilhado** pasta. Olá publishesnodes.json é gerada automaticamente no hello primeiro bem-sucedida de publicação de um nó OPC.

1. Telemetria agora flui de dispositivo de gateway de saudação. Você pode exibir a telemetria Olá no hello **locais de fábrica** exibir do portal de fábrica conectado Olá em **nova fábrica**.

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre a arquitetura de saudação de fábrica conectado Olá pré-configurado solução, consulte [conectada fábrica pré-configurado passo a passo de solução][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker para Windows]: https://www.docker.com/docker-windows
[catálogo de dispositivo IoT do Azure]: https://catalog.azureiotsuite.com/?q=opc
[portal do Azure]: http://portal.azure.com/
[cliente OPC UA de software livre]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Instale o Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT borda]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy