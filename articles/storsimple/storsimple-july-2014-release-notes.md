---
title: "Notas de versão versão aaaStorSimple 8000 | Microsoft Docs"
description: "Descreve novos recursos de hello, questões abertas e soluções alternativas disponíveis para hello julho de 2014 versão do Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>Notas de versão de lançamento do StorSimple série 8000 - julho de 2014
## <a name="overview"></a>Visão geral
Notas de versão de acompanhamento Olá identificam questões abertas fundamentais de saudação para Olá StorSimple 8000 Series versão de disponibilidade geral (GA) de julho de 2014 do Microsoft Azure StorSimple. Esta versão corresponde toosoftware versão 6.3.9600.17215.  

A menos que especificado o contrário, estas notas se aplicam a modelos de tooall do dispositivo do StorSimple hello. Notas de versão de saudação são continuamente atualizadas; à medida que são descobertas questões importantes que exijam uma solução alternativa, eles são adicionados. Antes de implantar sua solução do Microsoft Azure StorSimple, considere Olá informações a seguir.  

## <a name="known-issues-in-this-release"></a>Problemas conhecidos nesta versão
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.  

| Não. | Recurso | Problema | Comentários/soluções alternativas | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Redefinição de fábrica |Em alguns casos, quando você executar uma redefinição de fábrica, Olá dispositivo StorSimple pode travar e exibir esta mensagem: **toofactory redefinição está em andamento (fase 8)**. Isso ocorre se você pressionar CTRL + C enquanto Olá cmdlet está em andamento. |Não pressione CTRL + C após iniciar uma redefinição de fábrica. Se você já estiver nesse estado, entre em contato com o Suporte da Microsoft para as próximas etapas. |Sim |Não |
| 2 |Quorum de disco |Em casos raros, se a maioria de saudação dos discos no compartimento EBOD de saudação de um dispositivo 8600 é desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá estarão offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 3 |Falhas de instantâneo de nuvem |Em casos raros, um instantâneo de nuvem pode falhar com o erro Olá **atingido o limite máximo backup**. Isso ocorre se você ultrapassar 255 clones online no hello mesmo dispositivo, de saudação mesmo volume original que foi excluído. | |Sim |Sim |
| 4 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 5 |Gráficos de monitoramento de dispositivo |Em Olá serviço StorSimple Manager, gráficos de monitoramento de dispositivo de saudação não funcionam quando básica ou a autenticação NTLM é habilitada na configuração de servidor de proxy Olá para dispositivo hello. |Modifica configuração do proxy web Olá Olá dispositivo registrado com seu serviço StorSimple Manager para que a autenticação é definida tooNONE. toodo, Olá Olá de execução do Windows PowerShell para o cmdlet Set-HcsWebProxy do StorSimple. |Sim |Sim |
| 6 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. | |Sim |Sim |
| 7 |Failback |Não há suporte para um failback em até 24 horas após a recuperação de desastres (DR). | |Sim |Não |
| 8 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo. O failover de dispositivos de toomultiple um único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. | |Sim |Não |
| 9 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo para Olá install toofinish com êxito. | |Sim |Não |
| 10 |Interfaces de rede |Interfaces de rede DATA 2 e DATA 3 foram trocadas no software de saudação. |Entre em contato com Microsoft Support se você precisar tooconfigure essas interfaces. |Sim |Não |

