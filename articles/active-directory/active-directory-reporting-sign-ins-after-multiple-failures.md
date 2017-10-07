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
# <a name="sign-ins-after-multiple-failures"></a>Entradas após várias falhas
Este relatório indica os usuários que obtiveram êxito após várias tentativas de entrada malsucedidas consecutivas. Entre as possíveis causas estão:

* O usuário esqueceu a senha</li><li>O usuário é vítima de saudação de um ataque de força bruta de adivinhação de senha com êxito

Os resultados desse relatório mostrará Olá o número de tentativas consecutivas sem entrar feitas toohello anterior bem-sucedida-entrar e um carimbo associado Olá entrar pela primeira vez com êxito.

**Configurações de relatório**: você pode configurar o número mínimo de saudação de entrada com falha consecutivas nas tentativas que devem ocorrer antes que ele pode ser exibido no relatório de saudação. Quando você faz alterações toothis configurá-lo é importante toonote que essas alterações não serão aplicada tooany existente com falha entradas que aparecem no relatório existente no momento. No entanto, eles serão aplicadas tooall futuras entradas. Relatório de alterações de toothis só pode ser feito por administradores licenciados.

![Entradas após várias falhas](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

