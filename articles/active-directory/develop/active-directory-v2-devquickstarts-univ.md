---
title: aaaAzure AD v 2.0 aplicativo Universal do Windows | Microsoft Docs
description: "Como toobuild um aplicativo Universal do Windows que entra usuários com ambos os Account pessoal da Microsoft e contas corporativa ou escolar."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: d2c92b65-3c1d-46d1-81c8-88f32f6b2c4b
ms.service: active-directory
ms.workload: identity
ms.topic: article
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.date: 02/20/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 49b26c74fa5a76664c3229256c9bd128563b830c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-universal-app-using-hello-v20-endpoint"></a><span data-ttu-id="1442a-103">Adicionar entrada tooa aplicativo Universal do Windows usando o ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="1442a-103">Add sign-in tooa Windows Universal app using hello v2.0 endpoint</span></span>
  <span data-ttu-id="1442a-104">tutorial de início rápido de saudação para aplicativos universais do Windows não está totalmente pronta... Verifique novamente em breve e procure as atualizações de @AzureAD no Twitter.</span><span class="sxs-lookup"><span data-stu-id="1442a-104">hello quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="1442a-105">Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="1442a-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="1442a-106">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1442a-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="1442a-107">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="1442a-107">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

