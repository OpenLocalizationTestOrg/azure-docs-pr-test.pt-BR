---
title: "coleções de nuvem do RemoteApp aaaTroubleshoot - criação | Microsoft Docs"
description: "Saiba como tootroubleshoot RemoteApp nuvem falhas na criação de coleção"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Solucionar problemas na criação de coleções em nuvem do RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Se você estiver tendo problemas ao criar uma coleção de nuvem, confira Olá informações a seguir.

## <a name="your-image-is-invalid"></a>A imagem é inválida
Se você vir uma mensagem como "GoldImageInvalid" quando você está esperando por Azure tooprovision sua coleção, isso significa que a imagem de modelo não atende a saudação [definido requisitos de imagem](remoteapp-imagereqs.md). Assim, vá ler os [requisitos](remoteapp-imagereqs.md), corrija sua imagem e tente toocreate sua coleção novamente.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Erros comuns vistos no portal de gerenciamento do Azure Olá
    DNS server could not be reached
    ProvisioningTimeout

Coleções de nuvem geralmente falham durante a criação por você estar usando imagens personalizadas.  Se você vir um Olá acima erros e você estiver usando uma coleção de saudação toocreate imagem personalizada, consulte Olá coisas a seguir:

* Certifique-se de que essa imagem personalizada Olá carregado atende aos requisitos de imagem.
* Problema comum geralmente Olá é que imagem Olá não foi corretamente submetida a Sysprep.  
* Verifique se imagem Olá pode inicializar dentro do Hyper-V ou tente criar uma VM IAAS diretamente na sua assinatura do Azure usando a imagem de saudação. Se Olá VM falhar tooboot e não iniciar, em seguida, isso geralmente indica que essa imagem personalizada Olá não estava preparada corretamente.  Verifique se a imagem personalizada Olá foi criada seguindo hello como toocreate um modelo personalizado de imagem do RemoteApp

Se você estiver usando uma das imagens do Microsoft hello incluídas com sua assinatura, tente toocreate a coleção de saudação novamente. Se Olá problema persistir, entre em contato com o suporte da Microsoft.

    PlatformImageTrialModeOnly

Se você vir esse erro geral, isso significa que foram atualizados tooa paga conta, mas você está tentando toouse uma imagem fornecido pela Microsoft que é válida somente durante o modo de avaliação de saudação do serviço de saudação. Nesse caso, tente toocreate novamente sua coleção de nuvem, mas se toospecify Olá correto imagem.

