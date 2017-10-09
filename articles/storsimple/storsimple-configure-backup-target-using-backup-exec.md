---
title: "aaaStorSimple 8000 séries como destino de backup com Backup Exec | Microsoft Docs"
description: "Descreve a configuração de destino de backup de StorSimple Olá com Veritas Backup Exec."
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
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a>O StorSimple como destino de backup com o Backup Exec

## <a name="overview"></a>Visão geral

O Azure StorSimple é uma solução de armazenamento de nuvem híbrida da Microsoft. StorSimple aborda as complexidades de saudação do crescimento exponencial de dados usando uma conta de armazenamento do Azure como uma extensão de Olá local solução e colocar automaticamente dados em armazenamento local e o armazenamento em nuvem.

Neste artigo, abordamos a integração do StorSimple com o Veritas Backup Exec e as práticas recomendadas para a integração de ambas as soluções. Também fazemos recomendações sobre como integrar o tooset o Backup Exec toobest com StorSimple. Podemos adiar tooVeritas práticas recomendadas, backup arquitetos e administradores para Olá melhor maneira tooset requisitos de backup individuais do Backup Exec toomeet e contratos de nível de serviço (SLAs).

Embora ilustre os principais conceitos e as etapas de configuração, este artigo não é um guia passo a passo de configuração ou instalação. Pressupomos que que infra-estrutura e dos componentes básicos Olá são em funcionamento e toosupport pronto Olá conceitos que descrevemos.

### <a name="who-should-read-this"></a>Quem deve ler isso?

informações de saudação neste artigo serão administradores de toobackup mais úteis, os administradores de armazenamento e arquitetos de armazenamento que ter conhecimento de armazenamento, Windows Server 2012 R2, Ethernet, serviços de nuvem e Backup Exec.

## <a name="supported-versions"></a>Versões com suporte

-   [Backup Exec 16 e versões posteriores](http://backupexec.com/compatibility)
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
![Diagrama da disposição em camadas do StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)

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

| Capacidade de armazenamento       | 8100          | 8600            |
|------------------------|---------------|-----------------|
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

![StorSimple como um diagrama lógico de destino de backup principal](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

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

![StorSimple como um diagrama lógico de destino de backup secundário](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

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
3. Implantar Backup Exec.

Cada etapa é abordada em detalhes nas seções a seguir de saudação.

### <a name="set-up-hello-network"></a>Configurar rede Olá

Como StorSimple é uma solução integrada Olá nuvem do Azure, StorSimple requer uma conexão ativa e em funcionamento de toohello nuvem do Azure. Essa conexão é usada para operações como instantâneos de nuvem, gerenciamento e metadados de transferência e armazenamento em nuvem tooAzure tootier dados mais antigos e menos acessados.

Para Olá solução tooperform ideal, recomendamos que você siga essas práticas recomendadas de rede:

-   link de saudação que se conecta a seu tooAzure camada do StorSimple deve atender aos seus requisitos de largura de banda. tooachieve, aplicar Olá necessário qualidade de serviço (QoS) nível tooyour infraestrutura comutadores toomatch RTO (objetivo) SLAs de tempo de seu RPO e recuperação.
-   As latências máximas de acesso ao Armazenamento de Blobs do Azure devem ser cerca de 80 ms.

### <a name="deploy-storsimple"></a>Implantar o StorSimple

Para ver diretrizes passo a passo de implantação do StorSimple, acesse [Implantar seu dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-backup-exec"></a>Implantar Backup Exec

Para ver as práticas recomendadas de instalação do Backup Exec, veja [Práticas recomendadas para a instalação do Backup Exec](https://www.veritas.com/support/en_US/article.000068207).

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

- Não use volumes estendidos (criados pelo Gerenciamento de Disco do Windows). Não há suporte para discos estendidos.
- Formate os volumes usando o NTFS com tamanho de alocação de 64 KB.
- Mapear os volumes do StorSimple Olá servidor de Backup Exec toohello diretamente.
    - Use o iSCSI para servidores físicos.
    - Use discos de passagem para servidores virtuais.

## <a name="best-practices-for-storsimple-and-backup-exec"></a>Práticas recomendadas para StorSimple e Backup Exec

Configure sua solução de acordo com as diretrizes de toohello Olá seções a seguir.

### <a name="operating-system-best-practices"></a>Práticas recomendadas do sistema operacional

-   Desabilite a criptografia do Windows Server e eliminação de duplicação do sistema de arquivos NTFS hello.
-   Desabilite a desfragmentação do Windows Server em volumes do StorSimple hello.
-   Desabilite a indexação em Olá volumes do StorSimple do Windows Server.
-   Execute uma verificação antivírus no host de origem da saudação (não em volumes do StorSimple Olá).
-   Desativar saudação padrão [manutenção do Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) no Gerenciador de tarefas. Faça isso em uma saudação maneiras a seguir:
   - Desligue o Configurador de manutenção Olá no Agendador de tarefas do Windows.
   - Baixe [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) do Windows Sysinternals. Depois de baixar o PsExec, execute o Azure PowerShell como administrador e digite:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Práticas recomendadas do StorSimple

  -   Certifique-se de que esse dispositivo StorSimple de saudação é atualizado muito[Update 3 ou posterior](storsimple-install-update-3.md).
  -   Isolar tráfego de iSCSI e de nuvem. Use conexões iSCSI dedicado para o tráfego entre o servidor de backup StorSimple e hello.
  -   Verifique se o dispositivo do StorSimple é um destino de backup dedicado. Não há suporte para cargas de trabalho mistas porque elas afetam o RTO e RPO.

### <a name="backup-exec-best-practices"></a>Práticas recomendadas de Backup Exec

-   Backup Exec deve ser instalado em uma unidade local do servidor de saudação e não em um volume StorSimple.
-   Configure o armazenamento de Backup Exec Olá **operações de gravação simultâneos** toohello máximo permitido.
    -   Configure o armazenamento de Backup Exec Olá **tamanho de bloco e buffer** too512 KB.
    -   Ative a **leitura e gravação em buffer** do armazenamento do Backup Exec.
-   O StorSimple dá suporte a backups completos e incrementais do Backup Exec. Não é recomendável usar backups diferenciais e sintéticos.
-   Os arquivos de dados de backup devem conter apenas dados de um trabalho específico. Por exemplo, não são permitidos acréscimos de mídia em vários trabalhos diferentes.
-   Desabilite a verificação do trabalho. Se necessário, a verificação deve ser agendada após o trabalho de backup mais recente hello. É importante toounderstand esse trabalho afeta sua janela de backup.
-   Selecione **Armazenamento** > **Seu disco** > **Detalhes** > **Propriedades**. Desligue **Pré-alocar espaço em disco**.

Para configurações de Backup Exec hello mais recentes e práticas recomendadas para implementar esses requisitos, consulte [site de Veritas Olá](https://www.veritas.com).

## <a name="retention-policies"></a>Políticas de retenção

Um dos tipos de política de retenção de backup mais comuns Olá é uma diretiva avô, pai e filho (GFS). Em uma política GFS, um backup incremental é executado diariamente e backups completos são realizados semanalmente e mensalmente. Essa política resulta em seis volumes do StorSimple em camadas. Um volume contém Olá semanais, mensais e anuais backups completos. Olá, outros cinco volumes armazenam backups incrementais diariamente.

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

## <a name="set-up-backup-exec-storage"></a>Configurar o armazenamento de Backup Exec

### <a name="tooset-up-backup-exec-storage"></a>tooset o armazenamento de Backup Exec

1.  No console de gerenciamento de Backup Exec hello, selecione **armazenamento** > **configurar armazenamento** > **armazenamento baseado em disco**  >   **Próxima**.

    ![Console de gerenciamento do Backup Exec, página de configuração de armazenamento](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  Selecione **Armazenamento em Disco** e selecione **Avançar**.

    ![Console de gerenciamento do Backup Exec, página selecionar armazenamento](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  Insira um nome representativo, por exemplo, **Sábado Completo** e uma descrição. Selecione **Avançar**.

    ![Console de gerenciamento do Backup Exec, página de nome e descrição](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  Disco hello selecione onde dispositivo de armazenamento em disco toocreate hello e, em seguida, selecione **próximo**.

    ![Console de gerenciamento do Backup Exec, tela de seleção do disco de armazenamento](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  Aumente o número de saudação de operações de gravação muito**16**e, em seguida, selecione **próximo**.

    ![Console de gerenciamento do Backup Exec, página de configurações de operações de gravação simultâneas](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  Examine as configurações de saudação e, em seguida, selecione **concluir**.

    ![Console de gerenciamento do Backup Exec, página de resumo de configuração de armazenamento](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  Final de saudação de cada atribuição de volume, alterar configurações de dispositivo do hello armazenamento toomatch aqueles recomendado [práticas recomendadas para StorSimple e Backup Exec](#best-practices-for-storsimple-and-backup-exec).

    ![Console de gerenciamento do Backup Exec, página de configurações do dispositivo de armazenamento](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  Repita as etapas 1 a 7 até concluir a atribuição de seu volumes de StorSimple tooBackup Exec.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurar o StorSimple como destino de backup principal

> [!NOTE]
> Restauração de dados de um backup que tenha sido nuvem em camadas toohello ocorre em velocidades de nuvem.

Hello figura a seguir mostra o hello mapeamento de um trabalho de backup do volume típico tooa. Nesse caso, todos os backups semanais de saudação mapeiam toohello sábado total do disco, e os backups incrementais Olá mapeiam discos incremental tooMonday-sexta-feira. Olá a todos os backups e restaurações de um StorSimple hierárquico de volume.

![Diagrama lógico de configuração de destino de backup principal](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemplo de agendamento do StorSimple destino de backup principal GFS

Veja esta exemplo de uma agenda de rotação GFS de quatro semanas, mensal e anual:

| Frequência/tipo de backup | Completo | Incremental (1 a 5 dias)  |   
|---|---|---|
| Semanal (1 a 4 semanas) | Sábado | Segunda a sexta-feira |
| Mensal  | Sábado  |   |
| Anual | Sábado  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a>Atribuir o trabalho de backup do StorSimple volumes tooa Backup Exec

Olá sequência a seguir supõe que esse host de destino de Backup Exec e hello é configurada de acordo com as diretrizes de agente de Backup Exec hello.

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a>tooassign StorSimple volumes tooa Backup Exec trabalho de backup

1.  No console de gerenciamento de Backup Exec hello, selecione **Host** > **Backup** > **Backup tooDisk**.

    ![Console de gerenciamento de Exec de backup, selecione toodisk de host, backup e backup](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  Em Olá **propriedades de definição de Backup** caixa de diálogo **Backup**, selecione **editar**.

    ![Console de gerenciamento do Backup Exec, caixa de diálogo Propriedades de Definição de Backup](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  Configure os backups completos e incrementais para que eles atendem os requisitos de RPO e RTO e estar de acordo com as práticas recomendadas de tooVeritas.

4.  Em Olá **opções de Backup** caixa de diálogo, selecione **armazenamento**.

    ![Console de gerenciamento do Backup Exec, caixa de diálogo Armazenamento das Opções de Backup](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  Atribua correspondente StorSimple volumes tooyour agendamento de backup.

    > [!NOTE]
    > **Compactação** e **tipo de criptografia** são definidos de forma muito**nenhum**.

6.  Em **verificar**, selecione Olá **não verificar os dados para este trabalho** caixa de seleção. Usar esta opção pode afetar a disposição em camadas do StorSimple.

    > [!NOTE]
    > Desfragmentação, indexação e verificação de plano de fundo afetam negativamente Olá StorSimple camadas.

    ![Console de gerenciamento do Backup Exec, configurações de verificação das Opções de Backup](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  Quando você configurar o restante de saudação do toomeet suas opções de backup seus requisitos, selecione **Okey** toofinish.

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurar o StorSimple como destino de backup secundário

> [!NOTE]
>Restaurações de dados de um backup que tenha sido nuvem em camadas toohello ocorrerem em velocidades de nuvem.

Nesse modelo, você deve ter uma tooserve de mídia (além de StorSimple) de armazenamento como um cache temporário. Por exemplo, você pode usar uma matriz redundante de discos independentes (RAID) um volume tooaccommodate espaço, entrada/saída (e/s) e largura de banda. Recomendamos o uso de RAID 5, 50 e 10.

Olá figura a seguir mostra típica retenção de curto prazo local (servidor toohello) volumes de arquivos de volumes e retenção de longo prazo. Nesse cenário, todos os backups executado no local hello (toohello server) volume RAID. Esses backups são periodicamente duplicados e arquivado tooan arquiva volume. Ele é importante toosize local (servidor toohello) RAID volume para que ele possa manipular a seus requisitos de capacidade e desempenho de retenção curto prazo.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple como um exemplo GFS de destino de backup secundário

![StorSimple como diagrama lógico de destino de backup secundário](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

Olá seguinte tabela mostra como tooset backup toorun backups em discos do StorSimple e local de saudação. Ele inclui os requisitos de capacidade total e individuais.

### <a name="backup-configuration-and-capacity-requirements"></a>Configuração de backup e requisitos de capacidade

| Tipo de backup e retenção | Armazenamento configurado | Tamanho (TiB) | Multiplicador GFS | Capacidade total\* (TiB) |
|---|---|---|---|---|
| Semana 1 (completa e incremental) |Disco local (curto prazo)| 1 | 1 | 1 |
| StorSimple semanas 2 a 4 |Disco StorSimple (longo prazo) | 1 | 4 | 4 |
| Mensal completo |Disco StorSimple (longo prazo) | 1 | 12 | 12 |
| Anual completo |Disco StorSimple (longo prazo) | 1 | 1 | 1 |
|Requisito de tamanho de volumes do GFS |  |  |  | 18*|
A capacidade total do \* inclui 17 TiB de discos do StorSimple e 1 TiB de volume RAID local.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Agenda de exemplo GFS: agendamento de rotação GFS semanal, mensal e anual

| Semana | Completo | Incremental dia 1 | Incremental dia 2 | Incremental dia 3 | Incremental dia 4 | Incremental dia 5 |
|---|---|---|---|---|---|---|
| Semana 1 | Volume RAID local  | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local |
| Semana 2 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Semana 3 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Semana 4 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Mensal | StorSimple mensal |   |   |   |   |   |
| Anual | StorSimple anual  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a>Atribuir StorSimple volumes tooa Backup Exec arquivamento e eliminação de duplicação de trabalho

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a>tooassign StorSimple volumes tooa Backup Exec arquivamento e eliminação de duplicação trabalho

1.  No console de gerenciamento de Backup Exec hello, clique com botão direito trabalho Olá que você deseja tooarchive tooa StorSimple volume e, em seguida, selecione **propriedades de definição de Backup** > **editar**.

    ![Console de gerenciamento do Backup Exec, guia Propriedades de Definição de Backup](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  Selecione **Adicionar estágio** > **duplicado tooDisk** > **editar**.

    ![Console de gerenciamento de Backup Exec, adicionar estágio](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  Em Olá **opções duplicar** caixa de diálogo, selecione Olá valores toouse para **fonte** e **agenda**.

    ![Console de gerenciamento, propriedades de definição de backup e opções de duplicação do Backup Exec](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  Em Olá **armazenamento** lista suspensa, o volume de StorSimple hello selecione onde você deseja Olá arquivamento trabalho toostore Olá dados.

    ![Console de gerenciamento, propriedades de definição de backup e opções de duplicação do Backup Exec](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  Selecione **verificar**e, em seguida, selecione Olá **não verificar os dados para este trabalho** caixa de seleção.

    ![Console de gerenciamento, propriedades de definição de backup e opções de duplicação do Backup Exec](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  Selecione **OK**.

    ![Console de gerenciamento, propriedades de definição de backup e opções de duplicação do Backup Exec](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  Em Olá **Backup** coluna, adicione um novo estágio. Para a origem de hello, use **incremental**. Para o destino de saudação escolha Olá volume StorSimple onde o trabalho de backup incremental Olá é arquivado. Repita as etapas 1 a 6.

## <a name="storsimple-cloud-snapshots"></a>Instantâneos de nuvem do StorSimple

Instantâneos de nuvem do StorSimple protegem os dados de saudação que reside em seu dispositivo StorSimple. Criando um instantâneo de nuvem é instalação do tooshipping equivalente fitas de backup local tooan externa. Se você usar o armazenamento com redundância geográfica do Azure, criando um instantâneo de nuvem é equivalente tooshipping sites de toomultiple de fitas de backup. Se você precisar toorestore um dispositivo depois de um desastre, você pode colocar outro dispositivo StorSimple e execute um failover. Após o failover hello, seria tooaccess capaz de dados de Olá (em velocidades de nuvem) do instantâneo em nuvem hello mais recente.

Olá seção a seguir descreve como toocreate toostart um script curto e delete StorSimple instantâneos em nuvem durante o pós-processamento de backup.

> [!NOTE]
> Instantâneos são criados de forma manual ou por meio de programação não execute política de expiração de instantâneo StorSimple hello. Esses instantâneos devem ser excluídos manual ou programaticamente.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Iniciar e excluir instantâneos de nuvem usando um script

> [!NOTE]
> Avalie cuidadosamente repercussões de retenção de dados e a conformidade de saudação antes de excluir um instantâneo do StorSimple. Para obter mais informações sobre como toorun um script pós-backup, consulte Olá [documentação de Backup Exec](https://www.veritas.com/support/en_US/15047.html).

### <a name="backup-lifecycle"></a>Ciclo de vida de backup

![Diagrama de ciclo de vida de backup](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a>Requisitos

-   servidor de saudação que executa o script hello deve ter recursos de nuvem tooAzure acesso.
-   conta de usuário de saudação deve ter as permissões necessárias hello.
-   Uma política de backup StorSimple com hello associados StorSimple volumes devem ser configurados, mas não ativados.
-   Você precisará Olá nome de recurso de StorSimple, chave de registro, nome do dispositivo e ID de política de backup.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart ou excluir um instantâneo de nuvem

1.  [Instale o Azure PowerShell](/powershell/azure/overview).
2.  [Baixar e importar informações de assinatura e configurações de publicação](https://msdn.microsoft.com/library/dn385850.aspx).
3.  No hello portal clássico do Azure, obter o nome do recurso hello e [chave de registro para o serviço StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  No servidor de saudação que executa o script hello, execute o PowerShell como administrador. Digite este comando:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    ID da política de backup Olá nota.
5.  No bloco de notas, crie um novo script do PowerShell usando Olá código a seguir.

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
      Salvar toohello de script do PowerShell Olá mesmo local onde você salvou o Azure configurações de publicação. Por exemplo, salve como C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Adicione o trabalho de backup Olá script tooyour no Backup Exec editando processamento de suas opções trabalho de Backup Exec pré e pós-processamento de comandos.

    ![Console do Backup Exec, opções de backup, guia de comandos pré e pós-processamento](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> É recomendável que você execute sua política de backup de instantâneo do StorSimple nuvem como um script de pós-processamento final de saudação do seu trabalho de backup diário. Para obter mais informações sobre como tooback backup e restauração toohelp de ambiente seu aplicativo de backup você atingir seu RPO e RTO, consulte com o arquiteto de backup.

## <a name="storsimple-as-a-restore-source"></a>StorSimple como origem de restauração

As restaurações de um dispositivo StorSimple funcionam como qualquer dispositivo de armazenamento em bloco. Restaurações de dados hierárquico toohello nuvem ocorre em velocidades de nuvem. Para dados locais, restaurações ocorrem na velocidade do disco local de saudação do dispositivo de saudação. Para obter informações sobre como tooperform uma restauração, consulte a documentação de Backup Exec hello. É recomendável que você está de acordo com as práticas recomendadas para restauração Exec tooBackup.

## <a name="storsimple-failover-and-disaster-recovery"></a>Failover e recuperação de desastre do StorSimple

> [!NOTE]
> Para cenários de destino de backup, o StorSimple Cloud Appliance não tem suporte como um destino de restauração.

Um desastre pode ser causado por uma variedade de fatores. Olá, a tabela a seguir lista cenários comuns de recuperação de desastres.

| Cenário | Impacto | Como toorecover | Observações |
|---|---|---|---|
| Falha do dispositivo StorSimple | As operações de backup e restauração foram interrompidas. | Substitua o dispositivo com falha hello e executar [StorSimple failover e recuperação de desastres](storsimple-device-failover-disaster-recovery.md). | Se você precisar tooperform uma restauração após a recuperação do dispositivo, os conjuntos de trabalho de dados completos são recuperados do hello nuvem toohello novo dispositivo. Todas as operações ocorrem em velocidades de nuvem. Olá, indexação e verificar novamente o processo de catalogação pode causar todos os toobe de conjuntos de backup verificado e realizou Olá camada toohello dispositivo local da camada de nuvem, que pode ser um processo demorado. |
| Falha do servidor Backup Exec | As operações de backup e restauração foram interrompidas. | Recriar o servidor de backup hello e executar a restauração de banco de dados, conforme detalhado no [como toodo um banco de dados de Backup e restauração do Backup Exec (BEDB) manual](http://www.veritas.com/docs/000041083). | Você deve recriar nem restaurar o servidor de Backup Exec Olá no local de recuperação de desastres hello. Restaure ponto mais recente do toohello Olá banco de dados. Se Olá restaurado Backup Exec banco de dados não está em sincronizado com os trabalhos de backup mais recentes, indexação e catalogação é necessário. Esse índice e verificar novamente o processo de catálogo podem causar todos os toobe de conjuntos de backup verificado e realizou Olá camada toohello dispositivo local da camada de nuvem. Isso torna tudo ainda mais demorado. |
| Falha do site que resulta na perda de saudação do servidor de backup hello e StorSimple | As operações de backup e restauração foram interrompidas. | Restaure o StorSimple primeiro e depois o Backup Exec. | Restaure o StorSimple primeiro e depois o Backup Exec. Se você precisar tooperform uma restauração após a recuperação do dispositivo, Olá conjuntos de trabalho de dados completos são recuperados do hello nuvem toohello novo dispositivo. Todas as operações ocorrem em velocidades de nuvem. |

## <a name="references"></a>Referências

Olá documentos a seguir foram referenciado para este artigo:

- [Configuração de Multipath I/O de StorSimple](storsimple-configure-mpio-windows-server.md)
- [Cenários de armazenamento: provisionamento dinâmico](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Usando unidades GPT](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurar cópias de sombra para pastas compartilhadas](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre como muito[restauração a partir de um conjunto de backup](storsimple-restore-from-backup-set-u2.md).
- Saiba mais sobre como tooperform [dispositivo failover e recuperação de desastres](storsimple-device-failover-disaster-recovery.md).
