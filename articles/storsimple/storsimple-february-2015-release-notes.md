---
title: "aaaStorSimple 8000 atualizar 0,3 notas de versão | Microsoft Docs"
description: "Descreve Olá novos recursos e correções, questões abertas e soluções alternativas disponíveis para Olá fevereiro de 2015 versão do Microsoft Azure StorSimple (atualização 0.3)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>Notas de versão da Atualização 0.3 do StorSimple série 8000 - fevereiro de 2015
## <a name="overview"></a>Visão geral
Olá notas de versão a seguir identificar os problemas abertos críticos Olá para StorSimple 8000 Series atualização 0.3 lançada em fevereiro de 2015. Eles também contêm uma lista de saudação StorSimple software e atualizações de firmware incluídas nesta versão. Esta é a versão de terceiro de saudação após a versão de lançamento do StorSimple 8000 Series Olá foi disponibilizado em julho de 2014.

Essa atualização não altera a versão do software de dispositivo de saudação de atualização de janeiro de saudação. Ela continua toobe versão 6.3.9600.17312. Você pode confirmar essa atualização Olá foi instalada verificando Olá **última atualização** Data. Se a data de saudação é 2/10/2015 ou posterior, o hello atualização foi instalada com êxito.  

É recomendável que você procure e aplique todas as atualizações disponíveis imediatamente após a instalação do seu dispositivo StorSimple. Você também pode ativar toodownload atualizações automáticas e instalar atualizações de alta prioridade da Microsoft assim que elas são lançadas. Para obter mais informações, consulte [Atualizar seu dispositivo StorSimple](storsimple-update-device.md).  

Analise Olá informações contidas na versão Olá notas antes de implantar Olá atualizar em sua solução StorSimple.  

> [!IMPORTANT]
> * Use o serviço StorSimple Manager hello e não o Windows PowerShell para atualização de fevereiro do StorSimple tooinstall hello.   
> * Demora aproximadamente um tooinstall hora essa atualização. No entanto, se você estiver instalando atualizações cumulativas, o processo de saudação pode levar cerca de 3 toocomplete de horas.  
> * Olá versão de fevereiro do StorSimple não contém nenhum dispositivo virtual do atualizações toohello StorSimple. Você ainda poderá aplicar qualquer dispositivo virtual disponível do Windows atualizações toohello, incluindo segurança recente correções, mas você não verá uma alteração na versão para o dispositivo virtual hello.  
> 
> 

Certifique-se de que Olá seguintes pré-requisitos é atendido tooupdating anterior seu dispositivo StorSimple.  

* Verifique se ambos os controladores de dispositivo estão em execução antes de verificar se há atualizações. Se o controlador não está em execução, a verificação de saudação falhará. tooverify controladores Olá estão em um estado íntegro, navegue muito**Status do Hardware** em Olá **manutenção** página. Se houver componentes que **Precisam de atenção**, contate o Suporte da Microsoft antes de avançar.
* Certifique-se de que os IPs fixos para o controlador 0 e o controlador 1 são roteáveis e podem se conectar toohello da Internet são usados para manutenção de dispositivo de toohello atualizações hello. Você pode usar o hello [cmdlet de Conexão de teste](https://technet.microsoft.com/library/hh849808.aspx) tooping um endereço conhecido fora da rede hello, como outlook.com, tooverify que Olá controlador tem conectividade toohello fora da rede.
* Certifique-se de que as portas 80 e 443 estão disponíveis no seu dispositivo StorSimple para comunicação de saída. Para obter mais informações, consulte Olá [requisitos de rede para seu dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Se a versão do software de dispositivo de saudação é mais antiga que 6.3.9600.17312 (atualização de outubro de 2014), desabilite portas Data 2 e Data 3 hello, se habilitado, antes de iniciar a atualização de saudação. Deixar Olá Data 2 ou 3 habilitadas quando você aplicar a atualização de saudação de portas pode causar o toogo do controlador de dispositivo no modo de recuperação. Observe que ao desabilitar as interfaces de rede de hello, todos os volumes de saudação associado serão colocados offline e hello e/SS será interrompida durante atualização Olá Olá.  

## <a name="whats-new-in-hello-february-release"></a>Novidades na versão de fevereiro de saudação
Esta atualização contém uma correção para o problema de redefinição de fábrica Olá ocorridas em dispositivos que foram atualizados de saudação GA versão toohello versão de outubro de 2014. Para obter mais informações, consulte [Problemas corrigidos nesta versão](#issues-fixed-in-the-february-release).   

Esta atualização não contém novos recursos ou funcionalidades.  

## <a name="issues-fixed-in-hello-february-release"></a>Problemas corrigidos na versão de fevereiro de saudação
Olá, tabela a seguir descreve Olá problema foi corrigido nessa atualização.  

| Não. | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Redefinição de fábrica |Você tentar tooperform uma redefinição de fábrica em um dispositivo que tinha originalmente Olá GA versão (versão 6.3.9600.17215) instalado, mas foi atualizada toohello outubro (versão 6.3.9600.17312). Falha de redefinição de fábrica Hello e dispositivo Olá torna-se instável. |Sim |Não |

## <a name="known-issues-in-hello-february-release"></a>Problemas conhecidos na versão de fevereiro de saudação
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Comentários/soluções alternativas | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Redefinição de fábrica |Em alguns casos, quando você executar uma redefinição de fábrica, Olá dispositivo StorSimple pode travar e exibir esta mensagem: **toofactory redefinição está em andamento (fase 8)**. Isso ocorre se você pressionar CTRL + C enquanto Olá cmdlet está em andamento. |Não pressione CTRL + C após iniciar uma redefinição de fábrica. Se você já estiver nesse estado, entre em contato com o Suporte da Microsoft para as próximas etapas. |Sim |Não |
| 2 |Quorum de disco |Em casos raros, se maioria de saudação dos discos no compartimento EBOD de saudação de um 8600device forem desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá estarão offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 3 |Falhas de instantâneo de nuvem |Em casos raros, um instantâneo de nuvem pode falhar com o erro Olá **atingido o limite máximo backup**. Isso ocorre se você ultrapassar 255 clones online no hello mesmo dispositivo, de saudação mesmo volume original que foi excluído. | |Sim |Sim |
| 4 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 5 |Gráficos de monitoramento de dispositivo |Em Olá serviço StorSimple Manager, gráficos de monitoramento de dispositivo de saudação não funcionam quando básica ou a autenticação NTLM é habilitada na configuração de servidor de proxy Olá para dispositivo hello. |Modifica configuração do proxy web Olá Olá dispositivo registrado com seu serviço StorSimple Manager para que a autenticação é definida tooNONE. toodo, Olá Olá de execução do Windows PowerShell para o cmdlet Set-HcsWebProxy do StorSimple. |Sim |Sim |
| 6 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. | |Sim |Sim |
| 7 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo.    O failover de dispositivos de toomultiple um único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. | |Sim |Não |
| 8 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo na ordem para Olá install toofinish com êxito. | |Sim |Não |
| 9 |Proxy Web |Se a configuração de proxy web tiver HTTPS como Olá especificado protocolo, em seguida, a comunicação de serviço no dispositivo será afetada e dispositivo Olá ficará offline. Pacotes de suporte também serão gerados no processo de hello, consome recursos significativos em seu dispositivo. |Certifique-se de que URL do proxy web hello possui HTTP conforme Olá protocolo especificado. Para obter mais informações sobre como muito[configurar o proxy da web para seu dispositivo](storsimple-configure-web-proxy.md). |Sim |Não |
| 10 |Proxy Web |Se você configurar e habilitar o proxy da web em um dispositivo registrado, você precisará controlador ativo do toorestart Olá em seu dispositivo. | |Sim |Não |
| 11 |Latência de nuvem alta e alta carga de trabalho de E/S |Quando seu dispositivo StorSimple encontra uma combinação de latências de nuvem muita alta (ordem de segundos) e alta carga de trabalho de e/s, os volumes de dispositivos Olá entram em um estado degradado e hello e/ss pode falhar com um erro "o dispositivo não está pronto". |Você será necessário toomanually controladores de dispositivo de saudação de reinicialização ou executar um toorecover de failover do dispositivo dessa situação. |Sim |Não |

## <a name="physical-device-updates-in-hello-february-release"></a>Atualizações na versão de fevereiro de saudação do dispositivo físico
Esta fábrica de saudação de correções de atualização redefinir o problema ocorreu em dispositivos que foram atualizados de saudação GA versão toohello versão de outubro de 2014. Ele não contém quaisquer outro atualizações toohello o dispositivo StorSimple.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Ligação em série SCSI (SAS) controlador e firmware atualizações na versão de fevereiro de saudação
Esta versão não contém qualquer controlador de SCSI (SAS) conectado à série do atualizações toohello ou firmware hello. atualização do driver Olá estava em Olá outubro, versão de 2014.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Atualizações na versão de fevereiro de saudação do dispositivo virtual
Esta versão não contém todas as atualizações para o dispositivo virtual hello. Aplicar esta atualização não irá alterar a versão do software de saudação do dispositivo virtual.

