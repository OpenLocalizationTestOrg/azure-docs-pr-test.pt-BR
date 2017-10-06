---
title: "Visão geral do Mobile Engagement Web SDK do aaaAzure | Microsoft Docs"
description: "Olá procedimentos para Olá Web SDK e atualizações mais recentes para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a>SDK Web do Azure Mobile Engagement
Comece aqui para todos os detalhes sobre como de hello toointegrate do Azure Mobile Engagement em um aplicativo web. Se você quiser toogive-lo um bloco try antes da introdução com seu próprio aplicativo web, consulte nosso [tutorial de 15 minutos](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Procedimentos de integração
1. Saiba [como toointegrate Mobile Engagement em seu aplicativo web](mobile-engagement-web-integrate-engagement.md).
2. Para a implementação do plano de marca, saiba [como toouse Olá avançado marcação API em seu aplicativo web do Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Notas de versão
### <a name="202-10182016"></a>2.0.2 (18/10/2016)
* Falha corrigida na navegação particular (Safari).
* Falha corrigida em navegadores com cookies desabilitados.

Para todas as versões, consulte Olá [concluir notas de versão](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Procedimentos de atualização
### <a name="upgrade-from-121-too200"></a>Atualização do 1.2.1 too2.0.0
Olá seções a seguir descrevem como toomigrate uma integração do SDK do Mobile Engagement Web do serviço de Capptain hello, oferecido pelo Capptain SAS, aplicativo do Azure Mobile Engagement tooan. Se você estiver migrando de uma versão anterior que 1.2.1, consulte Olá Capptain site toomigrate too1.2.1 pela primeira vez e aplique Olá procedimentos a seguir.

Não dá suporte a esta versão do Olá Web SDK do Mobile Engagement Samsung Smart TV, Opera TV, webOS ou recurso de alcance hello.

> [!IMPORTANT]
> Capptain e do Azure Mobile Engagement não são Olá mesmo serviço e Olá procedimentos realce apenas como toomigrate Olá aplicativo cliente. Migrando Olá Web SDK do Mobile Engagement no aplicativo hello não serão migrados para os dados de um Capptain tooa Mobile Engagement server.
> 
> 

#### <a name="javascript-files"></a>Arquivos JavaScript
Substitua saudação de arquivo capptain-sdk.js com o arquivo de saudação do azure-engagement.js e atualize seu script importa adequadamente.

#### <a name="remove-capptain-reach"></a>Remover o Capptain Reach
Esta versão do Olá Web SDK do Mobile Engagement não dá suporte a recurso de alcance hello. Se você tiver integrado o alcance de Capptain em seu aplicativo, você precisa tooremove-lo.

Remover Olá alcançar CSS importar sua página e excluir o arquivo. CSS relacionados de saudação (capptain-reach.css, por padrão).

Excluir Olá alcance recursos a seguir: Olá fechar imagem (capptain-close.png, por padrão) e o ícone de marca de saudação (capptain--ícone de notificação, por padrão).

Remova hello alcançar da interface do usuário para notificações no aplicativo. layout da saudação padrão tem esta aparência:

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

Remova Olá alcançar da interface do usuário para notificações de texto e da web e pesquisas. layout da saudação padrão tem esta aparência:

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

Remover Olá `reach` do objeto de configuração, se ele existir. Ele tem esta aparência:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Remova qualquer outra personalização do Reach, como categorias.

#### <a name="remove-deprecated-apis"></a>Remover APIs substituídas
Algumas APIs de Capptain são preteridos no Olá Web SDK do Mobile Engagement.

Remova qualquer toohello chamadas seguintes APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.

Remova qualquer Olá retornos de chamada a seguir da configuração do seu Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.

#### <a name="configuration"></a>Configuração
Mobile Engagement usa uma conexão cadeia de caracteres tooconfigure SDK os identificadores, por exemplo, o identificador de aplicativo hello.

Substitua a ID do aplicativo de saudação com a cadeia de caracteres de conexão. Observe o objeto global Olá de saudação configuração SDK é alterado de `capptain` muito`azureEngagement`.

Antes da migração:

    window.capptain = {
      appId: ...,
      [...]
    };

Após a migração:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no portal do Azure de saudação.

#### <a name="javascript-apis"></a>APIs do JavaScript
objeto de JavaScript global Olá `window.capptain` foi renomeado `window.azureEngagement`, mas você pode usar o hello `window.engagement` alias para chamadas de API. Você não pode usar essa configuração de SDK do alias toodefine hello.

Por exemplo: `capptain.deviceId` se torna `engagement.deviceId`, `capptain.agent.startActivity` se torna `engagement.agent.startActivity` e assim por diante.

Se você já tiver integrado uma versão anterior do Olá Web SDK do Azure Mobile Engagement em seu aplicativo, leia sobre [atualizar procedimentos](mobile-engagement-web-upgrade-procedure.md).

