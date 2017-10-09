---
title: aaaValidate hello Azure VNET toouse com o Azure RemoteApp | Microsoft Docs
description: "Saiba como toomake-se de que sua rede virtual do Azure está pronto toouse com o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>Validar Olá toouse de rede virtual do Azure com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Antes de usar uma rede virtual do Azure com o Azure RemoteApp, talvez você queira Olá toovalidate VNET. Isso ajuda a evitar problemas com conectividade.

toovalidate VNET do Azure, Olá a seguir:

1. Crie uma máquina virtual do Azure Olá sub-rede de saudação VNET do Azure que você deseja toouse com o Azure RemoteApp.
2. Conecte-se toothat VM usando Olá **conectar** opção no portal de gerenciamento de saudação.
3. Unir Olá máquina virtual toohello mesmo domínio que você deseja toouse com o Azure RemoteApp. Se você estiver criando uma coleção híbrida que se conecta a rede de local de tooyour, ingresse no domínio local do tooyour Olá máquina virtual.

Se for bem-sucedida, Olá VNET do Azure está pronto toouse com o RemoteApp.

Para obter mais informações sobre o fluxo de trabalho de coleta do hello híbrida de ponta a ponta, consulte Olá artigos a seguir:

* [Como tooplan sua rede virtual do Azure RemoteApp](remoteapp-planvnet.md)
* [Criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md)
* [Implantar o Azure RemoteApp coleção tooyour rede Virtual do Azure (com suporte para o ExpressRoute)](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

