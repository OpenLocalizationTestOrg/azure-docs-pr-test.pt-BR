---
title: "aaaStorSimple 8000 séries como destino de backup com NetBackup | Microsoft Docs"
description: "Descreve a configuração de destino de backup do StorSimple Olá com Veritas NetBackup."
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
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>StorSimple como um destino de backup com o NetBackup

## <a name="overview"></a>Visão geral

O Azure StorSimple é uma solução de armazenamento de nuvem híbrida da Microsoft. StorSimple aborda as complexidades de saudação do crescimento exponencial de dados usando uma conta de armazenamento do Azure como uma extensão de Olá local solução e colocar automaticamente dados em armazenamento local e o armazenamento em nuvem.

Neste artigo, abordamos a integração do StorSimple com o Veritas NetBackup e as práticas recomendadas para a integração de ambas as soluções. Também fazemos recomendações sobre como integrar o tooset backup Veritas NetBackup toobest com StorSimple. Podemos adiar tooVeritas práticas recomendadas, backup arquitetos e administradores para Olá melhor maneira tooset Veritas NetBackup toomeet individuais aos requisitos de backup e contratos de nível de serviço (SLAs).

Embora ilustre os principais conceitos e as etapas de configuração, este artigo não é um guia passo a passo de configuração ou instalação. Pressupomos que que infra-estrutura e dos componentes básicos Olá são em funcionamento e toosupport pronto Olá conceitos que descrevemos.

### <a name="who-should-read-this"></a>Quem deve ler isso?

informações de saudação neste artigo serão administradores de toobackup mais úteis, os administradores de armazenamento e arquitetos de armazenamento que ter conhecimento de armazenamento, Windows Server 2012 R2, Ethernet, serviços de nuvem e Veritas NetBackup.

### <a name="supported-versions"></a>Versões com suporte

-   NetBackup 7.7.x e versões posteriores
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
![Diagrama da disposição em camadas do StorSimple](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

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

![StorSimple como um diagrama lógico de destino de backup principal](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Etapas de lógica de backup de destino principal

1.  contatos de servidor de backup Olá Olá agente de backup de destino e o agente de backup Olá transmite o servidor de backup de toohello de dados.
2.  servidor de backup Olá grava dados toohello StorSimple de volumes em camadas.
3.  servidor de backup Olá atualiza o banco de dados de catálogo hello e conclui o trabalho de backup hello.
4.  Um script de instantâneo aciona o Gerenciador de instantâneos do StorSimple hello (início ou exclusão).
5.  servidor de backup Olá exclui backups expirados com base em uma política de retenção.

### <a name="primary-target-restore-logical-steps"></a>Etapas lógicas de restauração de destino principal

1.  servidor de backup Olá inicia a restaurar os dados apropriados do hello do repositório hello.
2.  Agente de backup Olá recebe dados de saudação do servidor de backup hello.
3.  servidor de backup Olá concluirá o trabalho de restauração hello.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple como destino de backup secundário

Nesse cenário, os volumes do StorSimple são usados principalmente para retenção de longo prazo ou arquivamento.

Olá figura a seguir mostra uma arquitetura na qual os backups inicias e restaura o volume de destino de alto desempenho. Esses backups são copiados e arquivado tooa StorSimple hierárquico volume em um agendamento definido.

É importante toosize seu volume de alto desempenho, para que ele possa lidar com seus requisitos de capacidade e desempenho de política retenção.

![StorSimple como um diagrama lógico de destino de backup secundário](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Etapas de lógica de backup de destino secundário

1.  contatos de servidor de backup Olá Olá agente de backup de destino e o agente de backup Olá transmite o servidor de backup de toohello de dados.
2.  servidor de backup Olá grava toohigh desempenho, armazenamento de dados.
3.  servidor de backup Olá atualiza o banco de dados de catálogo hello e conclui o trabalho de backup hello.
4.  Olá tooStorSimple de backups de cópias de backup de servidor com base em uma política de retenção.
5.  Um script de instantâneo aciona o Gerenciador de instantâneos do StorSimple hello (início ou exclusão).
6.  Exclusões de servidor de backup Olá Olá expirado backups com base em uma política de retenção.

### <a name="secondary-target-restore-logical-steps"></a>Etapas lógicas de restauração de destino secundário

1.  servidor de backup Olá inicia a restaurar os dados apropriados do hello do repositório hello.
2.  Agente de backup Olá recebe dados de saudação do servidor de backup hello.
3.  servidor de backup Olá concluirá o trabalho de restauração hello.

## <a name="deploy-hello-solution"></a>Implantar solução Olá

Implantar essa solução exige três etapas:
1. Prepare a infraestrutura de rede hello.
2. Implante o dispositivo StorSimple como um destino de backup.
3. Implante o Veritas NetBackup.

Cada etapa é abordada em detalhes nas seções a seguir de saudação.

### <a name="set-up-hello-network"></a>Configurar rede Olá

Como StorSimple é uma solução integrada Olá nuvem do Azure, StorSimple requer uma conexão ativa e em funcionamento de toohello nuvem do Azure. Essa conexão é usada para operações como instantâneos de nuvem, gerenciamento de dados e metadados de transferência e armazenamento em nuvem tooAzure tootier dados mais antigos e menos acessados.

Para Olá solução tooperform ideal, recomendamos que você siga essas práticas recomendadas de rede:

-   link de saudação que se conecta a saudação StorSimple camada tooAzure deve atender aos seus requisitos de largura de banda. tooachieve, aplicar Olá adequada qualidade de serviço (QoS) nível tooyour infraestrutura comutadores toomatch RTO (objetivo) SLAs de tempo de seu RPO e recuperação.

-   As latências máximas de acesso ao Armazenamento de Blobs do Azure devem ser cerca de 80 ms.

### <a name="deploy-storsimple"></a>Implantar o StorSimple

Para ver diretrizes passo a passo de implantação do StorSimple, acesse [Implantar seu dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>Implantar o NetBackup

Para obter orientação passo a passo sobre implantação de 7.7.x NetBackup, consulte Olá [NetBackup 7.7.x documentação](http://www.veritas.com/docs/000094423).

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

- Não use volumes estendidos (criados pelo Gerenciador de Disco do Windows), pois não há suporte para eles.
- Formate os volumes usando o NTFS com tamanho de alocação de 64 KB.
- Mapear os volumes do StorSimple Olá diretamente toohello NetBackup server.
    - Use o iSCSI para servidores físicos.
    - Use discos de passagem para servidores virtuais.


## <a name="best-practices-for-storsimple-and-netbackup"></a>Práticas recomendadas para StorSimple e NetBackup

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

### <a name="netbackup-best-practices"></a>Práticas recomendadas do NetBackup

-   o banco de dados do Olá NetBackup deve ser toohello local server e não reside em um volume StorSimple.
-   Recuperação de desastres, faça Olá NetBackup em um volume StorSimple.
-   Há suporte para NetBackup backups completos e incrementais (também chamado tooas diferencial backups incrementais no NetBackup) para esta solução. Recomendamos que você não use backups incrementais sintéticos e cumulativos.
-   Arquivos de dados de backup devem conter apenas os dados de saudação de um trabalho específico. Por exemplo, não são permitidos acréscimos de mídia em vários trabalhos diferentes.

Para Olá configurações NetBackup mais recentes e práticas recomendadas para implementar esses requisitos, consulte a documentação de NetBackup Olá em [www.veritas.com](https://www.veritas.com).


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

## <a name="set-up-netbackup-storage"></a>Configurar o armazenamento do NetBackup

### <a name="tooset-up-netbackup-storage"></a>tooset o armazenamento de NetBackup

1.  No hello NetBackup Console de administração, selecione **gerenciamento de dispositivos e mídia** > **dispositivos** > **Pools de discos**. Em Olá Assistente de configuração do Pool de disco, selecione o tipo de servidor de armazenamento de saudação **AdvancedDisk**e, em seguida, selecione **próximo**.

    ![Console de Administração do NetBackup, Assistente de Configuração do Pool de Disco](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Selecione seu servidor e clique em **Avançar**.

    ![Console de administração do NetBackup, servidor de saudação select](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  Selecione seu volume StorSimple.

    ![Console de administração do NetBackup, disco de volume StorSimple Olá select](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Insira um nome para o destino de backup hello e, em seguida, selecione **próximo** > **próximo** toofinish Assistente de saudação.

5.  Examine as configurações de saudação e, em seguida, selecione **concluir**.

6.  Final de saudação de cada atribuição de volume, alterar Olá armazenamento dispositivo configurações toomatch aqueles recomendada em [práticas recomendadas para StorSimple e NetBackup](#best-practices-for-storsimple-and-netbackup).

7. Repita as etapas 1 a 6 até concluir a atribuição de volumes do StorSimple.

    ![Console de Administração do NetBackup, configuração do disco](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurar o StorSimple como destino de backup principal

> [!NOTE]
> Restaurações de dados de um backup que tenha sido nuvem em camadas toohello ocorrerem em velocidades de nuvem.

Hello figura a seguir mostra o hello mapeamento de um trabalho de backup do volume típico tooa. Nesse caso, todos os backups semanais de saudação mapeiam toohello sábado total do disco, e os backups incrementais Olá mapeiam discos incremental tooMonday-sexta-feira. Olá a todos os backups e restaurações de um StorSimple hierárquico de volume.

![Diagrama lógico de configuração de destino de backup principal ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemplo de agendamento do StorSimple destino de backup principal GFS

Veja esta exemplo de uma agenda de rotação GFS de quatro semanas, mensal e anual:

| Frequência/tipo de backup | Completo | Incremental (1 a 5 dias)  |   
|---|---|---|
| Semanal (1 a 4 semanas) | Sábado | Segunda a sexta-feira |
| Mensal  | Sábado  |   |
| Anual | Sábado  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>Atribuir o trabalho de backup do StorSimple volumes tooa NetBackup

Olá sequência a seguir supõe que esse host de destino NetBackup e hello é configurada de acordo com as diretrizes do hello NetBackup agente.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>tooassign StorSimple volumes tooa NetBackup trabalho de backup

1.  No hello NetBackup Console de administração, selecione **NetBackup gerenciamento**, clique com botão direito **políticas**e, em seguida, selecione **nova política**.

    ![Console de Administração do NetBackup, criar uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  Em Olá **adicionar uma nova diretiva** caixa de diálogo, digite um nome para a política de saudação e selecione Olá **Assistente de configuração de política de uso** caixa de seleção. Selecione **OK**.

    ![Console de Administração do NetBackup, caixa de diálogo Adicionar uma Nova Política](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  No Assistente de configuração de política de Backup do hello, elecione Olá tipo de backup você deseja e, em seguida, selecione **próximo**.

    ![Console de Administração do NetBackup, selecionar tipo de backup](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tipo de política Olá tooset, selecione **padrão**e, em seguida, selecione **próximo**.

    ![Console de Administração do NetBackup, selecionar tipo de política](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Selecione o host, selecione Olá **detectar o sistema operacional cliente** caixa de seleção e, em seguida, selecione **adicionar**. Selecione **Avançar**.

    ![Console de Administração do NetBackup, listar clientes em uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Selecione unidades de saudação que desejar tooback.

    ![Console de Administração do NetBackup, seleções de backup para uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Selecione a frequência de saudação e os valores de retenção que atendem aos seus requisitos de rotação de backup.

    ![Console de Administração do NetBackup, frequência e rotação de backup para uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Selecione **Avançar** > **Avançar** > **Concluir**.  Você pode modificar o agendamento de saudação depois Olá política é criada.

9.  Selecionar política de saudação tooexpand acabou criado e, em seguida, selecione **agendas**.

    ![Console de Administração do NetBackup, agendamentos para uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Clique com botão direito **Inc diferencial**, selecione **copiar toonew**e, em seguida, selecione **Okey**.

    ![Console de administração do NetBackup, cópia agenda tooa nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Agenda Olá recém-criada e, em seguida, selecione **alteração**.

12.  Em Olá **atributos** guia, selecione Olá **substituir a seleção de armazenamento de política** caixa de seleção e volume hello, em seguida, selecione onde segunda-feira backups incrementais ir.

    ![Console de Administração do NetBackup, alterar o agendamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  Em Olá **janela Iniciar** guia, janela de tempo de saudação select para seus backups.

    ![Console de Administração do NetBackup, alterar o início da janela](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  Selecione **OK**.

15.  Repita as etapas 10 a 14 para cada backup incremental. Selecione volume apropriado hello e agendamento para cada backup que você criar.

16.  Saudação de atalho **Inc diferencial** agendar e, em seguida, excluí-lo.

17.  Modifique seu toomeet agendamento completo que precisa de seu backup.

    ![Console de Administração do NetBackup, alterar o agendamento completo](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Janela de início de saudação de alteração.

    ![Console de administração do NetBackup, change Olá início janela](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  programação final Olá tem esta aparência:

    ![Console de Administração do NetBackup, agendamento final](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurar o StorSimple como destino de backup secundário

> [!NOTE]
>Restaurações de dados de um backup que tenha sido nuvem em camadas toohello ocorrerem em velocidades de nuvem.

Nesse modelo, você deve ter uma tooserve de mídia (além de StorSimple) de armazenamento como um cache temporário. Por exemplo, você pode usar uma matriz redundante de discos independentes (RAID) um volume tooaccommodate espaço, entrada/saída (e/s) e largura de banda. Recomendamos o uso de RAID 5, 50 e 10.

Olá figura a seguir mostra típica retenção de curto prazo local (servidor toohello) volumes de arquivos de volumes e retenção de longo prazo. Nesse cenário, todos os backups executado no local hello (toohello server) volume RAID. Esses backups são periodicamente duplicados e arquivado tooan arquiva volume. Ele é importante toosize local (servidor toohello) RAID volume para que ele possa manipular a seus requisitos de capacidade e desempenho de retenção curto prazo.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple como um exemplo GFS de destino de backup secundário

![StorSimple como um diagrama lógico de destino de backup secundário](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

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


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Atribuir StorSimple volumes tooa NetBackup arquivamento e eliminação de duplicação trabalho

Como NetBackup oferece uma ampla gama de opções de armazenamento e gerenciamento de mídia, recomendamos que você consulte Veritas ou seu tooproperly de arquiteto NetBackup avaliar os requisitos de política (SLP) de ciclo de vida de armazenamento.

Depois de definir os pools de discos inicial de saudação, você precisará toodefine três políticas de ciclo de vida de armazenamento adicional, para um total de quatro políticas de:
* LocalRAIDVolume
* StorSimpleWeek2-4
* StorSimpleMonthlyFulls
* StorSimpleYearlyFulls

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>tooassign StorSimple volumes tooa NetBackup arquivamento e eliminação de duplicação trabalho

1.  No hello NetBackup Console de administração, selecione **armazenamento** > **políticas do ciclo de vida de armazenamento** > **nova política de ciclo de vida de armazenamento**.

    ![Console de Administração do NetBackup, nova política de ciclo de vida de armazenamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Insira um nome para o instantâneo hello e, em seguida, selecione **adicionar**.

3.  Em Olá **nova operação** caixa de diálogo Olá **propriedades** guia, para **operação**, selecione **Backup**. Selecione valores hello desejados para **o armazenamento de destino**, **tipo de retenção**, e **período de retenção**. Selecione **OK**.

    ![Console de Administração do NetBackup, caixa de diálogo Nova Operação](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Isso define o repositório e a primeira operação de backup hello.

4.  Selecione a operação anterior de saudação toohighlight e, em seguida, selecione **adicionar**. Em Olá **operação de alteração de armazenamento** caixa de diálogo, valores hello selecione desejados para **o armazenamento de destino**, **tipo de retenção**, e **período de retenção** .

    ![Console de Administração do NetBackup, caixa de diálogo Alterar Operação de Armazenamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Selecione a operação anterior de saudação toohighlight e, em seguida, selecione **adicionar**. Em Olá **nova política de ciclo de vida de armazenamento** caixa de diálogo caixa, adicione backups mensais de um ano.

    ![Console de Administração do NetBackup, caixa de diálogo Nova Política do Ciclo de Vida de Armazenamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Repita as etapas 4 a 5 até que você criou Olá abrangente SLP política de retenção que você precisa.

    ![Console de administração do NetBackup, adicionar as diretivas na caixa de diálogo Nova política de ciclo de vida de armazenamento Olá](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Quando terminar de definir sua política de retenção SLP em **política**, definir uma política de backup seguindo as etapas Olá detalhadas [trabalho de backup do StorSimple atribuir volumes tooa NetBackup](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  Em **agendas**, em Olá **Alterar agendamento** caixa de diálogo, clique com botão direito **completo**e, em seguida, selecione **alteração**.

    ![Console de Administração do NetBackup, caixa de diálogo Alterar Agendamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Selecione Olá **substituir a seleção de armazenamento de política** caixa de seleção e política de retenção SLP hello, em seguida, selecione que você criou nas etapas 1 a 6.

    ![Console de Administração do NetBackup, substituir a seleção de armazenamento da política](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Selecione **Okey**e, em seguida, repita para agendamento de backup incremental hello.

    ![Console de Administração do NetBackup, caixa de diálogo Alterar Agendamento para backups incrementais](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Retenção de tipo de backup | Tamanho (TiB) | Multiplicador GFS\* | Capacidade total (TiB)  |
|---|---|---|---|
| Completo semanal |  1  |  4 | 4  |
| Incremental diário  | 0,5  | 20 (ciclos são toohello igual número de semanas por mês) | 12 (2 para a cota adicional) |
| Mensal completo  | 1 | 12 | 12 |
| Anual completo | 1  | 10 | 10 |
| Requisito de GFS  |     |     | 38 |
| Cota adicional  | 4  |    | Requisito total de GFS 42 |
\*Hello, multiplicador GFS é Olá número de cópias necessárias tooprotect e reter toomeet seus requisitos de política de backup.

## <a name="storsimple-cloud-snapshots"></a>Instantâneos de nuvem do StorSimple

Instantâneos de nuvem do StorSimple protegem os dados de saudação que reside em seu dispositivo StorSimple. Criando um instantâneo de nuvem é instalação do tooshipping equivalente fitas de backup local tooan externa. Se você usar o armazenamento com redundância geográfica do Azure, criando um instantâneo de nuvem é equivalente tooshipping sites de toomultiple de fitas de backup. Se você precisar toorestore um dispositivo depois de um desastre, você pode colocar outro dispositivo StorSimple e execute um failover. Após o failover hello, seria tooaccess capaz de dados de Olá (em velocidades de nuvem) do instantâneo em nuvem hello mais recente.

Olá seção a seguir descreve como toocreate toostart um script curto e delete StorSimple instantâneos em nuvem durante o pós-processamento de backup.

> [!NOTE]
> Instantâneos são criados de forma manual ou por meio de programação não execute política de expiração de instantâneo StorSimple hello. Esses instantâneos devem ser excluídos manual ou programaticamente.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Iniciar e excluir instantâneos de nuvem usando um script

> [!NOTE]
> Avalie cuidadosamente repercussões de retenção de dados e a conformidade de saudação antes de excluir um instantâneo do StorSimple. Para obter mais informações sobre como toorun um script pós-backup, consulte Olá [NetBackup documentação](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>Ciclo de vida de backup

![Diagrama de ciclo de vida de backup](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

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
6.  Adicione o trabalho de backup Olá script tooyour no NetBackup. toodo este, edite seu NetBackup opções pré-processando e pós-processamento de comandos do trabalho.

> [!NOTE]
> É recomendável que você execute sua política de backup de instantâneo do StorSimple nuvem como um script de pós-processamento final de saudação do seu trabalho de backup diário. Para obter mais informações sobre como tooback backup e restauração toohelp de ambiente seu aplicativo de backup você atingir seu RPO e RTO, consulte com o arquiteto de backup.

## <a name="storsimple-as-a-restore-source"></a>StorSimple como origem de restauração

As restaurações de um dispositivo StorSimple funcionam como qualquer dispositivo de armazenamento em bloco. Restaurações de dados hierárquico toohello nuvem ocorre em velocidades de nuvem. Para dados locais, restaurações ocorrem na velocidade do disco local de saudação do dispositivo de saudação. Para obter informações sobre como tooperform uma restauração, consulte Olá [NetBackup documentação](http://www.veritas.com/docs/000094423). É recomendável que você esteja em conformidade tooNetBackup restauração práticas recomendadas.

## <a name="storsimple-failover-and-disaster-recovery"></a>Failover e recuperação de desastre do StorSimple

> [!NOTE]
> Para cenários de destino de backup, o StorSimple Cloud Appliance não tem suporte como um destino de restauração.

Um desastre pode ser causado por uma variedade de fatores. Olá, a tabela a seguir lista cenários comuns de recuperação de desastres.

| Cenário | Impacto | Como toorecover | Observações |
|---|---|---|---|
| Falha do dispositivo StorSimple | As operações de backup e restauração foram interrompidas. | Substitua o dispositivo com falha hello e executar [StorSimple failover e recuperação de desastres](storsimple-device-failover-disaster-recovery.md). | Se você precisar tooperform uma restauração após a recuperação do dispositivo, os conjuntos de trabalho de dados completos são recuperados do hello nuvem toohello novo dispositivo. Todas as operações ocorrem em velocidades de nuvem. índice de saudação e verificar novamente o processo de catálogo podem causar todos os toobe de conjuntos de backup verificado e realizou Olá camada toohello dispositivo local da camada de nuvem, que pode ser um processo demorado. |
| Falha do servidor NetBackup | As operações de backup e restauração foram interrompidas. | Recriar o servidor de backup hello e executar a restauração do banco de dados. | Você deve recriar ou restaurar Olá NetBackup servidor no local de recuperação de desastres hello. Restaure ponto mais recente do toohello Olá banco de dados. Se hello banco de dados restaurado NetBackup não está em sincronizado com os trabalhos de backup mais recentes, indexação e catalogação serão necessária. Esse índice e verificar novamente o processo de catálogo podem causar todos os toobe de conjuntos de backup verificado e realizou Olá camada toohello dispositivo local da camada de nuvem. Isso torna tudo ainda mais demorado. |
| Falha do site que resulta na perda de saudação do servidor de backup hello e StorSimple | As operações de backup e restauração foram interrompidas. | Restaure o StorSimple primeiro e depois restaure o NetBackup. | Restaure o StorSimple primeiro e depois restaure o NetBackup. Se você precisar tooperform uma restauração após a recuperação do dispositivo, Olá conjuntos de trabalho de dados completos são recuperados do hello nuvem toohello novo dispositivo. Todas as operações ocorrem em velocidades de nuvem. |

## <a name="references"></a>Referências

Olá documentos a seguir foram referenciado para este artigo:

- [Configuração de Multipath I/O de StorSimple](storsimple-configure-mpio-windows-server.md)
- [Cenários de armazenamento: provisionamento dinâmico](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Usando unidades GPT](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurar cópias de sombra para pastas compartilhadas](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre como muito[restauração a partir de um conjunto de backup](storsimple-restore-from-backup-set-u2.md).
- Saiba mais sobre como tooperform [dispositivo failover e recuperação de desastres](storsimple-device-failover-disaster-recovery.md).
