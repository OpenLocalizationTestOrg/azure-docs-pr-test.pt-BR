---
title: "Visão geral do Azure StorSimple Virtual Array aaaMicrosoft | Microsoft Docs"
description: "Descreve Olá StorSimple Virtual Array, uma solução de armazenamento integrado que gerencia as tarefas de armazenamento entre uma matriz virtual local e o armazenamento de nuvem do Microsoft Azure."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Introdução toohello matriz Virtual StorSimple
## <a name="overview"></a>Visão geral
Olá Microsoft Azure StorSimple Virtual Array é uma solução de armazenamento integrado que gerencia as tarefas de armazenamento entre uma matriz virtual local em execução em um hipervisor e o armazenamento de nuvem do Microsoft Azure. matriz de saudação virtual é uma solução de servidor iSCSI que elimina muitos dos problemas de saudação e despesas associadas com a proteção de dados e armazenamento corporativo ou um servidor de arquivos eficiente, econômica e fácil de gerenciar. matriz virtual Olá é particularmente adequada para cenários de filiais/escritórios remotos.

Este tópico fornece uma visão geral de matriz virtual Olá - aqui estão alguns outros recursos:

* Para conhecer as práticas recomendadas, confira [Práticas recomendadas da Matriz Virtual do StorSimple](storsimple-ova-best-practices.md).
* Para obter uma visão geral dos dispositivos da série StorSimple 8000 do hello, vá muito[StorSimple série 8000: uma solução de nuvem híbrida](storsimple-overview.md). 
* Para obter informações sobre dispositivos da série Olá StorSimple 5000/7000, vá muito[Ajuda Online do StorSimple](http://onlinehelp.storsimple.com/).

oferece suporte a matriz virtual Olá Olá iSCSI ou o protocolo de bloco de mensagens de servidor (SMB). Ele é executado em sua infraestrutura existente do hipervisor e fornece camadas toohello nuvem, backup na nuvem, restauração rápida, recuperação em nível de item e os recursos de recuperação de desastres.

Olá tabela a seguir resume recursos importantes de saudação do hello matriz Virtual StorSimple.

| Recurso | Matriz Virtual do StorSimple |
| --- | --- |
| Requisitos de instalação |Usa a infraestrutura de virtualização (Hyper-V ou VMware) |
| Disponibilidade |Nó único |
| Capacidade total (incluindo nuvem) |Backup too64 TB de capacidade utilizável por matriz virtual |
| Capacidade local |GB 390 too6.4 TB de capacidade utilizável por virtual array (necessidade tooprovision 500 GB too8 TB de espaço em disco) |
| Protocolos nativos |iSCSI ou SMB |
| RTO (Objetivo de Tempo de Recuperação) |iSCSI: menos de 2 minutos, independentemente do tamanho |
| RPO (Objetivo de Ponto de Recuperação) |Backups diários e backups sob demanda |
| Disposição do armazenamento em camadas |Usa mapeamento toodetermine quais dados devem ser em camadas ou de calor |
| Suporte |Infraestrutura de virtualização com suporte pelo fornecedor de saudação |
| Desempenho |Varia de acordo com a infraestrutura subjacente |
| Mobilidade de dados |Pode restaurar toohello mesmo dispositivo ou no nível de item recovery (servidor de arquivos) |
| Camadas de armazenamento |Armazenamento local de hipervisor e nuvem |
| Tamanho do compartilhamento |Em camadas: backup too20 TB; localmente afixado: até too2 TB |
| Tamanho do volume |Em camadas: TB de too5 de 500 GB; localmente afixado: 50 GB too500 GB |
| Tamanho do volume |Em camadas: backup too5 TB; localmente afixado: até too500 GB |
| Instantâneos |Com controle de falhas |
| Recuperação em nível de item |Sim, os usuários podem fazer restauração de compartilhamentos |

## <a name="why-use-storsimple"></a>Por que usar StorSimple?
StorSimple conecta usuários e servidores de armazenamento de tooAzure em minutos, sem modificação do aplicativo.

Olá tabela a seguir descreve alguns dos principais benefícios de saudação que Olá StorSimple matriz Virtual solução fornece.

| Recurso | Benefício |
| --- | --- |
| Integração transparente |oferece suporte a matriz virtual Olá Olá iSCSI ou o protocolo SMB de saudação. movimentação de dados de saudação entre camadas de local de saudação e nuvem Olá é usuário toohello integrado e transparente. |
| Redução nos custos de armazenamento |Com o StorSimple, você provisionar demandas atuais do suficientes toomeet de local de armazenamento para dados mais acessados hello mais usado. Conforme as necessidades de armazenamento crescem, o StorSimple distribui dados de menor interesse em camadas para um armazenamento em nuvem com bom custo/benefício. Olá dados com eliminação de duplicação e compactados antes de enviar toohello nuvem toofurther reduzir os requisitos de armazenamento e de despesa. |
| Gerenciamento simplificado do armazenamento |StorSimple fornece gerenciamento centralizado na nuvem hello usando o Gerenciador de dispositivos de StorSimple toomanage vários dispositivos. |
| Aprimoramento da recuperação de desastres e conformidade |StorSimple facilita a recuperação de desastres mais rápida restaurando Olá metadados imediatamente e restaurando dados saudação conforme necessário. Isso significa que as operações normais podem continuar com um mínimo de interrupção. |
| Mobilidade de dados |Nuvem toohello em camadas pode ser acessado de outros sites para fins de recuperação e migração de dados. Observe que você pode restaurar dados somente toohello virtual matriz original. No entanto, você pode usar desastres recuperação recursos toorestore Olá matriz virtual inteira tooanother virtual matriz. |

## <a name="storsimple-workload-summary"></a>Resumo de carga de trabalho do StorSimple

Confira abaixo um resumo das cargas de trabalho com suporte do StorSimple.

|Cenário     |Carga de trabalho     |Suportado      |Restrições               |
|-------------|-------------|---------------|---------------------------|
|Colaboração do ROBO |Compartilhamento de arquivos     |Sim      |Consulte [limites máximos para o servidor de arquivos](storsimple-ova-limits.md).<br></br>Confira [requisitos do sistema para as versões suportadas por SMB](storsimple-ova-system-requirements.md).| Todas as versões     |

## <a name="workflows"></a>Fluxos de trabalho
Olá matriz Virtual StorSimple é especialmente adequado para Olá fluxos de trabalho a seguir:

* [Gerenciamento de armazenamento baseado em nuvem](#cloud-based-storage-management)
* [Backup independente de local](#location-independent-backup)
* [Recuperação de desastre e proteção de dados](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>Gerenciamento de armazenamento baseado em nuvem
Você pode usar o serviço do Gerenciador de dispositivos de StorSimple Olá executadas em Olá toomanage portal do Azure dados armazenados em vários dispositivos e em vários locais. Isso é particularmente útil em cenários de filiais distribuídas. Observe que você deve criar instâncias separadas de arrays do Gerenciador de dispositivos do StorSimple serviço toomanage virtuais hello e dispositivos de StorSimple físicos. Observe também que matriz virtual Olá agora usa o novo portal do Azure de saudação em vez da saudação portal clássico do Azure.

![Gerenciamento de armazenamento baseado em nuvem](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Backup independente de local
Matriz de virtual hello, instantâneos de nuvem fornecem uma cópia independente de local point-in-time de um volume ou compartilhamento. Instantâneos de nuvem são habilitados por padrão e não podem ser desabilitados. Todos os volumes e compartilhamentos são backup a saudação mesmo momento por meio de uma única política de backup diária, e você pode executar backups ad hoc adicionais sempre que necessário.

### <a name="data-protection-and-disaster-recovery"></a>Recuperação de desastre e proteção de dados
matriz virtual Olá dá suporte a saudação cenários de recuperação de desastres e proteção de dados a seguir:

* **Restauração de volume ou compartilhamento** – usar a restauração de hello como o novo fluxo de trabalho toorecover um volume ou compartilhamento. Use essa abordagem toorecover Olá todo o volume ou compartilhamento.
* **Recuperação em nível de item** – compartilhamentos permitem acesso simplificado toorecent backups. Você pode facilmente recuperar um arquivo individual de um especial *backup* pasta disponível na nuvem hello. Essa funcionalidade de restauração é controlada pelo usuário e nenhuma intervenção administrativa é necessária.
* **Recuperação de desastres** – Use Olá toorecover do recurso de failover de todos os volumes ou compartilhamentos tooa nova matriz virtual. Criar nova matriz de virtual hello e registrá-lo com hello serviço do Gerenciador de dispositivos do StorSimple e failover matriz virtual original de saudação. nova matriz de virtual Olá assumirá, em seguida, recursos de saudação provisionado. 

## <a name="storsimple-virtual-array-components"></a>Componentes da Matriz Virtual do StorSimple
matriz virtual Olá inclui Olá componentes a seguir:

* [Matriz virtual](#virtual-array) – um dispositivo de armazenamento de nuvem híbrida baseado em uma máquina virtual provisionada em seu ambiente virtualizado ou hipervisor.  
* [Serviço de Gerenciador de dispositivos de StorSimple](#storsimple-device-manager-service) – uma extensão de saudação portal do Azure que permite que você gerencie um ou mais dispositivos de StorSimple de uma única interface da web que você pode acessar de localizações geográficas diferentes. Você pode usar toocreate de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar serviços, exibir e gerenciar dispositivos e alertas e gerenciar volumes, compartilhamentos e instantâneos existentes.
* [Interface do usuário da web local](#local-web-user-interface) – uma interface de usuário baseada na web que é usado tooconfigure Olá para que ele se conectar a rede local toohello e, em seguida, registre o dispositivo de saudação com o serviço do Gerenciador de dispositivos de StorSimple hello. 
* [Interface de linha de comando](#command-line-interface) – uma interface do Windows PowerShell que você pode usar toostart uma sessão de suporte na matriz virtual hello.
  Olá seções a seguir descrevem cada um desses componentes em maiores detalhes e explicam como Olá solução organiza dados, aloca armazenamento e facilita o gerenciamento de armazenamento e proteção de dados.

### <a name="virtual-array"></a>Matriz virtual
matriz virtual Olá é uma solução de armazenamento de nó único que fornece armazenamento primário, gerencia a comunicação com o armazenamento em nuvem e ajuda a segurança de saudação tooensure e confidencialidade de todos os dados armazenados no dispositivo de saudação.

matriz virtual Hello está disponível em um modelo que está disponível para download. matriz virtual Olá tem a capacidade máxima de 6,4 TB no dispositivo de saudação (com um requisito de armazenamento subjacente de 8 TB) e 64 TB incluindo armazenamento em nuvem. 

matriz virtual Olá tem Olá recursos a seguir:

* Tem bom custo/benefício. Usa sua infraestrutura de virtualização existente e pode ser implantada em seu hipervisor Hyper-V ou VMware existente.
* Ele reside no datacenter hello e pode ser configurado como um servidor iSCSI ou um servidor de arquivos. 
* Ele é integrado com a nuvem de saudação.
* Backups são armazenados na nuvem hello, o que pode facilitar a recuperação de desastres e simplificar a recuperação em nível de item (ILR). 
* Você pode aplicar atualizações toohello virtual matriz exatamente como você poderia aplicar dispositivo físico tooa.

> [!NOTE]
> Uma matriz virtual não pode ser expandida. Portanto, é importante tooprovision de armazenamento ao criar matriz virtual hello. 
> 
> 

### <a name="storsimple-device-manager-service"></a>Serviço do Gerenciador de Dispositivos StorSimple
Microsoft Azure StorSimple fornece uma interface de usuário baseada na web, Olá serviço do Gerenciador de dispositivos de StorSimple, que permite que você toocentrally gerenciar o armazenamento do StorSimple. Você pode usar Olá Gerenciador de dispositivos do StorSimple service tooperform Olá tarefas a seguir:

* Gerenciar, de um único serviço, várias Matrizes Virtuais StorSimple. 
* Configurar e gerenciar configurações de segurança para Matrizes Virtuais StorSimple. (Criptografia na nuvem Olá é dependente de APIs do Microsoft Azure.)
* Configurar propriedades e credenciais da conta de armazenamento.
* Configurar e gerenciar volumes ou compartilhamentos.
* Fazer backup e restaurar dados em volumes ou compartilhamentos.
* Monitorar o desempenho.
* Revisar as configurações do sistema e identificar possíveis problemas.

Use o Olá Gerenciador de dispositivos de StorSimple tooperform diário administração do serviço da sua matriz virtual.

Para obter mais informações, vá muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Interface do usuário da Web local
matriz virtual Olá inclui uma interface de usuário baseada na web que é usado para configuração e o registro do dispositivo de saudação com hello serviço do Gerenciador de dispositivos do StorSimple. Você pode usá-lo tooshut para baixo e reinicie matriz virtual hello, execute testes de diagnóstico, atualização de software, alterar a senha de administrador do dispositivo hello, exibir logs do sistema e entre em contato com o Microsoft Support toofile uma solicitação de serviço. 

Para obter informações sobre como usar o hello da interface do usuário baseada na web, ir muito[Use Olá tooadminister de interface do usuário baseada na web a matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Interface de linha de comando
Olá incluído do Windows PowerShell interface permite que você tooinitiate uma sessão de suporte com o Microsoft Support para que eles podem ajudá-lo a solucionar problemas e resolver problemas que podem ser encontrados em sua matriz virtual.

## <a name="storage-management-technologies"></a>Tecnologias de gerenciamento de armazenamento
Além disso, array virtual toohello e outros componentes, Olá StorSimple solução usa Olá seguintes software tecnologias tooprovide acesso rápido tooimportant dados, reduzir o consumo de armazenamento e proteger os dados armazenados em sua matriz virtual:

* [Camadas de armazenamento automático](#automatic-storage-tiering) 
* [Volumes e compartilhamentos fixados localmente](#locally-pinned-shares-and-volumes)
* [Eliminação de duplicação e compactação de dados em camadas ou backup de nuvem toohello](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Backups agendados e sob demanda](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Camadas de armazenamento automático
matriz virtual Olá usa novos camadas mecanismo toomanage armazenado dados em nuvem virtual de matriz e Olá Olá. Há apenas duas camadas: matriz de virtual local hello e o Azure armazenamento em nuvem. Olá matriz Virtual StorSimple organiza automaticamente os dados em níveis de saudação com base em um mapa de calor, que controla os dados atuais de tooother de uso, idade e relações. Os dados que é mais ativas (mais) são armazenadas localmente, enquanto os dados menos ativos e inativos são automaticamente migrados toohello nuvem. (Todos os backups são armazenados na nuvem hello.) O StorSimple ajusta e reorganiza as atribuições de dados e armazenamento conforme os padrões de uso mudam. Por exemplo, algumas informações poderão ficar menos ativas ao longo do tempo. Como ele se torna progressivamente menos ativo, ele é hierárquico out toohello nuvem. Se esses mesmos dados ficarem ativos novamente, ele é hierárquico na matriz de armazenamento toohello.

Dados para um volume ou compartilhamento hierárquico específico garantem seu próprio espaço de camada local. (aproximadamente 10% do espaço total provisionado de saudação do compartilhamento ou volume). Enquanto isso reduz o armazenamento de saudação disponível na matriz de saudação virtual para esse compartilhamento ou volume, ele garante que camadas para um compartilhamento ou volume não serão afetados pelas necessidades de camadas de saudação de outros compartilhamentos ou volumes. Assim, uma carga de trabalho muito ocupada em um compartilhamento ou volume não pode forçar todos os outros nuvem de toohello de cargas de trabalho. 

![Camadas de armazenamento automático](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> Você pode especificar um volume fixado localmente, caso em que dados saudação permanecerá na matriz virtual hello e nunca é hierárquico toohello nuvem. Para obter mais informações, vá muito[localmente afixado compartilhamentos e volumes](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Volumes e compartilhamentos fixados localmente
Você pode criar os compartilhamentos e volumes apropriados como fixados localmente. Esse recurso garante que os dados exigidos por aplicativos críticos permanecem na matriz virtual hello e nunca é hierárquico toohello nuvem. Volumes e compartilhamentos localmente afixados têm Olá recursos a seguir: 

* Eles não são as latências de toocloud assunto ou problemas de conectividade.
* Eles ainda se beneficiam dos recursos de recuperação de desastre e backup em nuvem StorSimple.

Você pode restaurar um compartilhamento ou volume fixado localmente como em camadas, ou então um compartilhamento ou volume em camadas como fixado localmente. 

Para obter mais informações sobre volumes fixados localmente, vá muito[usar Olá Gerenciador de dispositivos do StorSimple service toomanage volumes](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>Eliminação de duplicação e compactação de dados em camadas ou backup de nuvem toohello
Toofurther compactação do StorSimple usa eliminação de duplicação e dados reduzir os requisitos de armazenamento em nuvem hello. Eliminação de duplicação reduz Olá quantidade geral de dados armazenados, eliminando a redundância no conjunto de dados Olá armazenado. Como alterações nas informações, StorSimple ignora dados saudação inalterado e captura Olá somente as alterações. Além disso, o StorSimple reduz a quantidade de saudação dos dados armazenados por identificar e remover informações duplicadas. 

> [!NOTE]
> Os dados armazenados na matriz virtual Olá não estiver com eliminação de duplicação ou compactados. Todos os de eliminação de duplicação e compactação ocorre somente antes de nuvem toohello os dados de saudação são enviados.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Backups agendados e sob demanda
Recursos de proteção de dados StorSimple permitem que você toocreate os backups sob demanda. Além disso, um agendamento padrão garante que o backup dos dados seja realizado diariamente. Backups são feitos na forma de saudação de instantâneos incrementais, que são armazenados na nuvem hello. Instantâneos, que registram apenas as alterações de saudação desde o último backup de hello, podem ser criados e restaurados rapidamente. Esses instantâneos podem ser extremamente importantes em cenários de recuperação de desastres pois substituir os sistemas de armazenamento secundária (como o backup em fita) e permitir toorestore dados tooyour datacenter ou tooalternate sites, se necessário.

## <a name="next-steps"></a>Próximas etapas
Saiba como muito[preparar o portal de matriz virtual Olá](storsimple-virtual-array-deploy1-portal-prep.md).

