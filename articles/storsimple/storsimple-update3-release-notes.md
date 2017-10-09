---
title: "Notas de versão do aaaStorSimple 8000 Series atualização 3 | Microsoft Docs"
description: "Descreve os novos recursos do hello, problemas e soluções alternativas para StorSimple 8000 Series atualização 3."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>Notas de versão da Atualização 3 para seu dispositivo StorSimple série 8000

## <a name="overview"></a>Visão geral
Hello notas de versão a seguir descrevem Olá novos recursos e identificam os problemas abertos críticos Olá StorSimple 8000 Series atualização 3 do. Eles também contêm uma lista de atualizações de software do hello StorSimple incluídas nesta versão. 

Atualização 3 pode ser aplicado tooany o dispositivo StorSimple execução da versão (GA) ou atualização 0,1 por meio de atualização 2.2. versão do dispositivo Olá associado com a atualização 3 é 6.3.9600.17759.

Analise Olá informações contidas na versão Olá notas antes de implantar Olá atualizar em sua solução StorSimple.

> [!IMPORTANT]
> * A Atualização 3 tem atualizações de software de dispositivo, firmware e driver LSI, Storport e Spaceport. Leva aproximadamente 1,5 a 2 horas tooinstall essa atualização. 
> * Para novas versões, você poderá não ver atualizações imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Aguarde alguns dias e procure atualizações novamente, uma vez que elas serão disponibilizadas em breve.
> 
> 

## <a name="whats-new-in-update-3"></a>Novidades na Atualização 3
Olá seguintes principais melhorias e correções de bugs foram feitas na atualização 3.

* **Automatizada alterações de reclamação de espaço** – Iniciando atualização 3, algoritmos de reclamação de espaço Olá executado no controlador em espera de saudação do sistema Olá resultando na execução mais rápida. Para obter mais informações sobre portas Olá toowork necessário à recuperação de espaço, consulte toohello [StorSimple requisitos de rede](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Aprimoramentos de desempenho** – atualização 3 melhorou o desempenho de leitura-gravação toohello nuvem.
* **Aprimoramentos de migração** – nesta versão, várias correções de bugs e aprimoramentos foram feitos para o recurso de migração de saudação de dispositivos da 7000/5000 série dispositivos too8000 série. Para obter mais informações sobre como toouse Olá o recurso de migração, vá muito[migração do dispositivo da série série 5000/7000 dispositivo too8000](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **Monitoramento de correções relacionadas ao** - nesta versão, bugs relacionadas toomonitoring gráficos, o painel de serviço e o painel do dispositivo foram corrigidos.

## <a name="issues-fixed-in-update-3"></a>Problemas corrigidos na Atualização 3
Olá tabelas a seguir fornece um resumo dos problemas que foram corrigidos na atualização 3.    

| Não | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Migração de dados do lado do host |Em hello versão anterior, Olá StorSimple Appliance de nuvem foi corrompido durante uma migração de dados do lado do host. Esse problema foi corrigido nesta versão. |Não |Sim |
| 2 |Volumes fixados localmente |Na versão anterior do hello, houve problemas relacionados tooI/S falhas, falhas de conversão do volume e caminho de dados para volumes fixados localmente. Esses problemas foram causados por raiz e corrigidos nesta versão. |Sim |Não |
| 3 |Monitoramento |Havia várias unidades de tooreporting relacionados a problemas e monitoramento, bem como gráficos de painel do dispositivo onde informações incorretas foi apresentadas para localmente fixados volumes. Esses problemas foram corrigidos nesta versão. |Sim |Não |
| 4 |Gravações pesadas E/S |Ao usar StorSimple para cargas de trabalho que envolvem gravações pesadas, usuário Olá seria executado em um bug incomum onde o conjunto de trabalho Olá foi sendo enviados em camadas em nuvem hello. Esse bug foi corrigido nesta versão. |Sim |Sim |
| 5 |Backup |Em certos casos raros, nas versões anteriores de saudação do software, quando o usuário executar um backup de um clone remoto, que seriam executados em erros de nuvem e operação Olá seria o erro. Nesta versão, Olá problema é corrigido e operação Olá concluído com êxito. |Sim |Sim |
| 6 |Política do backup |Em certos casos raros, em Olá versões anteriores do software, havia um bug relacionado toohello exclusão da política de backup. Esse problema foi corrigido nesta versão. |Sim |Sim |

## <a name="known-issues-in-update-3"></a>Problemas conhecidos na Atualização 3
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Comentários/solução alternativa | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Quorum de disco |Em casos raros, se a maioria de saudação dos discos no compartimento EBOD de saudação de um dispositivo 8600 é desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá ficará offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 2 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 3 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. | |Sim |Sim |
| 4 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo. O failover de dispositivos de toomultiple um único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. | |Sim |Não |
| 5 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo na ordem para Olá install toofinish com êxito. | |Sim |Não |
| 6 |Proxy Web |Se a configuração de proxy web tiver HTTPS como Olá especificado protocolo, em seguida, a comunicação de serviço no dispositivo será afetada e dispositivo Olá ficará offline. Pacotes de suporte também serão gerados no processo de hello, consome recursos significativos em seu dispositivo. |Certifique-se de que URL do proxy web hello possui HTTP conforme Olá protocolo especificado. Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](storsimple-configure-web-proxy.md). |Sim |Não |
| 7 |Proxy Web |Se você configurar e habilitar o proxy da web em um dispositivo registrado, você precisará controlador ativo do toorestart Olá em seu dispositivo. | |Sim |Não |
| 8 |Latência de nuvem alta e alta carga de trabalho de E/S |Quando seu dispositivo StorSimple encontra uma combinação de latências de nuvem muita alta (ordem de segundos) e alta carga de trabalho de e/s, os volumes de dispositivos Olá entram em um estado degradado e hello e/ss pode falhar com um erro "o dispositivo não está pronto". |Você será necessário toomanually controladores de dispositivo de saudação de reinicialização ou executar um toorecover de failover do dispositivo dessa situação. |Sim |Não |
| 9 |Azure PowerShell |Quando você usa o cmdlet do StorSimple Olá **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - espera primeiro 1 -** tooselect Olá primeiro objeto para que você possa criar um novo **VolumeContainer** do objeto, Olá cmdlet retorna todos os objetos de saudação. |Encapsular Olá cmdlet entre parênteses, da seguinte maneira: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - primeiro 1 - espera** |Sim |Sim |
| 10 |Migração |Quando vários contêineres de volume são passados para a migração, Olá ETA para o backup mais recente é preciso para o contêiner de volume primeiro hello. Além disso, migração paralela será iniciado após hello 4 backups no contêiner de volume primeiro Olá são migrados. |É recomendável que você migre um contêiner de volume por vez. |Sim |Não |
| 11 |Migração |Após a restauração de saudação volumes não são adicionados toohello backup hello ou política de grupo do disco virtual. |Você precisará tooadd política de backup esses tooa volumes nos backups de toocreate de ordem. |Sim |Sim |
| 12 |Migração |Após a conclusão da migração Olá, o dispositivo da série Olá 5000/7000 não deve acessar Olá migrados contêineres de dados. |É recomendável que você exclua Olá migrados contêineres de dados após a migração de saudação concluída e confirmada. |Sim |Não |
| 13 |Clonagem e recuperação de desastre |Um dispositivo StorSimple com atualização 1 não é possível clonar ou executar o dispositivo de tooa de recuperação de desastres executando o software de pré-atualização 1. |Você precisará tooupdate Olá destino dispositivo tooUpdate 1 tooallow essas operações |Sim |Sim |
| 14 |Migração |O backup de configuração para a migração poderá falhar em um dispositivo da série 5000-7000 quando houver grupos de volumes sem volumes associados. |Excluir todos os grupos de volume vazios Olá sem volumes associados e, em seguida, repita o backup de configuração de saudação. |Sim |Não |
| 15 |Cmdlets do Azure PowerShell e volumes fixados localmente |Não é possível criar um volume fixado localmente por meio de cmdlets do Azure PowerShell. (Qualquer volume criado por meio do Azure PowerShell será organizado em camadas.) |Sempre use volumes de tooconfigure localmente afixado em serviço Olá StorSimple Manager. |Sim |Não |
| 16 |Espaço disponível para volumes fixados localmente |Se você excluir um volume localmente afixado, espaço para novos volumes Olá pode não ser atualizado imediatamente. atualizações de serviço do StorSimple Manager Olá Olá espaço local disponível aproximadamente a cada hora. |Aguarde uma hora antes de tentar de novo volume do toocreate hello. |Sim |Não |
| 17 |Volumes fixados localmente |O trabalho de restauração expõe Olá temporário de backup de instantâneo em Olá catálogo de Backup, mas apenas para a duração de saudação do trabalho de restauração hello. Além disso, ele expõe um grupo de disco virtual com o prefixo **tmpCollection** em Olá **políticas de Backup** página, mas somente durante Olá Olá o trabalho de restauração. |Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá. Nenhuma intervenção do usuário é necessária. |Sim |Não |
| 18 |Volumes fixados localmente |Se você cancelar um trabalho de restauração e um failover de controlador ocorre imediatamente depois disso, o trabalho de restauração Olá mostrará **falha** em vez de **cancelado**. Se um trabalho de restauração falhará e um failover de controlador ocorre imediatamente depois disso, o trabalho de restauração Olá mostrará **cancelado** em vez de **falha**. |Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá. Nenhuma intervenção do usuário é necessária. |Sim |Não |
| 19 |Volumes fixados localmente |Se você cancelar um trabalho de restauração ou se uma restauração falha e ocorre um failover de controlador, um trabalho de restauração adicionais será exibido no hello **trabalhos** página. |Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá. Nenhuma intervenção do usuário é necessária. |Sim |Não |
| 20 |Volumes fixados localmente |Se você tentar tooconvert um volume em camadas (criado e clonado com atualização 1.2 ou anterior) tooa localmente fixados volume e seu dispositivo está ficando sem espaço ou há falta de nuvem e hello clone(s) pode estar corrompido. |Esse problema ocorre apenas com volumes que foram criados e clonados com software anterior à Atualização 2.1. Isso deve ser um cenário incomum. | | |
| 21 |Conversão de volume |Não atualizar Olá ACRs tooa anexado volume enquanto uma conversão de volume está em andamento (toolocally hierárquico fixado ou vice-versa). Atualizar Olá ACRs poderia resultar em corrupção de dados. |Se necessário, atualize a conversão do volume Olá ACRs toohello anterior e não fazer outras atualizações ACR durante a conversão hello está em andamento. | | |
| 22 |Atualizações |Ao aplicar a atualização 3, Olá **manutenção** página Olá será de portal clássico do Azure exibição Olá mensagem tooUpdate relacionado 2 - "o StorSimple 8000 series atualização 2 inclui a capacidade de saudação para coletar de tooproactively da Microsoft registrar informações de seu dispositivo quando detectamos potenciais problemas". Isto é confuso, ele indica que o dispositivo hello está sendo atualizada tooUpdate 2. Após o dispositivo Olá succeesfully atualizado tooUpdate 3, essa mensagem desaparecerá. |Esse comportamento será corrigido em uma atualização futura. |Sim |Não |

## <a name="controller-and-firmware-updates-in-update-3"></a>Atualizações de controlador e firmware na Atualização 3
Esta versão tem atualizações de firmware e driver LSI. Para obter mais informações sobre como o driver de saudação LSI tooinstall e atualizações de firmware, consulte [instalar a atualização 3](storsimple-install-update-3.md) em seu dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-3"></a>Atualizações do dispositivo virtual na Atualização 3
Esta atualização não pode ser aplicado toohello StorSimple Appliance de nuvem (também conhecido como dispositivo virtual Olá). Novos dispositivos virtuais precisará toobe criado. 

## <a name="next-step"></a>Próxima etapa
Saiba como muito[instalar a atualização 3](storsimple-install-update-3.md) em seu dispositivo StorSimple.

