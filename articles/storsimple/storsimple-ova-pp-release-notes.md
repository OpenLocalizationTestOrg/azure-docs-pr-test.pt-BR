---
title: "Notas de versão de matriz Virtual aaaStorSimple | Microsoft Docs"
description: "Descreve as questões abertas fundamentais e as resoluções para Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>Notas de versão do StorSimple Virtual Array
## <a name="overview"></a>Visão geral
Notas de versão seguintes Hello identificam problemas de abrir crítico do Olá versão de disponibilidade geral (GA) de março de 2016 saudação do hello Microsoft Azure StorSimple Virtual Array (também conhecido como dispositivo virtual local StorSimple de saudação ou Olá StorSimple virtual dispositivo). Esta versão corresponde toosoftware versão 10.0.10271.0.

Notas de versão de saudação são continuamente atualizadas, e que forem descobertas questões importantes que exijam uma solução alternativa, elas são adicionadas. Antes de implantar seu dispositivo virtual StorSimple, revise atentamente as informações de saudação contidas nas notas de versão de saudação. 

Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Solução alternativa/comentários |
| --- | --- | --- | --- |
| **1.** |Atualizações |dispositivos virtuais de saudação criados na versão de visualização de saudação não podem ser atualizada tooa suporte para versão de disponibilidade geral. |Esses dispositivos virtuais devem fazer failover para Olá versão disponibilidade geral usando um fluxo de trabalho de recuperação de desastres. |
| **2.** |Disco de dados provisionado |Uma vez que você possua um disco de dados de um determinado tamanho especificado e criar dispositivo virtual do hello correspondente StorSimple, você deve não expandir ou reduzir Olá disco de dados. Tentar toodo portanto resultará em perda de todos os dados de saudação nas camadas de local de saudação do dispositivo hello. | |
| **3.** |Política de grupo |Quando um dispositivo está ingressado no domínio, aplicar uma política de grupo pode afetar a operação de dispositivo hello. |Certifique-se de que sua matriz virtual está em sua própria unidade organizacional (UO) do Active Directory e nenhum objeto de diretiva de grupo (GPO) é aplicada tooit. |
| **4.** |Interface do Usuário da Web local |Se os recursos de segurança aprimorados estão habilitados no Internet Explorer (IE ESC), algumas páginas da interface do usuário da Web local, como Solução de Problemas ou Manutenção, podem não funcionar corretamente. Os botões nessas páginas também podem não funcionar. |Desligue os recursos de segurança reforçada do Internet Explorer. |
| **5.** |Interface do Usuário da Web local |Em uma máquina virtual de Hyper-V, Olá interfaces de rede na web hello interface do usuário são exibidos como interfaces de 10 Gbps. |Esse comportamento é um reflexo do Hyper-V. O Hyper-V sempre mostra 10 Gbps para adaptadores de rede virtual. |
| **6.** |Compartilhamentos ou volumes em camadas |Não há suporte para o intervalo de bytes de bloqueio para aplicativos que funcionam com hello StorSimple volumes em camadas. Se o bloqueio de intervalo de bytes estiver habilitado, a disposição em camadas do StorSimple não funcionará. |As medidas recomendadas incluem:  <br></br>Desligar o bloqueio de intervalo de bytes em sua lógica de aplicativo.<br></br>Escolha dados tooput para este aplicativo em volumes localmente afixados contrário como volumes de tootiered.<br></br>*Limitação*: se usando localmente fixados volumes e bloqueio de intervalo de bytes é habilitado, lembre-se de que volume Olá fixado localmente pode ser online antes mesmo de saudação restauração for concluída. Nesses casos, se uma restauração está em andamento, em seguida, você deve aguardar Olá toocomplete de restauração. |
| **7.** |Compartilhamentos em camadas |Trabalhar com arquivos grandes pode resultar em uma divisão em camadas lenta. |Ao trabalhar com arquivos grandes, é recomendável que esse arquivo maior Olá é menor do que 3% do tamanho do compartilhamento de saudação. |
| **8.** |Capacidade utilizada para compartilhamentos |Você pode ver compartilhar consumo na ausência de saudação de todos os dados no compartilhamento de saudação. Isso ocorre porque a capacidade de saudação usada para compartilhamentos inclui metadados. | |
| **9.** |Recuperação de desastre |Você só pode executar a recuperação de desastres de saudação de um toohello de servidor de arquivo mesmo domínio que o dispositivo de origem hello. Não há suporte para o dispositivo de destino de tooa de recuperação de desastres em outro domínio nesta versão. |Isso será implementado em uma versão posterior. |
| **10.** |Azure PowerShell |os dispositivos virtuais StorSimple Olá não podem ser gerenciados por meio de saudação do PowerShell do Azure nesta versão. |Todo o gerenciamento de saudação de dispositivos virtuais Olá deve ser feito por meio de hello portal clássico do Azure e a interface da web local hello. |
| **11.** |Alteração de senha |console de dispositivo virtual array Olá só aceita entrada no formato de teclado en-US. | |
| **12.** |CHAP |Não é possível remover as credenciais CHAP depois de criadas. Além disso, se você modificar as credenciais CHAP hello, será necessário tootake volumes de saudação offline e, em seguida, coloque-os online para Olá alterar tootake efeito. |Isso será corrigido em uma versão futura. |
| **13.** |Servidor iSCSI |Olá 'Usado armazenamento' exibido para um volume iSCSI pode ser diferente no serviço do StorSimple Manager hello e host iSCSI de saudação. |host de iSCSI Olá tem o modo de exibição de sistema de arquivos de hello.<br></br>dispositivo Olá vê blocos Olá distribuídos ao volume Olá estava no tamanho máximo de saudação. |

