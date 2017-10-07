---
title: "aaaStorSimple 8000 atualizar 0.2 notas de versão | Microsoft Docs"
description: "Descreve Olá novos recursos e correções, questões abertas e soluções alternativas disponíveis para saudação de janeiro de 2015 versão do Microsoft Azure StorSimple (atualização 0,2)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>Notas de versão da Atualização 0.2 do StorSimple série 8000 - janeiro de 2015
## <a name="overview"></a>Visão geral
Hello notas de versão a seguir identificam Olá abrir os problemas críticos de saudação versão de janeiro de 2015 do Microsoft Azure StorSimple. Eles também contêm uma lista de saudação StorSimple software e atualizações de firmware incluídas nesta versão. Esta é a versão de segundo de saudação após a versão de lançamento do StorSimple 8000 Series Olá foi disponibilizado em julho de 2014.

Esta atualização não altera a versão do software de dispositivo físico de saudação da atualização de outubro de saudação. Ela continua toobe versão 6.3.9600.17312. imagem de saudação usada pela imagem de dispositivo virtual Olá foi alterada nesta versão. Portanto, todos os Olá novos dispositivos virtuais criados após 20/1/2015 exibirão versão hello como 6.3.9600.17361.  

Analise Olá informações contidas nas notas de versão de saudação para atualização de janeiro de 2015 Olá a seguir.

> [!IMPORTANT]
> * Esta atualização não está disponível no Windows Update e não pode ser instalada da mesma forma que outras atualizações. Seu dispositivo não receberá essa atualização mesmo se você tiver aplicado atualizações hello usando Olá portal clássico do Azure. Essa atualização será aplicada somente a dispositivos toovirtual criados após 20 de janeiro de 2015. 
> * Olá versão de janeiro do StorSimple não contém nenhum dispositivo físico do StorSimple de toohello de atualizações. Você ainda poderá aplicar qualquer dispositivo virtual disponível do Windows atualizações toohello, incluindo segurança recente correções, mas você não verá uma alteração na versão para o dispositivo físico StorSimple hello.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Novidades na versão de janeiro de saudação
Esta atualização contém uma correção relacionada toohello volumes ficando offline no dispositivo virtual hello. (Consulte [Problemas corrigidos nesta versão](#issues-fixed-in-the-january-release).)  

atualização de saudação não contém novos recursos ou funcionalidade.  

## <a name="issues-fixed-in-hello-january-release"></a>Problemas corrigidos na versão de janeiro de saudação
Olá, tabela a seguir descreve Olá problema foi corrigido nessa atualização.

| Não. | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Volumes offline |Quando as latências de nuvem alta persistirem por vários minutos, os volumes de dispositivo virtual StorSimple Olá ficar offline em hosts de saudação. Essa correção aumenta o limite de saudação latências de nuvem, minimizando em situações de saudação que causam Olá toogo de volumes offline em hosts. |Não |Sim |

## <a name="known-issues-in-hello-january-release"></a>Problemas conhecidos na versão de janeiro de saudação
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Comentários/soluções alternativas | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Redefinição de fábrica |Em alguns casos, quando você executar uma redefinição de fábrica, Olá dispositivo StorSimple pode travar e exibir esta mensagem: **toofactory redefinição está em andamento (fase 8).** Isso ocorre se você pressionar CTRL + C enquanto Olá cmdlet está em andamento. |Não pressione CTRL + C após iniciar uma redefinição de fábrica. Se você já estiver nesse estado, entre em contato com o Suporte da Microsoft para as próximas etapas. |Sim |Não |
| 2 |Quorum de disco |Em casos raros, se a maioria de saudação dos discos no compartimento EBOD de saudação de um dispositivo 8600 é desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá estarão offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 3 |Falhas de instantâneo de nuvem |Em casos raros, um instantâneo de nuvem pode falhar com o erro Olá **atingido o limite máximo backup**. Isso ocorre se você ultrapassar 255 clones online no hello mesmo dispositivo, de saudação mesmo volume original que foi excluído. | |Sim |Sim |
| 4 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação  Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 5 |Gráficos de monitoramento de dispositivo |Em Olá serviço StorSimple Manager, gráficos de monitoramento de dispositivo de saudação não funcionam quando básica ou a autenticação NTLM é habilitada na configuração de servidor de proxy Olá para dispositivo hello. |Modifica configuração do proxy web Olá Olá dispositivo registrado com seu serviço StorSimple Manager para que a autenticação é definida tooNONE. toodo, Olá Olá de execução do Windows PowerShell para o cmdlet Set-HcsWebProxy do StorSimple. |Sim |Sim |
| 6 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. | |Sim |Sim |
| 7 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo. |O failover de dispositivos de toomultiple um único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. |Sim |Não |
| 8 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo na ordem para Olá install toofinish com êxito. | |Sim |Não |
| 9 |Proxy Web |Se a configuração de proxy web tiver HTTPS como Olá especificado protocolo, em seguida, a comunicação de serviço no dispositivo será afetada e dispositivo Olá ficará offline. Pacotes de suporte também serão gerados no processo de hello, consome recursos significativos em seu dispositivo. |Certifique-se de que URL do proxy web hello possui HTTP conforme Olá protocolo especificado. Veja mais informações sobre como muito[configurar o proxy da web para seu dispositivo](storsimple-configure-web-proxy.md). |Sim |Não |
| 10 |Proxy Web |Se você configurar e habilitar o proxy da web em um dispositivo registrado, você precisará controlador ativo do toorestart Olá em seu dispositivo. | |Sim |Não |
| 11 |Latência de nuvem alta e alta carga de trabalho de E/S |Quando seu dispositivo StorSimple encontra uma combinação de latências de nuvem muita alta (ordem de segundos) e alta carga de trabalho de e/s, os volumes de dispositivos Olá entram em um estado degradado e hello e/ss pode falhar com um erro "o dispositivo não está pronto". |Você será necessário toomanually controladores de dispositivo de saudação de reinicialização ou executar um toorecover de failover do dispositivo dessa situação. |Sim |Não |

## <a name="physical-device-updates-in-hello-january-release"></a>Atualizações na versão de janeiro de saudação do dispositivo físico
Esta atualização não contém quaisquer outro alterações toohello o dispositivo StorSimple.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Ligação em série SCSI (SAS) controlador e firmware atualizações na versão de janeiro de saudação
Esta versão não contém qualquer controlador de SCSI (SAS) conectado à série do atualizações toohello ou firmware hello. atualização do driver Olá estava em Olá outubro, versão de 2014. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Atualizações na versão de janeiro de saudação do dispositivo virtual
Esta versão contém uma imagem atualizada para o dispositivo virtual hello. Todos os dispositivos virtuais Olá criados após 20 de janeiro de 2015 exibirão a versão do software hello como 6.3.9600.17361.

