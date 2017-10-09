---
title: "administração do Gerenciador de instantâneos de aaaStorSimple | Microsoft Docs"
description: "Fornece uma visão geral e links toomore informações sobre tarefas de administração do Gerenciador de instantâneos StorSimple solução e fluxos de trabalho."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>Use o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple

## <a name="overview"></a>Visão geral
O StorSimple Snapshot Manager é um snap-in do Microsoft Management Console (MMC) que simplifica a proteção de dados e o gerenciamento de backup em um ambiente Microsoft Azure StorSimple. Com o Gerenciador de instantâneos do StorSimple, você pode gerenciar dados do Microsoft Azure StorSimple no Centro de dados hello e na nuvem Olá como uma solução única de armazenamento integrado, assim, simplificar os processos de backup e reduzindo os custos.

console de gerenciamento central do Gerenciador de instantâneos StorSimple Olá permite que você toocreate consistente e point-in-time cópias de backup local e dados na nuvem. Por exemplo, você pode usar o console de saudação para:

* Configurar, fazer backup e excluir volumes.
* Configurar o volume tooensure grupos que o backup dos dados é consistente com o aplicativo.
* Gerencie políticas de backup para que os dados sejam copiados em um agendamento predeterminado.
* Crie cópias independentes de dados, que podem ser armazenados na nuvem hello e usados para recuperação de desastres.

Este artigo fornece links tootutorials que descrevem o Gerenciador de instantâneos do StorSimple e como toouse-toocomplete fluxos de trabalho e tarefas de administração do sistema.

* Para obter mais informações sobre os componentes e arquitetura do StorSimple Snapshot Manager, consulte [O que é o StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md) 
* toodownload StorSimple Snapshot Manager, vá muito[página de download do Gerenciador de instantâneos StorSimple Olá](https://www.microsoft.com/download/details.aspx?id=44220).
* Para procedimentos de implantação StorSimple Snapshot Manager, vá muito[implantar o Gerenciador de instantâneos do StorSimple](storsimple-snapshot-manager-deployment.md).

> [!NOTE]
> Você não pode usar toomanage StorSimple Snapshot Manager Microsoft Azure StorSimple Virtual Arrays da (também conhecido como StorSimple local dispositivos virtuais).


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>Fluxos de trabalho e tarefas do StorSimple Snapshot Manager
Você pode usar o hello toomonitor Gerenciador de instantâneos do StorSimple e gerenciar trabalhos de backup atuais, agendados e concluídos. Além disso, o Gerenciador de instantâneos StorSimple fornece um catálogo de backups too64 concluída. Você pode usar o hello catálogo toofind e restaurar volumes ou arquivos individuais. 

| Se você quiser tooDO THIS... | USE ESTE TUTORIAL... |
|:--- |:--- |
| Saiba mais sobre o StorSimple Snapshot Manager |[O que é o StorSimple Snapshot Manager? ](storsimple-what-is-snapshot-manager.md) |
| Instalar o StorSimple Snapshot Manager<br>Reinstalar o StorSimple Snapshot Manager<br>Remover o StorSimple Snapshot Manager |[Implantar o StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md) |
| Use os menus e recursos do StorSimple Snapshot Manager:<ul><li>Barra de menus</li><li>Barra de ferramentas</li><li>Painel Escopo</li><li>Painel Resultados</li><li>Painel Ações</li><li>Navegação por teclado e atalhos</li></ul> |[Interface do usuário do StorSimple Snapshot Manager](storsimple-use-snapshot-manager.md) |
| Use Olá comuns MMC recursos incluídos no Gerenciador de instantâneos do StorSimple:<ul><li>Visualizar</li><li>Nova Janela a Partir Daqui</li><li>Atualizar</li><li>Exportar Lista</li><li>Ajuda</li></ul> |[Use as ações de menu do hello MMC no Gerenciador de instantâneos do StorSimple](storsimple-snapshot-manager-mmc-menu.md) |
| Adicionar ou substituir um dispositivo<br>Conectar um dispositivo<br>Verificar grupos de volume importados<br>Atualizar os dispositivos conectados<br>Autenticar um dispositivo<br>Exibir detalhes do dispositivo<br>Excluir uma configuração de dispositivo<br>Alterar uma senha de dispositivo<br>Substituir um dispositivo com falha<br> |[Use o Gerenciador de instantâneos StorSimple tooconnect e gerenciar dispositivos de StorSimple](storsimple-snapshot-manager-manage-devices.md) |
| Montar volumes<br>Exibir informações sobre volumes<br>Excluir um volume<br>Examinar volumes novamente<br>Configurar e fazer backup de um volume básico<br>Configurar e fazer backup de um volume espelhado dinâmico |[Use o Gerenciador de instantâneos StorSimple tooview e gerenciar volumes](storsimple-snapshot-manager-manage-volumes.md) |
| Exibir grupos de volumes<br>Criar um grupo de volumes<br>Fazer backup de um grupo de volumes<br>Editar um grupo de volumes<br>Excluir um grupo de volumes |[Use o Gerenciador de instantâneos StorSimple toocreate e gerenciar grupos de volume](storsimple-snapshot-manager-manage-volume-groups.md) |
| Criar uma política de backup <br>Editar uma política de backup<br>Excluir uma política de backup |[Use o Gerenciador de instantâneos StorSimple toocreate e gerenciar políticas de backup](storsimple-snapshot-manager-manage-backup-policies.md) |
| Exibir e gerenciar trabalhos de backup agendados<br>Exibir e gerenciar trabalhos de backup recentes<br>Exibir e gerenciar trabalhos de backup em execução |[Use o Gerenciador de instantâneos StorSimple tooview e gerenciar trabalhos de backup](storsimple-snapshot-manager-manage-backup-jobs.md) |
| Restaurar um volume<br>Clonar um volume ou grupo de volumes<br>Excluir um conjunto de backups<br>Recuperar um arquivo<br>Restaurar o banco de dados do hello Gerenciador de instantâneos StorSimple |[Use o Gerenciador de instantâneo StorSimple toomanage catálogo de backup Olá](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>Próximas etapas
[Baixar o StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220).

