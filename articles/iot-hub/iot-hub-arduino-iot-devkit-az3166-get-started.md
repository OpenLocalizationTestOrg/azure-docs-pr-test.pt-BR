---
title: aaaIoT DevKit toocloud - tooAzure conectar AZ3166 de DevKit de IoT IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se tooAzure AZ3166 de DevKit de IoT IoT Hub para ele plataforma de nuvem do Azure toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Conecte-se tooAzure AZ3166 de DevKit de IoT IoT Hub na nuvem Olá

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Olá [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) podem ser usado toodevelop e protótipo soluções de Internet das coisas (IoT) aproveita os serviços do Microsoft Azure. Ele inclui um quadro de Arduino compatível com periféricos avançados e sensores, um pacote de quadro do código-fonte aberto e um [catálogo de projetos](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) crescente.

## <a name="what-you-do"></a>O que fazer
Conecte-se [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub que você cria, Olá coletar os dados de temperatura e umidade de sensores e envia o hub de tooIoT Olá dados.

Você ainda não tem um DevKit? Obtenha um novo [aqui](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>O que você aprenderá

* Como tooconnect IoT DevKit tooWireless acesso aponte e preparar o ambiente de desenvolvimento.
* Como toocreate um hub IoT e registrar um dispositivo para MXChip DevKit de IoT.
* Como os dados do sensor toocollect executando um aplicativo de exemplo no MXChip DevKit de IoT.
* Como toosend Olá hub IoT do sensor dados tooyour.

## <a name="what-you-need"></a>O que você precisa

* Uma placa MXChip IoT DevKit com um cabo micro USB. [Experimente agora](https://aka.ms/iot-devkit-purchase)
* Um computador que executa o Windows 10 ou macOS 10.10 +
* Uma assinatura ativa do Azure
  * Ative uma [conta do Microsoft Azure de avaliação por 30 dias](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Prepare seu hardware

Conecte Olá hardware tooyour computador.

### <a name="hardware-you-need"></a>O hardware que você precisa

* Placa DevKit
* Cabo micro USB

![guia de introdução: hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Conectar o computador de tooyour DevKit

1. Conexão USB final tooyour PC
2. Conecte-se Micro USB final toohello DevKit
3. Olá verde LED próxima toopower confirma a conexão

![guia de introdução: conexão](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Configuração do Wi-Fi

Os projetos de IoT requerem conexão com a Internet. Use Olá instruções tooconfigure Olá DevKit tooconnect tooWiFi a seguir.

### <a name="enter-ap-mode"></a>Entrar no modo PA

Mantenha pressionado B, em seguida, enviar por push e liberar o botão de redefinição hello e versão botão B. Seu DevKit entrará no modo de ponto de acesso para a configuração de Wi-Fi. tela Hello exibirá Olá serviço definido Identifier(SSID) de saudação DevKit, bem como Olá configuração endereço IP do portal:

![guia de introdução: PA Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Conecte-se tooDevKit Pacífico

Agora, use outra WiFi habilitado dispositivos (PC ou telefone celular) tooconnect toohello DevKit SSID (realçado na captura de tela de saudação acima), deixe Olá senha em branco.

![guia de introdução: SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Configuração do Wi-Fi ao DevKit

Endereço IP hello abrir mostrado na tela de DevKit de saudação em seu computador ou navegador de telefone celular, selecione rede Wi-Fi de Olá deseja Olá DevKit tooconnect para e digite a senha de saudação. Clique em **conectar** toocomplete:

![Guia de Introdução: portal do Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Depois que a conexão de saudação for bem-sucedida, Olá DevKit reiniciará em alguns segundos. Se for bem-sucedida, você verá o hello WiFi nome e endereço IP na tela hello:

![Guia de Introdução: IP do Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
endereço IP de saudação exibido foto Olá pode não corresponder Olá o IP real atribuído e exibida na tela de DevKit hello. Isso é normal como Wi-Fi usa DHCP toodynamically atribuir IPs.

Após a configuração de Wi-Fi, suas credenciais serão mantidas no dispositivo Olá para essa conexão, mesmo se desconectado. Por exemplo, se você configurado Olá DevKit para Wi-Fi em casa e, em seguida, levou office de toohello DevKit Olá, você precisará tooreconfigure Pacífico modo (começando na etapa **insira Pacífico modo**) tooconnect Olá DevKit tooyour office Wi-Fi. 

## <a name="start-using-devkit"></a>Começar a usar o DevKit

saudação padrão aplicativo em execução no DevKit será verificar a versão mais recente de saudação do firmware hello e exibir alguns dados de diagnóstico de sensor para você.

### <a name="upgrade-toohello-latest-firmware"></a>Atualizar o firmware mais recente do toohello

Você será solicitado na tela hello que ambos Olá versão de firmware mais recente e atual, se houver uma atualização necessária. Execute [atualizar firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guia tooupgrade-lo.

![Guia de Introdução: firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Este é um esforço de uso único, quando você começar a desenvolver em Olá DevKit e carregar seu aplicativo, você terá mais recente do firmware Olá vêm com seu aplicativo.

### <a name="test-various-sensors"></a>Teste de vários sensores

Pressione sensores de tootest botão B, continue a pressionar e liberar Olá B botão toocycle cada sensor.

![Guia de Introdução: sensores](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Prepare o ambiente de desenvolvimento

Agora é hora tooset ambiente de desenvolvimento Olá: ferramentas e os pacotes para toobuild impressionantes IoT aplicativos. Você pode escolher a versão do Windows ou macOS de acordo com o sistema operacional de tooyour.


### <a name="windows"></a>Windows

Recomendamos que você toouse Olá instalação pacote tooprepare Olá ambiente de desenvolvimento. Se você encontrar algum problema, você pode seguir Olá [etapas manuais](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget suas tarefas.

#### <a name="download-latest-package"></a>Baixe o pacote mais recente

Olá `.zip` arquivo baixado contém todas as ferramentas necessárias e os pacotes necessários para o desenvolvimento de DevKit.

> [!div class="button"]
[Baixar](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Olá `.zip` arquivo contém o seguinte Olá ferramentas e os pacotes. Se você já tiver alguns componentes instalados, o script hello detectará e ignorá-los.
> * Node. js e Yarn: tempo de execução para o script de instalação hello e tarefas automatizadas
> * [MSI de 2.0 CLI do Azure](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -experiência de linha de comando de plataforma cruzada para gerenciar recursos do Azure, Olá MSI contém dependente Python e pip.
> * [Visual Studio Code](https://code.visualstudio.com/): editor de códigos simples para o desenvolvimento do DevKit
> * [Extensão do Visual Studio Code para Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): permite o desenvolvimento do Arduino no VS Code
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): extensão Olá para Arduino depende essa ferramenta
> * Pacote de quadro DevKit: Ferramenta cadeias, bibliotecas e projetos para Olá DevKit
> * Utilitário de Link-ST: utilitários e drivers essenciais

#### <a name="run-installation-script"></a>Execute o script de instalação

No Explorador de arquivos do Windows, localize Olá `.zip` e extraí-lo, localizar `install.cmd`, com o botão direito e selecione **"Executar como administrador"** toostart.

![Guia de Introdução: execução-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Durante a instalação, você verá o progresso de saudação de cada ferramenta ou o pacote.

![Introdução: instalação](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Confirmar tooinstall drivers

Olá código VS para extensão Arduino depende Olá Arduino IDE. Se esse for o hello estão instalando Olá Arduino IDE pela primeira vez, será solicitado tooinstall os drivers:

![Guia de Introdução: driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Instalação de toofinish cerca de 10 minutos dependendo da velocidade de Internet deve demorar. Após a conclusão da instalação Olá, você deve ver código do Visual Studio e Arduino IDE atalhos na área de trabalho.

> [!NOTE] 
Eventualmente, ao iniciar o VS Code, aparecerá um erro notificando que não foi possível encontrar o Arduino IDE nem o pacote de placa relacionado. toosolve-lo, código VS fechar, inicie Arduino IDE de uma vez e o código do VS devem localizar o caminho Arduino IDE corretamente.


### <a name="macos-preview"></a>macOS (visualização)

Execute o ambiente de desenvolvimento de tooprepare essas etapas na macOS.

#### <a name="install-azure-cli-20"></a>Instalar a CLI 2.0 do Azure

Siga Olá [guia oficial](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall 2.0 do CLI do Azure:

Instale a CLI 2.0 do Azure com um comando `curl`:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

E reiniciar o shell de comando para efeito de tootake alterações:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Instalação do Arduino IDE

Olá extensão Arduino de código do Visual Studio se baseia em Olá Arduino IDE. Baixe e instale Olá [Arduino IDE para macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code

Baixe e instale o [Visual Studio Code para macOS](https://code.visualstudio.com/). Essa será a ferramenta de desenvolvimento principal Olá para criar aplicativos de DevKit de IoT.

####  <a name="download-latest-package"></a>Baixe o pacote mais recente

1. Instale o Node.js. Você pode usar o Gerenciador de pacotes macOS populares [Homebrew](https://brew.sh/) ou [pré-criadas instalador](https://nodejs.org/en/download/) tooinstall-lo.

2. Baixe o arquivo `.zip` que contém scripts de tarefas necessárias para o desenvolvimento de DevKit no VS Code.

   > [!div class="button"]
   [Baixar](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Localizar Olá `.zip` e extraia-o. Em seguida, inicie **Terminal** aplicativo e execução hello tooconfigure comandos a seguir:

   Mova pasta extraída tooyour macOS usuário pasta:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Instale os pacotes `npm`:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Instalação da extensão de VS Code para Arduino

Código do Visual Studio permite extensões de mercado tooinstall diretamente na ferramenta hello, simplesmente clique ícone de extensões de saudação no painel de menus à esquerda do hello e procure `Arduino` tooinstall:

![extensões de instalação](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Instalação do pacote de placa do DevKit

Você precisará tooadd placa de DevKit de hello usando Olá Gerenciador de quadro no código do Visual Studio.

1. Use `Cmd+Shift+P` tooinvoke paleta e o tipo de comando **Arduino** , em seguida, localizar e selecionar **Arduino: Gerenciador de quadro**.

2. Clique em **'URLs adicionais'** na parte inferior de saudação à direita.
   ![instalação adicional de URLs](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. Em Olá `settings.json` arquivo, adicione uma linha na parte inferior de saudação do `USER SETTINGS` painel e salvar.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![instalação de configurações de json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Agora no hello placa Manager Pesquisar 'az3166' e instalar a versão mais recente do hello.
   ![instalação az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Agora você tem todas as ferramentas necessárias hello e pacotes instalados para macOS.


## <a name="open-project-folder"></a>Abra a pasta do projeto

### <a name="launch-vs-code"></a>Iniciar o Código VS

Verifique se que o DevKit não está conectado. Inicie o VS código primeiro e conectar Olá DevKit tooyour computador. O VS Code o encontra automaticamente e abre uma página pop up de introdução:

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Eventualmente, ao iniciar o VS Code, aparecerá um erro notificando que não foi possível encontrar o Arduino IDE nem o pacote de placa relacionado. toosolve-lo, código VS fechar, inicie o IDE Arduino novamente e o código do VS devem localizar o caminho Arduino IDE corretamente.

### <a name="open-arduino-examples-folder"></a>Abra a pasta de exemplos de Arduino

Alternar muito**'Arduino exemplos'** guia, navegue até muito`Examples for MXCHIP AZ3166 > AzureIoT` e clique em `GetStarted`.

![Exemplos de minisolução](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Se ocorrer o painel de saudação tooclose, tooreload-lo, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta e o tipo de comando tooinvoke **Arduino** toofind e selecione **Arduino: exemplos**.

## <a name="provision-azure-services"></a>Provisionamento dos serviços do Azure

Na janela de solução hello, executar a tarefa `Ctrl+P` (macOS: `Cmd+P`), digitando a provisão de nuvem de tarefas:

Em Olá o código de VS terminal, que uma linha de comando interativa orientará Olá provisionamento necessário serviços do Azure:

![provisionamento de nuvem de minisolução](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Compilação e carregamento do esboço do Arduino

### <a name="install-required-library"></a>Instalação da biblioteca necessária

1. Pressione `F1` ou `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta e o tipo de comando tooinvoke **Arduino** , em seguida, localizar e selecionar **Arduino: Gerenciador de biblioteca**.

2. Procure `ArduinoJson` biblioteca e clique em **instalar**

### <a name="build-and-upload-hello-device-code"></a>Criar e carregar o código de dispositivo Olá

Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'carregamento de dispositivo de tarefa'. Olá terminal solicitará que você tooenter modo de configuração. toodo, portanto, mantenha pressionado um e botão de redefinição de saudação push e versão. tela Hello exibirá 'Configuration'. Esta é cadeia de conexão do hello tooset recupera da etapa 'tarefa nuvem-provisão'.

Em seguida, iniciará Verificando e carregando um esboço de Arduino hello:

![carregamento de dispositivo de minisolução](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Olá DevKit reinicializará e iniciar a execução de código hello.

## <a name="test-hello-project"></a>Projeto de saudação do teste

No código VS, clique Olá power plug ícone tooopen Olá Monitor série da barra de status de saudação.

aplicativo de exemplo Hello está executando com êxito quando você vir Olá resultados a seguir:

* Olá exibe Serial Monitor Olá mesmas informações que o conteúdo de Olá Olá a captura de tela abaixo.
* Olá LED no MXChip IoT DevKit estiver piscando.

![Saída final no VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Comentários e problemas

Você pode encontrar [perguntas frequentes](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) se você encontrar problemas ou chegar toous de canais de saudação abaixo.

## <a name="next-steps"></a>Próximas etapas

Você se conectou com êxito um tooyour MXChip DevKit de IoT IoT Hub e enviado Olá capturados hub IoT do sensor dados tooyour.

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

- [Gerenciar mensagens do dispositivos de nuvem com o iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Salvar mensagens de IoT Hub tooAzure armazenamento de dados](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Usar dados de sensor em tempo real do Power BI toovisualize do Azure IoT Hub](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Usar dados de sensor em tempo real de toovisualize de aplicativos Web do Azure de Azure IoT Hub](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Previsão do tempo usando dados de sensor de saudação do seu hub IoT no aprendizado de máquina do Azure](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Gerenciamento de dispositivos com o iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Monitoramento remoto e notificações com Aplicativos Lógicos](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)