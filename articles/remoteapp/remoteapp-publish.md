---
title: aaaPublish um aplicativo no Azure RemoteApp | Microsoft Docs
description: Saiba como toopublish aplicativos e recursos no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Como toopublish um aplicativo no RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Depois de criar sua coleção do RemoteApp, você precisará toopublish Olá aplicativos ou recursos que você deseja toomake disponível para seus usuários. Olá imagens de modelo fornecidas com sua assinatura tem apenas alguns aplicativos publicados por padrão, - tooshare Olá outros aplicativos, você precisa toopublish-los.

> [!NOTE]
> Você precisa de um aplicativo de tooupdate? Você precisará de muito[atualização Olá imagem](remoteapp-update.md) primeiro.
> 
> 

Em Olá **publicação** no portal de saudação, clique em **publicar**. Você pode adicionar um aplicativo de sua imagem de modelo **iniciar** menu ou forneça Olá caminho toowhere Olá aplicativo está instalado na imagem de modelo hello. Se você escolher tooadd Olá **iniciar** menu, escolha Olá aplicativo toopublish Olá lista. Se você escolher tooprovide Olá caminho toohello aplicativo, insira um nome para o aplicativo hello e Olá caminho toohello aplicativo. Usar variáveis no caminho Olá - por exemplo, "% systemdrive %" em vez de "c:\".

> [!NOTE]
> Se você quiser tooadd seu aplicativo de saudação **iniciar** menu, você precisa toohave *adicionado toohello esse aplicativo **iniciar** menu em sua imagem de modelo.* Caso contrário, RemoteApp só verá o que *é* em Olá **iniciar** menu e você será confuso. 
> 
> toomake-se de que seu aplicativo estiver em Olá **iniciar** menu, colocar um arquivo de atalho - **. lnk** - Olá %systemdrive%\ProgramData\Microsoft\Windows\Start Iniciar\Programas pasta.
> 
> Se você esqueceu tooadd Olá aplicativo toohello **iniciar** menu quando você criou o modelo de saudação, escolha tooadd Olá caminho toohello aplicativo. (Ou recrie a imagem do seu modelo, mas é muito mais trabalhoso.)
> 
> 

