---
title: "aaaStorSimple 8000 atualizar 0,1 notas de versão | Microsoft Docs"
description: "Descreve Olá novos recursos e correções, questões abertas e soluções alternativas disponíveis para Olá outubro de 2014 versão do Microsoft Azure StorSimple (atualização 0,1)."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>Notas de versão da Atualização 0.1 do StorSimple série 8000 - outubro de 2014
## <a name="overview"></a>Visão geral
Olá notas de versão a seguir identificar os problemas abertos críticos Olá para StorSimple 8000 Series atualização 0,1 lançado em outubro de 2014. Eles também contêm uma lista de saudação StorSimple software e atualizações de firmware incluídas nesta versão. Isso é Olá primeira versão após a versão de lançamento do StorSimple 8000 Series Olá foi disponibilizado em julho de 2014 e corresponde toosoftware versão 6.3.9600.17312.  

É recomendável que você procure e aplica quaisquer atualizações disponíveis imediatamente após a instalação do dispositivo hello. Você também pode ativar toodownload atualizações automáticas e instalar atualizações de alta prioridade da Microsoft assim que elas são lançadas. Para obter mais informações, consulte como muito[atualizar seu dispositivo StorSimple](storsimple-update-device.md).  

Analise Olá informações contidas nas notas de versão de saudação antes de implantar atualizações de saudação em sua solução StorSimple.  

> [!IMPORTANT]
> * Use o serviço StorSimple Manager hello e não o Windows PowerShell para StorSimple tooinstall Olá de atualizações de outubro.  
> * atualizações de saudação geralmente levar cerca de 3 toocomplete de horas.  
> * Olá versão de outubro do StorSimple não contém nenhum dispositivo virtual do atualizações toohello StorSimple. Você ainda poderá aplicar quaisquer atualizações disponíveis do Windows, incluindo correções de segurança recentes, mas você não verá uma alteração na versão para o dispositivo virtual hello.  
> 
> 

Verifique se Olá seguintes pré-requisitos é atendido tooupdating anterior seu dispositivo StorSimple.  

* Verifique se ambos os controladores de dispositivo estão em execução antes de verificar se há atualizações. Se o controlador não está em execução, a verificação de saudação falhará. tooverify controladores Olá estão em um estado íntegro, navegue muito**Status do Hardware** em Olá **manutenção** página. Se houver componentes que **Precisam de atenção**, contate o Suporte da Microsoft antes de avançar.  
* Certifique-se de IPs fixos para o controlador 0 e 1 são roteáveis e podem se conectar toohello da Internet são usados para manutenção de dispositivo de toohello atualizações hello. Você pode usar o hello [cmdlet de Conexão de teste](https://technet.microsoft.com/library/hh849808.aspx) tooping um endereço conhecido fora da rede hello, como outlook.com, tooverify que Olá controlador tem conectividade toohello fora da rede.  
* Certifique-se de que Olá necessárias portas de saída estão disponíveis em seu dispositivo StorSimple para comunicação de saída. Para obter mais informações, consulte Olá [requisitos de rede para seu dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Se a versão do software de dispositivo de saudação é mais antiga que 6.3.9600.17312 (atualização de outubro de 2014), desabilite portas Data 2 e Data 3 hello, se habilitado, antes de iniciar a atualização de saudação. Se você deixar Olá Data 2 ou 3 habilitadas ao aplicar a atualização de saudação de portas, isso pode causar o toogo do controlador de dispositivo no modo de recuperação. Observe que ao desabilitar as interfaces de rede de hello, todos os volumes de saudação associado serão colocados offline e hello e/s será interrompida durante atualização Olá Olá.  

## <a name="whats-new-in-hello-october-release"></a>Novidades na versão de outubro de saudação
Esta atualização inclui Olá aprimoramentos a seguir:

* Agora você pode usar Olá StorSimple Manager serviço da interface do usuário toomanage os controladores de dispositivo. Olá ações de gerenciamento incluem reiniciar, desligar ou ativar um controlador. Para obter mais informações, vá muito[StorSimple gerenciar controladores de dispositivo](storsimple-manage-device-controller.md).  
* Você pode agendar a alocação de largura de banda WAN de acordo com as combinações de tooday da semana e hora do dia. Isso permite toomake melhor uso de largura de banda WAN durante horários de pouca atividade. Modelos diferentes de largura de banda são permitidos para contêineres de volume diferente. Para obter mais informações, vá muito[gerenciar seus modelos de largura de banda de StorSimple](storsimple-manage-bandwidth-templates.md).  
* Você pode configurar notificações por email tooproactively notificar Olá administrador (es) e outros problemas existentes ou possivelmente futuros. Para obter mais informações, vá muito[definir configurações de alerta](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Problemas corrigidos na versão de outubro de saudação
Olá tabela a seguir fornece um resumo dos problemas que foram corrigidos nesta atualização.  

| Não. | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Interfaces de rede |Na saudação anterior da versão, interfaces de rede Olá DATA 2 e DATA 3 foram trocadas no software de saudação. Esse problema foi corrigido nesta atualização. Limpe as configurações de saudação e desabilitar essas interfaces de rede antes de instalar a atualização de saudação. Depois de instalar a atualização de saudação, você terá tooreconfigure essas interfaces. |Sim |Não |
| 2 |Pacote de suporte |Na versão anterior do hello, se você executou a saudação do Windows PowerShell **Export-HcsSupportPackage** cmdlet tooretrieve Olá Baseboard Management Controller (BMC) registra, Olá Falha na operação com hello aviso a seguir: "Olá operação bem-sucedida neste controlador, mas falhou no controlador de par Olá devido a seguir toohello erro (s). Verifique se o par de saudação está íntegro e se o nó atual Olá pode se conectar toohello ponto a ponto." Esse problema está corrigido. |Sim |Não |
| 3 |Failover de dispositivo |Na versão anterior do hello, havia uma possibilidade de inconsistência de dados se um **descobrir backup** falha no trabalho durante um failover de dispositivo. Esse problema está corrigido. |Sim |Não |
| 4 |Failover de dispositivo |Na saudação anterior da versão, após um failover de dispositivo, backups eram visíveis, mas o contêiner de volume associado Olá não estava presente no dispositivo de destino hello. Esse problema está corrigido. |Sim |Não |
| 5 |Failover de dispositivo |Na versão anterior do hello, havia um bug na enumeração de saudação de backups de nuvem durante a operação de restauração do registro Olá que pode levar a inconsistência toodata se houvesse problemas de conectividade em nuvem. |Sim |Não |
| 6 |Atualização de firmware |Na versão anterior do hello, hello trabalho de atualização de firmware do dispositivo falhou e exibido um erro que informava que Olá cmdlets não eram reconhecidos e que a atualização Olá falhava como resultado. controlador Olá deu, em seguida, no modo de recuperação. Esse problema está corrigido. |Sim |Não |
| 7 |Instalação |Erros causados pelo dispositivo Olá não está sendo espelhado corretamente durante a instalação agora foram corrigidos. |Sim |Não |
| 8 |Redefinição de fábrica |Você pode agora opcionalmente ignorar verificação de firmware Olá para redefinição de fábrica. Essa é uma alteração de versão anterior de saudação. |Sim |Não |
| 9 |Redefinição de fábrica |Na versão anterior do hello, quando um cmdlet de redefinição de fábrica era executado, verificações da versão do firmware eram feitas apenas para alguns componentes de hardware. Verificações de firmware adicionais foram feitas após a primeira reinicialização Olá no processo de hello, que pode causar Olá redefinição toofail. Essa correção garante que todas as verificações de firmware Olá são feitas quando Olá cmdlet de redefinição de fábrica é executado e antes de saudação primeiro sistema reinicializar. |Sim |Não |
| 10 |Rotação de chaves da conta de armazenamento |Olá **Invoke-HcsmServiceDataEncryptionKeyChange** cmdlet usado chaves de conta de armazenamento toorotate Olá agora prompts Olá chave de criptografia de dados de serviço do usuário tooenter hello. Essa é uma alteração de versão anterior de saudação no qual Olá chave de criptografia de dados de serviço foi passada como um parâmetro embutido. |Sim |Não |
| 11 |Failback dentro de 24 horas |Durante a recuperação de desastres, limpeza de saudação no dispositivo de origem Olá não aconteceu failback corretamente, causando toofail. Isso foi corrigido nesta atualização. |Sim |Não |

## <a name="known-issues-in-hello-october-release"></a>Problemas conhecidos na versão de outubro de saudação
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Comentários/soluções alternativas | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Redefinição de fábrica |Em alguns casos, quando você executar uma redefinição de fábrica, Olá dispositivo StorSimple pode travar e exibir esta mensagem: **toofactory redefinição está em andamento (fase 8)**. Isso ocorre se você pressionar CTRL + C enquanto Olá cmdlet está em andamento. |Não pressione CTRL + C após iniciar uma redefinição de fábrica. Se você já estiver nesse estado, entre em contato com o Suporte da Microsoft para as próximas etapas. |Sim |Não |
| 2 |Redefinição de fábrica |Não redefina de fábrica um dispositivo StorSimple que é atualizado da versão de lançamento tooOctober 2014. |Esta operação só funcionará se um patch for instalado. Contate o Microsoft Support tooget esse patch necessário. |Sim |Não |
| 3 |Quorum de disco |Em casos raros, se a maioria de saudação dos discos no compartimento EBOD de saudação de um dispositivo 8600 é desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá estarão offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 4 |Falhas de instantâneo de nuvem |Em casos raros, um instantâneo de nuvem pode falhar com o erro Olá **atingido o limite máximo backup**. Isso ocorre se você ultrapassar 255 clones online no hello mesmo dispositivo, de saudação mesmo volume original que foi excluído. | |Sim |Sim |
| 5 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 6 |Gráficos de monitoramento de dispositivo |Em Olá serviço StorSimple Manager, gráficos de monitoramento de dispositivo de saudação não funcionam quando básica ou a autenticação NTLM é habilitada na configuração de servidor de proxy Olá para dispositivo hello. |Modifica configuração do proxy web Olá Olá dispositivo registrado com seu serviço StorSimple Manager para que a autenticação é definida tooNONE. toodo, Olá Olá de execução do Windows PowerShell para o cmdlet Set-HcsWebProxy do StorSimple. |Sim |Sim |
| 7 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. | |Sim |Sim |
| 8 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo. |O failover de dispositivos de toomultiple um único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. |Sim |Não |
| 9 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo na ordem para Olá install toofinish com êxito. | |Sim |Não |
| 10 |Proxy Web |Se a configuração de proxy web tiver HTTPS como Olá especificado protocolo, em seguida, a comunicação de serviço no dispositivo será afetada e dispositivo Olá ficará offline. Pacotes de suporte também serão gerados no processo de hello, consome recursos significativos em seu dispositivo. |Certifique-se de que URL do proxy web hello possui HTTP conforme Olá protocolo especificado. Para obter mais informações sobre como muito[configurar o proxy da web para seu dispositivo](storsimple-configure-web-proxy.md). |Sim |Não |
| 11 |Proxy Web |Se você configurar e habilitar o proxy da web em um dispositivo registrado, você precisará controlador ativo do toorestart Olá em seu dispositivo. | |Sim |Não |
| 12 |Latência de nuvem alta e alta carga de trabalho de E/S |Quando seu dispositivo StorSimple encontra uma combinação de latências de nuvem muita alta (ordem de segundos) e alta carga de trabalho de e/s, os volumes de dispositivos Olá entram em um estado degradado e hello e/ss pode falhar com um erro "o dispositivo não está pronto". |Você será necessário toomanually controladores de dispositivo de saudação de reinicialização ou executar um toorecover de failover do dispositivo dessa situação. |Sim |Não |

## <a name="physical-device-updates-in-hello-october-release"></a>Atualizações na versão de outubro de saudação do dispositivo físico
Quando essas atualizações são um dispositivo físico tooa aplicada, versão do software Olá alterará too6.3.9600.17312. A menos que especificado o contrário, estas notas se aplicam a modelos de tooall do dispositivo do StorSimple hello. Para obter mais informações sobre essas atualizações, consulte [Atualização de software do dispositivo físico de outubro de 2014 para o dispositivo do Microsoft Azure StorSimple](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Ligação em série SCSI (SAS) controlador e firmware atualizações na versão de outubro de saudação
Esta versão atualiza o driver hello e firmware de saudação no controlador SAS de saudação do seu dispositivo físico. Para obter mais informações sobre a atualização do controlador SAS hello, consulte [atualização de outubro de 2014 para controladores SAS LSI no dispositivo do Microsoft Azure StorSimple](http://support.microsoft.com/kb/2987020).   

Esta versão também se aplica a uma atualização de firmware cumulativa que resolve problemas de confiabilidade com componentes de hardware de dispositivo hello. Para obter mais informações sobre a atualização de firmware hello, consulte [atualização de firmware de outubro de 2014 para o dispositivo do Microsoft Azure StorSimple](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Atualizações na versão de outubro de saudação do dispositivo virtual
Esta versão não contém todas as atualizações para o dispositivo virtual hello. Aplicar esta atualização não irá alterar a versão do software de saudação do dispositivo virtual.

