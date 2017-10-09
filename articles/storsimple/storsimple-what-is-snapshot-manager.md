---
title: "aaaWhat é StorSimple Snapshot Manager? | Microsoft Docs"
description: "Descreve Olá StorSimple Snapshot Manager, sua arquitetura e seus recursos."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Um Gerenciador de instantâneos de tooStorSimple de Introdução

## <a name="overview"></a>Visão geral
O StorSimple Snapshot Manager é um snap-in do Microsoft Management Console (MMC) que simplifica a proteção de dados e o gerenciamento de backup em um ambiente Microsoft Azure StorSimple. Com o Gerenciador de instantâneos do StorSimple, você pode gerenciar dados do Microsoft Azure StorSimple no Centro de dados hello e na nuvem Olá como uma solução única de armazenamento integrado, assim, simplificar os processos de backup e reduzindo os custos.

Esta visão geral apresenta Olá StorSimple Snapshot Manager, descreve seus recursos e explica sua função no Microsoft Azure StorSimple. 

Para obter uma visão geral do sistema Microsoft Azure StorSimple inteira de hello, incluindo o dispositivo StorSimple hello, o serviço StorSimple Manager, Gerenciador de instantâneos do StorSimple e adaptador StorSimple para SharePoint, consulte [StorSimple série 8000: uma nuvem híbrida solução de armazenamento](storsimple-overview.md). 

> [!NOTE]
> * Você não pode usar toomanage StorSimple Snapshot Manager Microsoft Azure StorSimple Virtual Arrays da (também conhecido como StorSimple local dispositivos virtuais).
> * Se você planejar tooinstall StorSimple atualização 2 em seu dispositivo StorSimple, ser se toodownload Olá versão mais recente do StorSimple Snapshot Manager e instalá-lo **antes de instalar a atualização 2 do StorSimple**. versão mais recente de saudação do StorSimple Snapshot Manager é compatível com versões anteriores e funciona com todas as versões do Microsoft Azure StorSimple. Se você estiver usando a versão anterior de saudação do StorSimple Snapshot Manager, você precisará tooupdate it (você não é necessário versão anterior do toouninstall Olá antes de instalar a nova versão de hello).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Arquitetura e finalidade do StorSimple Snapshot Manager
Gerenciador de instantâneos StorSimple fornece um console de gerenciamento central que você pode usar toocreate consistente, cópias de backup point-in-time do local e nuvem dados. Por exemplo, você pode usar o console de saudação para:

* Configurar, fazer backup e excluir volumes.
* Configurar o volume tooensure grupos que o backup dos dados é consistente com o aplicativo.
* Gerencie políticas de backup para que os dados sejam copiados em um agendamento predeterminado.
* Criar um local e na nuvem, que podem ser armazenados na nuvem hello e usado para recuperação de desastres.

Olá StorSimple Snapshot Manager busca lista Olá de aplicativos registrados com o provedor VSS Olá no host de saudação. Em seguida, toocreate de backups consistentes com aplicativos, ele verifica volumes Olá usado por um aplicativo e sugere tooconfigure de grupos de volume. Gerenciador de instantâneos do StorSimple usa essas cópias de backup de toogenerate grupos do volume são consistentes com o aplicativo. (A consistência do aplicativo existe quando todos os arquivos relacionados e bancos de dados são sincronizados e representam o estado real de saudação do aplicativo hello em um ponto específico no tempo.) 

Gerenciador de instantâneos StorSimple backups assumem a forma de saudação de instantâneos incrementais, que capturam apenas as alterações de saudação desde o último backup de saudação. Como resultado, os backups exigem menos armazenamento e podem ser criados e restaurados rapidamente. Gerenciador de instantâneos do StorSimple usa Olá Windows Volume Shadow Copy Service (VSS) tooensure que os instantâneos capturem dados coerentes com o aplicativo. (Para obter mais informações, vá toohello integração com a seção do serviço de cópias de sombra de Volume do Windows.) Com o StorSimple Snapshot Manager, você pode criar agendamentos de backup ou fazer backups imediatos, conforme necessário. Se você precisar toorestore dados de um backup, permite de Gerenciador de instantâneos StorSimple que você selecionar um catálogo de locais ou instantâneos de nuvem. StorSimple do Azure restaura apenas Olá dados necessários conforme a necessidade, que evita atrasos na disponibilidade de dados durante operações de restauração).

![Arquitetura do StorSimple Snapshot Manager](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Arquitetura do StorSimple Snapshot Manager** 

## <a name="support-for-multiple-volume-types"></a>Suporte para vários tipos de volume
Você pode usar o hello tooconfigure Gerenciador de instantâneos do StorSimple e backup Olá seguintes tipos de volumes: 

* **Volumes básicos** – Um volume básico é uma única partição em um disco básico. 
* **Volumes simples** – Um volume simples é um volume dinâmico que contém espaço em disco de um único disco dinâmico. Um volume simples consiste em uma única região em um disco ou Olá de várias regiões vinculadas no mesmo disco. (Você pode criar volumes simples somente em discos dinâmicos). Volumes simples não são tolerantes a falhas.
* **Volumes dinâmicos** – Um volume dinâmico é um volume criado em um disco dinâmico. Os discos dinâmicos usam informações de tootrack um banco de dados sobre os volumes que estão contidos em discos dinâmicos em um computador. 
* **Volumes dinâmicos com espelhamento** – volumes dinâmicos com espelhamento são construídos na arquitetura de saudação RAID 1. Com o RAID 1, dados idênticos são gravados em dois ou mais discos, produzindo um conjunto espelhado. Uma solicitação de leitura pode ser tratada por qualquer disco que contém Olá dados solicitados.
* **Volumes compartilhados de cluster** – com volumes compartilhados de cluster (CSVs), vários nós em um cluster de failover ao mesmo tempo podem ler ou gravar toohello mesmo disco. Failover de nó de tooanother um nó pode ocorrer rapidamente, sem a necessidade de uma alteração na propriedade da unidade ou montagem, desmontagem e remoção de um volume. 

> [!IMPORTANT]
> Não misture os CSVs e não CSVs no hello mesmo instantâneo. Não há suporte para a combinação de CSVs e não CSVs em um instantâneo. 
> 
> 

Você pode usar grupos de todo o volume do Gerenciador de instantâneos StorSimple toorestore ou clonar volumes individuais e recuperar arquivos individuais.

* [Grupos de volumes e volumes](#volumes-and-volume-groups) 
* [Tipos de backup e políticas de backup](#backup-types-and-backup-policies) 

Para obter mais informações sobre os recursos do Gerenciador de instantâneos StorSimple e como toouse-los, consulte [interface de usuário do Gerenciador de instantâneos StorSimple](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Grupos de volumes e volumes
Com o StorSimple Snapshot Manager, você cria volumes e em seguida os configura em grupos de volumes. 

Gerenciador de instantâneos do StorSimple usa volume grupos toocreate cópias de backup consistentes com o aplicativo. Consistência do aplicativo existe quando todos os arquivos relacionados e bancos de dados são sincronizados e representam Olá o estado real de um aplicativo em um ponto específico no tempo. Grupos de volumes (que também são conhecidas como *grupos de consistência*) formam a base de saudação de um backup ou restauração.

Grupos de volume não são Olá igual a contêineres de volume. Um contêiner de volume contém um ou mais volumes que compartilham uma conta de armazenamento em nuvem e outros atributos, como o consumo de largura de banda e criptografia. Um contêiner de volume único pode conter volumes do StorSimple too256 escassamente provisionado. Para obter mais informações sobre contêineres de volume, vá muito[gerenciar seus contêineres de volume](storsimple-manage-volume-containers.md). Grupos de volumes são conjuntos de volumes que você configure toofacilitate as operações de backup. Se você selecionar dois volumes que pertencem a contêineres de volume toodifferent, colocá-los em um único grupo de volumes e, em seguida, criar uma política de backup para esse grupo de volume, cada volume será feito no contêiner de volume apropriado hello, usando o armazenamento adequado Olá conta.

> [!NOTE]
> Todos os volumes em um grupo de volumes devem vir de um único provedor de serviço de nuvem.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integração com o Serviço de Cópias de Sombra de Volume do Windows
Gerenciador de instantâneos do StorSimple usa Olá dados consistentes com aplicativos do Windows Volume Shadow Copy Service (VSS) toocapture. VSS facilita a consistência do aplicativo, comunicando-se com reconhecimento de VSS aplicativos toocoordinate Olá a criação de instantâneos incrementais. VSS garante que os aplicativos de saudação estejam temporariamente inativos ou inativo, quando os instantâneos são realizados. 

implementação do Gerenciador de instantâneos StorSimple de saudação do VSS funciona com o SQL Server e volumes NTFS genéricos. processo de saudação é o seguinte: 

1. Um solicitante, que é geralmente um gerenciamento de dados e solução de proteção (como o StorSimple Snapshot Manager) ou um aplicativo de backup, invoca o VSS e pede que ele toogather informações do software de gravador Olá no aplicativo de destino hello.
2. Contatos VSS Olá gravador componente tooretrieve uma descrição dos dados de saudação. Gravador de saudação retorna a descrição de saudação do hello dados toobe backup. 
3. O VSS sinaliza o aplicativo de saudação do hello gravador tooprepare para backup. Gravador de saudação prepara os dados de saudação para backup ao concluir transações abertas, atualizar logs de transações e assim por diante e notifica o VSS.
4. O VSS instrui o gravador de saudação tootemporarily parar Olá dados de aplicativo armazenam e certifique-se de que nenhum dado seja gravado toohello volume enquanto a cópia de sombra de saudação é criada. Essa etapa garante a consistência de dados e não passa de 60 segundos.
5. O VSS instrui a cópia de sombra Olá provedor toocreate hello. Provedores, que podem se basear em software ou hardware-, gerenciar volumes Olá que estão atualmente em execução e criam cópias de sombra neles sob demanda. Olá provedor cria cópias de sombra de saudação e notifica o VSS quando ele for concluído.
6. VSS contatos Olá gravador toonotify aplicativo hello que pode retomar a e/s e também tooconfirm que a e/s foi pausada com êxito durante a sombra copiar criação. 
7. Se Olá cópia teve êxito, o VSS retorna Olá solicitante de toohello de local da cópia. 
8. Se os dados foram gravados enquanto a cópia de sombra Olá foi criada, backup Olá será inconsistente. O VSS exclui a cópia de sombra de saudação e notifica o solicitante hello. Olá solicitante pode repetir o processo de backup Olá automaticamente ou notificar Olá administrador tooretry-lo mais tarde.

Consulte Olá ilustração a seguir.

![Processo de VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Processo do Serviço de Cópias de Sombra de Volume do Windows** 

## <a name="backup-types-and-backup-policies"></a>Tipos de backup e políticas de backup
Com o Gerenciador de instantâneos do StorSimple, você pode fazer backup de dados e armazená-lo localmente e na nuvem de saudação. Você pode usar o Gerenciador de instantâneos StorSimple tooback os dados imediatamente, ou você pode usar uma política de backup de toocreate um agendamento para fazer backups automaticamente. Políticas de backup também permitem que você toospecify quantos instantâneos serão retidos. 

### <a name="backup-types"></a>Tipos de backup
Você pode usar o hello toocreate StorSimple Snapshot Manager tipos de backups a seguir:

* **Os instantâneos locais** – instantâneos locais são cópias point-in-time de dados de volume que estão armazenados no dispositivo do StorSimple hello. Normalmente, esse tipo de backup pode ser criado e restaurado rapidamente. Você pode usar um instantâneo local como faria com uma cópia de backup local.
* **Instantâneos na nuvem** – instantâneos na nuvem são cópias point-in-time de dados de volume que estão armazenados na nuvem hello. Um instantâneo de nuvem é equivalente instantâneo tooa replicado em um sistema de armazenamento externo, diferentes. Instantâneos de nuvem são particularmente úteis em cenários de recuperação de desastres.

### <a name="on-demand-and-scheduled-backups"></a>Backups agendados e sob demanda
Com o Gerenciador de instantâneos do StorSimple, você pode iniciar uma única toobe backup criado imediatamente, ou você pode usar um tooschedule de política de backup recorrente operações de backup.

Uma política de backup é um conjunto de regras automatizadas que você pode usar backups regulares de tooschedule. Uma política de backup permite que você toodefine Olá frequência e os parâmetros para a criação de instantâneos de um grupo de volume específico. Você pode usar as datas de início e vencimento de toospecify políticas, horários, frequências e requisitos de retenção, para locais e na nuvem. Uma política é aplicada imediatamente após você defini-la. 

Você pode usar o Gerenciador de instantâneos StorSimple tooconfigure ou reconfigurar as políticas de backup sempre que necessário. 

Configurar Olá informações para cada política de backup que você criar a seguir:

* **Nome** – nome exclusivo Olá Olá selecionado a política de backup.
* **Tipo** – Olá tipo de política de backup; instantâneo local ou instantâneo em nuvem.
* **Grupo de volume** – Olá volume grupo toowhich Olá selecionado política de backup é atribuída.
* **Retenção** – Olá o número de cópias de backup tooretain. Se você verificar Olá **todos os** caixa, todas as cópias de backup são retidas até que Olá o número máximo de cópias de backup por volume for alcançado, no qual Olá ponto política falhará e gerar uma mensagem de erro. Como alternativa, você pode especificar um número de backups tooretain (entre 1 e 64).
* **Data** – date de hello quando a política de backup Olá foi criada.

Para obter informações sobre como configurar políticas de backup, vá muito[toocreate Use o Gerenciador de instantâneo StorSimple e gerenciar políticas de backup](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Gerenciamento e monitoramento do trabalho de backup
Você pode usar o hello toomonitor Gerenciador de instantâneos do StorSimple e gerenciar trabalhos de backup futuros, agendados e concluídos. Além disso, o Gerenciador de instantâneos StorSimple fornece um catálogo de backups too64 concluída. Você pode usar o hello catálogo toofind e restaurar volumes ou arquivos individuais. 

Para obter informações sobre como monitorar trabalhos de backup, vá muito[tooview Use o Gerenciador de instantâneo StorSimple e gerenciar trabalhos de backup](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [usando o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Baixe o [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220).

