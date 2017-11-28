---
title: "aaaSign ins após várias falhas"
description: "Um relatório que indica os usuários que obtiveram êxito após várias tentativas de entrada malsucedidas consecutivas."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="51d04-103">Entradas após várias falhas</span><span class="sxs-lookup"><span data-stu-id="51d04-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="51d04-104">Este relatório indica os usuários que obtiveram êxito após várias tentativas de entrada malsucedidas consecutivas.</span><span class="sxs-lookup"><span data-stu-id="51d04-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="51d04-105">Entre as possíveis causas estão:</span><span class="sxs-lookup"><span data-stu-id="51d04-105">Possible causes include:</span></span>

* <span data-ttu-id="51d04-106">O usuário esqueceu a senha</span><span class="sxs-lookup"><span data-stu-id="51d04-106">User had forgotten their password</span></span></li><li><span data-ttu-id="51d04-107">O usuário é vítima de saudação de um ataque de força bruta de adivinhação de senha com êxito</span><span class="sxs-lookup"><span data-stu-id="51d04-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="51d04-108">Os resultados desse relatório mostrará Olá o número de tentativas consecutivas sem entrar feitas toohello anterior bem-sucedida-entrar e um carimbo associado Olá entrar pela primeira vez com êxito.</span><span class="sxs-lookup"><span data-stu-id="51d04-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="51d04-109">**Configurações de relatório**: você pode configurar o número mínimo de saudação de entrada com falha consecutivas nas tentativas que devem ocorrer antes que ele pode ser exibido no relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="51d04-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="51d04-110">Quando você faz alterações toothis configurá-lo é importante toonote que essas alterações não serão aplicada tooany existente com falha entradas que aparecem no relatório existente no momento.</span><span class="sxs-lookup"><span data-stu-id="51d04-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="51d04-111">No entanto, eles serão aplicadas tooall futuras entradas. Relatório de alterações de toothis só pode ser feito por administradores licenciados.</span><span class="sxs-lookup"><span data-stu-id="51d04-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Entradas após várias falhas](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

