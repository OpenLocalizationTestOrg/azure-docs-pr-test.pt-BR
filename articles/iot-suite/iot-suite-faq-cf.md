---
title: "aaaAzure IoT Suite conectado perguntas Frequentes de fábrica | Microsoft Docs"
description: "Perguntas frequentes sobre a fábrica conectada do IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Perguntas frequentes sobre a solução pré-configurada de fábrica conectada do IoT Suite

Consulte também, Olá geral [perguntas frequentes sobre](iot-suite-faq.md) IoT Suite.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Onde posso encontrar o código-fonte Olá para solução de saudação pré-configurado?

código-fonte Olá é armazenado no hello repositório GitHub a seguir:

* [Solução pré-configurada de fábrica conectada](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>O que é OPC UA?

O OPC UA (Unified Architecture), lançado em 2008, é um padrão de interoperabilidade orientado a serviços e independente de plataforma. O OPC UA é usado por vários sistemas e dispositivos industriais, como computadores, PLCs e sensores do setor. OPC UA integra a funcionalidade de saudação de especificações de OPC clássico Olá em uma estrutura extensível com segurança interna. É um padrão que é controlado pelo Olá OPC Foundation. Olá [OPC Foundation](http://opcfoundation.org/) é uma organização não fins lucrativos com mais de 440 membros. meta de saudação da organização Olá é toouse OPC especificações toofacilitate vários fornecedor, multiplataforma, segura e confiável interoperabilidade por meio de:

* Infraestrutura
* Especificações
* Tecnologia
* Processos

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Por que a Microsoft escolheu que OPC UA para Olá conectado solução pré-configurada de fábrica?

A Microsoft escolheu OPC UA porque ele é um padrão aberto, comprovado, não proprietário, independente de plataforma e reconhecido no setor. É um requisito para soluções de arquitetura de referência Industrie 4.0 (RAMI4.0) garantindo a interoperabilidade entre um amplo conjunto de processos de fabricação e equipamento. Microsoft vê a demanda de soluções de toobuild 4.0 Industrie nossos clientes. Suporte para OPC UA ajuda a barreira de saudação inferior para os clientes tooachieve suas metas e fornece toothem de valor comercial imediato.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Como adicionar uma simulação da toohello de endereço do IP pública VM?

Você tem duas opções tooadd Olá endereço:

* Usar script do PowerShell Olá `Simulation/Factory/Add-SimulationPublicIp.ps1` em Olá [repositório](https://github.com/Azure/azure-iot-connected-factory). Passar o nome da implantação como um parâmetro. Para uma implantação local, use `<your username>ConnFactoryLocal`. script Hello imprime endereço IP Olá Olá VM.

* No hello portal do Azure, localize o grupo de recursos de saudação da sua implantação. Com exceção de uma implantação local, o grupo de recursos de saudação tem nome hello especificado como solução ou implantação. Para uma implantação local usando o script de compilação Olá, nome de Olá Olá do grupo de recursos é `<your username>ConnFactoryLocal`. Agora, adicione um novo **endereço IP público** grupo de recursos toohello de recursos.

> [!NOTE]
> Em qualquer caso, certifique-se de instalar patches mais recentes Olá seguindo as instruções de Olá Olá [Ubuntu site](https://wiki.ubuntu.com/Security/Upgrades). Manter instalação Olá backup toodate para desde que a VM está acessível por meio de um endereço IP público.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Como remover o hello pública IP endereço toohello simulação VM?

Você tem duas opções tooremove Olá endereço:

* Usar script do PowerShell Olá Simulation/Factory/Remove-SimulationPublicIp.ps1 de saudação [repositório](https://github.com/Azure/azure-iot-connected-factory). Passar o nome da implantação como um parâmetro. Para uma implantação local, use `<your username>ConnFactoryLocal`. script Hello imprime endereço IP Olá Olá VM.

* No hello portal do Azure, localize o grupo de recursos de saudação da sua implantação. Com exceção de uma implantação local, o grupo de recursos de saudação tem nome hello especificado como solução ou implantação. Para uma implantação local usando o script de compilação Olá, nome de Olá Olá do grupo de recursos é `<your username>ConnFactoryLocal`. Remover agora Olá **endereço IP público** recurso saudação do grupo de recursos.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Como entrar toohello simulação VM?

Assinatura toohello simulação VM só tem suporte se você tiver implantado a solução usando o script do PowerShell Olá `build.ps1` em Olá [repositório](https://github.com/Azure/azure-iot-connected-factory).

Se você implantar a solução de saudação do www.azureiotsuite.com, você não pode entrar toohello VM. Você não pode entrar, porque a senha de saudação é gerada aleatoriamente e não é possível redefini-lo.

1. Adicione um toohello de endereço IP público VM. Consulte [como adicionar uma simulação da toohello de endereço do IP pública VM?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Criar uma sessão SSH tooyour VM usando o endereço IP Olá Olá VM.
1. Olá toouse de nome de usuário é: `docker`.
1. Olá senha toouse depende da versão Olá usado toodeploy:
    * Para soluções implantadas usando o script de build.ps1 Olá antes de 1 de junho de 2017, senha Olá é: `Passw0rd`.
    * Em soluções implantadas usando o script de build.ps1 Olá após 1 de junho de 2017, você pode encontrar senha Olá em Olá `<name of your deployment>.config.user` arquivo. Olá senha é armazenada no hello **VmAdminPassword** configuração. Olá senha é gerada aleatoriamente no momento da implantação, a menos que você especificar usando Olá `build.ps1` parâmetro do script`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Como parar e iniciar todos os processos de docker em simulação de saudação VM?

1. Entrar toohello simulação VM. Consulte [como assinar o toohello simulação VM?](#how-do-i-sign-in-to-the-simulation-vm)
1. toocheck quais contêineres estão ativos, execute: `docker ps`.
1. execução de todos os contêineres de simulação, toostop: `./stopsimulation`.
1. toostart todos os contêineres de simulação:
    * Exportar uma variável de shell com o nome da saudação **IOTHUB_CONNECTIONSTRING**. Usar valor Olá Olá **IotHubOwnerConnectionString** definindo no hello `<name of your deployment>.config.user` arquivo. Por exemplo:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Execute `./startsimulation`.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Como atualizar o simulação de saudação em Olá VM?

Se você tiver feito alterações toohello simulação, você pode usar o script do PowerShell Olá `build.ps1` em Olá [repositório](https://github.com/Azure/azure-iot-connected-factory) usando Olá `updatedimulation` comando. Esse script cria todos os componentes de simulação hello, para de simulação de saudação em Olá VM, carrega, instala e inicia-los.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Como descobrir cadeia de caracteres de conexão de saudação do hub IoT de saudação usado pelo minha solução?

Se você implantou sua solução com hello `build.ps1` script hello [repositório](https://github.com/Azure/azure-iot-connected-factory), cadeia de caracteres de conexão de saudação é o valor de saudação do **IotHubOwnerConnectionString** em Olá `<name of your deployment>.config.user` arquivo.

Você também pode encontrar a cadeia de caracteres de conexão de saudação usando Olá portal do Azure. No hello recurso IoT Hub no grupo de recursos de saudação da sua implantação, localize as configurações de cadeia de caracteres de conexão de saudação.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Quais dispositivos de IoT Hub Olá para uso de simulação conectados de fábrica?

Olá simulação self registra Olá seguintes dispositivos:

* proxy.beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.rio.corp.contoso
* proxy.seattle.corp.contoso
* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Usando Olá [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) ou [Gerenciador de Hub IOT](https://github.com/azure/iothub-explorer) ferramenta, você pode verificar quais dispositivos são registrados com o hub IoT de saudação sua solução está usando. toouse essas ferramentas, você precisa cadeia de caracteres de conexão Olá para o hub IoT de saudação em sua implantação.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Como posso obter dados de log de componentes de simulação Olá?

Todos os componentes de simulação Olá registrar informações em arquivos de toolog. Esses arquivos podem ser encontrados no hello VM na pasta Olá `home/docker/Logs`. logs de saudação tooretrieve, você pode usar o script do PowerShell Olá `Simulation/Factory/Get-SimulationLogs.ps1` em Olá [repositório](https://github.com/Azure/azure-iot-connected-factory).

Esse script precisa toosign em toohello VM. Talvez seja necessário tooprovide credenciais para entrar no hello. Consulte [como assinar o toohello simulação VM?](#how-do-i-sign-in-to-the-simulation-vm) toofind credenciais de saudação.

script Hello adiciona/remove um toohello de endereço IP público VM, se ele ainda não tiver um e remove-o. script Hello coloca todos os arquivos de log em um arquivo morto e downloads de estação de trabalho de desenvolvimento tooyour Olá arquivamento.

Como alternativa, faça logon toohello VM por meio do SSH e inspecionar os arquivos de log de saudação em tempo de execução.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Como verificar se simulação hello está enviando dados toohello na nuvem?

Com hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) ou hello [Gerenciador de Hub IOT](https://github.com/azure/iothub-explorer) ferramenta, você pode inspecionar dados saudação enviados tooIoT Hub de determinados dispositivos. toouse essas ferramentas, você precisa cadeia de caracteres de conexão do tooknow Olá para o hub IoT de saudação em sua implantação. Consulte [como descobrir cadeia de caracteres de conexão de saudação do hub IoT de saudação usado pelo minha solução?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Inspecione dados de saudação enviados por um dos dispositivos de publicador hello:

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Se você ver os dados enviados tooIoT Hub, há um problema com a simulação de saudação. Como uma primeira etapa de análise, você deve analisar arquivos de log Olá dos componentes de simulação de saudação. Consulte [como posso obter dados de log da saudação componentes de simulação?](#how-can-i-get-log-data-from-the-simulation-components) Em seguida, tente toostop e iniciar Olá simulação e se ainda não há nenhum dado enviado, atualizar simulação Olá completamente. Consulte [como atualizar a simulação de saudação em Olá VM?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Próximas etapas

Você também pode explorar alguns Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:

* [Visão geral da solução pré-configurada de manutenção preditiva](iot-suite-predictive-overview.md)
* [Visão geral da solução pré-configurada de fábrica conectada](iot-suite-connected-factory-overview.md)
* [Segurança de IoT da saudação de plano de fundo para cima](securing-iot-ground-up.md)
