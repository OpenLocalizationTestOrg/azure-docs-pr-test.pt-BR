---
title: "aaaStorSimple 8000 séries como destino de backup com Veeam | Microsoft Docs"
description: "Descreve a configuração de destino de backup do StorSimple Olá com Veeam."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a>StorSimple como um destino de backup com o Veeam

## <a name="overview"></a>Visão geral

O Azure StorSimple é uma solução de armazenamento de nuvem híbrida da Microsoft. StorSimple aborda as complexidades de saudação do crescimento exponencial de dados usando uma conta de armazenamento do Azure como uma extensão de dados automaticamente em camadas e solução de local de saudação em armazenamento local e o armazenamento em nuvem.

Neste artigo, abordamos a integração do StorSimple com o Veeam e as práticas recomendadas para a integração de ambas as soluções. Também fazemos recomendações sobre como integrar o tooset backup Veeam toobest com StorSimple. Podemos adiar tooVeeam práticas recomendadas, backup arquitetos e administradores para Olá melhor maneira tooset Veeam toomeet individuais aos requisitos de backup e contratos de nível de serviço (SLAs).

Embora ilustre os principais conceitos e as etapas de configuração, este artigo não é um guia passo a passo de configuração ou instalação. Pressupomos que que infra-estrutura e dos componentes básicos Olá são em funcionamento e toosupport pronto Olá conceitos que descrevemos.

### <a name="who-should-read-this"></a>Quem deve ler isso?

informações de saudação neste artigo serão administradores de toobackup mais úteis, os administradores de armazenamento e arquitetos de armazenamento que ter conhecimento de armazenamento, Windows Server 2012 R2, Ethernet, serviços de nuvem e Veeam.

### <a name="supported-versions"></a>Versões com suporte

-   Veeam 9 e versões posteriores
-   [StorSimple Atualização 3 e versões posteriores](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Por que o StorSimple como um destino de backup?

O StorSimple é uma boa escolha para um destino de backup porque:

-   Ele fornece o local de armazenamento padrão para toouse de aplicativos de backup como um destino de backup rápido, sem qualquer alteração. Você também pode usar o StorSimple para uma restauração rápida de backups recentes.
-   Sua nuvem camadas é totalmente integrada com um toouse de conta de armazenamento de nuvem do Azure econômico armazenamento do Azure.
-   Ele oferece armazenamento externo para recuperação de desastre automaticamente.


## <a name="key-concepts"></a>Principais conceitos

Assim como acontece com qualquer solução de armazenamento, uma avaliação cuidadosa do desempenho do armazenamento da solução hello, SLAs, taxa de alteração e às necessidades de crescimento de capacidade é toosuccess crítico. ideia principal Olá é que introduzindo uma camada de nuvem, sua nuvem toohello tempos de acesso e taxas de transferência papel fundamental na capacidade de saudação do StorSimple toodo seu trabalho.

StorSimple é projetado tooprovide tooapplications de armazenamento que operam em um conjunto de trabalho bem definido de dados (dados quentes). Nesse modelo, conjunto de dados do trabalho de saudação é armazenado nas camadas de local de saudação e hello, conjunto de folga/frio/arquivado restante de dados é nuvem toohello em camadas. Esse modelo é representado na figura a seguir de saudação. linha Hello quase simples verde representa dados de saudação armazenados nas camadas de local de saudação do dispositivo do StorSimple hello. Olá linha vermelha representa a quantidade total Olá dos dados armazenados em Olá solução StorSimple em todas as camadas. espaço Olá entre a linha de saudação simples verde e curva vermelha exponencial de saudação representa a quantidade total de saudação dos dados armazenados na nuvem de saudação.

**Disposição em camadas do StorSimple**
![Diagrama da disposição em camadas do StorSimple](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)

Com essa arquitetura em mente, você encontrará StorSimple é ideal toooperate como um destino de backup. Você pode usar o StorSimple para:

-   Execute seu restaurações mais frequentes do conjunto de trabalho local Olá de dados.
-   Use nuvem Olá para recuperação de desastres externa e os dados mais antigos, em que as restaurações são menos frequentes.

## <a name="storsimple-benefits"></a>Benefícios do StorSimple

StorSimple fornece uma solução local que é totalmente integrada com o Microsoft Azure, aproveitando perfeita acessar tooon local e armazenamento em nuvem.

StorSimple usa camadas automática entre o dispositivo local hello, o que tem um dispositivo de estado sólido (SSD) e serial anexado armazenamento SCSI (SAS) e armazenamento do Azure. Mantém camadas automática local nas camadas SSD e a SAS de saudação de dados acessados com frequência. Ele move dados pouco acessados tooAzure armazenamento.

O StorSimple oferece os seguintes benefícios:

-   Algoritmos de eliminação de duplicação e compactação exclusivos que usam níveis de eliminação de duplicação precedentes Olá nuvem tooachieve
-   Alta disponibilidade
-   Replicação geográfica usando a replicação geográfica do Azure
-   Integração do Azure
-   Criptografia de dados na nuvem Olá
-   Aprimoramento da recuperação de desastres e conformidade

Embora o StorSimple apresente dois cenários de implantação principais (destinos de backup primário e secundário), basicamente, ele é um dispositivo de armazenamento em bloco simples. StorSimple todos Olá eliminação de duplicação e compactação. Ele perfeitamente envia e recupera os dados entre a nuvem hello e aplicativo hello e sistema de arquivos.

Para saber mais sobre o StorSimple, confira [StorSimple série 8000: solução de armazenamento de nuvem híbrida](storsimple-overview.md). Além disso, você pode examinar Olá [especificações técnicas da série StorSimple 8000](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> Há suporte para o uso do dispositivo StorSimple como destino de backup apenas para StorSimple 8000 Atualização 3 e versões posteriores.

## <a name="architecture-overview"></a>Visão geral da arquitetura

Olá, tabelas a seguir mostram diretrizes de arquitetura do modelo de dispositivo de saudação inicial.

**Capacidades do StorSimple de armazenamento local e em nuvem**

| Capacidade de armazenamento | 8100 | 8600 |
|---|---|---|
| Capacidade de armazenamento local | &lt; 10 TiB\*  | &lt; 20 TiB\*  |
| Capacidade de armazenamento em nuvem | &gt;200 TiB\* | &gt;500 TiB\* |

\*O tamanho de armazenamento não assume nenhuma eliminação de duplicação ou compactação.

**Capacidade do StorSimple para backups primários e secundários**

| Cenário de backup  | Capacidade de armazenamento local  | Capacidade de armazenamento em nuvem  |
|---|---|---|
| Backup principal  | Backups recentes armazenados no armazenamento local para o objetivo de ponto de recuperação rápida toomeet recuperação (RPO) | O histórico de backup (RPO) cabe na capacidade da nuvem |
| Backup secundário | Uma cópia secundária dos dados de backup pode ser armazenada na capacidade da nuvem  | N/D  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple como destino de backup principal

Nesse cenário, os volumes StorSimple são apresentados toohello o aplicativo de backup como único repositório Olá para backups. Olá figura a seguir mostra uma arquitetura de solução em que todo o uso de backups StorSimple hierárquico volumes para backups e restaurações.

![StorSimple como um diagrama lógico de destino de backup principal](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Etapas de lógica de backup de destino principal

1.  contatos de servidor de backup Olá Olá agente de backup de destino e o agente de backup Olá transmite o servidor de backup de toohello de dados.
2.  servidor de backup Olá grava dados toohello StorSimple de volumes em camadas.
3.  servidor de backup Olá atualiza o banco de dados de catálogo hello e conclui o trabalho de backup hello.
4.  Um script de instantâneo dispara Olá nuvem Gerenciador de instantâneos StorSimple (início ou exclusão).
5.  servidor de backup Olá exclui backups expirados com base em uma política de retenção.

### <a name="primary-target-restore-logical-steps"></a>Etapas lógicas de restauração de destino principal

1.  servidor de backup Olá inicia a restaurar os dados apropriados do hello do repositório hello.
2.  Agente de backup Olá recebe dados de saudação do servidor de backup hello.
3.  servidor de backup Olá concluirá o trabalho de restauração hello.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple como destino de backup secundário

Nesse cenário, os volumes do StorSimple são usados principalmente para retenção de longo prazo ou arquivamento.

Olá figura a seguir mostra uma arquitetura na qual os backups inicias e restaura o volume de destino de alto desempenho. Esses backups são copiados e arquivado tooa StorSimple hierárquico volume em um agendamento definido.

Ele é importante toosize seu volume de alto desempenho, para que ele possa manipular a seus requisitos de capacidade e desempenho de política retenção.

![StorSimple como um diagrama lógico de destino de backup secundário](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Etapas de lógica de backup de destino secundário

1.  contatos de servidor de backup Olá Olá agente de backup de destino e o agente de backup Olá transmite o servidor de backup de toohello de dados.
2.  servidor de backup Olá grava toohigh desempenho, armazenamento de dados.
3.  servidor de backup Olá atualiza o banco de dados de catálogo hello e conclui o trabalho de backup hello.
4.  Olá tooStorSimple de backups de cópias de backup de servidor com base em uma política de retenção.
5.  Um script de instantâneo dispara Olá nuvem Gerenciador de instantâneos StorSimple (início ou exclusão).
6.  servidor de backup Olá exclui backups expirados com base em uma política de retenção.

### <a name="secondary-target-restore-logical-steps"></a>Etapas lógicas de restauração de destino secundário

1.  servidor de backup Olá inicia a restaurar os dados apropriados do hello do repositório hello.
2.  Agente de backup Olá recebe dados de saudação do servidor de backup hello.
3.  servidor de backup Olá concluirá o trabalho de restauração hello.

## <a name="deploy-hello-solution"></a>Implantar solução Olá

Implantar solução Olá requer três etapas:

1. Prepare a infraestrutura de rede hello.
2. Implante o dispositivo StorSimple como um destino de backup.
3. Implantar Veeam.

Cada etapa é abordada em detalhes nas seções a seguir de saudação.

### <a name="set-up-hello-network"></a>Configurar rede Olá

Como StorSimple é uma solução integrada Olá nuvem do Azure, StorSimple requer uma conexão ativa e em funcionamento de toohello nuvem do Azure. Essa conexão é usada para operações como instantâneos de nuvem, gerenciamento de dados e metadados de transferência e armazenamento em nuvem tooAzure tootier dados mais antigos e menos acessados.

Para Olá solução tooperform ideal, recomendamos que você siga essas práticas recomendadas de rede:

-   link de saudação que se conecta a seu tooAzure camada do StorSimple deve atender aos seus requisitos de largura de banda. Fazer isso aplicando Olá necessário qualidade de serviço (QoS) nível tooyour infraestrutura comutadores toomatch seu RPO e recuperação SLAs RTO (objetivo) de tempo.
-   As latências máximas de acesso ao Armazenamento de Blobs do Azure devem ser cerca de 80 ms.

### <a name="deploy-storsimple"></a>Implantar o StorSimple

Para ver diretrizes passo a passo de implantação do StorSimple, acesse [Implantar seu dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-veeam"></a>Implantar Veeam

Para práticas recomendadas de instalação Veeam, consulte [Veeam Backup e práticas recomendadas de replicação](https://bp.veeam.expert/), e leia o guia do usuário Olá em [Veeam Centro de Ajuda (documentação técnica)](https://www.veeam.com/documentation-guides-datasheets.html).

## <a name="set-up-hello-solution"></a>Configurar a solução de saudação

Nesta seção, demonstraremos alguns exemplos de configuração. Olá exemplos e as recomendações a seguir ilustram implementação mais básicas e fundamental de saudação. Essa implementação pode não se aplicar diretamente tooyour requisitos específicos de backup.

### <a name="set-up-storsimple"></a>Configurar o StorSimple

| Tarefas de implantação do StorSimple  | Comentários adicionais |
|---|---|
| Implantação do seu dispositivo StorSimple local. | Versões com suporte: atualização 3 e versões posteriores. |
| Ative o destino de backup hello. | Use esses comandos tooturn ou desativar o modo de destino de backup e o status de tooget. Para obter mais informações, consulte [se conectar remotamente o dispositivo StorSimple tooa](storsimple-remote-connect.md).</br> tooturn no modo de backup: `Set-HCSBackupApplianceMode -enable`. </br> tooturn desativar o modo de backup: `Set-HCSBackupApplianceMode -disable`. </br> estado atual do hello tooget das configurações do modo de backup: `Get-HCSBackupApplianceMode`. |
| Crie um contêiner de volume comuns para o volume que armazena dados de backup hello. Todos os dados de um contêiner de volume passam por eliminação de duplicação. | Contêineres de volume do StorSimple definem domínios de eliminação de duplicação.  |
| Crie os volumes do StorSimple. | Crie volumes com tamanhos como fechar toohello antecipado uso possível, porque o tamanho do volume afeta o tempo de duração de instantâneo de nuvem. Para obter informações sobre como toosize um volume, leia sobre [políticas de retenção](#retention-policies).</br> </br> Use StorSimple hierárquico volumes e selecione Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção. </br> Não há suporte para usar volumes afixados localmente. |
| Crie uma política de backup StorSimple exclusiva para todos os volumes de destino de backup de saudação. | Uma política de backup StorSimple define o grupo de consistência do volume de saudação. |
| Desabilite o cronograma de saudação instantâneos Olá expirar. | Os instantâneos são disparados como uma operação de pós-processamento. |

### <a name="set-up-hello-host-backup-server-storage"></a>Configurar o armazenamento de backup do servidor de host Olá

Configure o armazenamento de backup do servidor de host de saudação de acordo com as diretrizes de toothese:  

- Não use volumes estendidos (criados pelo Gerenciamento de Disco do Windows). Não há suporte para volumes estendidos.
- Formate os volumes usando o NTFS com tamanho da unidade de alocação de 64 KB.
- Mapear os volumes do StorSimple Olá diretamente o toohello Veeam server.
    - Use o iSCSI para servidores físicos.


## <a name="best-practices-for-storsimple-and-veeam"></a>Práticas recomendadas para StorSimple e Veeam

Configure sua solução de acordo com as diretrizes de toohello Olá algumas seções a seguir.

### <a name="operating-system-best-practices"></a>Práticas recomendadas do sistema operacional

-   Desabilite a criptografia do Windows Server e eliminação de duplicação do sistema de arquivos NTFS hello.
-   Desabilite a desfragmentação do Windows Server em volumes do StorSimple hello.
-   Desabilite a indexação em Olá volumes do StorSimple do Windows Server.
-   Execute uma verificação antivírus no host de origem da saudação (não em volumes do StorSimple Olá).
-   Desativar saudação padrão [manutenção do Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) no Gerenciador de tarefas. Faça isso em uma saudação maneiras a seguir:
    - Desligue o Configurador de manutenção Olá no Agendador de tarefas do Windows.
    - Baixe [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) do Windows Sysinternals. Depois de baixar o PsExec, execute o Windows PowerShell como administrador e digite:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Práticas recomendadas do StorSimple

-   Certifique-se de que esse dispositivo StorSimple de saudação é atualizado muito[Update 3 ou posterior](storsimple-install-update-3.md).
-   Isolar tráfego de iSCSI e de nuvem. Use conexões iSCSI dedicado para o tráfego entre o servidor de backup StorSimple e hello.
-   Verifique se o dispositivo do StorSimple é um destino de backup dedicado. Não há suporte para cargas de trabalho mistas porque elas afetam o RTO e RPO.

### <a name="veeam-best-practices"></a>Práticas recomendadas de Veeam

-   o banco de dados do Hello Veeam deve ser local toohello servidor e não reside em um volume StorSimple.
-   Recuperação de desastres, faça Olá Veeam em um volume StorSimple.
-   Oferecemos suporte a backups completos e incrementais do Veeam para esta solução. É recomendável que você não use backups diferenciais e sintéticos.
-   Arquivos de dados de backup devem conter apenas os dados de saudação de um trabalho específico. Por exemplo, não são permitidos acréscimos de mídia em vários trabalhos diferentes.
-   Desligue a verificação do trabalho. Se necessário, a verificação deve ser agendada após o trabalho de backup mais recente hello. É importante toounderstand esse trabalho afeta sua janela de backup.
-   Desative a pré-alocação de mídia.
-   Verifique se processamento em paralelo está habilitado.
-   Desligue a compactação.
-   Desative a eliminação de duplicação no trabalho de backup hello.
-   Configurar a otimização muito**LAN destino**.
-   Ative **Criar backup ativo completo** (a cada 2 semanas).
-   No repositório de backup hello, configure **usar arquivos de backup por VM**.
-   Definir **usar vários fluxos de carregamento por trabalho** muito**8** (é permitido um máximo de 16). Ajuste esse número para cima ou para baixo com base na utilização de CPU no dispositivo do StorSimple hello.

## <a name="retention-policies"></a>Políticas de retenção

Um dos tipos de política de retenção de backup mais comuns Olá é uma diretiva avô, pai e filho (GFS). Em uma política GFS, um backup incremental é executado diariamente e backups completos são realizados semanalmente e mensalmente. Essa política resulta em seis StorSimple de volumes em camadas: um volume contém Olá semanais, mensais e anuais backups completos; Olá, outros cinco volumes armazenam backups incrementais diariamente.

Saudação de exemplo a seguir, usamos uma rotação GFS. exemplo Hello presume o seguinte hello:

-   Serão usados dados compactados ou com eliminação de duplicação.
-   Os backups completos têm 1 TiB cada.
-   Backups incrementais diários têm 500 GiB cada.
-   Quatro backups semanais são mantidos por um mês.
-   Doze backups mensais mantidos por um ano.
-   Um backup anual é mantido por 10 anos.

Com base em Olá anterior suposições, criar um TiB 26 StorSimple de volume em backups de total mensal e anual Olá em camadas. Criar um TiB 5 volume em camadas de StorSimple para cada um dos backups diários incrementais de saudação.

| Retenção de tipo de backup | Tamanho (TiB) | Multiplicador GFS\* | Capacidade total (TiB)  |
|---|---|---|---|
| Completo semanal | 1 | 4  | 4 |
| Incremental diário | 0,5 | 20 (ciclos, igual ao número de semanas por mês) | 12 (2 para a cota adicional) |
| Mensal completo | 1 | 12 | 12 |
| Anual completo | 1  | 10 | 10 |
| Requisito de GFS |   | 38 |   |
| Cota adicional  | 4  |   | Requisito total de GFS 42  |
\*Hello, multiplicador GFS é Olá número de cópias necessárias tooprotect e reter toomeet seus requisitos de política de backup.

## <a name="set-up-veeam-storage"></a>Configurar o armazenamento de Veeam

### <a name="tooset-up-veeam-storage"></a>tooset Veeam armazenamento

1.  No console de replicação e Olá Veeam Backup em **repositório ferramentas**, ir muito**infra-estrutura de Backup**. Clique com o botão direito do mouse em **Repositórios de Backup** e selecione **Adicionar Repositório de Backup**.

    ![Console de gerenciamento do Veeam, página de repositório de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  Em Olá **novo repositório de Backup** caixa de diálogo, digite um nome e uma descrição para o repositório de saudação. Selecione **Avançar**.

    ![Console de gerenciamento do Veeam, página de nome e descrição](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  Para o tipo de saudação, selecione **do Microsoft Windows server**. Selecione o servidor de Veeam de saudação. Selecione **Avançar**.

    ![Console de gerenciamento Veeam, selecione o tipo de repositório de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  toospecify **local**, navegue e selecione o volume de saudação. Selecione Olá **limite máximo de tarefas simultâneo para:** caixa de seleção e conjunto Olá valor muito**4**. Isso garante que somente quatro discos virtuais serão processados simultaneamente enquanto cada VM (máquina virtual) é processada. Selecione Olá **avançado** botão.

    ![Console de gerenciamento Veeam, selecione o volume](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  Em Olá **as configurações de compatibilidade do armazenamento** caixa de diálogo, selecione Olá **usar arquivos de backup por VM** caixa de seleção.

    ![Console de gerenciamento Veeam, configurações de compatibilidade do armazenamento](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  Em Olá **novo repositório de Backup** caixa de diálogo, selecione Olá **habilitar serviços NFS vPower no servidor de montagem hello (recomendado)** caixa de seleção. Selecione **Avançar**.

    ![Console de gerenciamento do Veeam, página de repositório de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  Examine as configurações de saudação e, em seguida, selecione **próximo**.

    ![Console de gerenciamento do Veeam, página de repositório de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    Um repositório é adicionado toohello Veeam server.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurar o StorSimple como destino de backup principal

> [!IMPORTANT]
> Restauração de dados de um backup que tenha sido nuvem em camadas toohello ocorre em velocidades de nuvem.

Hello figura a seguir mostra o hello mapeamento de um trabalho de backup do volume típico tooa. Nesse caso, todos os backups semanais de saudação mapeiam toohello sábado total do disco, e os backups incrementais Olá mapeiam discos incremental tooMonday-sexta-feira. Olá a todos os backups e restaurações de um StorSimple hierárquico de volume.

![Diagrama lógico de configuração de destino de backup principal](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemplo de agendamento do StorSimple destino de backup principal GFS

Veja esta exemplo de uma agenda de rotação GFS de quatro semanas, mensal e anual:

| Frequência/tipo de backup | Completo | Incremental (1 a 5 dias)  |   
|---|---|---|
| Semanal (1 a 4 semanas) | Sábado | Segunda a sexta-feira |
| Mensal  | Sábado  |   |
| Anual | Sábado  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a>Atribuir o trabalho de backup do StorSimple volumes tooa Veeam

Para o cenário de destino principal de backup, crie um trabalho diário com seu volume StorSimple do Veeam primário. Para um cenário de destino de backup secundário, crie um trabalho diário usando o DAS (Armazenamento Anexado Direto), NAS (Armazenamento Anexado à Rede) ou JBOD (Apenas um Monte de Discos).

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a>tooassign StorSimple volumes tooa Veeam trabalho de backup

1.  No console de replicação e Olá Veeam Backup, selecione **Backup e replicação**. Clique com botão direito do mouse em **Backup** e selecione **VMware** ou **Hyper-V** de acordo com seu ambiente.

    ![Console de gerenciamento do Veeam, trabalho de novo backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  Em Olá **novo trabalho de Backup** caixa de diálogo, digite um nome e uma descrição para o trabalho de backup diário hello.

    ![Console de gerenciamento do Veeam, página novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  Selecione até tooback uma máquina virtual.

    ![Console de gerenciamento do Veeam, página novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  Selecione valores hello desejados para **Backup proxy** e **repositório de Backup**. Selecione um valor para **tookeep os pontos de restauração no disco** de acordo com toohello definições de RPO e RTO para seu ambiente no local de armazenamento conectado. Selecione **Avançado**.

    ![Console de gerenciamento do Veeam, página novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. Em Olá **configurações avançadas** caixa de diálogo Olá **Backup** guia, selecione **Incremental**. Certifique-se de que Olá **criar backups completos sintéticos periodicamente** caixa de seleção é desmarcada. Selecione Olá **criar backups completos active periodicamente** caixa de seleção. Em **backup completo Active**, selecione Olá **semanalmente nos dias selecionados** caixa de seleção para sábado.

    ![Console de gerenciamento do Veeam, página de configurações avançadas de novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. Em Olá **armazenamento** guia, certifique-se de que Olá **habilitar a eliminação de duplicação de dados embutidos** caixa de seleção é desmarcada. Selecione Olá **blocos de arquivo de permuta de exclusão** caixa de seleção e selecione Olá **excluir excluído blocos de arquivo** caixa de seleção. Definir **nível de compactação** muito**nenhum**. Desempenho equilibrado e eliminação de duplicação, defina **otimização de armazenamento** muito**destino LAN**. Selecione **OK**.

    ![Console de gerenciamento do Veeam, página de configurações avançadas de novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    Para obter detalhes sobre as configurações de eliminação de duplicação e compactação do Veeam, consulte [Compactação de Dados e Eliminação de Duplicação](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).

7.  Em Olá **editar trabalho de Backup** caixa de diálogo, você pode selecionar Olá **habilitar o processamento de reconhecimento de aplicativos** caixa de seleção (opcional).

    ![Console de gerenciamento do Veeam, página de processamento convidado de novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  Definir Olá agenda toorun uma vez por dia, em um momento em que você pode especificar.

    ![Console de gerenciamento do Veeam, página agendar novo trabalho de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurar o StorSimple como destino de backup secundário

> [!NOTE]
> Restaurações de dados de um backup que tenha sido nuvem em camadas toohello ocorrerem em velocidades de nuvem.

Nesse modelo, você deve ter uma tooserve de mídia (além de StorSimple) de armazenamento como um cache temporário. Por exemplo, você pode usar uma matriz redundante de discos independentes (RAID) um volume tooaccommodate espaço, entrada/saída (e/s) e largura de banda. Recomendamos o uso de RAID 5, 50 e 10.

Olá figura a seguir mostra típico volumes de local (toohello server) de retenção curto prazo e longo prazo volumes de arquivamento de retenção. Nesse cenário, todos os backups executado no local hello (toohello server) volume RAID. Esses backups são periodicamente duplicados e arquivados tooan volume de arquivamento. Ele é importante toosize local (servidor toohello) RAID volume para que ele possa manipular a seus requisitos de capacidade e desempenho de retenção curto prazo.

![StorSimple como diagrama lógico de destino de backup secundário](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple como um exemplo GFS de destino de backup secundário

Olá seguinte tabela mostra como tooset backup toorun backups em discos do StorSimple e local de saudação. Ele inclui os requisitos de capacidade total e individuais.

| Tipo de backup e retenção | Armazenamento configurado | Tamanho (TiB) | Multiplicador GFS | Capacidade total\* (TiB) |
|---|---|---|---|---|
| Semana 1 (completa e incremental) |Disco local (curto prazo)| 1 | 1 | 1 |
| StorSimple semanas 2 a 4 |Disco StorSimple (longo prazo) | 1 | 4 | 4 |
| Mensal completo |Disco StorSimple (longo prazo) | 1 | 12 | 12 |
| Anual completo |Disco StorSimple (longo prazo) | 1 | 1 | 1 |
|Requisito de tamanho de volumes do GFS |  |  |  | 18*|
A capacidade total do \* inclui 17 TiB de discos do StorSimple e 1 TiB de volume RAID local.


### <a name="gfs-example-schedule"></a>Exemplo de agenda do GFS

Agenda semanal, mensal e anual da rotação do GFS

| Semana | Completo | Incremental dia 1 | Incremental dia 2 | Incremental dia 3 | Incremental dia 4 | Incremental dia 5 |
|---|---|---|---|---|---|---|
| Semana 1 | Volume RAID local  | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local |
| Semana 2 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Semana 3 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Semana 4 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Mensal | StorSimple mensal |   |   |   |   |   |
| Anual | StorSimple anual  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a>Atribuir o trabalho de cópia do StorSimple volumes tooa Veeam

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a>trabalho de cópia tooassign StorSimple volumes tooa Veeam

1.  No console de replicação e Olá Veeam Backup, selecione **Backup e replicação**. Clique com botão direito do mouse em **Backup** e selecione **VMware** ou **Hyper-V** de acordo com seu ambiente.

    ![Console de gerenciamento Veeam, página de trabalho de nova cópia de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  Em Olá **novo trabalho de cópia de Backup** caixa de diálogo, digite um nome e uma descrição para o trabalho de saudação.

    ![Console de gerenciamento Veeam, página de trabalho de nova cópia de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  Selecione VMs Olá deseja tooprocess. Selecione de backups e selecione Olá backup diário que você criou anteriormente.

    ![Console de gerenciamento Veeam, página de trabalho de nova cópia de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  Exclua objetos de trabalho de cópia de backup hello, se necessário.

5.  Selecione o repositório de backup e definir um valor para **tookeep os pontos de restauração**. Ser Olá-se de tooselect **a seguir Olá manter pontos de restauração para fins de arquivamento** caixa de seleção. Definir a frequência de backup hello e, em seguida, selecione **avançado**.

    ![Console de gerenciamento Veeam, página de trabalho de nova cópia de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  Especifique as configurações avançadas do seguinte hello:

    * Em Olá **manutenção** guia, desative a proteção de nível corrupção do armazenamento.

    ![Console de gerenciamento do Veeam, página de configurações avançadas de novo trabalho de cópia de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * Em Olá **armazenamento** guia, certifique-se de que a eliminação de duplicação e compactação estão desativados.

    ![Console de gerenciamento do Veeam, página de configurações avançadas de novo trabalho de cópia de backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  Especifica que a transferência de dados de saudação é direta.

8.  Definir Olá agenda de janela de cópia de backup de acordo com as necessidades de tooyour e, em seguida, conclua o Assistente de saudação.

Para obter mais informações, consulte [Criar trabalhos de cópia de backup](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).

## <a name="storsimple-cloud-snapshots"></a>Instantâneos de nuvem do StorSimple

Instantâneos de nuvem do StorSimple protegem os dados de saudação que reside em seu dispositivo StorSimple. Criando um instantâneo de nuvem é instalação do tooshipping equivalente fitas de backup local tooan externa. Se você usar o armazenamento com redundância geográfica do Azure, criando um instantâneo de nuvem é equivalente tooshipping sites de toomultiple de fitas de backup. Se você precisar toorestore um dispositivo depois de um desastre, você pode colocar outro dispositivo StorSimple e execute um failover. Após o failover hello, seria tooaccess capaz de dados de Olá (em velocidades de nuvem) do instantâneo em nuvem hello mais recente.

Olá seção a seguir descreve como toocreate toostart um script curto e delete StorSimple instantâneos em nuvem durante o pós-processamento de backup.

> [!NOTE]
> Instantâneos são criados de forma manual ou por meio de programação não execute política de expiração de instantâneo StorSimple hello. Esses instantâneos devem ser excluídos manual ou programaticamente.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Iniciar e excluir instantâneos de nuvem usando um script

> [!NOTE]
> Avalie cuidadosamente repercussões de retenção de dados e a conformidade de saudação antes de excluir um instantâneo do StorSimple. Para obter mais informações sobre como toorun um script pós-backup, consulte a documentação de Veeam hello.


### <a name="backup-lifecycle"></a>Ciclo de vida de backup

![Diagrama de ciclo de vida de backup](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a>Requisitos

-   servidor de saudação que executa o script hello deve ter recursos de nuvem tooAzure acesso.
-   conta de usuário de saudação deve ter as permissões necessárias hello.
-   Uma política de backup StorSimple com hello associados StorSimple volumes devem ser configurados, mas não ativados.
-   Você precisará Olá nome de recurso de StorSimple, chave de registro, nome do dispositivo e ID de política de backup.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart ou excluir um instantâneo de nuvem

1. [Instale o Azure PowerShell](/powershell/azure/overview).
2. [Baixar e importar informações de assinatura e configurações de publicação](https://msdn.microsoft.com/library/dn385850.aspx).
3. No hello portal clássico do Azure, obter o nome do recurso hello e [chave de registro para o serviço StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4. No servidor de saudação que executa o script hello, execute o PowerShell como administrador. Digite este comando:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    ID da política de backup Olá nota.
5. No bloco de notas, crie um novo script do PowerShell usando Olá código a seguir.

    Copie e cole este trecho de código:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
6. backup de tooyour tooadd Olá script de trabalho, edite seu trabalho Veeam opções avançadas.

    ![Guia de scripts de configurações avançadas de backup Veeam](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

É recomendável que você execute sua política de backup de instantâneo do StorSimple nuvem como um script de pós-processamento final de saudação do seu trabalho de backup diário. Para obter mais informações sobre como tooback backup e restauração toohelp de ambiente seu aplicativo de backup você atingir seu RPO e RTO, consulte com o arquiteto de backup.

## <a name="storsimple-as-a-restore-source"></a>StorSimple como origem de restauração

As restaurações de um dispositivo StorSimple funcionam como qualquer dispositivo de armazenamento em bloco. Restaurações de dados hierárquico toohello nuvem ocorre em velocidades de nuvem. Para dados locais, restaurações ocorrem na velocidade do disco local de saudação do dispositivo de saudação.

Para obter recuperação rápida, granular de nível de arquivo por meio de StorSimple com Veeam, por meio de exibições de Gerenciador interna Olá no console de Veeam hello. Use os pesquisadores Veeam toorecover itens individuais, como mensagens de email, objetos do Active Directory e itens do SharePoint de backups. recuperação Olá pode ser feita sem interrupção do VM no local. Você também pode realizar uma recuperação pontual para bancos de dados do Banco de Dados SQL do Azure e Oracle. Veeam e StorSimple tornam o processo de saudação de recuperação em nível de item do Azure rápida e fácil. Para obter informações sobre como tooperform uma restauração, consulte a documentação de Veeam hello:

- Para [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)
- Para [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)
- Para [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)
- Para [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)
- Para [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)


## <a name="storsimple-failover-and-disaster-recovery"></a>Failover e recuperação de desastre do StorSimple

> [!NOTE]
> Para cenários de destino de backup, o StorSimple Cloud Appliance não tem suporte como um destino de restauração.

Um desastre pode ser causado por uma variedade de fatores. Olá, a tabela a seguir lista cenários comuns de recuperação de desastres.

| Cenário | Impacto | Como toorecover | Observações |
|---|---|---|---|
| Falha do dispositivo StorSimple | As operações de backup e restauração foram interrompidas. | Substitua o dispositivo com falha hello e executar [StorSimple failover e recuperação de desastres](storsimple-device-failover-disaster-recovery.md). | Se você precisar tooperform uma restauração após a recuperação do dispositivo, os conjuntos de trabalho de dados completos são recuperados do hello nuvem toohello novo dispositivo. Todas as operações ocorrem em velocidades de nuvem. índice de saudação e verificar novamente o processo de catálogo podem causar todos os toobe de conjuntos de backup verificado e realizou Olá camada toohello dispositivo local da camada de nuvem, que pode ser um processo demorado. |
| Falha do servidor Veeam | As operações de backup e restauração foram interrompidas. | Recriar o servidor de backup hello e executar a restauração de banco de dados, conforme detalhado no [Veeam Centro de Ajuda (documentação técnica)](https://www.veeam.com/documentation-guides-datasheets.html).  | Você deve recriar ou restaurar Olá Veeam servidor no local de recuperação de desastres hello. Restaure ponto mais recente do toohello Olá banco de dados. Se hello banco de dados restaurado Veeam não está em sincronizado com os trabalhos de backup mais recentes, indexação e catalogação serão necessária. Esse índice e verificar novamente o processo de catálogo podem causar todos os toobe de conjuntos de backup verificado e realizou Olá camada toohello dispositivo local da camada de nuvem. Isso torna tudo ainda mais demorado. |
| Falha do site que resulta na perda de saudação do servidor de backup hello e StorSimple | As operações de backup e restauração foram interrompidas. | Restaure o StorSimple primeiro e depois o Veeam. | Restaure o StorSimple primeiro e depois o Veeam. Se você precisar tooperform uma restauração após a recuperação do dispositivo, Olá conjuntos de trabalho de dados completos são recuperados do hello nuvem toohello novo dispositivo. Todas as operações ocorrem em velocidades de nuvem. |


## <a name="references"></a>Referências

Olá documentos a seguir foram referenciado para este artigo:

- [Configuração de Multipath I/O de StorSimple](storsimple-configure-mpio-windows-server.md)
- [Cenários de armazenamento: provisionamento dinâmico](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Usando unidades GPT](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurar cópias de sombra para pastas compartilhadas](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre como muito[restauração a partir de um conjunto de backup](storsimple-restore-from-backup-set-u2.md).
- Saiba mais sobre como tooperform [dispositivo failover e recuperação de desastres](storsimple-device-failover-disaster-recovery.md).
