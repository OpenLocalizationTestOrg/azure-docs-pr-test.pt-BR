---
title: aplicativos aaaUsing App-V com o Azure RemoteApp | Microsoft Docs
description: Saiba como aplicativos toouse App-V no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Usando os aplicativos App-V no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Você pode usar os aplicativos do App-V em uma coleção híbrida do Azure RemoteApp, o que requer o ingresso no domínio.

Antes de começar, certifique-se de cliente de App-V 5.1 Olá tooinstall com atualizações mais recentes de saudação. Você precisará toocreate um [imagem personalizada](remoteapp-create-custom-image.md) que inclui o cliente Olá App-V.  

É fácil toouse sua infraestrutura existente do App-V com o Azure RemoteApp. Como uma coleção híbrida é implantada em uma rede virtual do Azure com o controlador de domínio do acesso tooyour e VMs Olá são ingressados no domínio, você pode aproveitar seu existente aplicativo App-v infraestrutura e a implantação de métodos tooeasyily host App-V no Azure RemoteApp. Aqui estão algumas considerações que você deve estar atento, com base no tipo de saudação da implantação do App-V que no momento:

| Opções de configuração |  | Positivo | Negativo |
| --- | --- | --- | --- |
| Método de entrega |Streaming (por demanda) |Aplicativo é sempre Olá nova e mais recente |Latência da primeira vez |
| Montado |Mais rápido; aplicativo já está presente no hello VM |Inchaço - ocupa o espaço da imagem (limite de 127 GB) | |
| Armazenamento de local de aplicativo |Conteúdo compartilhado |O aplicativo é executado na memória da instância do Azure RemoteApp |Consome memória e boa conexão toostreaming (arquivo) servidor em que reside o aplicativo hello |
| Disco (em cache) |Execução rápida. O aplicativo não depende de disponibilidade da Fonte de Conteúdo |Inchaço - ocupa o espaço da imagem (limite de 127 GB) | |
| Direcionamento |Usuário |Exige a infraestrutura completa do App-V autônomo | |
| Global (máquina) |Pré-publicar ou destinar usando o servidor de Publicação |Necessário tooupdate sua imagem do Azure se você quiser tooupdate Olá aplicativo (grande). Ocupa algum espaço na imagem. | |

 Depois de criar sua imagem personalizada e sua coleção híbrida, publique seu aplicativo, atribuir usuários e aproveitar seus aplicativos existentes do App-V hospedados no Azure RemoteApp entregues tooany dispositivo em qualquer lugar.

