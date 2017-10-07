---
title: folha de resumo aaaStorSimple Array Virtual dispositivo | Microsoft Docs
description: "Descreve a folha de resumo de dispositivo Olá para o Gerenciador de dispositivos do StorSimple e explica como toouse-toomonitor integridade de saudação da sua matriz Virtual StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a>Folha resumida de dispositivo de saudação do uso para o Gerenciador de dispositivos do StorSimple conectado tooStorSimple Array Virtual

## <a name="overview"></a>Visão geral

folha de dispositivo do Gerenciador de dispositivos de StorSimple Olá fornece uma exibição resumida de uma matriz de StorSimple Virtual que está registrado com um determinado StorSimple Gerenciador de dispositivos, realçando os problemas de dispositivos que precisam de atenção do administrador do sistema. Este tutorial apresenta a folha de resumo de dispositivo hello, explica a função e o conteúdo de saudação e descreve Olá tarefas que você pode executar com esta folha.

folha de resumo de dispositivo Olá exibe Olá informações a seguir:

![Painel do dispositivo](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a>Gerenciamento

Na folha de dispositivo do StorSimple Olá, você verá opções de saudação para gerenciar seu dispositivo StorSimple. Você ver os comandos de gerenciamento de saudação na superior de saudação da folha de saudação e no lado esquerdo da saudação. Usar essas opções tooadd compartilhamentos ou volumes, ou atualizar ou fazer failover sua matriz virtual.

Olá área essentials captura algumas das propriedades de saudação importantes, como, Olá status, modelo, versão de software bem como toohello um link **IU da Web** da matriz de saudação. Se você estiver em uma rede interna, você pode iniciar diretamente Olá [interface da web local](storsimple-ova-web-ui-admin.md) tooadminister sua matriz virtual.

![Conceitos básicos do dispositivo](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a>Resumo do dispositivo StorSimple

* Olá **alertas** lado a lado fornece um instantâneo de todos os alertas ativos de saudação para sua matriz virtual, agrupado por severidade do alerta. Clique em Olá bloco tooopen Olá **alertas** folha e depois clique em um indivíduo alerta tooview mais detalhes sobre esse alerta, incluindo as ações recomendadas. Você também pode limpar o alerta de saudação se Olá problema foi resolvido.

* Olá **capacidade** Olá lado a lado exibe Olá armazenamento primário provisionado e o restante em Olá dispositivo virtual relativo toohello armazenamento total disponível para a mesma. **Provisionado** refere-se a quantidade de toohello de armazenamento preparado e alocado para uso, **restante** refere-se toohello capacidade que pode ser provisionada por este dispositivo restante. Olá **camadas restantes** capacidade é a capacidade disponível de saudação que pode ser provisionada incluindo nuvem durante a saudação **restantes Local** é a capacidade restante em discos de saudação de saudação anexado toothis virtual matriz.

* Em Olá **uso** gráfico, você pode exibir o armazenamento primário de saudação usado em matriz virtual, bem como o armazenamento em nuvem Olá consumida durante saudação últimos 7 dias, o padrão de saudação período de tempo. Saudação de uso **editar** opção no canto superior direito Olá Olá gráfico toochoose uma escala de tempo diferentes.

* Olá **compartilhamentos** ou **Volumes** lado a lado fornece um resumo do número de saudação de compartilhamentos ou volumes em seu dispositivo agrupados por status. Clique em Olá bloco tooopen Olá **compartilhamentos** ou **Volumes** folha e, em seguida, clique em um tooview individual de compartilhamento ou volume ou modificar suas propriedades. Para obter mais informações, consulte como muito[gerenciar compartilhamentos](storsimple-virtual-array-manage-shares.md) ou [gerenciar volumes](storsimple-virtual-array-manage-volumes.md).

## <a name="next-steps"></a>Próximas etapas
Saiba como:
- [Gerenciar compartilhamentos em uma matriz virtual StorSimple](storsimple-virtual-array-manage-shares.md)
    
- [Gerenciar volumes em uma matriz virtual StorSimple](storsimple-virtual-array-manage-volumes.md)

