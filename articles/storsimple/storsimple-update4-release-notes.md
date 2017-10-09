---
title: "Notas de versão do aaaStorSimple 8000 Series atualização 4 | Microsoft Docs"
description: "Descreve os novos recursos do hello, problemas e soluções alternativas para StorSimple 8000 Series atualização 4."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Notas de versão da Atualização 4 para o StorSimple 8000 Series

## <a name="overview"></a>Visão geral

Olá notas de versão a seguir descrevem Olá novos recursos e identificam os problemas abertos críticos Olá para StorSimple 8000 Series atualização 4. Eles também contêm uma lista de atualizações de software do hello StorSimple incluídas nesta versão. 

Atualização 4 pode ser aplicado tooany o dispositivo StorSimple execução da versão (GA) ou atualização 0,1 por meio de atualização 3.1. versão do dispositivo Olá associado com a atualização 4 é 6.3.9600.17820.

Analise Olá informações contidas na versão Olá notas antes de implantar Olá atualizar em sua solução StorSimple.

> [!IMPORTANT]
> * A Atualização 4 tem o software de dispositivo, firmware USM, driver e firmware LSI, firmware de disco, Storport e Spaceport, segurança e outras atualizações do sistema operacional. Demora cerca de 4 horas tooinstall essa atualização. A atualização de firmware de disco é uma atualização com tempo de inatividade e resulta em um tempo de inatividade para o dispositivo. É recomendável que você aplique a atualização 4 tookeep seu dispositivo atualizado. 
> * Para novas versões, você poderá não ver atualizações imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Aguarde alguns dias e procure atualizações novamente, uma vez que elas serão disponibilizadas em breve.

## <a name="whats-new-in-update-4"></a>Novidades na Atualização 4

Olá seguintes principais melhorias e correções de bugs foram feitas na atualização 4.

* **Mais inteligente automatizada algoritmos de reclamação de espaço** – na atualização 4, hello algoritmos de reclamação de espaço automatizada são reclamação de espaço tooadjust avançados Olá ciclos com base em Olá esperado recuperada espaço disponível na nuvem hello. 

* **Aprimoramentos de desempenho para volumes localmente afixados** – atualização 4 melhorou o desempenho Olá dos volumes fixados localmente em cenários que têm a ingestão de dados alta (tamanho dos dados comparável toovolume).

* **Restauração baseada em mapa de calor** - na Olá anteriormente versões, após uma recuperação de desastres (DR), dados saudação foi restaurados da nuvem de saudação com base nos padrões de acesso de hello, resultando em um desempenho lento. 

    Um novo recurso é implementado na atualização 4 que rastreia acessados com frequência dados toocreate um mapa de calor quando o dispositivo de saudação estiver no tooDR anterior de uso (partes de dados mais usadas têm alta calor enquanto menos usadas partes têm pouco aquecimento). Após a recuperação de desastres, StorSimple usa Olá mapa de calor tooautomatically restauração e realimentar dados saudação da nuvem de saudação. 

    Todas as restaurações Olá agora são restaurações de mapa de calor com base. Para obter mais informações sobre como o mapa de calor tooquery e Cancelar com base em trabalhos de restauração e reidratação, vá muito[do Windows PowerShell para referência de cmdlet do StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

* **Ferramenta de diagnóstico de StorSimple** – na atualização 4, um diagnóstico StorSimple ferramenta está sendo liberado tooallow para diagnosticar fácil e solução de problemas relacionados a integridade dos componentes de hardware, rede, desempenho e toosystem. Essa ferramenta é executada por meio de saudação do Windows PowerShell para StorSimple. Para obter mais informações, vá muito[solucionar problemas usando a ferramenta de diagnóstico de StorSimple](storsimple-8000-diagnostics.md).

* **Ferramenta de migração StorSimple com base na interface do usuário** -toothis anteriores de versão, a migração de dados da 7000 5000 série necessário Olá usuários tooexecute uma parte do fluxo de trabalho de migração de saudação usando a interface do PowerShell do Azure hello. Nesta versão, uma fácil de usar migração de StorSimple baseada em interface do usuário ferramenta é disponibilizada para suporte toofacilitate Olá mesmo fluxo de trabalho de migração. Essa ferramenta também permite consolidação de saudação de buckets de recuperação. 

* **Alterações relacionadas a FIPS** – essa versão em diante, FIPS está habilitado por padrão em todos os dispositivos da série StorSimple 8000 de saudação para ambos Olá Microsoft Azure Government e contas de nuvem pública do Azure.

* **Atualizar alterações** - nesta versão, bugs tooupdate relacionados falhas foram corrigidas.

* **Alerta de falhas de disco** -um novo alerta que avisa o usuário de saudação de falhas iminentes de disco é adicionado nesta versão. Se você encontrar esse alerta, entre em contato com o Microsoft Support tooship um disco de substituição. Para obter mais informações, vá muito[alertas de hardware no dispositivo StorSimple](storsimple-manage-alerts.md#hardware-alerts).

* **Alterações de substituição do controlador** -um cmdlet que permite que o status do hello usuário tooquery saudação do processo de substituição de controlador Olá é adicionado nesta versão. Para obter mais informações, consulte toohello [status de substituição do controlador do cmdlet tooquery](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problemas corrigidos na Atualização 4

Olá tabela a seguir fornece um resumo dos problemas que foram corrigidos na atualização 4.    

| Não | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Failover |Em Olá versão anterior, após o failover hello, há foi um problema relacionado toocleanup observado no site de saudação do cliente. Esse problema foi corrigido nesta versão. |Sim |Sim |
| 2 |Volumes fixados localmente |Na versão anterior do hello, houve criação de volume toorelated um problema para volumes localmente afixados que pode resultar em falhas na criação do volume. Esse problema foi causado pela raiz e corrigido nesta versão. |Sim |Não |
| 3 |Pacote de suporte |Na versão anterior, havia pacote tooSupport relacionados de problemas que possam resultar em uma exceção de System.OutOfMemory ou outros erros, resultando em uma falha de criação de pacote de suporte. Esses bugs foram corrigidos nesta versão. |Sim |Sim |
| 4 |Monitoramento |Na versão anterior, há um problema relacionado toomonitoring gráficos para volumes localmente afixados onde consumo foi exibido na Web. Esse bug foi corrigido nesta versão. |Sim |Sim |
| 5 |Migração |Na versão anterior, havia vários confiabilidade toohello relacionados de problemas de migração de dispositivos da série 7000 5000 série too8000. Esses problemas foram resolvidos nesta versão. |Sim |Sim |
| 6 |Atualização |Em versões anteriores, se houver uma falha na atualização, controladores de saudação entrará em modo de recuperação e, portanto, usuário Olá não foi possível prosseguir com a atualização de saudação e precisaria toocontact Microsoft Support. <br> Esse comportamento foi alterado nesta versão. Se o usuário Olá tem uma falha de atualização após os dois controladores Olá execução Olá mesma versão (atualização 4), Olá controladores não entrar no modo de recuperação. Se o usuário Olá encontrar essa falha, recomendamos que aguarde um pouco e, em seguida, tente novamente a atualização de saudação. repetição de saudação foi bem-sucedida. Se a repetição de saudação falhar, eles devem contatar Microsoft Support. |Sim |Sim |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Problemas conhecidos na atualização 4 de versões anteriores

Não há nenhum problema conhecido de novo na atualização 4. Para obter uma lista dos problemas transportadas tooUpdate 4 de versões anteriores, ir muito[notas de versão da atualização 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Controlador SCSI (SAS) anexado em série e atualizações na Atualização 4

Esta versão tem controlador SAS e atualizações de firmware e driver LSI. Para obter mais informações sobre como tooinstall essas atualizações, consulte [instalar a atualização 4](storsimple-install-update-4.md) em seu dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-4"></a>Atualizações do dispositivo virtual na Atualização 4

Esta atualização não pode ser aplicado toohello StorSimple Appliance de nuvem (também conhecido como dispositivo virtual Olá). Novos dispositivos virtuais precisará toobe criado. 

## <a name="next-step"></a>Próxima etapa

Saiba como muito[instalar a atualização 4](storsimple-install-update-4.md) em seu dispositivo StorSimple.

