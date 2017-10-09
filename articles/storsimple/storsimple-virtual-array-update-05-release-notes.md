---
title: "Notas de versão de 0,5 de atualização de matriz Virtual de aaaStorSimple | Microsoft Docs"
description: "Descreve abrir crítico problemas e resoluções para a execução de matriz Virtual StorSimple Olá atualizar 0,5."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>Notas de versão da Matriz Virtual do StorSimple Atualização 0.5

## <a name="overview"></a>Visão geral

Olá notas de versão a seguir identificam problemas abertos críticos de saudação e Olá problemas resolvidos para atualizações do Microsoft Azure StorSimple Virtual Array.

Notas de versão de saudação são continuamente atualizadas, e que forem descobertas questões importantes que exijam uma solução alternativa, elas são adicionadas. Antes de implantar sua matriz Virtual StorSimple, revise atentamente informações Olá contidas nas notas de versão de saudação.

Atualização de 0,5 corresponde a versão do software toohello **10.0.10290.0**.

> [!NOTE]
> As atualizações causam interrupção e reiniciam seu dispositivo. Se a e/s estão em andamento, o dispositivo Olá incorre em tempo de inatividade. Para obter instruções detalhadas sobre como tooapply Olá atualização, vá muito[instale a atualização de 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>O que há de novo no hello atualização 0,5
A Atualização 0.5 é, basicamente, um build de correção de bug. correções de bug e aperfeiçoamentos principal Olá são da seguinte maneira:

- **Aprimoramentos de resiliência de backup** -esta versão contém correções para aumentar a resiliência de backup hello. Em Olá versões anteriores, os backups foram repetidas apenas para determinadas exceções. Esta versão repete todas as exceções de backup Olá e torna Olá backups mais resilientes.

- **Atualizações para o monitoramento de uso do armazenamento** -a partir de 30 de junho de 2017, Olá monitoramento de uso de armazenamento para a série de dispositivo Virtual StorSimple será desativada. Isso se aplica a toohello gráficos em todos os conjuntos de saudação virtual executando atualização 0,4 ou inferior de monitoramento. Esta atualização contém alterações de saudação necessárias para você toocontinue Olá uso do uso do armazenamento de monitoramento no hello portal do Azure. Instalar esta atualização crítica antes de 30 de junho de 2017 toocontinue usando o recurso de monitoramento de saudação.


## <a name="issues-fixed-in-hello-update-05"></a>Problemas corrigidos Olá atualização 0,5

Olá tabela a seguir fornece um resumo dos problemas corrigidos nesta versão.

| Não. | Recurso | Problema |
| --- | --- | --- |
| 1 |Resiliência de backup| Em Olá versões anteriores, os backups foram repetidas apenas para determinadas exceções. Esta versão contém backups de toomake uma correção mais resiliente, repita todas as exceções de backup hello.|
| 2 |Monitoramento| Olá monitoramento de uso do armazenamento para a série de dispositivo Virtual StorSimple será substituído iniciando em 30 de junho de 2017. Esta ação afeta Olá monitoramento gráficos no serviço do Gerenciador de dispositivos de StorSimple Olá em execução em matrizes de Virtual do StorSimple (modelo de 1200). Esta versão contém atualizações que permitem o uso de saudação do hello usuário toocontinue de monitoramento de uso do armazenamento em matrizes de saudação virtual além de 30 de junho de 2017.|
| 3 |Servidor de arquivos| Em Olá versões anteriores, um usuário por engano poderiam copiar a matriz de virtual de toohello de arquivos criptografados. Esta versão contém uma correção que não permite que uma cópia de matriz de toovirtual arquivos criptografados. Se seu dispositivo tem toohello anteriores de arquivos criptografados existente de atualização, os backups continuarão toofail até que todos os arquivos de saudação criptografado serão excluídos do sistema de saudação. |


## <a name="known-issues-in-hello-update-05"></a>Problemas conhecidos no hello atualização 0,5

Olá tabela a seguir fornece um resumo dos problemas conhecidos Olá matriz Virtual do StorSimple e inclui os problemas de saudação observado na versão de versões anteriores do hello.

| Não. | Recurso | Problema | Solução alternativa/comentários |
| --- | --- | --- | --- |
| **1.** |Atualizações |dispositivos virtuais de saudação criados na versão de visualização de saudação não podem ser atualizada tooa suporte para versão de disponibilidade geral. |Esses dispositivos virtuais devem fazer failover para Olá versão disponibilidade geral usando um fluxo de trabalho de recuperação de desastres. |
| **2.** |Disco de dados provisionado |Uma vez que você possua um disco de dados de um determinado tamanho especificado e criar dispositivo virtual do hello correspondente StorSimple, você deve não expandir ou reduzir Olá disco de dados. Tentativa de resultados de toodo em uma perda de todos os dados de saudação nas camadas de local de saudação do dispositivo hello. | |
| **3.** |Política de grupo |Quando um dispositivo está ingressado no domínio, aplicar uma política de grupo pode afetar a operação de dispositivo hello. |Certifique-se de que sua matriz virtual está em sua própria unidade organizacional (UO) do Active Directory e nenhum objeto de diretiva de grupo (GPO) é aplicada tooit. |
| **4.** |Interface do Usuário da Web local |Se os recursos de segurança aprimorados estão habilitados no Internet Explorer (IE ESC), algumas páginas da interface do usuário da Web local, como Solução de Problemas ou Manutenção, podem não funcionar corretamente. Os botões nessas páginas também podem não funcionar. |Desligue os recursos de segurança reforçada do Internet Explorer. |
| **5.** |Interface do Usuário da Web local |Em uma máquina virtual de Hyper-V, Olá interfaces de rede na web hello interface do usuário são exibidos como interfaces de 10 Gbps. |Esse comportamento é um reflexo do Hyper-V. O Hyper-V sempre mostra 10 Gbps para adaptadores de rede virtual. |
| **6.** |Compartilhamentos ou volumes em camadas |Não há suporte para o intervalo de bytes de bloqueio para aplicativos que funcionam com hello StorSimple volumes em camadas. Se o bloqueio de intervalo de bytes estiver habilitado, a disposição em camadas do StorSimple não funcionará. |As medidas recomendadas incluem:  <br></br>Desligar o bloqueio de intervalo de bytes em sua lógica de aplicativo.<br></br>Escolha dados tooput para este aplicativo em volumes localmente afixados contrário como volumes de tootiered.<br></br>*Limitação*: quando usar localmente fixados volumes e bloqueio de intervalo de bytes é habilitado, volume Olá fixado localmente pode ser online antes mesmo de saudação restauração for concluída. Nesses casos, se uma restauração está em andamento, em seguida, você deve aguardar Olá toocomplete de restauração. |
| **7.** |Compartilhamentos em camadas |Trabalhar com arquivos grandes pode resultar em uma divisão em camadas lenta. |Ao trabalhar com arquivos grandes, é recomendável que esse arquivo maior Olá é menor do que 3% do tamanho do compartilhamento de saudação. |
| **8.** |Capacidade utilizada para compartilhamentos |Você pode ver compartilhar consumo quando não há nenhum dado no compartilhamento de saudação. Esse consumo é porque a capacidade de saudação usada para compartilhamentos inclui metadados. | |
| **9.** |Recuperação de desastre |Você só pode executar a recuperação de desastres de saudação de um toohello de servidor de arquivo mesmo domínio que o dispositivo de origem hello. Não há suporte para o dispositivo de destino de tooa de recuperação de desastres em outro domínio nesta versão. |Isso será implementado em uma versão posterior. Para obter mais informações, vá muito[Failover e recuperação de desastres para sua matriz Virtual StorSimple](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |os dispositivos virtuais StorSimple Olá não podem ser gerenciados por meio de saudação do PowerShell do Azure nesta versão. |Todo o gerenciamento de saudação de dispositivos virtuais Olá deve ser feito por meio de hello Azure portal e hello interface da web local. |
| **11.** |Alteração de senha |Olá console de dispositivo virtual array só aceita entrada em en-us formato de teclado. | |
| **12.** |CHAP |Não é possível remover as credenciais CHAP depois de criadas. Além disso, se você modificar as credenciais CHAP Olá, precisa de volumes de saudação tootake offline e, em seguida, coloque-os online para Olá alterar tootake efeito. |Esse problema será corrigido em uma versão futura. |
| **13.** |Servidor iSCSI |Olá 'Usado armazenamento' exibido para um volume iSCSI pode ser diferente no serviço do Gerenciador de dispositivos de StorSimple hello e host iSCSI de saudação. |host de iSCSI Olá tem o modo de exibição de sistema de arquivos de hello.<br></br>dispositivo Olá vê blocos Olá distribuídos ao volume Olá estava no tamanho máximo de saudação. |
| **14.** |Servidor de arquivos |Se um arquivo em uma pasta tiver um fluxo de dados alternativo (ADS) associado a ele, Olá anúncios não é copiado ou restaurado por meio de recuperação de desastres, clonagem e recuperação em nível de Item. | |
| **15.** |Servidor de arquivos |Não há suporte para links simbólicos. | |
| **16.** |Servidor de arquivos |Arquivos protegidos pelo Windows Encrypting File System (EFS) quando copiou ou armazenado em Olá resultado do servidor de arquivo de matriz Virtual do StorSimple em uma configuração sem suporte.  | |

## <a name="next-step"></a>Próxima etapa
[Instale a Atualização 0.5](storsimple-virtual-array-install-update-05.md) na Matriz Virtual do StorSimple.

## <a name="references"></a>Referências
Procurando uma nota de versão mais antiga? Acesse:

* [Notas de versão da Matriz Virtual do StorSimple Atualização 0.4](storsimple-virtual-array-update-04-release-notes.md)
* [Notas de versão da atualização 0.3 da StorSimple Virtual Array](storsimple-ova-update-03-release-notes.md)
* [Notas de versão as Atualizações 0.1 e 0.2 do StorSimple Virtual Array](storsimple-ova-update-01-release-notes.md)
* [Notas de versão de disponibilidade geral do StorSimple Virtual Array](storsimple-ova-pp-release-notes.md)

