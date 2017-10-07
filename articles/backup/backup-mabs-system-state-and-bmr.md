---
title: aaaAzure fazer Backup do servidor protege o estado do sistema e restaura metal toobare | Microsoft Docs
description: "Use o Azure Backup Server tooback backup do estado do sistema e fornecer proteção de recuperação bare-metal (BMR)."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Fazer backup do estado do sistema e restaurar metal toobare com o servidor de Backup do Azure

Use o Servidor de Backup do Azure para fazer backup do estado do sistema e fornecer proteção de recuperação bare-metal (BMR).

*   **Backup de estado do sistema**: faz backup de arquivos do sistema operacional, para que possa recuperar quando um computador é iniciado, mas os arquivos de sistema e o registro de hello serão perdidas. Um backup de estado do sistema inclui:
    * Membro do domínio: arquivos de inicialização, o banco de dados de registro da classe COM+, o registro
    * Controlador de domínio: Windows Server Active Directory (NTDS), arquivos de inicialização, o banco de dados de registro da classe COM+, o registro, o volume do sistema (SYSVOL)
    * Computador que executa os serviços de cluster: metadados do servidor de Cluster
    * Computador que executa os serviços de certificados: dados de certificado
* **Backup bare-metal**: faz backup de arquivos do sistema operacional e todos os dados em volumes críticos (exceto dados do usuário). Por definição, um backup de BMR inclui um backup de estado do sistema. Ele oferece proteção quando um computador não será iniciado e você tem toorecover tudo.

Olá, a tabela a seguir resume o que você pode fazer backup e recuperar. Para obter informações detalhadas sobre as versões de aplicativo que podem ser protegidos com o estado do sistema e a BMR, consulte [O que faz o servidor de Backup do Azure?](backup-mabs-protection-matrix.md).

|Backup|Problema|Recuperar de backup do Servidor de Backup do Azure|Recuperar de backup de estado do sistema|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**Dados de arquivo**<br /><br />Backup de dados regular<br /><br />Backup de estado do sistema/BMR|Dados de arquivos perdidos|S|N|N|
|**Dados de arquivo**<br /><br />Backup de arquivos de dados do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Sistema operacional perdido ou danificado|N|S|S|
|**Dados de arquivo**<br /><br />Backup de arquivos de dados do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Servidor perdido (volumes de dados intactos)|N|N|S|
|**Dados de arquivo**<br /><br />Backup de arquivos de dados do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Servidor perdido (volumes de dados intactos)|S|Não|Sim (BMR, seguida de recuperação regular de dados do arquivo de backup)|
|**Dados do SharePoint**:<br /><br />Backup de dados do farm do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Site perdido, listas, itens de lista, documentos|S|N|N|
|**Dados do SharePoint**:<br /><br />Backup de dados do farm do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Sistema operacional perdido ou danificado|N|S|S|
|**Dados do SharePoint**:<br /><br />Backup de dados do farm do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Recuperação de desastre|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Backup do Servidor de Backup do Azure do host do Hyper-V ou convidado<br /><br />Backup de estado do sistema de host/BMR|VM perdida|S|N|N|
|Hyper-V<br /><br />Backup do Servidor de Backup do Azure do host do Hyper-V ou convidado<br /><br />Backup de estado do sistema de host/BMR|Sistema operacional perdido ou danificado|N|S|S|
|Hyper-V<br /><br />Backup do Servidor de Backup do Azure do host do Hyper-V ou convidado<br /><br />Backup de estado do sistema de host/BMR|Host do Hyper-V perdido (VMs intactas)|N|N|S|
|Hyper-V<br /><br />Backup do Servidor de Backup do Azure do host do Hyper-V ou convidado<br /><br />Backup de estado do sistema de host/BMR|Host do Hyper-V perdido (VMs perdidas)|N|N|S<br /><br />BMR, seguida de recuperação regular do Servidor de Backup do Azure|
|SQL Server/Exchange<br /><br />Backup de aplicativo do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Dados do aplicativo perdidos|S|N|N|
|SQL Server/Exchange<br /><br />Backup de aplicativo do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Sistema operacional perdido ou danificado|N|y|S|
|SQL Server/Exchange<br /><br />Backup de aplicativo do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Servidor perdido (logs de transação/banco de dados intactos)|N|N|S|
|SQL Server/Exchange<br /><br />Backup de aplicativo do Servidor de Backup do Azure<br /><br />Backup de estado do sistema/BMR|Servidor perdido (logs de transação/banco de dados perdidos)|N|N|S<br /><br />Recuperação de BMR, seguida de recuperação regular do Servidor de Backup do Azure|

## <a name="how-system-state-backup-works"></a>Como funciona o backup de estado do sistema

Quando é executado um backup de estado do sistema, Backup servidor se comunica com Backup do Windows Server toorequest um backup de estado do sistema do servidor de saudação. Por padrão, o servidor de Backup e Backup do Windows Server usam unidade Olá com hello mais espaço livre. Informações sobre a unidade é salva no arquivo de PSDataSourceConfig.xml hello. Essa é a unidade de saudação que usa o Backup do Windows Server para backups.

Você pode personalizar a unidade de saudação usada pelo servidor de Backup para backup de estado do sistema de saudação. No servidor de saudação protegida, vá tooC:\Program Files\Microsoft Manager\MABS\Datasources de proteção de dados. Abra arquivo do hello PSDataSourceConfig.xml para edição. Saudação de alteração \<FilesToProtect\> valor para a letra da unidade hello. Salve e feche o arquivo hello. Se houver que um grupo de proteção definir o estado do sistema Olá tooprotect do computador Olá, execute uma verificação de consistência. Se um alerta for gerado, selecione **modificar grupo de proteção** no alerta hello e Assistente hello, em seguida, concluir. Em seguida, execute outra verificação de consistência.

Observe que, se o servidor de proteção de saudação está em um cluster, é possível que uma unidade de cluster seja selecionada como unidade Olá com hello mais espaço livre. Se essa propriedade da unidade tiver sido desligados tooanother nó e executa um backup de estado do sistema, unidade de saudação não está disponível e Olá backup falhará. Nesse cenário, modificar PSDataSourceConfig.xml toopoint tooa local unidade.

Em seguida, o Backup do Windows Server cria uma pasta chamada WindowsImageBackup na raiz de saudação da pasta de restauração de saudação. Enquanto o Backup do Windows Server cria backup Olá, todos os dados de saudação são colocados nessa pasta. Quando Olá backup for concluído, o arquivo hello é toohello transferidos computador de servidor de Backup. Observe Olá informações a seguir:

* Esta pasta e seu conteúdo não forem limpos quando o backup de saudação ou transferência for concluída. Olá melhor maneira toothink disso é que espaço hello está sendo reservado para Olá próxima vez que um backup for concluído.
* pasta de saudação é criada toda vez que um backup é feito. carimbo de data e hora Olá reflete o tempo de saudação de seu último backup de estado do sistema.

## <a name="bmr-backup"></a>Backup de BMR

Para a BMR (incluindo um backup de estado do sistema), o trabalho de backup Olá é salvo diretamente tooa compartilhamento no computador do servidor de Backup hello. Ele não será salvo tooa pasta no servidor de saudação protegida.

Servidor de backup chama o Backup do Windows Server e compartilha o volume de réplica Olá para esse backup BMR. Nesse caso, ela não informa a unidade de saudação do Backup do Windows Server toouse com hello mais espaço livre. Em vez disso, ele usa o compartilhamento Olá que foi criado para o trabalho de saudação.

Quando Olá backup for concluído, o arquivo hello é toohello transferidos computador de servidor de Backup. Logs são armazenados em C:\windows\logs\WindowsServerBackup.

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações

-   BMR não tem suporte para computadores que executam o Windows Server 2003 ou para computadores que executam um sistema operacional cliente.

-   Você não pode proteger a BMR e estado do sistema para Olá mesmo computador em grupos de proteção diferentes.

-   Um computador do Servidor de Backup não pode se proteger de BMR.

-   Curto prazo tootape proteção (disco para fita ou D2T) não tem suporte para a BMR. Há suporte para longo prazo tootape de armazenamento (disco para disco para fita ou D2D2T).

-   Para proteção de BMR, Backup do Windows Server deve ser instalado no computador de saudação protegida.

-   Para proteção de BMR, diferentemente para proteção de estado do sistema, o servidor de Backup não tem requisitos de espaço no computador protegida de saudação. Backup do Windows Server transfere diretamente o computador do servidor de Backup de toohello de backups. trabalho de transferência de backup de saudação não aparece na Olá Server Backup **trabalhos** exibição.

-   Servidor de backup reserva 30 GB de espaço no volume de réplica Olá para BMR. Você pode alterar isso na Olá **alocação de disco** página no Assistente para modificar grupo de proteção de saudação ou usando os cmdlets Get-DatasourceDiskAllocation e Set-DatasourceDiskAllocation PowerShell de saudação. No volume de ponto de recuperação hello, a proteção BMR exige cerca de 6 GB para uma retenção de cinco dias.
    * Observe que você não pode reduzir tooless de tamanho de volume de réplica de saudação de 15 GB.
    * Servidor de backup não calcula o tamanho de Olá Olá BMR da fonte de dados. Ele presume 30 GB para todos os servidores. Altere o valor de saudação com base no tamanho de saudação dos backups da BMR esperados no seu ambiente. tamanho de saudação de um backup de BMR pode ser calculado aproximadamente como soma de saudação do espaço usado em todos os volumes críticos. Volumes críticos = volume de inicialização + volume do sistema + volume que hospeda os dados de estado do sistema, como o Active Directory.

-   Se você alterar de tooBMR proteção de estado do sistema, a proteção BMR exige menos espaço no hello *volume de ponto de recuperação*. No entanto, hello espaço extra no volume de saudação não é recuperado. Você manualmente pode reduzir o tamanho do volume de saudação em Olá **modificar alocação do disco** página do Assistente para modificar grupo de proteção de saudação ou usando os cmdlets Get-DatasourceDiskAllocation e Set-DatasourceDiskAllocation PowerShell de saudação.

    Se você alterar de tooBMR proteção de estado do sistema, a proteção BMR exige mais espaço no hello *volume de réplica*. volume de saudação é estendido automaticamente. Se você quiser alocações de espaço toochange saudação padrão, use Olá Modify-DiskAllocation PowerShell cmdlet.

-   Se você alterar a proteção de estado de toosystem proteção BMR, você precisa de mais espaço no volume de ponto de recuperação de saudação. Servidor de backup pode tentar tooautomatically volume de saudação de aumento. Se houver espaço suficiente no pool de armazenamento hello, ocorrerá um erro.

    Se você alterar a proteção de estado de toosystem proteção BMR, é necessário espaço no computador Olá protegido. Isso ocorre porque a proteção de estado do sistema primeiro grava o computador local do toohello Olá réplica e, em seguida, transfere-toohello computador de servidor de Backup.

## <a name="before-you-begin"></a>Antes de começar

1.  **Implantar o Servidor de Backup do Azure**. Verifique se o Servidor de Backup é implantado corretamente. Para obter mais informações, confira:
    * [Requisitos de sistema para o Servidor de Backup do Azure](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Matriz de proteção do Servidor de Backup](backup-mabs-protection-matrix.md)

2.  **Configurar o armazenamento**. Você pode armazenar dados de backup em disco, fita e na nuvem de saudação com o Azure. Para obter mais informações, consulte [Preparar dados de armazenamento](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Configurar o agente de proteção de saudação**. Instale o agente de proteção de saudação no computador de saudação que desejar tooback. Para obter mais informações, consulte [agente de proteção do DPM implantar Olá](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Fazer backup do estado do sistema e bare-metal
Configurar um grupo de proteção, conforme descrito em [Implantar grupos de proteção](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). Observe que você não pode proteger a BMR e estado de sistema para Olá mesmo computador em grupos diferentes. Além disso, quando você seleciona a BMR, o estado do sistema é habilitado automaticamente.


1.  Assistente de novo grupo de proteção de Olá tooopen no hello Console do administrador do servidor de Backup, selecione **proteção** > **ações** > **criar proteção Grupo**.

2.  Em Olá **Selecionar tipo de grupo de proteção** , selecione **servidores**e, em seguida, selecione **próximo**.

3.  Em Olá **selecionar membros do grupo** página, expanda Olá computador e, em seguida, selecione **BMR** ou **o estado do sistema**.

    Lembre-se de que você não pode proteger a BMR e o sistema de estado para Olá mesmo computador em grupos diferentes. Além disso, quando você seleciona a BMR, o estado do sistema é habilitado automaticamente. Para obter mais informações, consulte [Implantar Grupos de proteção](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  Em Olá **Selecionar método de proteção de dados** , selecione como você deseja que o backup de curto e longo prazo toohandle. Backup de curto prazo está sempre toodisk primeiro e, em seguida, com a opção de saudação de backup de toohello de disco de saudação do Azure na nuvem usando o Backup do Azure (curto ou longo prazo). Uma nuvem de backup toohello termo toolong alternativo é tooset backup de longo prazo tooa backup autônomo fita ou dispositivo de biblioteca de fitas que se conectou tooBackup Server.

5.  Em Olá **selecionar objetivos de curto prazo** , selecione como você deseja tooback o armazenamento tooshort prazo em disco:
    1. Para **período de retenção**, selecione quanto tempo deseja que os dados de saudação tookeep no disco. 
    2. Para **frequência de sincronização**, selecione a frequência na qual você deseja toorun um toodisk backup incremental. Se você não quiser tooset um intervalo de backup, você pode verificar Olá **logo antes de um ponto de recuperação** opção. Servidor de Backup será executado um backup completo expresso antes de cada ponto de recuperação for agendado.

6.  Se você deseja toostore dados em fita para armazenamento de longo prazo, no hello **especificar objetivos de longo prazo** , selecione quanto tempo deseja que os dados da fita tookeep (1-99 anos). 
    1. Para **frequência de backup**, selecione com que frequência tootape backup deve ser executado. Olá frequência é baseada no período de retenção de saudação selecionado:
        * Quando o período de retenção de saudação é de 1 a 99 anos, você pode selecionar backups toooccur diária, semanal, quinzenal, mensal, trimestral, semestral ou anual.
        * Quando o período de retenção de saudação é de 1 a 11 meses, você pode selecionar backups toooccur diária, semanal, quinzenal ou mensal.
        * Quando o período de retenção de saudação é de 1 a 4 semanas, você pode selecionar backups toooccur diária ou semanal.

    2. Em Olá **selecionar detalhes de fita e biblioteca** página, selecione Olá toouse fita e biblioteca, e se os dados devem ser compactados e criptografados.

7.  Em Olá **rever alocação do disco** , reveja o espaço em disco de pool de armazenamento de saudação que é alocado para o grupo de proteção de saudação.

    1. **Tamanho total dos dados** Olá tamanho dos dados Olá desejar tooback.
    2. **Toobe de espaço em disco provisionado no Azure Backup Server** Olá espaço que o servidor de Backup recomenda para o grupo de proteção hello. Servidor de backup escolhe Olá ideal volume de backup com base nas configurações de saudação. No entanto, você pode editar as opções de backup do volume Olá **detalhes de alocação de disco**. 
    3. Para cargas de trabalho, no menu suspenso de saudação, selecione Olá armazenamento preferido. As edições alterar valores de saudação do **armazenamento Total** e **livre de armazenamento** em Olá **armazenamento em disco disponível** painel. Espaço pela falta de provisionamento é a quantidade de saudação do que fazer Backup do servidor sugere que adicionar backups smooth tooensure toohello volume de armazenamento.

8.  Em Olá **escolher método de criação de réplica** , selecione como você deseja que a replicação toohandle saudação inicial de dados completo. Se você escolher tooreplicate pela rede hello, recomendamos que você escolha um horário de pico. Para grandes quantidades de dados ou condições de rede que estão abaixo do ideal, considere a possibilidade de replicar dados Olá offline usando mídia removível.

9. Em Olá **escolher opções de verificação de consistência** , selecione como você deseja que as verificações de consistência tooautomate. Você pode escolher uma verificação de toorun somente quando os dados de réplica se tornar inconsistente, ou em uma agenda. Se você não quiser tooconfigure a verificação de consistência automática, você pode executar uma verificação manual a qualquer momento. toorun uma verificação manual, no hello **proteção** área da saudação Console do administrador do servidor de Backup, clique com botão direito proteção Olá grupo e, em seguida, selecione **executar verificação de consistência**.

10. Se você tiver selecionado tooback backup toohello nuvem usando o Backup do Azure, em Olá **especificar dados de proteção Online** página, certifique-se de que você selecione as cargas de trabalho Olá deseja tooback backup tooAzure.

11. Em Olá **especificar agendamento de Backup Online** , selecione os backups incrementais frequência tooAzure ocorrerá. Você pode agendar backups toorun cada dia, semana, mês e ano e selecione Olá data e a hora em que ele deve ser executado. Backups podem ocorrer se tootwice por dia. Cada vez que um backup é executado, um ponto de recuperação de dados é criado no Azure da cópia Olá Olá dos dados de backup armazenados no disco do servidor de Backup hello.

12. Em Olá **especificar política de retenção Online** , selecione como os pontos de recuperação de saudação que são criados a partir de backups de saudação diária, semanal, mensal e anual são mantidos no Azure.

13. Em Olá **escolher replicação Online** , selecione como a saudação inicial total replicação de dados ocorre. Você pode replicar pela rede hello ou faça uma off-line (propagação off-line) do backup. Backup offline usa o recurso de importação do Azure hello. Para obter mais informações, consulte [Fluxo de trabalho de backup offline no Backup do Azure](backup-azure-backup-import-export.md).

14. Em Olá **resumo** , examine as configurações. Depois de selecionar **criar grupo**, ocorre a replicação inicial dos dados de saudação. Quando termina a replicação de dados, em Olá **Status** página status do grupo de proteção Olá é **Okey**. O backup, em seguida, ocorre por proteção Olá as configurações de grupo.

## <a name="recover-system-state-or-bmr"></a>Recuperar o estado do sistema ou BMR
Você pode recuperar o local de rede do sistema ou BMR estado tooa. Se você tiver feito backup da BMR, usar o ambiente de recuperação do Windows (WinRE) toostart seu sistema e conectá-lo toohello rede. Em seguida, use toorecover de Backup do Windows Server de um local de rede hello. Se você tiver feito backup do estado do sistema, basta use toorecover de Backup do Windows Server de local de rede hello.

### <a name="restore-bmr"></a>Restaurar BMR
Execute a recuperação no computador do servidor de Backup hello:

1.  Em Olá **recuperação** painel, computador de saudação localizar você deseja toorecover e, em seguida, selecione **recuperação Bare-Metal**.

2.  Pontos de recuperação disponíveis são indicados em negrito no calendário hello. Selecione Olá data e hora para que você deseja toouse de ponto de recuperação hello.

3.  Em Olá **Selecionar tipo de recuperação** , selecione **copiar tooa a pasta de rede.**

4.  Em Olá **especificar destino** página, selecione onde você deseja que toocopy Olá dados. Lembre-se de que precisa de destino selecionado Olá toohave espaço suficiente. É recomendável que você crie uma nova pasta.

5.  Em Olá **especificar opções de recuperação** página, selecione Olá tooapply de configurações de segurança. Em seguida, selecione se deseja que a rede de área de armazenamento (SAN) toouse-com base em instantâneos de hardware, para uma recuperação mais rápida. (Essa é uma opção apenas se você tiver uma SAN com essa funcionalidade disponível e Olá toocreate de capacidade e dividir toomake um clone-lo gravável. In addition, hello computador protegido e o computador do servidor de Backup devem ser conectado toohello mesma rede.)

6.  Configure opções de notificação. Em Olá **confirmação** página, selecione **recuperar**.

Configure o local de compartilhamento de saudação:

1.  No local de restauração hello, vá pasta toohello com backup hello.

2.  Compartilhar pasta de saudação que é um nível acima de WindowsImageBackup, para que a raiz da pasta compartilhada Olá Olá é pasta WindowsImageBackup de saudação. Se você não fizer isso, a restauração não localizará backup hello. tooconnect usando o ambiente de recuperação do Windows (WinRE), você precisa de um compartilhamento que você pode acessar no WinRE com as credenciais e o endereço IP correto de saudação.

Restaure o sistema de saudação:

1.  Inicie Olá o computador no qual você deseja toorestore imagem de saudação usando Olá DVD do Windows para o sistema de saudação que você está restaurando.

2.  Na primeira página de saudação, verifique as configurações de idioma e localidade. Em Olá **instalar** página, selecione **reparar o computador**.

3.  Em Olá **opções de recuperação do sistema** página, selecione **restaurar o computador usando uma imagem do sistema que você criou anteriormente**.

4.  Em Olá **selecionar um backup de imagem do sistema** , selecione **selecionar uma imagem do sistema** > **avançado** > **pesquisa de sistema imagem em rede Olá**. Se um aviso for exibido, selecione **Sim**. Vá toohello caminho de compartilhamento, insira as credenciais de saudação e, em seguida, selecione o ponto de recuperação de saudação. Isso verifica os backups específicos disponíveis nesse ponto de recuperação. Selecione o ponto de recuperação de saudação que você deseja toouse.

5.  Em Olá **escolher como toorestore Olá backup** página, selecione **Formatar e reparticionar discos**. Na página seguinte do hello, verifique as configurações. 

6.  restauração de saudação toobegin, selecione **concluir**. Uma reinicialização é necessária.

### <a name="restore-system-state"></a>Restaurar o estado do sistema

Execute a recuperação no Servidor de Backup:

1.  Em Olá **recuperação** painel, localizar Olá computador que você deseja toorecover e, em seguida, selecione **recuperação Bare-Metal**.

2.  Pontos de recuperação disponíveis são indicados em negrito no calendário hello. Selecione Olá data e hora para que você deseja toouse de ponto de recuperação hello.

3.  Em Olá **Selecionar tipo de recuperação** , selecione **copiar pasta de rede tooa**.

4.  Em Olá **especificar destino** página, selecione onde você deseja toocopy Olá dados. Lembre-se de que destino selecionado Olá precisa de espaço suficiente. É recomendável que você crie uma nova pasta.

5.  Em Olá **especificar opções de recuperação** página, selecione Olá tooapply de configurações de segurança. Em seguida, selecione se deseja toouse instantâneos de hardware baseados em SAN para uma recuperação mais rápida. (Essa é uma opção apenas se você tiver uma SAN com essa funcionalidade e Olá toocreate de capacidade e dividir toomake um clone-lo gravável. In addition, computador protegido de saudação e servidor de Backup deve ser conectado toohello mesma rede.)

6.  Configure opções de notificação. Em Olá **confirmação** página, selecione **recuperar**.

Fazer backup do Windows Server:

1.  Selecione **Ações** > **Recuperação** > **Este Servidor** > **Avançar**.

2.  Selecione **outro servidor**, selecione Olá **especificar tipo de local** página e, em seguida, selecione **pasta compartilhada remota**. Digite a saudação caminho toohello pasta que contém o ponto de recuperação de saudação.

3.  Em Olá **Selecionar tipo de recuperação** , selecione **o estado do sistema**. 

4. Em Olá **Selecionar local para recuperação do estado do sistema** , selecione **local Original**.

5.  Em Olá **confirmação** página, selecione **recuperar**. Após a restauração hello, reinicie o servidor de saudação.

6.  Você também pode executar Olá restauração de estado do sistema em um prompt de comando. toodo, iniciar o Backup do Windows Server no computador Olá deseja toorecover. Identificador de versão de hello tooget, em um prompt de comando, digite:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Use a restauração de estado do hello versão identificador toostart saudação do sistema. No prompt de comando hello, digite:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Confirme que você deseja toostart recuperação de saudação. Você pode ver o processo de saudação na janela de Prompt de comando hello. Um log de restauração é criado. Após a restauração hello, reinicie o servidor de saudação.

