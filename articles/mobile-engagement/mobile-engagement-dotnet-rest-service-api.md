---
title: "Olá aaaUsing tooaccess da API REST APIs de serviço do Azure Mobile Engagement"
description: "Descreve como toouse Olá tooaccess de APIs de REST do Mobile Engagement APIs de serviço do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a>Usando REST tooaccess APIs de serviço do Azure Mobile Engagement
O Azure Mobile Engagement fornece Olá [API REST do Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) para você toomanage dispositivos, campanhas de alcance/enviar por Push etc.

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Se você não quiser toouse Olá APIs REST diretamente, nós também fornecemos um [arquivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que você pode usar com ferramentas toogenerate SDKs para seu idioma preferencial. É recomendável usar Olá [AutoRest](https://github.com/Azure/AutoRest) ferramenta toogenerate o SDK do nosso arquivo Swagger. Criamos um SDK .NET de maneira semelhante, que permite que você toointeract com essas APIs usando um wrapper em c# e você não tiver toodo Olá negociação do token de autenticação e atualização por conta própria. Consulte [amostra do SDK do serviço de API .NET](mobile-engagement-dotnet-sdk-service-api.md) toolearn como toouse Olá .net SDK para API
