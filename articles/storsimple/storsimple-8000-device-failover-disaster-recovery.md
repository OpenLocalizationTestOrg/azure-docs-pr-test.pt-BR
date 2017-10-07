---
title: "aaaStorSimple failover, recuperação de desastres para dispositivos da 8000 série | Microsoft Docs"
description: "Saiba como toofail através de seu tooitself de dispositivo StorSimple, outro dispositivo físico ou um dispositivo de nuvem."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>Failover e recuperação de desastre para seu dispositivo StorSimple da série 8000

## <a name="overview"></a>Visão geral

Este artigo descreve o recurso de failover de dispositivo Olá para dispositivos da série StorSimple 8000 do hello e como esse recurso pode ser usado toorecover StorSimple dispositivos se ocorrer um desastre. StorSimple usa dados da saudação toomigrate dispositivo failover de um dispositivo de origem no dispositivo de destino em tooanother Olá datacenter. diretrizes de saudação neste artigo se aplicam a dispositivos físicos de série tooStorSimple 8000 e soluções de nuvem que executam versões do software Update 3 e posterior.

StorSimple usa Olá **dispositivos** recurso de failover de dispositivo folha toostart Olá no evento de saudação de um desastre. Esta folha lista todos os Olá StorSimple dispositivos conectados tooyour dispositivo o serviço StorSimple Manager.

![Folha Dispositivos](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Recuperação de desastres (DR) e failover de dispositivo

Em um cenário de recuperação de desastre, dispositivo primário Olá parará de funcionar. StorSimple usa dispositivo primário do hello como _fonte_ e move Olá associado nuvem dados tooanother _destino_ dispositivo. Esse processo é chamado tooas Olá *failover*. Olá gráfico a seguir ilustra o processo de saudação de failover.

![O que acontece no failover de dispositivo?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

dispositivo de destino Olá para um failover pode ser um dispositivo físico ou até mesmo um dispositivo de nuvem. Olá dispositivo de destino pode ser localizado no hello mesma ou em um local geográfico diferente que o dispositivo de origem hello.

Durante a saudação failover, você pode selecionar contêineres de volume para migração. StorSimple, em seguida, altera a propriedade de saudação desses contêineres de volume do dispositivo de destino toohello do dispositivo de origem hello. Depois de alterar a propriedade, contêineres de volume Olá StorSimple exclui esses contêineres de dispositivo de origem hello. Após a conclusão da exclusão hello, pode falhar dispositivo de destino de backup Olá. _Failback_ transferências Olá dispositivo de origem original propriedade toohello voltar.

### <a name="cloud-snapshot-used-during-device-failover"></a>Instantâneo de nuvem usado durante o failover do dispositivo

Após a recuperação de desastres, backup na nuvem hello mais recente é o dispositivo de destino de toohello do toorestore usado Olá dados. Para obter mais informações sobre instantâneos de nuvem, consulte [usar tootake de serviço de Gerenciador de dispositivos de StorSimple Olá um backup manual](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

Em um StorSimple da série 8000, as políticas de backup são associadas aos backups. Se houver várias políticas de backup para hello mesmo volume, em seguida, seleciona StorSimple Olá política de backup com o maior número de saudação de volumes. StorSimple, em seguida, usa o backup mais recente de saudação de saudação selecionada política de backup toorestore Olá dados no dispositivo de destino hello.

Suponha que existam duas políticas de backup, *defaultPol* e *customPol*:

* *defaultPol*: um volume, *vol1*, executada diariamente a partir das 22h30.
* *customPol*: quatro volumes, *vol1*, *vol2*, *vol3* e *vol4*, executada diariamente a partir das 22h.

Nesse caso, o StorSimple prioriza o controle de falhas e usa *customPol*, pois ela tem mais volumes. Olá o backup mais recente dessa política é usada toorestore dados. Para obter mais informações sobre como toocreate e gerenciar políticas de backup, acesse muito[usar políticas de backup do hello Gerenciador de dispositivos do StorSimple service toomanage](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Considerações comuns para failover de dispositivo

Antes de executar o failover de um dispositivo, examine Olá informações a seguir:

* Antes de inicia um failover de dispositivo, todos os volumes de saudação em contêineres de volume Olá devem estar offline. Em um failover não planejado, os volumes do StotSimple ficarão offline automaticamente. Mas se você estiver executando um failover planejado (tootest DR), você deve colocar todos os volumes de saudação offline.
* Olá apenas contêineres de volume que têm um tipo de instantâneo em nuvem são listados para recuperação de desastres. Deve haver pelo menos um contêiner de volume com dados de toorecover de instantâneo uma nuvem associada.
* Se houver instantâneos de nuvem que se estendem por vários contêineres de volume, o StorSimple fará failover desses contêineres de volume como um conjunto. Um caso raro, se houver instantâneos locais que se estendem por vários contêineres de volume, mas não instantâneos de nuvem associados, StorSimple failover instantâneos locais hello e dados de local de saudação são perdidos após a recuperação de desastres.
* Olá destino disponíveis para DR são dispositivos que têm tooaccommodate de espaço suficiente Olá contêineres de volume selecionados. Dispositivos que não têm espaço suficiente não são listados como dispositivos de destino.
* Após a recuperação de desastres (por tempo limitado), Olá desempenho de acesso a dados pode ser afetado significativamente, como dispositivo Olá precisa tooaccess Olá dados da nuvem hello e armazená-lo localmente.

#### <a name="device-failover-across-software-versions"></a>Failover de dispositivo em versões de software

Um serviço do Gerenciador de Dispositivos do StorSimple em uma implantação pode ter vários dispositivos, tanto físicos quanto de nuvem, todos executando versões de software diferentes.

Use Olá toodetermine tabela a seguir se você pode fazer failover ou falha de dispositivo de backup tooanother executando uma versão de software diferente e como os tipos de volume Olá se comportam durante a recuperação de desastres.

#### <a name="failover-and-failback-across-software-versions"></a>Failover e failback entre versões de software

| Failover/failback de | Dispositivo físico | Dispositivo de nuvem |
| --- | --- | --- |
| Atualização 3 tooUpdate 4 |Volumes em camadas fazem failover em camadas. <br></br>Volumes fixados localmente fazem failover fixados localmente. <br></br> Após um failover, quando você usa um instantâneo no dispositivo Olá atualização 4, [controle de mapa de calor](storsimple-update4-release-notes.md#whats-new-in-update-4) é acionado. |Volumes fixados localmente fazem failover em camadas. |
| Atualização 4 tooUpdate 3 |Volumes em camadas fazem failover em camadas. <br></br>Volumes fixados localmente fazem failover fixados localmente. <br></br> Backups usados toorestore manter metadados de mapa de calor. <br></br>O acompanhamento de mapa de calor não está disponível na Atualização 3 após um failback. |Volumes fixados localmente fazem failover em camadas. |


## <a name="device-failover-scenarios"></a>Cenários de failover de dispositivo

Se houver um desastre, você pode escolher toofail em seu dispositivo StorSimple:

* [dispositivo físico tooa](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [dispositivo de nuvem tooa](storsimple-8000-device-failover-cloud-appliance.md).

Olá artigos anteriores fornecem etapas detalhadas para cada Olá acima casos de failover.


## <a name="failback"></a>Failback

A partir da Atualização 3, o StorSimple também dá suporte para failback. Failback é apenas Olá inversa de failover, destino Olá se torna a origem de saudação e dispositivo de origem original Olá durante o failover de saudação agora torna-se o dispositivo de destino hello. 

Durante o failback, StorSimple sincroniza novamente Olá dados toohello back primário local é interrompida hello e/s e atividade do aplicativo e faz a transição de local original toohello voltar.

Após um failover estiver concluído, StorSimple realiza Olá ações a seguir:

* StorSimple limpa os contêineres de volume Olá failover de dispositivo de origem hello.
* StorSimple inicia um trabalho em segundo plano por contêiner de volume (failover) no dispositivo de origem hello. Se você tentar toofail enquanto Olá trabalho está em andamento, você receberá um efeito de toothat de notificação. Aguarde até que o trabalho Olá é concluída toostart Olá failback.
* tempo Olá toocomplete exclusão de saudação de contêineres de volume depende de vários fatores, como a quantidade de dados, a idade dos dados hello, número de backups e largura de banda de rede do hello disponível para a operação de saudação.

Se você estiver planejando fazer failbacks ou failovers de teste, recomendamos testar os contêineres de volume com menos dados (Gbs). Normalmente, você pode iniciar Olá failback 24 horas após a conclusão do failover de saudação.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

P. **O que acontece se Olá DR falha ou se tiver êxito parcial?**

R. Se Olá DR falhar, recomendamos que você tente novamente. trabalho de failover de dispositivo segundo Hello está ciente do progresso de saudação do trabalho primeiro hello e inicia a partir desse ponto em diante.

P. **Excluir um dispositivo enquanto Olá failover do dispositivo está em andamento?**

R. Você não pode excluir um dispositivo enquanto uma DR está em andamento. Você só pode excluir o dispositivo após a conclusão da saudação DR. Você pode monitorar o andamento do trabalho de failover do hello dispositivo em Olá **trabalhos** folha.

P. **Quando a coleta de lixo Olá inicia no dispositivo de origem Olá para que Olá de dados local no dispositivo de origem é excluído?**

R. Coleta de lixo está habilitada no dispositivo de origem Olá somente depois que o dispositivo Olá completamente é limpo. Limpeza de saudação inclui limpeza de objetos que falharam do dispositivo de origem hello como objetos de backup (não de dados), volumes, contêineres de volume e políticas.

P. **O que acontece se Olá excluir trabalho associado aos contêineres de volume Olá no dispositivo de origem Olá falha?**

R.  Se Olá excluir trabalho falhar, poderá excluir manualmente os contêineres de volume hello. Em Olá **dispositivos** folha, selecione o dispositivo de origem e clique em **contêineres de Volume**. Clique em contêineres de volume Olá Select que falharam em e na parte inferior da saudação da folha de saudação **excluir**. Após ter excluído todas as Olá falha em contêineres de volume no dispositivo de origem hello, você pode iniciar Olá failback. Para obter mais informações, vá muito[excluir um contêiner de volume](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>BCDR (recuperação de desastre de continuidade de negócios)

Um cenário de recuperação (BCDR) de desastres de continuidade de negócios ocorre quando Olá data center inteiro do Azure para de funcionar. Essa situação pode afetar o serviço do Gerenciador de dispositivos do StorSimple e Olá associados dispositivos StorSimple.

Se um dispositivo StorSimple foi registrado antes de um desastre ocorreu, em seguida, este dispositivo pode ser necessário tooundergo redefinição de fábrica. Após o desastre hello, o dispositivo StorSimple Olá aparece na Olá portal do Azure como offline. Este dispositivo deve ser excluído do portal de saudação. Redefinir padrões de toofactory Olá dispositivo e registrá-lo novamente com o serviço de saudação.

## <a name="next-steps"></a>Próximas etapas

Se você estiver pronto tooperform um failover de dispositivo, escolha um dos seguintes cenários para obter instruções detalhadas de saudação:

- [O failover de dispositivo físico tooanother](storsimple-8000-device-failover-physical-device.md)
- [Failover toohello mesmo dispositivo](storsimple-8000-device-failover-same-device.md)
- [Failover tooStorSimple Appliance de nuvem](storsimple-8000-device-failover-cloud-appliance.md)

Se o failover do dispositivo, escolha um destes Olá as opções a seguir:

* [Desativar e excluir um dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* [Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

