---
title: aaaEstimate uso de largura de banda de rede do Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre os requisitos de largura de banda de rede Olá para seus aplicativos e coleções do RemoteApp do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Estimar o uso de largura de banda de rede do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp usa Olá toocommunicate de protocolo de área de trabalho remota (RDP) entre os aplicativos em execução no hello nuvem do Azure e seus usuários. Este artigo fornece algumas diretrizes básicas você pode usar tooestimate que o uso de rede e potencialmente avaliar o uso de largura de banda de rede por usuário do Azure RemoteApp.

Estimar o uso de largura de banda por usuário é muito complexo e exige executar vários aplicativos simultaneamente em cenários multitarefa, nos quais os aplicativos podem afetar o desempenho uns dos outros com base em sua demanda de largura de banda de rede. Tipo de mesmo saudação do cliente de área de trabalho remota (como o cliente Mac versus cliente HTML5) pode levar a resultados de largura de banda de toodifferent. toohelp que você trabalhar com essas complicações, podemos quebrar cenários de uso de saudação em vários cenários do hello comuns categorias tooreplicate reais. (Onde o cenário do mundo real Olá é, logicamente, uma combinação de categorias e difere pelo usuário.)

Antes de ir adiante - Observe que estamos supondo RDP fornece uma experiência tooexcellent BOM na maioria dos cenários de uso em redes com latência abaixo de 120 ms e largura de banda com mais de 5 MBs - isso se baseia na toodynamically de capacidade do RDP ajustar usando rede disponível Olá largura de banda e hello estimado necessidades de largura de banda do aplicativo. Este artigo vai além daquelas toolook de "maioria dos cenários de uso" na borda hello, onde cenários começam toounwind e toodegrade começa a experiência do usuário.

Agora, confira Olá artigos para obter detalhes hello, incluindo tooconsider fatores, recomendações de linha de base e o que não incluímos em nossas estimativas a seguir.

* [Como a largura de banda de rede e a qualidade da experiência funcionam juntas?](remoteapp-bandwidthexperience.md)
* [Testando o uso da largura de banda de sua rede com alguns cenários comuns](remoteapp-bandwidthtests.md)
* [Diretrizes rápidas se você não tiver tootest de tempo ou a capacidade de saudação](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>O que não estamos incluindo?
Ao examinar Olá proposto testes e nossas recomendações gerais (e reconhecidamente genéricas), lembre-se de que há vários fatores que não considerada. Por exemplo, Olá complicações de experiência do usuário fornecidas por natureza assimétrica de saudação de carregamento vs. de largura de banda de download. Além disso terá impacto sobre a natureza assimétrica Olá da maioria das redes Wi-Fi desempenho hello e percepção de experiência do usuário de saudação. Para cenários interativos tráfego downstream Olá pode ter uma prioridade inferior a saudação upstream, que pode aumentar o número de saudação de quadros de vídeo ou áudio perdidos e, portanto, afetar a percepção do usuário de saudação do hello experiência de fluxo contínuo. Você pode executar seu próprio toosee experiências o que é bom para sua rede e o caso de uso específico.

Embora, abordamos o redirecionamento do dispositivo, nós não continha em impacto de largura de banda consideração Olá Olá de tráfego de rede causado pelos dispositivos conectados, como armazenamento, impressoras, scanners, câmeras da web e outros dispositivos USB. Olá desses dispositivos geralmente picos de necessidades de largura de banda Olá temporariamente e o efeito desaparece quando Olá tarefa seja concluída. Mas se feito com frequência, essa demanda de largura de banda poderá ser bastante perceptível.

Também não é abordada como um usuário pode afetar outros usuários no hello mesma rede. Por exemplo, um usuário consumindo 4K vídeo em uma rede de 100 MB/s significativamente pode afetar outros usuários na mesma rede tentar toodo Olá a mesma tarefa. Infelizmente obtém impacto de saudação toodetermine progressivamente mais difícil de uso simultâneo toogive uma recomendação que abranja tudo ou comuns sobre o desempenho do sistema Olá na agregação. Tudo o que podemos dizer é que Olá tecnologia de protocolo de base tornará melhor o uso de largura de banda de rede disponível Olá Olá, mas ele tem suas limitações.

