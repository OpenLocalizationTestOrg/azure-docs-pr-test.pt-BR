---
title: Atividades de entrada irregulares
description: "Um relatório que inclui entradas identificadas como anômalas pelos nossos algoritmos de aprendizado de máquina."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a><span data-ttu-id="e7ca5-103">Atividades de entrada irregulares</span><span class="sxs-lookup"><span data-stu-id="e7ca5-103">Irregular sign-in activity</span></span>
<span data-ttu-id="e7ca5-104">Entradas irregulares são aquelas que foram identificadas por nossos algoritmos de aprendizado de máquina, com base em uma condição de “viagem impossível” combinada a um dispositivo e um local de entrada anômalos.</span><span class="sxs-lookup"><span data-stu-id="e7ca5-104">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign in location and device.</span></span> <span data-ttu-id="e7ca5-105">Isso pode indicar que um hacker entrou com êxito usando essa conta.</span><span class="sxs-lookup"><span data-stu-id="e7ca5-105">This may indicate that a hacker has successfully signed in using this account.</span></span>
<span data-ttu-id="e7ca5-106">Enviaremos uma notificação por email aos administradores globais se encontrarmos 10 ou mais eventos de entrada anômalos dentro de um período de 30 dias ou menos.</span><span class="sxs-lookup"><span data-stu-id="e7ca5-106">We will send an email notification to the global admins if we encounter 10 or more anomalous sign-in events within a span of 30 days or less.</span></span> <span data-ttu-id="e7ca5-107">Inclua aad-alerts-noreply@mail.windowsazure.com em sua lista de remetentes seguros.</span><span class="sxs-lookup"><span data-stu-id="e7ca5-107">Please be sure to include aad-alerts-noreply@mail.windowsazure.com in your safe senders list.</span></span>

