---
title: uso de Caches Redis aaaManaging hello Azure Explorer para IntelliJ | Microsoft Docs
description: Saiba como toomanage o redis do Azure armazena em cache usando hello Azure Explorer para IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a>Gerenciando Caches Redis usando hello Azure Explorer para IntelliJ

Olá Explorer do Azure, que faz parte da saudação Kit de ferramentas do Azure para IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar caches em sua conta do Azure de dentro de redis Olá IntelliJ IDE.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Criar um Cache Redis utilizando IntelliJ

Olá, as etapas a seguir mostram Olá etapas toocreate um cache redis usando hello Azure Explorer.

1. Entrar tooyour conta do Azure usando as etapas de saudação em Olá [entrada em instruções hello Azure Toolkit for IntelliJ] artigo.

1. Em hello **Azure Explorer** janela de ferramenta, expanda Olá **Azure** nó, clique com botão direito **Caches Redis**e, em seguida, clique em **criar Cache Redis**.

   ![Criar menu Cache Redis][CR01]

1. Olá quando **novo Cache Redis** caixa de diálogo aparece, especifique Olá as opções a seguir:

   ![Criar uma caixa de diálogo Novo Cache Redis][CR02]

   a. **Nome DNS**: Especifica o subdomínio DNS Olá Olá novo redis cache, que são pré-anexados muito ". redis.cache.windows .net"; por exemplo: *wingtiptoys.redis.cache.windows.net*.

   b. **Assinatura**: especifica Olá assinatura do Azure que você deseja toouse para cache redis da nova hello.

   c. **Grupo de recursos**: Especifica o grupo de recursos de saudação do cache redis; é necessário toochoose de saudação as opções a seguir:
      * **Criar novo**: Especifica que você deseja toocreate um novo grupo de recursos.
      * **Usar Existente**: especifica que você escolherá entre uma lista dos grupos de recursos associados à sua conta do Azure.

   d. **Local**: especifica Olá local em que o cache redis é criado; por exemplo, *Oeste dos EUA*.

   e. **Camada de preços**: especifica qual tipo de preço usa o cache redis; essa configuração determina o número de saudação de conexões de cliente. (Para saber mais, veja [Preço do Cache Redis]).

   f. **Porta não SSL**: especifica se o cache redis permite conexões não SSL; por padrão, apenas as conexões SSL são permitidas.

1. Quando tiver especificado todas as configurações de cache redis, clique em **OK**.

Depois que o cache redis tiver sido criado, ele será exibido no hello Azure Explorer.

   ![Cache Redis no Azure Explorer][CR03]

> [!NOTE]
>
> Para obter mais informações sobre como configurar o Azure redis as configurações de cache, consulte [como tooconfigure Cache Redis do Azure].
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a>Exibir as propriedades de saudação do Cache Redis no IntelliJ

1. Em hello Azure Explorer, mouse seu cache redis e clique em **Mostrar propriedades**.

   ![Azure Explorer contexto menu toodisplay propriedades para um cache redis][SP01]

1. Hello Azure Explorer exibe as propriedades de saudação do cache redis.

   ![Propriedades de cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Exclua o Cache Redis utilizando o IntelliJ

1. Em hello Azure Explorer, mouse seu cache redis e clique em **excluir**.

   ![Explorer contexto menu toodelete um cache redis do Azure][DE01]

1. Clique em **Sim** quando solicitado toodelete seu cache redis.

   ![Excluir prompt do cache redis][DE02]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Para obter mais informações sobre caches redis do Azure, as definições de configuração e preços, consulte Olá links a seguir:

* [Cache Redis do Azure]
* [Documentação do Cache Redis]
* [Preço do Cache Redis]
* [como tooconfigure Cache Redis do Azure]

<!-- URL List -->

[Preço do Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis do Azure]: https://azure.microsoft.com/services/cache/
[Documentação do Cache Redis]: ./redis-cache/index.md
[como tooconfigure Cache Redis do Azure]: ./redis-cache/cache-configure.md
[entrada em instruções hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
