---
title: aaaAzure RemoteApp - como largura de banda de rede e a qualidade do tiver trabalho juntas? | Microsoft Docs
description: "Saiba como a largura de banda de rede no Azure RemoteApp pode afetar a qualidade da experiência do usuário."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - como a largura de banda de rede e a qualidade da experiência funcionam juntas?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Quando você está vendo hello [largura de banda de rede geral](remoteapp-bandwidth.md) necessário para o Azure RemoteApp, lembre-Olá mente fatores a seguir – essas são todas as partes de um sistema dinâmico impactos Olá experiência de um usuário. 

* **Largura de banda disponível e as condições de rede atual** -um conjunto de parâmetros (perda, latência, tremulação) Olá mesmo de rede em um determinado momento pode afetar o aplicativo hello experiência de fluxo contínuo, o que significa uma experiência de usuário geral menor. largura de banda de saudação disponível em sua rede é uma função de congestionamento, perda aleatória, latência porque todos estes parâmetros afetam mecanismo de controle de congestionamento hello, que por sua vez controles Olá colisões de tooavoid de velocidade de transmissão.  Por exemplo, uma rede com perdas ou com alta latência tornará Olá usuário experiência ruim mesmo em uma rede com largura de banda de 1000 MB. Olá perda e latência variam com base no número de saudação de usuários que estão em hello mesma rede e o que os usuários estão fazendo (por exemplo, assistir vídeos, baixando ou carregamento de grandes arquivos, impressão).
* **Cenário de uso** -experiência Olá depende de quais Olá os usuários estão fazendo individualmente e como um grupo de saudação mesmo rede. Por exemplo, ler um slide requer apenas um toobe único quadro atualizado; Se o usuário de saudação aborda e rola sobre o conteúdo de saudação de um documento de texto, eles precisam de um número maior de quadros toobe atualizado por segundo. Olá comunicação novamente e sucessivamente toohello servidor neste cenário eventualmente irá consumir mais largura de banda de rede. Além disso, considere um exemplo extremo: vários usuários estão assistindo vídeos de alta definição (como resolução de 4K), mantendo teleconferências HD, jogando video games em 3D ou trabalhando em sistemas CAD. Todos esses itens podem tornar até mesmo uma rede de largura de banda realmente alta praticamente inutilizável.
* **Número de resolução e hello de telas de tela** -mais largura de banda de rede é necessária toofull atualização maiores telas de telas menores. a tecnologia subjacente Olá faz um trabalho muito bom de codificação e transmissão de regiões de saudação somente de telas de saudação que foram atualizadas, mas de vez em quando, a tela inteira hello precisa toobe atualizado. Quando o usuário Olá tem uma tela de resolução mais alta (por exemplo resolução de 4 KB), essa atualização exige mais largura de banda de rede de uma tela com uma resolução menor (como 1024x768px). Essa mesma lógica se aplicará se você usar mais de uma tela para redirecionamento. Largura de banda deve tooincrease com número de saudação de telas.
* **Redirecionamento de área de transferência e o dispositivo** - esse é um problema não óbvio, mas, em muitos casos se um usuário armazena um grande bloco de dados toohello da área de transferência, levará algum tempo para que tootransfer informações de cliente de área de trabalho remota Olá toohello server. experiência de downstream Olá pode ser afetada pela experiência de saudação de enviar o conteúdo da área de transferência de saudação upstream. Olá mesmo se aplica para redirecionamento do dispositivo - se um scanner de webcam produz muitos dados que precisa de servidor de upstream toohello toobe enviado, ou uma impressora precisa tooreceive um documento grande ou toobe tooan disponível aplicativo em execução no hello nuvem toocopy as necessidades de armazenamento local um arquivo grande, os usuários podem notar quadros ignorados ou temporariamente "congelado" vídeo porque dados Olá necessários para o redirecionamento de dispositivo de saudação está aumentando a largura de banda de rede Olá precisa. 

Quando você avaliar suas necessidades de largura de banda de rede, tooconsider se torne todos esses fatores funcionando como um sistema.

Agora, volte toohello [artigo de largura de banda da rede principal](remoteapp-bandwidth.md), ou mova tootesting seu [largura de banda de rede](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Saiba mais
* [Estimar o uso de largura de banda de rede do Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp - testando o uso da largura de banda de sua rede com alguns cenários comuns](remoteapp-bandwidthtests.md)
* [Largura de banda de rede do Azure RemoteApp - diretrizes gerais (se não puder testar a sua)](remoteapp-bandwidthguidelines.md)

