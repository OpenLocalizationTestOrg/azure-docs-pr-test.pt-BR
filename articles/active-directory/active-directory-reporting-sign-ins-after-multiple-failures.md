---
title: "Entradas após várias falhas"
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
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="92123-103">Entradas após várias falhas</span><span class="sxs-lookup"><span data-stu-id="92123-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="92123-104">Este relatório indica os usuários que obtiveram êxito após várias tentativas de entrada malsucedidas consecutivas.</span><span class="sxs-lookup"><span data-stu-id="92123-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="92123-105">Entre as possíveis causas estão:</span><span class="sxs-lookup"><span data-stu-id="92123-105">Possible causes include:</span></span>

* <span data-ttu-id="92123-106">O usuário esqueceu a senha</span><span class="sxs-lookup"><span data-stu-id="92123-106">User had forgotten their password</span></span></li><li><span data-ttu-id="92123-107">O usuário for vítima de uma ataque de força bruta de detecção de senha bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="92123-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="92123-108">Os resultados desse relatório mostrarão o número de tentativas consecutivas de entrada com falha feitas antes da entrada bem-sucedida e um carimbo de data/hora associado à primeira entrada bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="92123-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="92123-109">**Configurações do Relatório**: é possível configurar o número mínimo de tentativas consecutivas de entrada com falha que devem ocorrer antes que ele possa ser exibido no relatório.</span><span class="sxs-lookup"><span data-stu-id="92123-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="92123-110">Quando você fizer alterações nessa configuração, é importante observar que essas alterações não serão aplicadas a qualquer entrada com falha existente exibido no momento no relatório existente.</span><span class="sxs-lookup"><span data-stu-id="92123-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="92123-111">Todavia, elas serão aplicadas a todas as entradas futuras.</span><span class="sxs-lookup"><span data-stu-id="92123-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="92123-112">Alterações a esse relatório só podem ser feitas por administradores licenciados.</span><span class="sxs-lookup"><span data-stu-id="92123-112">Changes to this report can only be made by licensed admins.</span></span>

![Entradas após várias falhas](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

