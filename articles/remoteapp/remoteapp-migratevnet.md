---
title: toomigrate aaaHow de tooan uma VNET do RemoteApp VNET do Azure | Microsoft Docs
description: Saiba como toomigrate de tooan uma VNET do RemoteApp VNET do Azure
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Como toomigrate uma coleção híbrida de tooan uma VNET do RemoteApp VNET do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Boas notícias! Habilitamos coleções do RemoteApp híbrida toodeploy diretamente no seu existente do Azure redes virtuais (VNETs) em vez de criar VNETs RemoteApp específicos. Isso permite que você tire proveito de hello mais recentes recursos de rede virtual (como a rota expressa) e dê sua tooother de acesso direto rede híbrida coleções serviços do Azure e máquinas virtuais implantadas toothat VNET.  (Isso apresenta um desempenho melhor e mais fácil instalação que configurações de VNET para VNET).

Digamos que você já criou uma coleção híbrida de RemoteApp chamada *ColeçãoOriginal* com uma VNET do RemoteApp chamada *RemoteAppVNET*. Aqui estão Olá etapas toomigrate-tooa nova rede virtual do Azure chamado *AzureVNET*.

1. Em Olá **redes** guia Olá [portal de gerenciamento](http://manage.windowsazure.com/), crie uma rede virtual chamada *AzureVNET*usando hello mesmo local, a configuração de DNS e o espaço de endereço (para pelo menos um de saudação *AzureVNET* sub-redes) que você usou para *RemoteAppVNET*.
2. Configurar *AzureVNET* tooeither de host ou tem conectividade de rede toohello implantação de Active Directory que *OriginalCollection* é integrado ao domínio.
3. Em Olá **RemoteApps** guia, crie uma nova coleção do RemoteApp chamada *nova coleção*. (Olá use **criar com uma rede virtual** opção, não **criação rápida**.)
4. Configurar *NewCollection* toobe implantado sub-rede tooa *AzureVNET*.
5. Configurar *NewCollection* toouse Olá a mesma imagem e informações de associação de domínio que você usou para *OriginalCollection*.
6. Após algumas horas, *NovaColeção* aparecerá na sua lista de coleções com um estado Ativo.

Agora, se você não precisa toomigrate qualquer informação de usuário do hello original toohello nova coleção, segue estas etapas:

1. Exclua *ColeçãoOriginal*.
2. Exclua *RemoteAppVNET*.

E pronto!

Como alternativa, se você precisar de informações de usuário de toomigrate de saudação original toohello nova coleção, segue estas etapas:

1. Enviar um email muito[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) com sua ID de assinatura do Azure, Olá nome de sua coleção original e o nome de saudação da nova coleção e peça-lhes toomigrate as informações do usuário.
2. Dentro de 2 dias úteis o equipe do RemoteApp Olá moverá lista de acesso de usuário hello e todos os documentos do usuário e configurações de usuário do hello original toohello nova coleção.
3. Exclua *ColeçãoOriginal*.
4. Exclua *RemoteAppVNET*.

E pronto!

Se você tiver dúvidas ou precisar de ajuda especial, envie um email para [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

