---
title: "aaaUpdate sua coleção do RemoteApp do Azure | Microsoft Docs"
description: "Saiba como tooupdate sua coleção do RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Criar uma coleção de RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Virão um tempo, inevitavelmente, quando você precisar tooupdate Olá aplicativos ou imagem em sua coleção do RemoteApp. Se você estiver usando uma das imagens de saudação incluídas com a sua assinatura do Azure RemoteApp na coleção de uma nuvem ou híbrida, todas as atualizações são manipuladas pelo Azure RemoteApp em si, para que você possa ter fácil.

No entanto, se você estiver usando uma imagem personalizada (que é criado do zero ou que você criou, modificando uma das nossas imagens), será responsável pela manutenção de aplicativos e a imagem de saudação. Se você precisar tooupdate sua imagem ou qualquer um dos aplicativos hello dentro dele, será necessário toocreate uma nova versão da imagem de Olá e, em seguida, substituir Olá existente imagem atualizada em sua coleção com a nova imagem atualizada.

Então, como você para atualizar sua coleção? É bem simples:

1. Atualize imagem Olá usado na sua coleção. Aplique os patches ou atualizações necessárias e salve-a com um novo nome.
2. [Carregar](remoteapp-uploadimage.md) ou [importar](remoteapp-image-on-azurevm.md) tooRemoteApp essa imagem.
3. Agora, na página de coleção de saudação, clique em **atualização**.
4. Escolher imagem nova Olá Olá **imagem de modelo** lista.
5. Esta é uma parte complicada Olá - precisar toodecide como toodeal com todos os usuários que estão usando um aplicativo na coleção de saudação. Você tem Olá opções a seguir:
   
   * **Fornecer aos usuários 60 minutos após a atualização de saudação**. Assim que Olá atualização estiver concluída, Azure RemoteApp exibirá uma mensagem tooany ativa os usuários informando toosave seus trabalhos e log off e faça logon. Após 60 minutos, quaisquer usuários ativos que não tiverem feito logoff serão automaticamente desconectados. Os usuários podem fazer logon de novo imediatamente.
   * **Desconectar os usuários imediatamente**. Como Olá atualização estiver concluída, fazer logoff de todos os usuários automaticamente sem aviso. Se você escolher essa opção, os usuários poderão perder dados. No entanto, eles poderão se reconectar toohello aplicativo imediatamente.
6. Clique em atualizar de Olá Olá marca de seleção toostart.

