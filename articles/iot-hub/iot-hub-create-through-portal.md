---
title: "aaaUse Olá toocreate portal do Azure um IoT Hub | Microsoft Docs"
description: "Como toocreate, gerenciar e excluir hubs de IoT do Azure por meio de saudação portal do Azure. Inclui informações sobre tipos de preço, escala, segurança e configurações de mensagens."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Criar um hub IoT usando Olá portal do Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Este artigo descreve:

* Como toofind Olá serviço de IoT Hub no hello portal do Azure.
* Como toocreate e gerenciar os hubs IoT.

## <a name="where-toofind-hello-iot-hub-service"></a>Onde toofind Olá serviço IoT Hub

Você pode encontrar hello serviço IoT Hub Olá seguintes locais no portal de saudação:

* Escolha **+ Novo**, em seguida, escolha **Internet das Coisas**.
* No hello Marketplace, escolha **Internet das coisas**.

## <a name="create-an-iot-hub"></a>Crie um hub IoT

Você pode criar um hub IoT usando Olá métodos a seguir:

* Olá **+ novo** opção abre a folha de saudação mostrada na seguinte captura de tela de saudação. Olá etapas para criar o hub IoT de saudação por este método e por meio do marketplace Olá são idênticas.
* No hello Marketplace, escolha **criar** folha de saudação tooopen mostrada na seguinte captura de tela de saudação.

Olá, seções a seguir descrevem Olá um hub IoT toocreate de várias etapas:

### <a name="choose-hello-name-of-hello-iot-hub"></a>Escolher nome de saudação do hub IoT de saudação

toocreate um hub IoT, você deve nomear o hub IoT de saudação. Esse nome deve ser exclusivo entre todos os Hubs IoT.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Escolha a saudação de preço

Você pode escolher entre quatro camadas: **Gratuita**, **Padrão 1**, **Padrão 2** e **Padrão S3**. camada gratuita Olá permite somente 500 toobe de dispositivos conectados toohello IoT hub e backup too8, 000 mensagens por dia.

**Standard S1**: edição de saudação S1 de uso para soluções de IoT com um grande número de dispositivos que cada um gerará pequenas quantidades de dados. Cada unidade de edição Olá S1 permite que até too400, 000 mensagens por dia em todos os dispositivos conectados.

**Standard S2**: edição de saudação S2 Use para soluções de IoT em quais dispositivos geram grandes quantidades de dados. Cada unidade de edição de S2 Olá permite que até too6 milhões de mensagens por dia entre todos os dispositivos conectados.

**Standard S3**: edição de saudação S3 de uso para soluções de IoT que gerem grandes quantidades de dados. Cada unidade de edição de S3 Olá permite que até too300 milhões de mensagens por dia entre todos os dispositivos conectados.

![][4]

> [!NOTE]
> O Hub IoT só permite um hub gratuito por assinatura do Azure.

### <a name="iot-hub-units"></a>Unidades do Hub IoT

número de saudação de mensagens permitido por unidade por dia depende de preço do hub. Por exemplo, se você quiser Olá ingresso de toosupport de hub IoT de 700.000 mensagens, escolha duas unidades de camada de S1.

### <a name="device-toocloud-partitions-and-resource-group"></a>Partições de toocloud do dispositivo e grupo de recursos

Você pode alterar o número de saudação de partições para um hub IoT. número de partições do saudação padrão é 4, você pode escolher um número diferente de lista suspensa de saudação.

Você não precisa tooexplicitly criar um grupo de recurso vazio. Quando você cria um recurso, você pode escolher qualquer toocreate um novo ou use um grupo de recursos existente.

![][5]

### <a name="choose-subscription"></a>Escolha uma assinatura

IoT Hub do Azure automaticamente Olá listas de conta de usuário de saudação de assinaturas do Azure está vinculado. Você pode escolher Olá assinatura do Azure tooassociate Olá IoT hub.

### <a name="choose-hello-location"></a>Escolha o local de saudação

opção de local de saudação fornece uma lista de regiões Olá onde o IoT Hub está disponível.

### <a name="create-hello-iot-hub"></a>Criar hello IoT hub

Quando todas as etapas anteriores forem concluídas, você pode criar o hub IoT de saudação. Clique em **criar** toostart Olá toocreate do processo de back-end e implantar o hub IoT de saudação com opções de saudação escolhidas.

Pode levar alguns hub IoT toocreate Olá de minutos como demora Olá toorun de implantação de back-end em servidores do hello local apropriado.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Alterar as configurações de saudação do hub IoT de saudação

Você pode alterar as configurações de saudação de um hub IoT existente depois que ele é criado da saudação folha de IoT Hub.

![][8]

**Políticas de acesso compartilhado**: essas políticas definem permissões de saudação para dispositivos e serviços tooconnect tooIoT Hub. Você pode acessar essas políticas clicando em **Políticas de acesso compartilhado** em **Geral**. Nessa folha, você pode modificar as políticas existentes ou adicionar uma nova política.

### <a name="create-a-policy"></a>Criar uma política

* Clique em **adicionar** tooopen uma folha. Aqui você pode digitar o nome da nova política hello e permissões de saudação que você deseja tooassociate com essa política, conforme mostrado na seguinte Olá Figura:

    Há várias permissões que podem ser associadas a essas políticas compartilhadas. Olá **registro ler** e **gravação de registro** políticas concederem leitura e registro de identidade de toohello de direitos de acesso de gravação. Escolhendo a opção de gravação da saudação automaticamente escolhe Olá ler opção.

    Olá **conexão de serviço** diretiva concede pontos de extremidade do serviço de permissão tooaccess como **receber o dispositivo para nuvem**. Olá **dispositivo se conectar** diretiva concede permissões para enviar e receber mensagens usando pontos de extremidade Olá IoT Hub do lado do dispositivo.

* Clique em **criar** tooadd nesse recém-criado lista existente de toohello de política.

![][10]

## <a name="endpoints"></a>Pontos de extremidade

Clique em **pontos de extremidade** toodisplay uma lista de pontos de extremidade de hub IoT Olá que você está modificando. Há dois tipos de pontos de extremidade: pontos de extremidade que são integrados ao hub IoT de saudação e pontos de extremidade que você adicione toohello IoT hub após sua criação.

![][11]

### <a name="built-in-endpoints"></a>Pontos de extremidade internos

Há dois pontos de extremidade internos: **toodevice comentários de nuvem** e **eventos**.

* **Nuvem comentários toodevice** configurações: essa configuração tem duas subsettings: **tooDevice TTL de nuvem** (time-to-live) e **tempo de retenção** (em horas) para mensagens de saudação. Quando seu primeiro criar um hub IoT, essas duas configurações tem valor padrão de saudação de uma hora. tooadjust essas configurações, use os controles deslizantes de saudação ou digite os valores de saudação.
* Configurações de **Eventos**: essa configuração tem várias subconfigurações, algumas das quais são somente leitura. Olá lista a seguir descreve essas configurações:

  * **Partições**: um valor padrão é definido quando Olá IoT hub é criado. Você pode alterar o número de saudação de partições por meio dessa configuração.

  * **Nome do evento compatível com o Hub e o ponto de extremidade**: quando Olá IoT hub é criado, um Hub de eventos é criado internamente que você pode precisar acessar toounder determinadas circunstâncias. Não é possível personalizar os valores de nome e o ponto de extremidade Olá compatível com o Hub de eventos, mas você pode copiá-los clicando **cópia**.

  * **Tempo de retenção**: definir dia tooone por padrão, mas você pode alterá-la usando a lista suspensa de saudação. Esse valor é em dias para a configuração de dispositivo para nuvem hello.

  * **Grupos de consumidores**: grupos de consumidores habilitar várias mensagens de tooread leitores independentemente do hub IoT de saudação. Todos os Hub IoT são criados com um grupo de consumidores padrão. No entanto, você pode adicionar ou excluir hubs de IoT consumidor grupos tooyour usando essa configuração.

  > [!NOTE]
  > grupo de consumidores saudação padrão não pode ser editado ou excluído.

### <a name="custom-endpoints"></a>Pontos de extremidade personalizados

Você pode adicionar pontos de extremidade personalizados em seu hub IoT usando o portal de saudação. De saudação **pontos de extremidade** folha, clique em **adicionar** em Olá tooopen superior Olá **Adicionar ponto de extremidade** folha. Digite as informações de saudação necessárias e clique em **Okey**. O ponto de extremidade personalizado agora está listado no hello principal **pontos de extremidade** folha.

![][13]

Você pode ler mais sobre pontos de extremidade personalizados em [Referência — Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].

## <a name="routes"></a>Rotas

Clique em **rotas** toomanage como o IoT Hub envia as mensagens de dispositivo para nuvem.

![][14]

Você pode adicionar o hub de IoT tooyour rotas clicando **adicionar** na parte superior de saudação do hello **rotas*** folha, inserir informações de saudação necessárias e, em seguida, clicando em **Okey**. A rota é então listada em Olá principal **rotas** folha. Você pode editar uma rota clicando na lista de saudação de rotas. tooenable uma rota, clique na lista de saudação de rotas e defina Olá **habilitado** alternar muito**Off**. alteração de saudação toosave, clique em **Okey** na parte inferior da saudação da folha de saudação.

![][15]

## <a name="pricing-and-scale"></a>Preços e dimensionamento

Olá preços de um hub IoT existente podem ser alterado por meio de saudação **preços** configurações com hello exceções a seguir:

* Na implementação atual do hello, um hub IoT com um SKU livre não é possível alterar tooone de camadas de saudação paga SKUs, ou vice-versa.
* Pode haver apenas um hub IoT de camada gratuita em Olá assinatura do Azure.

![][12]

Você pode mover de uma camada superior de toolower somente quando o número de Olá de mensagens enviadas desse dia exceder a cota de saudação de nível mais baixo de saudação. Por exemplo, se o número de saudação de mensagens por dia exceder 400.000, Olá camada para Olá IoT hub pode ser alterado. No entanto, se você alterar o nível de S1 toohello hub IoT de saudação está limitada para esse dia.

## <a name="delete-hello-iot-hub"></a>Excluir Olá IoT hub

Você pode procurar o hub IoT de toohello toodelete desejado clicando **procurar**, e escolhendo Olá toodelete hub apropriado. toodelete Olá IoT hub, clique em Olá **excluir** botão abaixo do nome de hub IoT hello.

## <a name="next-steps"></a>Próximas etapas

Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:

* [Gerenciamento em massa de dispositivos IoT][lnk-bulk]
* [Métricas do Hub IoT][lnk-metrics]
* [Monitoramento de operações][lnk-monitor]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com IoT Edge][lnk-iotedge]
* [Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
