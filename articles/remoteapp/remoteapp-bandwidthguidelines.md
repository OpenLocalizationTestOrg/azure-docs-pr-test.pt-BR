---
title: aaaAzure RemoteApp de largura de banda - diretrizes gerais | Microsoft Docs
description: "Compreenda algumas diretrizes básicas de largura de banda de rede para as coleções e aplicativos do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Largura de banda de rede do Azure RemoteApp - diretrizes gerais (se não puder testar a sua)
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Se você não tiver Olá tempo ou a funcionalidade de toorun Olá [testes de largura de banda de rede](remoteapp-bandwidthtests.md) do Azure RemoteApp, aqui estão algumas diretrizes razoavelmente genéricas que podem ajudá-lo a estimar a largura de banda de rede por usuário.

Se você tiver uma combinação desses cenários, não recomendamos nada menor que (ou igual a) 10 MB/s como Olá largura de banda mínima para aplicativos modernos conectados à Internet, em um ambiente remoto. (Embora, conforme discutido, isso não assegure uma experiência de usuário acima da média.)

## <a name="complex-powerpoint-simple-powerpoint"></a>PowerPoint complexo, PowerPoint simples
O Azure RemoteApp funciona melhor em LAN de 100 MB. Em Olá 10 MB/perfil de rede % s, quando mais de 5% usuário Olá tremulação acima 120 ms verá uma experiência média. No hello de 1 MB/s diferentes é evidente - por exemplo, em uma apresentação de slides, usuário Olá talvez não veja transições animadas em todos os porque quadros são ignorados.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, PDF misto, PDF, Texto
Perfil de 10 MB/s de rede é fechar tooLAN na maioria dos aspectos. 1 MB/s fornecem uma experiência de Okey, embora possa haver algumas tremulação quando um usuário rola enquanto há imagens na tela hello.

## <a name="flash-video-youtube"></a>Vídeo em Flash (YouTube)
100 MB/s LAN fornece melhor experiência de hello, enquanto 10 MB/s é aceitável (que significa acompanhar a taxa de quadros hello, mas tremulação aumenta). A 1 MB/s, a tremulação é muito alta e perceptível.

## <a name="word-typing-word-remote-input"></a>Digitação de palavras (entrada remota do Word)
Esse é um cenário de uso de baixa largura de banda. A 256 KB/s fornecemos uma experiência tão boa quanto aquela obtida com LAN.

## <a name="learn-more"></a>Saiba mais
* [Estimar o uso de largura de banda de rede do Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp - como a largura de banda de rede e a qualidade da experiência funcionam juntas?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - testando o uso da largura de banda de sua rede com alguns cenários comuns](remoteapp-bandwidthtests.md)

