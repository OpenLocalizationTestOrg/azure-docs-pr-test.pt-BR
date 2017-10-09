---
title: "filtros de conexão de IP de Hub IoT aaaAzure | Microsoft Docs"
description: "Como endereços IP de toouse tooblock conexões de IP específica de filtragem para tooyour Azure IoT hub. Você pode bloquear conexões de endereços IP individuais ou de intervalos de endereços IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>Usar filtros IP

A segurança é um aspecto importante de qualquer solução de IoT com base no Hub IoT do Azure. Às vezes você precisa tooexplicitly especificar endereços IP de saudação do qual o dispositivo pode se conectar como parte da configuração de segurança. Olá _filtro IP_ recurso permite que as regras de tooconfigure para rejeitar ou aceitar tráfego de endereços IPv4 específicos.

## <a name="when-toouse"></a>Quando toouse

Há dois casos de uso específicos quando se trata de pontos de extremidade de Hub IoT Olá de tooblock úteis para determinados endereços IP:

- O Hub IoT deve receber tráfego somente de um intervalo específico de endereços IP e rejeitar todo o resto. Por exemplo, você está usando o hub IoT com [rota expressa do Azure] toocreate de conexões privadas entre um hub IoT e sua infraestrutura local.
- É necessário tooreject tráfego de endereços IP que foram identificados como suspeita pelo administrador de hub IoT hello.

## <a name="how-filter-rules-are-applied"></a>Como são aplicadas as regras de filtro

regras de filtro IP Hello são aplicadas em Olá nível de serviço de IoT Hub. Portanto regras de filtro IP hello aplicam tooall conexões de dispositivos e aplicativos de back-end usando qualquer protocolo com suporte.

Todas as tentativas de conexão de um endereço IP que corresponde a uma regra IP de rejeição em seu Hub IoT recebem um código de status 401 não autorizado e uma descrição. mensagem de resposta de saudação não mencionar a regra de IP hello.

## <a name="default-setting"></a>Configuração padrão

Por padrão, Olá **filtro IP** grade no portal de saudação para um hub IoT está vazio. Essa configuração padrão significa que o hub aceita conexões de qualquer endereço IP. Essa configuração padrão é a regra de tooa equivalente que aceita o intervalo de endereços IP hello 0.0.0.0/0.

![Configurações de filtro IP padrão do Hub IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>Adicionar ou editar uma regra de filtro IP

Quando você adiciona uma regra de filtro IP, você será solicitado para Olá valores a seguir:

- Um **nome de regra de filtro IP** que deve ser uma cadeia de caracteres exclusiva, diferencia maiusculas de minúsculas, alfanumérica backup too128 caracteres. Somente caracteres alfanuméricos de saudação ASCII de 7 bits mais `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` são aceitas.
- Selecione um **rejeitar** ou **aceitar** como Olá **ação** para regra de filtro IP hello.
- Forneça um endereço IPv4 único ou um bloco de endereços IP na notação CIDR. Por exemplo, CIDR notação 192.168.100.0/22 representa os endereços IPv4 Olá 1024 de 192.168.100.0 too192.168.103.255.

![Adicionar um hub IoT do IP filtro regra tooan][img-ip-filter-add-rule]

Depois de salvar regra Olá, verá um alerta, notificando que essa atualização Olá estiver em andamento.

![Notificação sobre como salvar uma regra de filtro IP][img-ip-filter-save-new-rule]

Olá **adicionar** opção é desabilitada quando você atingir o máximo de saudação de 10 regras de filtro IP.

Você pode editar uma regra existente clicando duas vezes em linha hello que contém a regra de saudação.

> [!NOTE]
> Rejeitar IP endereços podem impedir que outros serviços do Azure (como o Stream Analytics do Azure, máquinas virtuais do Azure ou Olá Gerenciador de dispositivo no portal de saudação) interagir com o hub IoT de saudação.

> [!WARNING]
> Se você usar mensagens de tooread de análise de fluxo do Azure (ASA) de um hub IoT com a filtragem de IP habilitado, use o nome de Hub de eventos-compatível com de Olá e ponto de extremidade do seu IoT Hub em Olá cadeia de caracteres de conexão ASA.

## <a name="delete-an-ip-filter-rule"></a>Excluir uma regra de filtro IP

toodelete uma regra de filtro IP, selecione uma ou mais regras no hello grade e clique em **excluir**.

![Excluir uma regra de filtro IP de Hub IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>Avaliação da regra de filtro IP

Regras de filtro IP são aplicadas na ordem e a primeira regra de saudação que corresponde ao endereço IP de saudação determina Olá aceitar ou rejeitar a ação.

Por exemplo, se você quiser tooaccept endereços Olá intervalo 192.168.100.0/22 e rejeitar tudo, a primeira regra Olá na grade de saudação deve aceitar Olá endereço intervalo 192.168.100.0/22. próxima regra do Hello deve rejeitar todos os endereços usando o intervalo de saudação 0.0.0.0/0.

Você pode alterar a ordem de saudação as regras de filtro IP na grade de saudação clicando em três pontos verticais Olá no início de saudação de uma linha e usando arrastar e soltar.

filtro de seu novo IP toosave ordem de regras, clique em **salvar**.

![Alterar a ordem das regras de filtro de IP de Hub IoT Olá][img-ip-filter-rule-order]

## <a name="next-steps"></a>Próximas etapas

toofurther explorar recursos de saudação do IoT Hub, consulte:

- [Monitoramento de operações][lnk-monitor]
- [Métricas do Hub IoT][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[rota expressa do Azure]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md